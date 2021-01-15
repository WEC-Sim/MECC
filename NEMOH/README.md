# Nemoh

This readme is intended to be a quick guide for getting started with Nemoh v113 or v115 - using the Sphere and RM3 examples provided. For more detailed information about how to use Nemoh, please refer to the [documentation provided by ECN](https://lheea.ec-nantes.fr/valorisation/logiciels-et-brevets/nemoh-presentation). 

## Downloading Nemoh

There are two Nemoh versions available:
- [Nemoh v113](https://github.com/LHEEA/Nemoh): The latest official release of Nemoh available from Ecole Centrale de Nantes.
- [Nemoh v115](https://github.com/izabala123/Nemoh): A more recent version of Nemoh, for which @izabala123 has kindly provided good quality builds.

Nemoh v115 has superior accuracy (including irregular frequency removal capabilities), whereas the binaries included with Nemoh v113 are faster.

Once you have selected a version, download or clone the code's repository to your machine.

## Overview of the Nemoh project folders

- Main input files

  | Filename          | Description                                       |
  |-------------------|---------------------------------------------------|
  | `Nemoh.cal`       | Main input file                                   |
  | `Mesh.cal`        | Required by Mesh.exe for hydrostatic calculations |
  | `ID.dat`          | ID of the calculation                             |
  | `input.txt`       | Some parameters for the solver                    |
  | `{modelName}.png` | Just a screenshot of the system's mesh(es) for visualization |
  | `bemio.m`         | Not part of Nemoh; this script will post-process the Nemoh results and create a WEC-Sim compatible `.h5` file |

- `Mesh/` directory

  Contains the mesh file(s) that should be provided by the user (i.e. `float.dat` & `spar.dat` for RM3, `sphere.dat` for Sphere). The files `Hydrostatics.dat` and `KH.dat` are created by Nemoh's hydrostatics solver.

- `Results/` directory

  Contains the hydrodynamic coefficients for excitation force, radiation damping and added mass

For more detailed descriptions about the contents and format of these files, please refer to the [Nemoh documentation](https://lheea.ec-nantes.fr/valorisation/logiciels-et-brevets/nemoh-running).

## Running Nemoh

### v113

In v113 the Nemoh executables are seperate:
- `Mesh.exe`
    Computes hydrostatic properties of a single mesh.
- `preProcessor.exe`
    Prepares the mesh and defines all of the problems to be solved
- `Solver.exe`
    The main Nemoh program; this sequentially solves each frequency domain problem
- `postProcessor.exe`
    Post-processes the frequency domain data to obtain added mass, radiation damping in a more standard format. Also computes radiation impulse response functions (RIRFs) if they are defined in `Nemoh.cal`

### v115

In Nemoh v115, all of the functionality of Nemoh is available from a single executable - `Nemoh.exe`. Check [the Nemoh v115 repo](https://github.com/izabala123/Nemoh) documentation for more information about which arguments to pass when you call `Nemoh.exe` from the command line.

### Calling the `.exe` program(s)

Whether running Nemoh v113 or v115, the program is called from the command line at the Nemoh project folder. A quick and easy way to get the command line here is `Shift` + `Right click` on the project folder (i.e. Sphere) and then select `'Open PowerShell window here'`.

Once you have your command line at the project folder there are two options for calling the programs:

- add the directory containing the Nemoh `.exe` file(s) (e.g `C:\code\Nemoh\bin\GNU`) to your PATH (requires admin rights) and just call `Nemoh` directly at the command line
- pass the complete path to the `.exe` file to the command line (e.g. `C:\work\MECC\Nemoh\Sphere> C:\code\Nemoh\bin\GNU\Nemoh.exe -all`)

## Post-processing results for WEC-Sim

After Nemoh has computed all of the hydrodynamic coefficients, `bemio.m` can be run to post-process the data and create a `.h5` file that WEC-Sim can read for time-domain modelling.
