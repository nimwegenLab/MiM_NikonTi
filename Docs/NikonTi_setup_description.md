
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
connected to the computer's serial port (no USB converter)

By default, excitation filters are placed in the SpectraX.

Color band (nm)   | Fluorophore	    | Excitation Filter	| Power (uW; 3 mm LLG)
------------------|-----------------|-------------------|---------------------
Violet (380-410)	| DAPI, Hoechst	  | 386/23            | 150	
Blue (420-455)	  | CFP             |	438/24            | 275	
Cyan (460-490)	  | GFP, FITC	      | 475/35            | 215	
Teal (500-520)	  | YFP	            | 513/17            | 65	
*Green* (535-600) | *TRITC*&#42;    | 560/25  	        | 380	
*Yellow* (535-600)| *mCherry*&#42;  | 575/25	          | 210
Red (620-750)	    | Cy5             | 650/13	          | 105	
Far red (620-750)	| Cy5.5           | 657/30	          | 	
NIR	              | Cy7	            | 740/13	          | 40

Full table and more available from [Lumencor website](http://www.lumencor.com/docs/Power%20&%20Intensity%20Levels%202.28.11.pdf) ([alt link](http://lumencor.com/wp-content/uploads/2012/06/SPECTRA-P-I-06-12.pdf)). \
&#42; for italicized colours filters are mounted in the corresponding microscope cubes.


## Filter cubes

Pos | Fluorophore                      | Emission filter    | Beam splitter | Emission filter
----|----------------------------------|--------------------|---------------|----------------
1   | --                               | --                 | --            | --
2   | [CFP](http://tiny.cc/ksnu5x)     | --                 | 458 (AHF)     | 480/17 (Semrock BrightLine HC
*2* | *DAPI*                           | --                 | 416 (AHF)     | 460/50 (Chroma ET)
3   | [GFP](http://tiny.cc/6dvkzx)     | --                 | 495 (AHF)     | 525/50 (Chroma ET 265146)
*3* | [*YFP*](http://tiny.cc/8evkzx)   | --                 | 520 (AHF)     | 542/27 (Semrock BrightLine HC)
4   | [RFP](http://tiny.cc/t9ukzx)     | 560/25 (Semrock)   | 573 (Chroma)  | 609/54 (Semrock BrightLine HC)
5   | [mCherry](http://tiny.cc/egvkzx) | 575/25 (Semrock)   | 594 (Chroma)  | 647/70 (DELTA TopPride)
6   | [Cy5.5](http://tiny.cc/k6mu5x)   |--                  | 700 (Semrock) | 775/140 (Semrock BrightLine HC)


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


## Camera
Hamamatsu ORCA-Flash4.0  
Model: C11440-22CU  
SN: 720701

Connected to the computer with USB3 (NB: works only on PCIe USB3 ports)
Camera cooler: CoolCare (set to 20ºC)

## Arduino
A Arduino Uno programmed with MM default AOTF firmware is used to control the state of the diascopic illumination LED (TTL control). The TTL output is connected to pin 8; since the on-board LED is connected to pin 13, arduino's "Switch State" must be set to 33 (1 for pin 8 + 32 for pin 13).

Additionally, analog inputs A0 to A2 are connected to 3-way connectors in order to read Hall effect sensors (A1324LUA-T, Digikey #620-1432-ND) outputs. This is used to encode the position of several mechanical switches.

Function   | Connector (9-pol female) | Cable    | PCB header
-----------|--------------------------|----------|-------------
+5V        |                        1 | white    | P2/1	
A0, A1, A2 |                        2 | green    | P4/1	
GND        |                        3 | brown    | P2/2	


# Computer
Dell Precision Tower 7910 (pz-kben01-pdw08)
System drive (C): SSD (256gb)
Data drive (D): RAID10 volume (2tb; hardware RAID powered by `MegaRAID SAS 9361-8i` PCIe controller and 4 SAS HD)
USB3 connection for Flash4 camera: only on PCIe USB3 ports (card U3-PCIE1XG202)


# Temperature regulation
Life Imaging Services "The Cube 2"
SN: 12400

The integrated temperature controller is [Omron E5CN-H](https://www.ia.omron.com/products/family/1946/).


# Maintenance

## 20150131 (Thomas)
SpectraX illumination aligned and characterized.

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
- Adjust diaphragm of fluo excitation light path.
Using the centering tool, aperture diaphragm is set to fill the objective (light contour on the ring).
Using a uniform fluo slide, the field diaphragm is set tom minimal opening not producing vignetting in the camera field of view.
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


## To do
- measure power for all filter sets (e.g. at 2")
