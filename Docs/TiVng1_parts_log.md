---
title: "Parts description for `TiVng1`"
author: Thomas Julou
output: html_document
---

## Objectives

Magnification | NA    | WD (mm) | Phase contrast | Model
--------------|-------|---------|----------------|------
100x          | 1.45  | 0.13    | Ph3            | Plan Apo Lambda DM 100x oil (MRD31905)
60x           | 1.40  | 0.13    | Ph1 ??         | Plan Apo Lambda DM 60x oil (MRD31605)
10x           | 0.30  | 15.2    | Ph1            | Plan Fluor DL 10x (MRH20101)


## Condenser & Phase rings


# Fluorescence

## Spectra X

Model: SPECTRAX-6_LCR_SA  
SN: 3486  

Power is measured in mW at the end of a 3mm LLG.

Color band (nm)   | Fluorophore	    | Excitation Filter	| Power (5%) | Power (97%) | Power (spec)
------------------|-----------------|-------------------|------------|-------------|-------------
Violet (380-410)	| DAPI, Hoechst	  | 386/23            | 6.6        | 108         | 150	   
Blue (420-455)	  | CFP             |	438/24            | 13.2       | 164         | 275	   	
Cyan (460-490)	  | GFP, FITC	      | 474/23            | 4.4        | 111         | 215		 
Teal (500-520)	  | YFP	            | 510/10            | 1.5        | 31.5        | 40	   
Yellow (535-600)  | mCherry         | 578/21	          | 5.9        | 144         | 210-300
*Green* (535-600) | *TRITC*&#42;    | 554/23  	        | 9.4        | 218         | ~250	
Far red (620-750)	| Cy5.5           | 667/30	          | 0          | 7.6         | <50

Other filters available (compatible with single-band cubes):

Color band (nm)   | Fluorophore	    | Excitation Filter	| Power (5%) | Power (97%) | Power (spec)
------------------|-----------------|-------------------|------------|-------------|-------------
Cyan (460-490)	  | GFP, FITC	      | 475/35            | 6.1        | 124         | 215	
Yellow (535-600)  | mCherry         | 575/25	          |            |             | 210-300
Red (620-750)	    | Cy5             | 650/13	          |            |             | 105


&#42; for italicized colours, filters are must be exchanged in the SpectraX. \
NB: 667/30 should be replaced by 650/60 or 647/57...


## Filter cubes

Pos | Fluorophore                      | Excitation filter    | Beam splitter | Emission filter
----|----------------------------------|--------------------|---------------|----------------
1   | --                               | --                 | --            | --
*1* | *DAPI*&#42;&#42;                 | --                 | 416 (AHF)     | 460/50 (Chroma ET)
2   | [*GFP*](http://tiny.cc/6dvkzx)   | --                 | 495 (AHF)     | 525/50 (Chroma ET 265146)
3   | [RFP](http://tiny.cc/t9ukzx)     | &#42;&#42;         | 573 (Chroma)  | 609/54 (Semrock BrightLine HC)
4   | [Cy5.5](http://tiny.cc/k6mu5x)   | --                 | 700 (Semrock) | 775/140 (Semrock BrightLine HC)
5   | [**GFP**/**mCherry**]()   | --                 | 495/605 (Semrock)  | 527/ - 645/ (Semrock BrightLine HC)
6   | [CFP/YFP/*mCherry*]()     | --                 | 459/526/596 (Semrock)  | 475/-543/-702/ (Semrock BrightLine HC)

Whenever possible, the bold filters should be preferred over the italicized ones.  
&#42;&#42; these filters or cubes must be exchanged (NB: RFP cannot be used in combination with mCherry).


ALWAYS PUT BACK THE DEFAULT FILTER SET FOR THIS POSITION ONCE YOU ARE DONE.


## Camera
Hamamatsu ORCA-Flash4.0  
Model: C11440-22CU  
SN: 720701

Connected to the computer with USB3 (NB: works only on PCIe USB3 ports)
Camera cooler: CoolCare (set to 20ºC)


# Computer
Dell Precision Tower 7910 (pz-kben01-pdw08)
System drive (C): SSD (256gb)
Data drive (D): RAID10 volume (2tb; hardware RAID powered by `MegaRAID SAS 9361-8i` PCIe controller and 4 SAS HD)
USB3 connection for Flash4 camera: only on PCIe USB3 ports (card U3-PCIE1XG202)


# Temperature regulation
Life Imaging Services "The Cube 2"
SN: 12400

The integrated temperature controller is [Omron E5CN-H](https://www.ia.omron.com/products/family/1946/).


# Flow control

ID | SN           | Use | Comments
---|--------------|-----|---------
1  | FLOW-02-4854 | Ch1 | was clogged by GW in 09.2016, cleaned up and in use again since 12.2016
2  | FLOW-02-4852 | Ch2 | 
3  | FLOW-02-4853 |     | used temporarily for Ch1 (10-11.2016)
4  | FLOW-02-4855 |     | 



# Maintenance

## 20150201 (Thomas)
SpectraX illumination aligned and characterized: aperture (resp. field) shutters adjusted to most homogeneous (resp. smallest without vigneting) pictures.
(cf clibration report).

## 20150619 (Thomas)
20150619: characterization of Flash4 read noise.\
using 2s exposure and Defect Correct Mode ON, with a capped camera (light in the room??)

20150626: characterization of Flash4 gain.\
pseudo-unifrom illumination of the sensor is achieved using an iphone (min brightness, flashlight app at 100%; Plane mode ON and on charge), the GIF filter of NikonTi TRANS illumination and 3 plastic cups as a diffuser (with their side covered by black paper).
use a modified version of Sturman's camera lab to acquire 20 different exposures (from 13 to 1950 ms; stored as stack slices) with 200 images for each exposure.
Defect Correct Mode ON.

## 20151120 (Thomas)
- Reordered filter cubes (empty on 1). TRITC and mcherry excitation filters moved to the cubes
- Upgraded Hamamatsu DCAM API to 15.10.4787
- Upgraded micromanager to 1.4.22

## 20151124 (Thomas)
- Configured camera for water cooling.

## 20151127 (Thomas)
- Adjust diaphragms of fluo excitation light path.
Using the centering tool, aperture diaphragm is set to fill the objective (light contour on the ring).
Using a uniform fluo slide, the field diaphragm is set to the minimal opening not producing vignetting in the camera field of view.
Flat field pictures have been saved before and after adjusting the diaphragms.

## 20151203 (Thomas)
- Improved DIA TTL control: Trek5 USB-TTL box (unreliable) replaced by an Arduino Uno with default AOTF firmware from MM.
- Added 3 Hall effect sensor to the Arduino: analog inputs A0 to A2 will be used to encode the position of the magnifying lens and the position of the 2 ND filters on fluo excitation light path.

## 20151214 (Thomas)
- Upgraded Hamamatsu DCAM API to 15.12.4823 (fix the water / air cooling display in DCAM config)

## 20160108 (Thomas & Guillaume)
- new `System` property in MM (set arduino and camera cooling; better than using MMstartup.bsh)
- connected new computer
    - SpectraX connected to serial port (COM1) instead of using a USB adapter
    - Updated Nemesys software to last version
    - renamed Arduino serial adapter to `ArduinoDIA`, verbose mode disabled
- connected a second arduino (`Arduino SpectraX`) to test the stability before iplementing SpectraX TTL control via arduino
- tested streaming acquisiiton to RAID: 1000 frames at 25fps in 30sec (ca. 7gb in total)

## 20160119
- new arduino shutter with a custom shield to control the DIA LED and the SpectraX using TTL (through a demux connected to pins 8-10). Configuration reworked accordingly.

## 20160205
- installed replacement camera (switch back to air cooling)

## 20160408
- lab camera is back (installed with air cooling)


## 20160429 (Thomas)
- renamed `DIA` (brightfield) and `DIA Ph3` (phase contrast). remove the condenser ppty form the objective group.
- restore water cooling in default config (including `Startup` preset).
- upgraded Hamamatsu DCAM API (and USB driver) to 16.2.4843
- Adjust diaphragms of fluo excitation light path (using centering tool and adjusted to match 20151127 flat field images).
NB: Flat field pictures have been saved before and after adjusting the diaphragms.
- measured SpectraX power at the end of LLG:

LED           	  |                |	          | Doc  | LLG  | Thorlabs LLG
------------------|----------------|------------|------|------|----
Blue (420-455)	  | CFP            | 438/24     | 275	 | 192  | 198
Cyan (460-490)	  | GFP, FITC	     | 475/35     | 215	 | 124  | 135
Teal (500-520)	  | YFP	           | 510/10     | 40	 | 34   | 35.6
*Green* (535-600) | TRITC, mCherry | no filter	| >380 | 595  | 645
Far red (620-750)	| Cy5.5          | 667/30	    | <50  | 9.85 | 10

## 20160628 (?? Thomas)
- one screw maintaining the holder is broken. I unmount the stage and bring it to the workshop to extract it.
NB: Nikon advised us later to use a screwdriver (pushed in by hitting gently) to unscrew it.
- all 3 plastic screws (crosshead) are replaced with slot plastic screws (in acrylic?).

## 20160719 (Claudio.Wenger@nikon.com & Gwendoline)
- Following repeated stage drift problems (sudden shifts in long timelapses + slow relaxing along one axis after reaching the target position) the stage (SN: 661951) is replaced by a temporary stage (SN: 662806).
- C. Wenger notices that the slot screws currently in use are longer than the original screws (by ca. 0.5mm).
NB: this fits very well with the observed issues (by scratching the lower plate of the stage, the screws would mess up the displacement in one direction only; large shift accoruing randomly would correspond to a sudden change in the screw position after too much constraints have been accumulated).

## 20160802 (Thomas)
- Long multiposition timelapse show no stage instability anymore.

## 20160805 (INCIDENT)
- At the end of the experiment, the cooler is at 47.4 degC!!!
It sounds like the water circulation is lower than previously (noticed a few days earlier by Guillaume but the cooling was still working...)

## 20161028 (Thomas)
- the order of the objectives is changed to facilitate plates imaging.
- several single band filters replaced by the new dual and tri cubes:
  + 2 new cubes (Dual: GFP/mCheery; Tri: CFP/YFP/mCherry)
  + excitation filters changed: GFP (475/35 => 474/23) and mCherry (575/25 => 578/21)
- BREAKING CHANGES:
  + the GFP excitation filter has changed; in order to obtain results comparable which previous experiments, you should change the GFP filter in the SpectraX.
  + mCherry and RFP excitation filters are now back in the SpectraX rather than in the cubes

## 20161122 (Thomas)
- measured all intensities using the Xcite powermeter (from IMCF), at the output of the LLG (NB: low battery of the powermeter).


## 20161202 (Thomas)
- checked the aperture diaphragm of the epifluo arm (was correct).

## 20170207 (Thomas)
- fixed windows resizing problem on new Dell U3417W (following http://superuser.com/a/508782)
- acquired PTC files and PSF

## 20170227 (Thomas)
- installed MM2

##20180403 (tHOMAS)
- checked EPI-FL diaphragm (still good, slightly recentered) 
