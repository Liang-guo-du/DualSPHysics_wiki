The user can download the package from [http://dual.sphysics.org/index.php/downloads/](http://dual.sphysics.org/index.php/downloads/).

Figure 5-1 shows the structure of the content of **DualSPHysics_v4.2.**

<p align="center">
<img width="400px" src="https://i.imgur.com/YuJMXnR.png"/>
</p>

<p align="center">
<strong>Figure 5-1.</strong> Directory tree of the DualSPHysics v4.2 package.
</p>



**bin:**
* Contains the binaries executables for **linux** and **windows**. 
* Some libraries needed for the codes are also included.

**doc:**
* The folder **guides** contains the following PDF files:
  * DualSPHysics_v4.2_GUIDE.pdf: This manuscript.
  * DualSPHysics_v4.0_LiquidGas_GUIDE.pdf
  * XML_v4.2_GUIDE.pdf: Helps to create a new case using the input XML file and all XML parameters are explained and related to SPH equations.
  * ExternalModelsConversion_GUIDE.pdf: Describes how to convert the file format of any external geometry of a 3-D model to VTK, PLY or STL using open-source codes.
  * PostprocessingCalculations_v4.2.pdf: Explains how numerical magnitudes are computed.

 * The folder **help** contains files with description of the execution parameters of the different codes is presented in HELP_Code.out and templates of positions of points to be used with MeasureTool (FilePointsTemplate.txt, FilePointsPosTemplate.csv) and how to create domains with FlowTool (FileBoxesTemplate.txt) codes.
 * The folder **xml_format** contains CaseTemplate.xml, an XML with all the different labels and formats that can be used in the input file. It also contains the _FmtXML_XXX.xml files that are examples of the format and options of some special functionalities in XML (such as damping, wave paddles, etc.).

**examples:**
 * This directory contains examples of working cases. Each CASE directory includes input XML, batch scripts to execute the cases and additional files to be used for DualSPHysics code. The output files will be created in the same directory. 
 * The **main** examples will use the DualSPHysics_v4.2 executables
 * The examples in **twophases** will use the multiphase codes.
 * The **motion** folder contains the scripts to perform 9 examples with the different type of movements that can be described with DualSPHysics.

**src:**
 * The folder **source** contains the source files of v4.2 (.cpp, .cu and .h). The makefile of linux and the text file for CMAKE.txt are also included in this folder.
 * Visual studio (Community 2015) project for windows can be found in **VS**.
 * The libraries (_.a_ and _.lib_) necessary for compilation are included in **lib**.

**src_extra:**
 * The release includes not only the source files of DualSPHysics v4.2 but also the source files of a code named “ToVTK4”. This code is provided to show how to load particle data, how to read .bi4 files and how to create .vtk or .csv files.

**src_twophases:**
 * The source files of the of DualSPHysics_v4.0_LiquidGas are included here.
 
Figure 5-2 shows the workflow with representative example input and output files of the executable files. This figure will be used later to explain in detail each of the codes and the main tools.

<p align="center">
<img src="https://i.imgur.com/FlF8S7I.png"/>
</p>

<p align="center">
<strong>Figure 5-2.</strong> Workflow of DualSPHysics v4.2.
</p>

As mentioned before, each “example” directory includes batch scripts that can be used to run all the previous workflow shown in Figure 5-2. This batch files include the following steps:

1. The paths of the pre-processing, processing and post-processing tools are defined 
2. The name of the output folder is created using the name of the case.
3. GenCase is executed: this pre-processing tool creates the initial state of the particles (position, velocity and density) and defines the different SPH parameters for the simulation 
4. DualSPHysics is executed once the case was created with GenCase. The SPH solver is used to solve the fluid-fluid, fluid-solid and solid-solid interactions in order to define the time evolution of the system. Output files with state of the particles are stored in the output folder. By default, binary format is used.
5. Once the simulation is finished, different post-processing tools can be used to convert the binary output files into other formats to analyse the results (VTK, CSV…). Therefore, these post-processing codes are used to visualise the simulation or to compute magnitudes of interest (vorticity, surface elevation, forces, overtopping…).

<p align="center">
<img src="https://i.imgur.com/5DShKzg.png"/>
</p>

<p align="center">
<strong>Figure 5-3.</strong> Example of Case.bat (windows).
</p>