---
title: "Setup description of `vng` Nikon Ti"
author: Thomas Julou
output: html_document
---

## Objectives

Magnification | NA    | WD (mm) | Phase contrast | Model
--------------|-------|---------|----------------|------
100x          | 1.45  | 0.13    | Ph3            | Plan Apo Lambda DM 100x oil (MRD31905)


## Condenser & Phase rings


# Fluorescence

## Spectra X

Model: SPECTRAX-6_LCR_SA  
SN: 3486  
connected to the computer's serial port (no USB converter). Serial communication (through MM device adapter) is used only to set the intensity;   LEDs are switched ON and OFF using TTL signals produced by the Arduino box.

Excitation filters are placed in the SpectraX.  
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


Full table and more available from[Lumencor](https://github.com/vanNimwegenLab/MiM_NikonTi/blob/master/Manuals/SpectraX/SpectraX_power.pdf). \
&#42; for italicized colours, filters are must be exchanged in the SpectraX. \
NB: 667/30 should be replaced by 650/60 or 647/57...


## Filter cubes

Pos | Fluorophore                      | Excitation filter    | Beam splitter | Emission filter
----|----------------------------------|--------------------|---------------|----------------
1   | --                               | --                 | --            | --
2   | --                               | --                 | --            | --
3   | --                               | --                 | --            | --
4   | --                               | --                 | --            | --
5   | [**GFP**/**mCherry**]()   | --                 | 495/605 (Semrock)  | 527/ - 645/ (Semrock BrightLine HC)
6   | [CFP/YFP/*mCherry*]()     | --                 | 459/526/596 (Semrock)  | 475/-543/-702/ (Semrock BrightLine HC)


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
Model: C13440-20CU  
SN: 300291

Connected to the computer with USB3 (NB: works only on PCIe USB3 ports)


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

## 20170216 (Thomas)

http://micro-manager.3463995.n2.nabble.com/Installation-Error-File-is-not-supported-tp7584500p7584648.html
