---
title: 'Hardware-triggering with Micro-Manager: a case study'
author:
- name: Thomas Julou
  affiliation: Biozentrum, Basel University
- name: Guillaume Witz
  affiliation: Biozentrum, Basel University
date: 'February 2016'
include-after: <hr><a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/80x15.png" /></a> This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.
output: html_document
---


## Motivation

Why you might want to use hardware-triggering to acquire image series is nicely summarized by MM's developers in the Journal of Biological Methods [@edelstein2014advanced]. The principle of hardware-based synchronization is also explained:

> A central capability of μManager is Multi-Dimensional Acquisition (MDA), which allows image sets to be acquired at multiple XY positions, Z slices, time points, and channels. Conventionally, MDA is accomplished by sending commands from the computer to the devices each time a change (in, e.g., stage position or illumination) is required. This communication can add unnecessary latency (up to 100 ms) between image frames. In the case of a time series, the timing to issue commands to the devices and camera is controlled by the application software, a method that cannot consistently produce accurate timings on a standard desktop operating system. The resulting timing jitter can be on the order of tens of milliseconds, unacceptable for fast time series.
> 
> Much faster and accurately timed operation is possible with most cameras (when acquiring a preset sequence of frames) as well as many other devices (when executing a pre-programmed sequence of commands). μManager’s built-in hardware synchronization support can take advantage of these capabilities to perform fast MDA, such as a fast Z stack with a piezo stage or fast multi-channel imaging with lasers shuttered by acousto-optical tunable filters (AOTFs). From the microscope user’s perspective, this is done seamlessly, such that μManager’s MDA engine automatically delegates control to hardware when possible.
> 
> Synchronization between the camera and the other devices is achieved by routing TTL (Transistor-Transistor Logic) pulses over signal cables. In the configuration currently supported by μManager, the camera, operated in sequence acquisition mode, acts as the timing-generating device, sending out TTL pulses at each exposure. The pulses are sent (typically via BNC cable) to a sequencing device, which may be standalone or built into a stage or illumination controller. Upon each pulse, the sequencing device advances the hardware to the correct state for the next exposure, based on a sequence of positions or illumination settings uploaded ahead of time.

Here we describe (i) how we used an Arduino board with a simple custom extension shield to control several TTL-controlled light sources using hardware-triggering and (ii) which external triggers of the camera we use in order to acquire images only once the setup has reached the expected state.


### Capture mode *vs* sequence mode

In order to get a feeling of the difference between capture mode *vs* sequence mode, the easiest is to run Multi-Dimensional Acquisition with time points only. If the delay is shorter than the exposure, the camera is run in sequence mode and the illumination stays on (e.g. a Flash4 connected with USB3 using 33ms delay and 33.3355ms exposure will take 33.99s to acquire 1000 frames, i.e. 34fps). However, if the delay is longer than the exposure, the camera is run in capture mode and the illumination is switched on and off for each frame: the acquisition speed drops (e.g. the same task acquired with 34ms delay takes 373.68s i.e. ≈2.7fps) and the overall timing becomes erratic (not shown).

This clearly illustrates that running the camera in sequence mode with hardware synchronization of devices is a prerequisite for fast-image acquisition. You might think that it would be easier to write your own simple script to control your setup and acquire images in sequence mode. While this is fully possible, setting up your hardware to be "sequencable" gives you access to all the power and flexibility of MDA: set exposure per channels, skip frames / z-stack acquisition for any channel, acquire multiple positions with autofocus, save image with all metadata, etc.


## Integrating several TTL-controlled light sources into a single sequencable device

### using an arduino board to control an illumination device through TTL
how to replace a USB-TTL controllerusing an arduino...


### Overview
In our setup, the camera is an Hamamatsu Flash4, the transmitted light illumination is produced by a pE-100 (CoolLED) and the epifluorescence illumination by a Spectra X (Lumencor). In principle, the approach described below could be taken to control any set of TTL-controlled light sources.

While there is a device adapter for the Spectra X, the pE-100 require a USB-TTL converter, for instance an Arduino board with the default firmware (a.k.a. AOTF). However, we need the Spectra X to be "sequencable" and, in order to run hardware-triggered MDA with both transmitted light and epifluorescence, to combine the two light sources into a single "sequencable" device. Hence we created a simple custom extension shield allowing to control which channel is active using TTL signals. Hence the shield has one BNC connector to trigger the pE-100 and DB-15HD connector to trigger each LED of the Spectra X individually. The intensity of the Spectra X is still set using the dedicated device adapter. 

### Custom shield design
Several points have been taken into consideration:

- we want to control one TTL output for the pE-100 and 6 TTL outputs for the Spectra X (one per LED). Unfortunately, the default arduino firmware for MM has only 6 outputs. Instead of hacking this firmware and the corresponding device adapter, we took advantage of the fact that we only want LEDs to be active one at a time and used demultiplexer chip ([CD74HCT138](../Manuals/Arduino/cd74hc238.pdf)). Such an IC take a binary signal as input (here 3 bits encoding a 0-7 value) and set the corresponding output pin (out of here 8 pins) active; for instance if the signal (provided by the 3 lowest bits of the arduino `switch state` variable) is b011 then pin 5 is active. The chip we chose is a demux-inverter which means that output pins are HIGH by default and become LOW when active. This is convenient because the Spectra X external trigger is active-low. Output pins 1-6 are connected to DB-15HD connector (a.k.a. VGA connector) following the Spectra X connector mapping. Pin 0 must remain unconnected in order to be able to turn the Spectra X dark.
- in order to save arduino pins for future applications, we control the pE-100 with the eighth pin of the demux-inverter. Since this device is active-high, the output pin 7 of the demux-inverter is connected to a BNC connector through an inverter IC ([MC74H04N](../Manuals/Arduino/mc74hc04.pdf)).
- in order to use hardware-based synchronization, it is important that the arduino has an external trigger connected to its pin 2: illumination will occur only when the camera is exposing (to minimize bleaching and photodamage) and the setup state will be updated every time a new signal is detected. Since the Flash4 outputs 3.3V signals (CMOS logic with ($V_{OH}=2.4V$)), and the arduino logic is 5V ($V_{IH}=3.0V$), a level converter is required to raise the 3.3V signal to 5V; we use a design inspired by Sparkfun's "[Logic Level Converter](https://learn.sparkfun.com/tutorials/bi-directional-logic-level-converter-hookup-guide#board-overview)" with a similar transistor ([Fairchild BS170](../Manuals/Arduino/BS170.pdf)).
- in order to be able to us this shield for software-based control as well, we set a 5V pull-up on the input so that the output is always active when no cable is connected to the input (but when the arduino switch state is 0).

NB: although the demux-inverter has ENABLE inputs that could be use to set all pins inactive when the camera is not exposing (instead of the arduino trigger pin), it is not suitable for hardware-based synchronization since it does not allow the setup state to be updated when a new signal is received.

NB: it is in principle possible to control the pE-100 using a native arduino pin (instead of one of the demux-inverter). But why would you?


### Circuit schematic and control table

![demux_scheme](figs/arduinoTi_trigger_dual_simple.png)

A custom DB15HD cable is used since VGA cables have unspecified pins (e.g. 11) which are usually connected to the ground.

The following table recapitulate which pin of the DB-15HD connector controls which LED and the value of arduino's switch state activating the correspomding LED:

Channel | DB15 pin        | SwitchState
--------|-----------------|-------------
Violet  | 13              | 1
Blue    | 12              | 2
Cyan    | 3               | 3
Teal    | 11              | 4 
Green   | 2               | 5
Red     | 1               | 6
GND     | 6-8             | -   
GND     | 10 (other wire) | -
DIA     | BNC (inverted)  | 7



## hardware triggering

### Flash4 trigger output explained

When running an MDA, micromanager detects whether devices are sequenceable, meaning that they can internally store series of states that they then reach upon successive triggers. If all devices are sequenceable, the camera runs in streaming mode and sends the triggers to other devices. On the Flash4 you can set each of the three triggers (numbered [0], [1] and [2]) independently and each time an image is acquired, those triggers will be sent out. There are several options for each trigger (explained in detail but not always very clearly in the Hamamatsu manual): 
-Trigger polarity: choose positive or negative depending on what the receiving device needs. Apparently you need positive for the ASI stage 
-Trigger kind: you will probably use either the "exposure" or the "programmable" options. In "exposure" the trigger goes active when all the pixel rows are exposing. In a CMOS each row of pixels start exposure with a slight delay compared to its neighbor (starting from the middle row), and it takes about 10ms to start exposure of all rows. So your trigger will be low for 10ms and high the rest of the time and your stage will move at the moment where all pixels have started exposing. This is probably not an ideal solution. In "programmable" you can precisely define the pulse that you want to send with the following options. 
-Trigger period: sets the duration of the "programmable" trigger 
-Trigger delay: sets a delay before a pulse is sent. 
-Trigger source: you have two choices on how to set the delay. Either its a delay since the end of read-out ("Readout end" mode), i.e. from the moment the last row of pixels of the current image has been read out by the camera. Or its a delay since the start of readout ("Vsync" mode), i.e since the moment where the first row of pixels of the current image is read-out (figure 10-12 of the camera manual explains this with graphics). 

Note that period, delay and source only affect triggers in "programmable" mode. 

So for example you could use the trigger [0] ("1" one the back of the camera) with: positive polarity, "Readout end" mode, zero delay and a pulse of 10ms. Like that, at the end of every picture acquisition, a 10ms pulse is sent to your stage (I guess length doesn't matter as the stage reacts to raising edge). Be aware that since the camera works in streaming mode (it overlaps image acquisitions), whatever your choice of delays, you will always be moving the stage while pixels are exposing. This is not a problem only if your exposure time is quite larger than the time it takes your stage to move. To avoid that, you'd also have to synchronize illumination with a camera trigger and only illuminate when the stage is not moving, but that involves a bit more work. 


### first use case: illuminate sample only during camera exposure

blanking with global exposure trigger (not sequencable)
effective is -10ms for full frame

### Using camera trigger outputs for hardware-triggered control of illumination

aim: sequencable MDA with illumination during global exposure
- requires:
  + arduino sequencable ON
  + trigger kind "exposure" and polarity positive
  + auto-shutter OFF and blanking OFF
- blanking is superseeded by sequencable. NB: mysteriously when auto-shutter is ON, blanking disables spurious illumination (not during camera exposure)
- using global exposure trigger generates additional pulse(s) at the end of the sequence (which doesn't produce an image). However, the triggering sequence is restarted from the beginning at the next frame / position...


### Hardware-triggered control of z positions

aim: sequencable MDA with illumination during global exposure and piezo moves during "partial" frame exposure (must take < 10ms) 




<!-- ## Remarks -->


### References
<!-- bibliography is automatically put at the end -->

---
references:
- id: edelstein2014advanced
  type: article-journal
  title: Advanced methods of microscope control using μManager software
  container-title: Journal of Biological Methods
  volume: '1'
  issue: '2'
  DOI: 10.14440/jbm.2014.36
  ISSN: 2326-9901
  language: ENG
  author:
    - family: Edelstein
      given: Arthur D.
    - family: Tsuchida
      given: Mark A.
    - family: Amodaj
      given: Nenad
    - family: Pinkard
      given: Henry
    - family: Vale
      given: Ronald D.
    - family: Stuurman
      given: Nico
  issued:
    date-parts:
      - - 2014
  PMID: '25606571'
  PMCID: PMC4297649
  container-title-short: J Biol Methods
...
