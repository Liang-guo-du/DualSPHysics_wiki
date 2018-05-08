**Creating new cases**

There are more information in **doc/help** that will guide users to create their own cases:
* XML_GUIDE_v4.2.pdf
* ExternalModelsConversion_GUIDE.pdf

<br>
<br>

**Source files of the SPH solver**

To add new formulation or changes, the following files (in **src/source**) are the ones that require your attention:

CPU and GPU executions: 	
* main.cpp
* JCfgRun (.h .cpp)
* JSph (.h .cpp)
* JSphMk (.h .cpp)
* JPartsLoad4 (.h .cpp)
* JPartsOut (.h .cpp)     
* ParticlesDef.h
* Types.h

For only CPU executions: 	
* JSphCpu (.h .cpp)
* JSphCpu (.h .cpp)
* JSphCpuSingle (.h .cpp)
* JCellDivCpu (.h .cpp)
* JCellDivCpuSingle (.h .cpp)

For only GPU executions: 	
* JSphGpu (.h .cpp)
* JSphGpu_ker (.h .cu)
* JSphGpuSingle (.h .cpp)
* JCellDivGpu (.h .cpp)
* JCellDivGpu_ker (.h .cu)
* JCellDivGpuSingle (.h .cpp)
* JCellDivGpuSingle_ker (.h .cu)

Please read [Section 6](https://github.com/DualSPHysics/DualSPHysics/wiki/DualSPHysics-open-source-code) for a complete description of these files.

<br>
<br>

**Example code “ToVtk”**

The release includes not only the source files of DualSPHysics v4.2 but also the source files of a code named “ToVtk”. This code is provided to show how to load and interpret particle data, how to read .bi4 files and how to create .vtk or .csv files.

<br>
<br>

**New variables defined by the user in DualSPHysics and in the post-processing tools**

In the actual code, the particle data to be stored in the .bi4 files are: id, position, velocity and density. Other magnitudes such as mass, pressure, acceleration, vorticity, etc are computed starting from the first ones using the post-processing tools. However, the .bi4 format allows adding new arrays with particle data defined by the user, which can be managed by the post-processing codes.

Therefore, in order to store new data arrays in the .bi4 files, the user should follow the example included in the source files of DualSPHysics. The example is included in the function _SavePartData()_ in the file **JSph.cpp** and shows how to store (in .bi4) an array with pressure of the particles computed starting from density. This example is explained here:

<p align="center">
<img src="https://imgur.com/xBXRP3M.png"/>
</p>

The new data arrays introduced by the users in the .bi4 files are recognized by the post-processing tools (PartVTK4, MeasureTool4 y IsoSurface4). If we want to obtain these data in VTK or CSV files, then the option **–vars:name** should be used.

Following, an example with PartVTK4 to obtain the data “Pressure” is shown:

_PartVTK4_win64.exe –dirin . -savevtk parts –vars:pressure_


