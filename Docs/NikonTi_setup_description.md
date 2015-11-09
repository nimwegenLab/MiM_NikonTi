
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
1   | [CFP](http://tiny.cc/ksnu5x)     | --                 | 458 (AHF)     | 480/17 (Semrock BrightLine HC
*1* | *DAPI*                           | --                 | 416 (AHF)     | 460/50 (Chroma ET)
2   | [GFP](http://tiny.cc/6dvkzx)     | --                 | 495 (AHF)     | 525/50 (Chroma ET 265146)
*2* | [*YFP*](http://tiny.cc/8evkzx)   | --                 | 520 (AHF)     | 542/27 (Semrock BrightLine HC)
3   | [RFP](http://tiny.cc/t9ukzx)     | 560/25 (Semrock)   | 573 (Chroma)  | 609/54 (Semrock BrightLine HC)
4   | [mCherry](http://tiny.cc/egvkzx) | 575/25 (Semrock)   | 594 (Chroma)  | 647/70 (DELTA TopPride)
5   | [Cy5.5](http://tiny.cc/k6mu5x)   |--                  | 700 (Semrock) | 775/140 (Semrock BrightLine HC)
6   | --                               | --                 | --            | --


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


# Computer
Dell Optiplex 990 (pz-kben01-pdw06)


# Maintenance

## 20150131
SpectraX illumination aligned and characterized (Thomas).

## 20150619
20150619: characterization of Flash4 read noise (Thomas).\
using 2s exposure and Defect Correct Mode ON, with a capped camera (light in the room??)

20150626: characterization of Flash4 gain (Thomas).\
pseudo-unifrom illumination of the sensor is achieved using an iphone (min brightness, flashlight app at 100%; Plane mode ON and on charge), the GIF filter of NikonTi TRANS illumination and 3 plastic cups as a diffuser (with their side covered by black paper).
use a modified version of Sturman's camera lab to acquire 20 different exposures (from 13 to 1950 ms; stored as stack slices) with 200 images for each exposure.
Defect Correct Mode ON.

## To do
- check field diaphragm for fluo excitation
- measure power for all filter sets (e.g. at 2")

