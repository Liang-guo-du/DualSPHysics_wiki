This section provides a brief description of the source files of DualSPHysics v4.0. The
source code is freely redistributable under the terms of the GNU General Public License
(GPL) as published by the Free Software Foundation (www.gnu.org/licenses/).

The documentation has been created using the documentation system Doxygen
(www.doxygen.org). The user can open the HTML file index.html (Figure 6-1) located
in the directory mentioned above to navigate through the full documentation.

## Common Files

### Functions.h & Functions.cpp
Declares/implements basic/general functions for the entire application.

### JBinaryData.h & JBinaryData.cpp
Declares/implements the class that defines any binary format of a file.

### JException.h & JException.cpp
Declares/implements the class that defines exceptions with the information of the class and method.

### JLog2.h & JLog2.cpp
Declares/implements the class that manages the output of information in the file Run.out and on screen.

### JMatrix4.h
Declares the template for a matrix 4x4 used for geometric transformation of points in space.

### JMeanValues.h & JMeanValues.cpp
Declares/implements the class that calculates the average value of a sequence of values.

### JObject.h & JObject.cpp
Declares/implements the class that defines objects with methods that throw exceptions.

### JObjectGpu.h & JObjectGpu.cpp
Declares/implements the class that defines objects with methods that throw exceptions for tasks on the
GPU.

### JPartDataBi4.h & JPartDataBi4.cpp
Declares/implements the class that allows reading files with data of particles in format bi4.

### JPartFloatBi4.h & JPartFloatBi4.cpp
Declares/implements the class that allows reading information of floating objects saved during
simulation.

### JPartOutBi4Save.h & JPartOutBi4Save.cpp
Declares/implements the class that allows writing information of excluded particles during simulation.

### JRadixSort.h & JRadixSort.cpp
Declares/implements the class that implements the algorithm RadixSort.

### JRangeFilter.h & JRangeFilter.cpp
Declares/implements the class that facilitates filtering values within a list.

### JReadDatafile.h & JReadDatafile.cpp
Declares/implements the class that allows reading data in ASCII files.

### JSpaceCtes.h & JSpaceCtes.cpp
Declares/implements the class that manages the info of constants from the input XML file.

### JSpaceEParms.h & JSpaceEParms.cpp
Declares/implements the class that manages the info of execution parameters from the input XML file.

### JSpaceParts.h & JSpaceParts.cpp
Declares/implements the class that manages the info of particles from the input XML file.

### JSpaceProperties.h & JSpaceProperties.cpp
Declares/implements the class that manages the properties assigned to the particles in the XML file.

### JTimer.h
Declares the class that defines a class to measure short time intervals.

### JTimerCuda.h
Declares the class that defines a class to measure short time intervals on the GPU using cudaEvent.

### TypesDef.h
Declares general types and functions for the entire application.

### JFormatFiles2.h
Declares the class that provides functions to store particle data in formats VTK, CSV, ASCII.

### JFormatFiles2.lib (libjformatfiles2.a)
Precompiled library that provides functions to store particle data in formats VTK, CSV, ASCII.

### JSphMotion.h
Declares the class that provides the displacement of moving objects during a time interval

### JSphMotion.lib (libjsphmotion.a)
Precompiled library that provides the displacement of moving objects during a time interval.

### JXml.h
Declares the class that helps to manage the XML document using library TinyXML

### JXml.lib (libjxml.a)
Precompiled library that helps to manage the XML document using library TinyXML.

### JWaveGen.h
Declares the class that implements wave generation for regular and irregular waves.

### JWaveGen.lib (libjwavegen.a)
Precompiled library that implements wave generation for regular and irregular waves.

## SPH Solver

### main.cpp
Main file of the project that executes the code on CPU or GPU.

### JCfgRun.h & JCfgRun.cpp
Declares/implements the class that defines the class responsible for collecting the execution parameters by
command line.

### JPartsLoad4.h & JPartsLoad4.cpp
Declares/implements the class that manages the initial load of particle data.

### JPartsOut.h & JPartsOut.cpp
Declares/implements the class that stores excluded particles at each instant until writing the output file.

### JSaveDt.h & JSaveDt.cpp
Declares/implements the class that manages the use of prefixed values of DT loaded from an input file.

### JSph.h & JSph.cpp
Declares/implements the class that defines all the attributes and functions that CPU and GPU simulations
share.

### JSphAccInput.h & JSphAccInput .cpp
Declares/implements the class that manages the application of external forces to different blocks of
particles (with the same MK).

### JSphDtFixed.h & JSphDtFixed.cpp
Declares/implements the class that manages the info of dt.

### JSphVisco.h & JSphVisco.cpp
Declares/implements the class that manages the use of viscosity values from an input file.

### JTimerClock.h
Defines a class to measure time intervals with precision of clock().

### JTimeOut.h & JTimeOut.cpp
Declares/implements the class that manages the use of variable output time to save PARTs.

### Types.h
Defines specific types for the SPH application.

## SPH Solver only for CPU executions

### JSphCpu.h & JSphCpu.cpp
Declares/implements the class that defines the attributes and functions used only in CPU simulations.

### JSphCpuSingle.h & JSphCpuSingle.cpp
Declares/implements the class that defines the attributes and functions used only in Single-CPU.

### JSphTimersCpu.h
Measures time intervals during CPU execution.

### JCellDivCpu.h & JCellDivCpu.cpp
Declares/implements the class responsible of generating the Neighbour List in CPU.

### JCellDivCpuSingle.h & JCellDivCpuSingle.cpp
Declares/implements the class responsible of generating the Neighbour List in Single-CPU.

### JArraysCpu.h & JArraysCpu.cpp
Declares/implements the class that manages arrays with memory allocated in CPU.

## SPH Solver only for GPU executions

### JSphGpu.h & JSphGpu.cpp
Declares/implements the class that defines the attributes and functions used only in GPU simulations.

### JSphGpu_ker.h & JSphGpu_ker.cu
Declares/implements functions and CUDA kernels for the Particle Interaction (PI) and System Update
(SU).

### JSphGpuSingle.h & JSphGpuSingle.cpp
Declares/implements the class that defines the attributes and functions used only in single-GPU.

### JSphTimersGpu.h
Measures time intervals during GPU execution.

### JCellDivGpu.h & JCellDivGpu.cpp
Declares/implements the class responsible of generating the Neighbour List in GPU.

### JCellDivGpu_ker.h & JCellDivGpu_ker.cu
Declares/implements functions and CUDA kernels to generate the Neighbour List in GPU.

### JCellDivGpuSingle.h & JCellDivGpuSingle.cpp
Declares/implements the class that defines the class responsible of generating the Neighbour List in
Single-GPU.

### JCellDivGpuSingle_ker.h & JCellDivGpuSingle_ker.cu
Declares/implements functions and CUDA kernels to compute operations of the Neighbour List.

### JArraysGpu.h & JArraysGpu.cpp
Declares/implements the class that manages arrays with memory allocated in GPU.

### JBlockSizeAuto.h & JBlockSizeAuto.cpp
Declares/implements the class that manages the automatic computation of optimum Blocksize in kernel
interactions.

## CPU source files
The source file JSphCpuSingle.cpp can be better understood with the help of the
diagram of calls represented in Figure 6-2. Note that now particle interactions are no
longer performed in terms of cells as used in previous versions.

<p align="center">
<img src="https://i.imgur.com/Bu7tmkr.png"/>
</p>

<p align="center">
<img src="https://i.imgur.com/GYVqD73.png"/>
</p>

<p align="center">
<strong>Figure 6-2.</strong> Workflow of JSphCpuSingle.cpp when using Verlet time algorithm.
</p>

When the Symplectic timestepping integration scheme is used the step is split in
predictor and corrector steps. Thus, Figure 6-3 shows the workflow and calls of the
CPU code using this time scheme:

<p align="center">
<img src="https://i.imgur.com/PxjXocW.png"/>
</p>

<p align="center">
<img src="https://i.imgur.com/oxzRrCo.png"/>
</p>

<p align="center">
<strong>Figure 6-3.</strong> Workflow of JSphCpuSingle.cpp when using Symplectic timestepping algorithm
</p>

Note that JSphCpu::Interaction_Forces performs the particle interaction in CPU using
the template InteractionForcesT. Thus, the interaction between particles is carried out
considering different parameters and considering the type of particles involved in the
interaction as it can be seen in Figure 6-4 and Table 6-2:

<p align="center">
<img src="https://i.imgur.com/MevDRYk.png"/>
</p>

<p align="center">
<strong>Figure 6-4.</strong> Call graph for the template InteractionForcesT.
</p>

<p align="center">
<img src="https://i.imgur.com/Ql5kni9.png"/>
</p>

<p align="center">
<strong>Table 6-2.</strong> Different particle interactions can be performed depending on the type of particles.
</p>

As mentioned before, a more complete documentation has been generated using
Doxygen.

## GPU source files

The source file JSphGpuSingle.cpp can be better understood with the workflow
represented in Figure 6-5 that includes the functions implemented in the GPU files. The
dashed boxes indicates the CUDA kernels implemented in the CUDA files
(JSphGpu_ker.cu).

<p align="center">
<img src="https://i.imgur.com/9uCX0eg.png"/>
</p>

<p align="center">
<img src="https://i.imgur.com/B8i8Npv.jpg"/>
</p>

<p align="center">
<strong>Figure 6-5.</strong> Workflow of JSphGpuSingle.cpp when using Verlet time algorithm.
</p>