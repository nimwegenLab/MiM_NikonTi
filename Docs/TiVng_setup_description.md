---
title: "Description of `vng` Nikon Ti setups"
author: Thomas Julou
output: html_document
---

# Fluorescence

## Spectra X

connected to the computer's serial port (no USB converter). Serial communication (through MM device adapter) is used only to set the intensity;   LEDs are switched ON and OFF using TTL signals produced by the Arduino box.

Excitation filters are placed in the SpectraX.

Full table and more available from[Lumencor](https://github.com/vanNimwegenLab/MiM_NikonTi/blob/master/Manuals/SpectraX/SpectraX_power.pdf). 


## Filter cubes

- Positions are written on the flat bottom of the turret.
- Filter cubes can be opened by pushing the lever toward the center of the emission filter.
- Chroma and Nikon filters: arrow toward dichroic.
  Omega and Semrock filters: arrow in the direction of light.


## Exchanging a filter cube
At some positions, the default filter set can be exchanged with the following steps:

1. select filter position - 2 (e.g. 6 for GFP/YFP) and turn off the setup
2. remove the turret cap, pull out the cube. Then put the other cube in place (push until the stopper) and close the cap.
3. Acquire the picture using the appropriate illumination group. \
NB: it is not possible to create two identical presets with different names although this would sometimes be useful to use save appropriate metadata for the picture.

ALWAYS PUT BACK THE DEFAULT FILTER SET FOR THIS POSITION ONCE YOU ARE DONE.


## Arduino
An Arduino Uno programmed with MM default firmware (aka AOTF) is used as a global shutter to switch the transmitted light LED (TTL control) and the SpectraX's LEDs. Using this setup, it is possible to change the illumination in a "sequencable" manner (i.e. using hardware triggering). Pin 2 is connected to a BNC connector (through a level shifter SN74HCT125 connected for 3.3V > 5V) for trigger input at 3.3V. Pins 8-10 are connected to a demux-inverter, itself connected to the DB15HD connector (SpectraX triggering) and to a BNC connector (output for DIA triggering, through an inverter since active-high). A custom DB15HD cable is used since VGA cables have unspecified pins (e.g. 11) which are usually connected to the ground.

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


Additionally, analog inputs A0 to A2 are connected to 3-way connectors in order to read Hall effect sensors (A1324LUA-T, Digikey #620-1432-ND) outputs. This is used to encode the position of several mechanical switches.

Function   | Connector (9-pol female) | Cable    | PCB header
-----------|--------------------------|----------|-------------
+5V        |                        1 | white    | P2/1	
A0, A1, A2 |                        2 | green    | P4/1	
GND        |                        3 | brown    | P2/2	


