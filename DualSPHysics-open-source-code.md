This section provides a brief description of the source files of DualSPHysics v4.2. The source code is freely redistributable under the terms of LGPL v2.1- GNU Lesser General Public License (LGPL) as published by the Free Software Foundation ([www.gnu.org/licenses/](www.gnu.org/licenses/)). 

Thus, users can download the files from DualSPHysics_v4.2/src. 

A complete list of these source files is summarised in Table 6-1. Some files are shared with other codes such as GenCase, BoundaryVTK, PartVTK, PartVTKOut, MeasureTool and IsoSurface. The rest of the files implement the SPH solver, some of them are used both for CPU/GPU executions and others are specific.

<p align="center">
<img src="https://i.imgur.com/sLCH6VJ.png"/>
</p>
<p align="center">
<img src="https://i.imgur.com/bSPABnU.png"/>
</p>
<p align="center">
<strong>Table 6-1.</strong> List of source files of DualSPHysics v4.2 code.
</p>

## COMMON:

### Functions.h & Functions.cpp
Declares/implements basic/general functions for the entire application.

### FunctionsMath.h & FunctionsMath.cpp
Declares/implements basic/general math functions.

### JDsphConfig.h & JDsphConfig.cpp
Declares/implements the class that loads configuration from DphConfig.xml.

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

### JParticlesDef.h 
Defines type of particles and basic methods for particles.

### JPeriodicDef.h
Defines type of periodic conditions and basic functionalities.

### JRadixSort.h & JRadixSort.cpp
Declares/implements the class that implements the algorithm RadixSort.

### JRangeFilter.h & JRangeFilter.cpp
Declares/implements the class that facilitates filtering values within a list.

### JReadDatafile.h & JReadDatafile.cpp
Declares/implements the class that allows reading data in ASCII files. 

### JSaveCsv2.h & JSaveCsv2.cpp
Declares/implements the class that create CSV files. 

### JSpaceCtes.h & JSpaceCtes.cpp
Declares/implements the class that manages the info of constants from the input XML file.

### JSpaceEParms.h & JSpaceEParms.cpp
Declares/implements the class that manages the info of execution parameters from the input XML file.

### JSpaceParts.h & JSpaceParts.cpp
Declares/implements the class that manages the info of particles from the input XML file.

### JSpaceProperties.h & JSpaceProperties.cpp
Declares/implements the class that manages the properties assigned to the particles in the XML file.

### JTimeControl.h & JTimeControl.cpp
Declares/implements the class that manages the information of runtime in long processes.

### JTimer.h 
Declares the class that defines a class to measure short time intervals.

### JTimerClock.h 
Declares the class to measure time intervals with precision of clock().

### JXml.h & JXml.cpp
Declares the class that helps to manage the XML document using library TinyXML.

### TypesDef.h
Declares general types and functions for the entire application.

## COMMON_BINARYFILES:

### JBinaryData.h & JBinaryData.cpp
Declares/implements the class that defines any binary format of a file. 

### JPartDataBi4.h & JPartDataBi4.cpp
Declares/implements the class that allows reading files with data of particles in format bi4.

### JPartDataHead.h & JPartDataHead.cpp
Declares/implements the class that manages the information of simulation data.

### JPartFloatBi4.h & JPartFloatBi4.cpp
Declares/implements the class that allows reading information of floating objects saved during simulation.

### JPartOutBi4Save.h & JPartOutBi4Save.cpp
Declares/implements the class that allows writing information of excluded particles during simulation.

### COMMON_GPU:

### FunctionsCuda.h & FunctionsCuda.cpp
Declares/implements basic/general GPU functions for the entire application.

### FunctionsMath_ker.cu
Declares/implements basic/general math functions for the GPU execution.

### JObjectGpu.h & JObjectGpu.cpp
Declares/implements the class that defines objects with methods that throw exceptions for tasks on the GPU.

### JReduSum_ker.h &  JReduSum_ker.cu
Declares/implements the class that defines objects with methods that throw exceptions for tasks on the GPU.

### JTimerCuda.h 
Declares the class that defines a class to measure short time intervals on the GPU using cudaEvent.

## COMMON_LIBJFORMATFILES2:

### JFormatFiles2.h
Declares the class that provides functions to store particle data in formats VTK, CSV, ASCII and geometric elements in VTK format

### JFormatFiles2_x64.lib (libjformatfiles2_64.a)
Precompiled library that provides functions to store particle data in formats VTK, CSV, ASCII and geometric elements in VTK format

## COMMON_LIBJWAVEGEN:

### JWaveGen.h
Declares the class that implements wave generation for regular and irregular waves.

### JWaveOrder2_ker.h & JWaveOrder2_ker.cu
Declares/implements functions and CUDA kernels for second order irregular wave generation.

### JWaveSpectrumGpu.h & JWaveSpectrumGpu.cpp
Declares/implements the class that manages the GPU computations for irregular wave generation.

### JWaveGen_x64.lib (libjwavegen_64.a)
Precompiled library that implements wave generation for regular and irregular waves.

## COMMON_MOTION:

### JMotion.h & JMotion.CPP
Declares/ implements the class that provides the displacement of moving objects during a time interval.

### JMotionEvent.h
Declares the class that manages events for motions.  

### JMotionList.h & JMotionList.cpp
Declares/implements the classes that manages the state and the list of different motions.

### JMotionMov.h & JMotionMov.cpp
Declares/implements the class that defines data for each motion type.

### JMotionObj.h & JMotionObj.cpp
Declares/implements the classes that manages the active motions and the hierarchy of motions.

### JMotionPos.h & JMotionPos.cpp
Declares/implements the class that manages the position of objects.

## SPH SOLVER:

### main.cpp
Main file of the project that executes the code on CPU or GPU.

### JCfgRun.h & JCfgRun.cpp
Declares/implements the class that defines the class responsible for collecting the execution parameters by command line.

### JDamping.h & JDamping.cpp
Declares/implements the class that manages the info of damping zones. 

### JGaugeItem.h & JGaugeItem.cpp
Declares/implements the class that defines the common part of different gauge types.

### JGaugeSystem.h & JGaugeSystem.cpp
Declares/implements the class that manages the list of configured gauge.

### JPartsLoad4.h & JPartsLoad4.cpp
Declares/implements the class that manages the initial load of particle data.

### JPartsOut.h & JPartsOut.cpp
Declares/implements the class that stores excluded particles at each instant until writing the output file.

### JSaveDt.h & JSaveDt.cpp
Declares/implements the class that manages the use of prefixed values of DT loaded from an input file.

### JSph.h & JSph.cpp
Declares/implements the class that defines all the attributes and functions CPU & GPU simulations share.

### JSphAccInput.h & JSphAccInput .cpp
Declares/implements the class that manages the external forces applied to different blocks of particles.

### JSphDtFixed.h & JSphDtFixed.cpp
Declares/implements the class that manages the info of dt.

### JSphInitialize.h & JSphInitialize.cpp
Declares/implements the class that manages the info of particles from the input XML file.

### JSphMk.h & JSphMk.cpp
Declares/implements the class that manages the info of particles according Mk.

### JSphMotion.h & JSphMotion.cpp
Declares/implements the class that provides the displacement for moving particles during a time interval.

### JSphVisco.h & JSphVisco.cpp
Declares/implements the class that manages the use of viscosity values from an input file.

### JTimeOut.h & JTimeOut.cpp
Declares/implements the class that manages the use of variable output time to save PARTs.

### OmpDefs.h 
Defines constants to use of OpenMP.

### Types.h 
Defines specific types for the SPH application.

## SPH SOLVER ONLY FOR CPU EXECUTIONS:

### JArraysCpu.h & JArraysCpu.cpp
Declares/implements the class that manages arrays with memory allocated in CPU.

### JCellDivCpu.h & JCellDivCpu.cpp
Declares/implements the class responsible of generating the Neighbour List in CPU.

### JCellDivCpuSingle.h & JCellDivCpuSingle.cpp
Declares/implements the class responsible of generating the Neighbour List in Single-CPU.

### JSphCpu.h & JSphCpu.cpp
Declares/implements the class that defines the attributes and functions used only in CPU simulations.

### JSphCpuSingle.h & JSphCpuSingle.cpp
Declares/implements the class that defines the attributes and functions used only in Single-CPU.

### JSphTimersCpu.h
Measures time intervals during CPU execution.

## SPH SOLVER ONLY FOR GPU EXECUTIONS:

### JArraysGpu.h & JArraysGpu.cpp
Declares/implements the class that manages arrays with memory allocated in GPU.

### JBlockSizeAuto.h & JBlockSizeAuto.cpp
Declares/implements the class that manages the automatic computation of optimum Blocksize.

### JCellDivGpu.h & JCellDivGpu.cpp
Declares/implements the class responsible of generating the Neighbour List (NL) in GPU.

### JCellDivGpu_ker.h & JCellDivGpu_ker.cu
Declares/implements functions and CUDA kernels to generate the NL in GPU.

### JCellDivGpuSingle.h & JCellDivGpuSingle.cpp
Declares/implements the class that defines the class responsible of generating the NL in Single-GPU.

### JCellDivGpuSingle_ker.h & JCellDivGpuSingle_ker.cu
Declares/implements functions and CUDA kernels to compute operations of the NL.

### JGauge_ker.h & JGauge_ker.cu
Declares/implements functions and CUDA kernels for classes that manage gauges.

### JSphGpu.h & JSphGpu.cpp
Declares/implements the class that defines the attributes and functions used only in GPU simulations.

### JSphGpu_ker.h & JSphGpu_ker.cu
Declares/implements functions and CUDA kernels for the Particle Interaction and System Update.

### JSphGpuSingle.h & JSphGpuSingle.cpp
Declares/implements the class that defines the attributes and functions used only in single-GPU.

### JSphTimersGpu.h
Measures time intervals during GPU execution.

## CPU Source files
The source file **JSphCpuSingle.cpp** can be better understood with the help of the diagram of calls represented in Figure 6-1. Note that now particle interactions are no longer performed in terms of cells as used in previous versions.

<p align="center">
<img src="https://i.imgur.com/o7t9E1h.png"/>
</p>
<p align="center">
<img src="https://i.imgur.com/TS63t6H.png"/>
</p>

<p align="center">
<strong>Figure 6-1.</strong> Workflow of <strong>JSphCpuSingle.cpp</strong> (v4.0) when using Verlet time algorithm
</p>

When the Symplectic time integration scheme is used the step is split in predictor and corrector steps. Thus, Figure 6-2 shows the workflow and calls of the CPU code using this time scheme:

<p align="center">
<img src="https://i.imgur.com/anNNKsn.jpg"/>
</p>
<p align="center">
<img src="https://i.imgur.com/AvpEFkq.png"/>
</p>

<p align="center">
<strong>Figure 6-2.</strong> Workflow of JSphCpuSingle.cpp (v4.0) when using Symplectic time algorithm.
</p>

Note that _JSphCpu::Interaction_Forces_ performs the particle interaction in CPU using the template _InteractionForcesT_. Thus, the interaction between particles is carried out considering different parameters and considering the type of particles involved in the interaction as it can be seen in Figure 6-3 and Table 6-2:

<p align="center">
<img src="https://i.imgur.com/CwUqQWU.png" width="400px" />
</p>

<p align="center">
<strong>Figure 6-3.</strong> Call graph for the template InteractionForcesT (v4.0).
</p>

<p align="center">
<strong>Table 6-2.</strong> Different particle interactions can be performed depending on the type of particles.
</p>

<p align="center">
<img src="https://i.imgur.com/a3hSy5u.png"/>
</p>

## GPU source files

The source file **JSphGpuSingle.cpp** can be better understood with the workflow represented in Figure 6-4 that includes the functions implemented in the GPU files. The dashed boxes indicate the CUDA kernels implemented in the CUDA files (_JSphGpu_ker.cu_).

<p align="center">
<img src="https://i.imgur.com/13pZSp5.jpg"/>
</p>
<p align="center">
<img src="https://i.imgur.com/A8XR8WV.png"/>
</p>
<p align="center">
<img src="https://i.imgur.com/nqhtVzt.png"/>
</p>

<p align="center">
<strong>Figure 6-4.</strong> Workflow of <strong>JSphGpuSingle.cpp</strong> (v4.0) when using Verlet time algorithm.
</p>