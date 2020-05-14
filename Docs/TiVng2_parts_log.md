---
title: "Parts description for `TiVng2`"
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

Model: SPECTRAX-6_LCR_SG  
SN: 11854  

Power is measured in mW at the end of a 3mm LLG.

Color band (nm)   | Fluorophore	    | Excitation Filter	| Power (5%) | Power (97%) | Power (spec)
------------------|-----------------|-------------------|------------|-------------|-------------
Violet (380-410)	| DAPI, Hoechst	  | 390/22            | 8.7        | 186         | 150	   
Blue (420-455)	  | CFP             |	440/20            | 19.2       | 246         | 275	   	
Cyan (460-490)	  | GFP, FITC	      | 470/24            | 9.9        | 132         | 215		 
Teal (500-520)	  | YFP	            | 511/16            | 2.1        | 33.5        | 40	   
Yellow (535-600)  | mCherry         | 578/21	          | 9.0        | 270         | 210-300
*Green* (535-600) | *TRITC*&#42;    | 555/28  	        | 11.1       | 321         | ~250	
Far red (620-750)	| Cy5.5           | 640/30	          | 8.5        | 182         | <50

&#42; for italicized colours, filters are must be exchanged in the SpectraX. \


## Filter cubes

Pos | Fluorophore                      | Excitation filter    | Beam splitter | Emission filter
----|----------------------------------|--------------------|---------------|----------------
1   | --                               | --                 | --            | --
2   | --                               | --                 | --            | --
3   | --                               | --                 | --            | --
4   | --                               | --                 | --            | --
5   | [**GFP**/**mCherry**]()   | --                 | 495/605 (Semrock)  | 527/ - 645/ (Semrock BrightLine HC)
6   | [CFP/YFP/*mCherry*]()     | --                 | 459/526/596 (Semrock)  | 475/-543/-702/ (Semrock BrightLine HC)


## Camera
Hamamatsu ORCA-Flash4.0  
Model: C13440-20CU  
SN: 300291

Connected to the computer with USB3 (NB: works only on PCIe USB3 ports)


## Piezo

Stage: Nano-F25HS (serial no: MCLS03519)
Controller: ND85-USB161-ISS (serial no: MCLC03519)

Analog input: 0V to 10V


# Computer
Dell Precision Tower 7910 (pz-rgen02-pdw01)
System drive (C): SSD (256gb)
Data drive (D): RAID10 volume (2tb; hardware RAID powered by `MegaRAID SAS 9361-8i` PCIe controller and 4 SAS HD)
USB3 connection for Flash4 camera: only on PCIe USB3 ports (card U3-PCIE1XG205-1S)


# Temperature regulation



# Flow control

ID | SN             | Use | Comments
---|----------------|-----|---------
1  | FLOW-02D-10228 | Ch1 | 
2  | FLOW-02D-10228 | Ch2 | 
3  | FLOW-02D-10228 |     | 


# Maintenance

## 20170220 (Thomas)
Installation completed.

- Micro-Manager installed in a directory whose path has no space (`/C/Programs/`)
- Flash4 v3 condifured using the v2-compatible mode
- fluorescence illumination manually centered (introducing a small tilt at the LLG port)
- hall effect sensors are not installed yet

# 20170411 (Thomas)
- upgraded MM2 to the last nightly build: fix the position name tag issue.

## 20200212 (Thomas)
- OS updated to Win 10 Enterprise LTSC (clone of TiVng1 computer)
- had to uninstall-reinstall ESI v 3.04 (NB: declined again NI request to disable Win "Fast startup")
- calibrated OB1 to -850;+5000 mbar range

- replaced LED controller (LEDD1B M00486934) with same model (M00493622). Disconnected the breakout box to hack TiDIA control. LED Controller now used in TRIG mode (intensity set by the manual knob).
