Smoothed Particle Hydrodynamics is a Lagrangian meshless method that has been used
in an expanding range of applications within the field of Computation Fluid Dynamics
(CFD) [Gómez-Gesteira et al., 2010] where particles represent the flow, interact with
structures, and exhibit large deformation with moving boundaries. The SPH model is
approaching a mature stage for CFD with continuing improvements and modifications
such that the accuracy, stability and reliability of the model are reaching an acceptable
level for practical engineering applications.

The DualSPHysics code originates from SPHysics, which is an open-source SPH model
developed by researchers at the Johns Hopkins University (US), the University of Vigo
(Spain), the University of Manchester (UK) and the University of Rome, La Sapienza.
The software is available to free download at [www.sphysics.org](http://www.sphysics.org). A complete guide of
the FORTRAN code is found in [Gómez-Gesteira et al., 2012a; 2012b].

The SPHysics FORTRAN code was validated for different problems of wave breaking
[Dalrymple and Rogers, 2006], dam-break behaviour [Crespo et al., 2008], interaction
with coastal structures [Gómez-Gesteira and Dalrymple, 2004] or with a moving
breakwater [Rogers et al., 2010].

Although SPHysics allows problems to be simulated using high resolution and a wide
range of formulations, the main problem for its application to real engineering problems
is the excessively long computational runtimes, meaning that SPHysics is rarely applied
to large domains. Hardware acceleration and parallel computing are required to make
SPHysics more useful and versatile for engineering application.

Originating from the computer games industry, Graphics Processing Units (GPUs) have
now established themselves as a cheap alternative to High Performance Computing
(HPC) for scientific computing and numerical modelling. GPUs are designed to manage
huge amounts of data and their computing power has developed in recent years much
faster than conventional central processing units (CPUs). Compute Unified Device
Architecture (CUDA) is a parallel programming framework and language for GPU
computing using some extensions to the C/C++ language. Researchers and engineers of
different fields are achieving high speedups implementing their codes with the CUDA
language. Thus, the parallel power computing of GPUs can be also applied for SPH
methods where the same loops for each particle during the simulation can be
parallelised.

The FORTRAN SPHysics code is robust and reliable but is not properly optimised for
huge simulations. DualSPHysics is implemented in C++ and CUDA language to carry
out simulations on either the CPU or GPU respectively. The new CPU code presents
some advantages, such as more optimised use of the memory. The object-oriented
programming paradigm provides a code that is easy to understand, maintain and modify
with a sophisticated control of errors available. Furthermore, better optimisations are
implemented, for example particles are reordered to give faster access to memory, and
the best approach to create the neighbour list is implemented [Domínguez et al., 2011].
The CUDA language manages the parallel execution of threads on the GPUs. The best
approaches were considered to be implemented as an extension of the C++ code, so the
most appropriate optimizations to parallelise particle interaction on GPU were
implemented [Domínguez et al., 2013a; 2013b]. The first rigorous validations were
presented in [Crespo et al., 2011]. The version 3.0 of the code is fully documented in
[Crespo et al., 2015].

Version 4 of the code has been developed to include the latest developments including
coupling with the Discrete Element Method (DEM) and multi-phase developments as
detailed in Section 3.

In the following sections we will describe the SPH formulation available in
DualSPHysics, the implementation and optimization techniques, how to compile and
run the different codes of the DualSPHysics package and future developments.