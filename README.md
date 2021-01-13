# Marine Energy Collegiate Competition (MECC)

This respository provides examples of running a Sphere and the RM3 in the Boundary Element solvers [NEMOH](https://github.com/LHEEA/Nemoh) and [Capytaine](https://github.com/mancellin/capytaine).


**Instructions for using Capytaine examples:**
1. conda install Capytaine using Anaconda or GitHub (Use Python 3.7, there might be a bug with using Capytaine in Python 3.8)
2. conda install meshmagick
3. Use the demo.py or call_capytaine.py + CASE.py for examples on how to run Capytaine for a geometry (imported from a mesh, or created with Capytaine). The demo.py script walks through the basic steps necessary for getting a Capytaine case up and running. Also see the user manual and cookbook in the Capytaine documentation for getting started, examples and moving past a basic case.

In each case folder (/RM3, /Sphere):
* Hydrostatics.dat, KH.dat - same as Nemoh hydrostatics files for each body. This MUST be created outside of Capytaine's current capabilities. See body_hydrostatics() in call_capytaine.py
* .dat, .gdf - sample meshes for each geometry
* CASE.nc - Capytaine output file. Read with BEMIO Read_CAPYTAINE() function
* CASE.py - sample of how to call capytaine using an additional wrapper

In Capytaine/ directory:
* call_capytaine.py - example of a wrapper used with the CASE.py scripts to call_capytaine easily and consistently for multiple cases. See body_hydrostatics() function for a method to get and output the hydrostatic stiffness (KH.dat) and center of gravity, center of buoyancy, displaced volume (Hydrostatics.dat) 
* demo.py - sample script that creates / loads a mesh and calls capytaine for it


