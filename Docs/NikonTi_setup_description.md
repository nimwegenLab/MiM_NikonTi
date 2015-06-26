
## Objectives

Magnification | NA    | WD (mm) | Phase contrast | Model
--------------|-------|---------|----------------|------
100x          | 1.45  | 0.13    | Ph3            | Plan Apo Lambda DM 100x oil (MRD31905)
60x           | 1.40  | 0.13    | Ph1 ??         | Plan Apo Lambda DM 60x oil (MRD31605)
10x           | 0.30  | 15.2    | Ph1            | Plan Fluor DL 10x (MRH20101)


## Condenser & Phase rings


# Fluorescence

## Spectra X

Color band (nm)   | Fluorophore	    | Excitation Filter	| Power (uW; 3 mm LLG)
------------------|-----------------|-------------------|---------------------
Violet (380-410)	| DAPI, Hoechst	  | 386/23            | 150	
Blue (420-455)	  | CFP             |	438/24            | 275	
Cyan (460-490)	  | GFP, FITC	      | 475/35            | 215	
Teal (500-520)	  | YFP	            | 513/17            | 65	
*Green*&#42; (535-600) | *TRITC*         | *560/25*	        | *380*	
*Yellow*&#42; (535-600)| *mCherry*       | *575/25*	        | *210*	
Red (620-750)	    | Cy5	            | 650/13	          | 105	
NIR	            | Cy7	            | 740/13	          | 40

Full table and more on http://www.biovis.com/lumencor_spectra-x.htm
&#42; These filters need to be exchanged manually.

## Filter cubes

Pos | Fluorophore                      | Beam splitter | Emission filter
----|----------------------------------|---------------|----------------
1   | DAPI                             | 416 (AHF)     | 460/50 (Chroma ET)
2   | CFP                              | 458 (AHF)     | 480/17 (Semrock BrightLine HC)
3   | [GFP](http://tiny.cc/6dvkzx)     | 495 (AHF)     | 525/50 (Chroma ET 265146)
4   | [YFP](http://tiny.cc/8evkzx)     | 520 (AHF)     | 542/27 (Semrock BrightLine HC)
5   | [mCherry](http://tiny.cc/egvkzx) | 594 (Chroma)  | 647/70 (DELTA TopPride)
6   | --                               | --            | --

to come: [RFP](http://tiny.cc/t9ukzx) 573 - 609/54 (Semrock BrightLine HC)

- Positions are written on the flat bottom of the turret.
- Filter cubes can be opened by pushing the lever toward the center of the emission filter.
- Chroma and Nikon filters: arrow toward dichroic.
  Omega and Semrock filters: arrow in the direction of light.

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

