The main code which performs the SPH simulation is named DualSPHysics.

The input files to run DualSPHysics code include one XML file (Case.xml in Figure
10-1) and a binary file (Case.bi4 in Figure 10-1). Case.xml contains all the parameters
of the system configuration and its execution such as key variables (smoothing length,
reference density, gravity, coefficients to compute pressure starting from density, speed
of sound...), the number of particles in the system, movement definition of moving
boundaries and properties of moving bodies. The binary file Case.bi4 contains the
particle data; arrays of position, velocity and density and headers. The output files
consist of binary format files with the particle information at different instants of the
simulation (Part0000.bi4, Part0001.bi4, Part0002.bi4 ...) file with excluded particles
(PartOut.obi4) and text file with execution log (Run.out).

<p align="center">
<img src="https://i.imgur.com/4VFnlMt.png"/>
</p>

<p align="center">
<strong>Figure 10-1.</strong> Input (red) and output (blue) files of DualSPHysics code.
</p>

Different parameters defined in the XML file can be be changed using executions
parameters of DualSPHysics: time stepping algorithm specifying Symplectic or Verlet
(-symplectic, -verlet[:steps]) , choice of kernel function which can be Cubic or Wendland (-
cubic, -wendland), the value for artificial viscosity (-viscoart: <float>) or laminar+SPS
viscosity treatment (-viscolamsps:<float>), activation of the Delta-SPH formulation (-
deltasph: <float>), use of shifting algorithm (-shifting: <mode>) the maximum time of
simulation and time intervals to save the output data (-tmax:, -tout:). To run the code, it is
also necessary to specify whether the simulation is going to run in CPU or GPU mode (-
cpu, -gpu[:id]), the format of the output files ( -sv:[formats,...], none, binx, ascii, vtk, csv), that
summarises the execution process (-svres:<0/1>) with the computational time of each
individual process (-svtimers:<0/1>). It is also possible to exclude particles as being out of
limits according to prescribed minimum and maximum values of density (-
rhopout:min:max) or that travel further than maximum Z position (-incz:<float>).

For CPU executions, a multi-core implementation using OpenMP enables executions in
parallel using the different cores of the machine. It takes the maximum number of cores
of the device by default or users can specify it ( -ompthreads:<int>). On the other hand,
different cell divisions of the domain can be used (-cellmode:<mode>) that differ in
memory usage and efficiency.

One of the novelties version 4 of DualSPHysics is the use of double precision in
variables of position of the particles (-posdouble:<mode>) for the computation of particle
interactions. The particle interaction is one of the most time-consuming parts of the
simulation, hence the precision in this part can be controlled using the -posdouble
parameter, which takes the following values:

* 0: particle interaction is performed using single precision for position variables (x, y, z)
When “dp” is much smaller than size of the domain, the user is recommended to choose
one of the following:
* 1: particle interaction is performed using double precision for position variables but
final position is stored using simple precision
* 2: particle interaction is performed using double precision for position variables and
final position is stored using double precision.

Other important novelty in v4.0 is the determination of the optimum BlockSize for the
CUDA kernels that execute particle interaction (-blocksize:<mode>):

* Fixed (-blocksize:0): A fixed block size of 128 threads is used. This value does not
always provides the maximum performance but it usually offers good performance for
those type of kernels.
* Occupancy (-blocksize:1): Occupancy Calculator of CUDA is used to determine the
optimum block size according to the features of the kernel (registers and shared memory
however data used in the kernels are not considered). This option is available from
CUDA 6.5
* Empirical (-blocksize:2): Here, data used in the CUDA kernels is also considered. The
optimum BlockSize is evaluated every certain number of steps (500 by default). In this
way, block size can change during the simulation according to input data.



