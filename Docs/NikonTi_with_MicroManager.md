---
title: "Instructions for using [vng] Nikon Ti with Micro-Manager"
author: Thomas Julou
output: html_document
---


# Fluorescence illumination

## Using the correct preset after exchanging a cube



## Acquiring fluorescence excitation flatfield images
- in MiM Tools>Options, uncheck "Save XY positions in separate stack files".
- adjust illumination and exposure in main window. Select an area of the fluorescent slide without dust nor bubbles.
- in MDA, check only "Multiple positions". In position list, use "Create grid", press "..." 5 times, then "Center Here", and finally "OK" (this should create a list of 25 positions). Acquire!
- Check that there is no position with an unexpected illumination pattern (e.g. bubbles) 
- Save as image stack file.

## Fluorescence excitation timing using the SpectraX

from Lumencor support: 

> When the filters are installed inside the SPECTRA X, then the total time to switch between colors is only limited by speed of turning one channel OFF (~10 micro-seconds) and the next channel ON (~5 micro-seconds). If you install those filters in the microscope, then the performance limitation will be the speed of your filter wheel.
> 
> The electronic switching of the Green and Yellow filters is actually a feature of the SPECTRA and not the SPECTRA X. The SPECTRA has all internally mounted and non-exchangeable excitation filters. The Green and Yellow filters are mounted on a solenoid and so a TTL pulse to that cable will switch between the Green/Yellow filters. Your SPECTRA X has quickly exchangeable filters, but loses that single feature.
> 
> For your application (using several filter sets excited by the same LED), it sounds like you would be best served by installing the Green and Yellow excitation filters in your microscope. That is quicker than manually swapping the filter paddle in the SPECTRA X. The other channels would be best with the excitation filter in place within the SPECTRA X.

# Transmitted light illumination

For phase contrast, use the manual GIF filter and the diffuser (D). With our 100x objective, use phase ring Ph3.
Adjust the focus and the centering of the condenser to achieve Kohler illumination.


# PFS autofocus

from http://micro-manager.3463995.n2.nabble.com/Perfect-Focus-and-MDA-tp7582535p7582551.html

> In summary, there are mainly two ways to use the PFS with Micro-Manager MDA (in 1.4.16): 
> 
> 1. Continuous. Turn on PFS on the microscope stand and uncheck Autofocus in the MDA. This works well for simple samples (e.g. a single coverslip) when you are imaging a simple XY position, or multiple XY positions with moderate Z change between positions. There must also be no focus-disrupting barriers between positions (such as well edges). 
> 
> 2. Per-frame. Check Autofocus in the MDA windows, configure Autofocus to use PFSStatus, and make sure to turn off PFS on the microscope stand before starting. If using multiple XY positions, make sure to include the Z drive in the position list (see Kurt's explanation above). Including the PFSOffset in the position list is optional (include only if you want different offsets per position). 


# Flash4 camera

The Flash camera uses an sCMOS chip which has a uniquely high quantum efficiency but at the cist of variable pixels readout noise and gain. In order to compensate for those pixels innacuracy, the default camera behaviour is to replace them in real-time by their neighbours average. In order to disable this feature, set the property "DEFECT CORRECT MODE" TO OFF.

