

# Using Nikon Ti with Micro-Manager
## PFS autofocus

from http://micro-manager.3463995.n2.nabble.com/Perfect-Focus-and-MDA-tp7582535p7582551.html

	In summary, there are mainly two ways to use the PFS with Micro-Manager 
	MDA (in 1.4.16): 

	1. Continuous. Turn on PFS on the microscope stand and uncheck Autofocus 
	in the MDA. This works well for simple samples (e.g. a single coverslip) 
	when you are imaging a simple XY position, or multiple XY positions with 
	moderate Z change between positions. There must also be no 
	focus-disrupting barriers between positions (such as well edges). 

	2. Per-frame. Check Autofocus in the MDA windows, configure Autofocus to 
	use PFSStatus, and make sure to turn off PFS on the microscope stand 
	before starting. If using multiple XY positions, make sure to include 
	the Z drive in the position list (see Kurt's explanation above). 
	Including the PFSOffset in the position list is optional (include only 
	if you want different offsets per position). 

