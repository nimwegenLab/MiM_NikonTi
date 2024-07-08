---
title: "Parts description for `TiVng1`"
author: Thomas Julou
output: html_document
---

### Important: this setup has been upgraded to a Nikon Ti2 model, see more at https://github.com/nimwegenLab/MiM_NikonTi2/blob/master/Docs/Ti2Vng1_parts_log.md.

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

Note that this pressure controller is the legacy MK3 and hence unable to connect to digital flow meters.

ID | SN           | Use | Comments
---|--------------|-----|---------
1  | FLOW-02-4854 |     | was clogged by GW in 09.2016, cleaned up and in use again since 12.2016
2  | FLOW-02-4852 |     | formerly Ch2: clogged by GW
3  | FLOW-02-4853 | Ch1 | used for Ch1 since 10-11.2016
4  | FLOW-02-4855 | Ch2 | used for Ch2: clogged by TJ



# Maintenance

The maintenance log of this setup lives in [our group wiki](https://wiki.biozentrum.unibas.ch/x/LxP9Fg).
