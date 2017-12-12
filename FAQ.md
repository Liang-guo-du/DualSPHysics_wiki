# What do I need to use DualSPHysics? What are the hardware and software requirements?\

DualSPHysics can be executed either on CPU or GPU. In order to use DualSPHysics
code on a GPU, you need a CUDA-enabled Nvidia GPU card on your machine
(http://developer.nvidia.com/cuda-gpus). 

If you want to run GPU simulations (i.e. not
develop the source code) the latest version of the driver for your graphics card must be
installed. If no source code development is required, there is no need to install any
compiler to run the binary of the code, only the driver must be updated. If you also want
to compile the code you must install the nvcc compiler and a C++ compiler. The nvcc
compiler is included in the CUDA Toolkit that can be downloaded from the Nvidia
website and must be installed on your machine.

## Why DualSPHysics binary is not running?

If you are trying to run the executable GPU version on a CUDA-enabled Nvidia GPU
card, the error message: Exception (JSphGpuSingle::SelecDevice)
Text: Failed getting devices info. (CUDA error: CUDA driver version is insufficient for CUDA runtime version)
can be solved by installing the latest version of the driver for the GPU card.

## How can I compile the code with different environments/compilers?

The provided source files in this release can be compiled for linux using a ‘makefile’
along with gcc and nvcc compilers, and for windows using a project for Visual Studio
(both VS2010 and VS2013 are provided). In case you use another compiler or other
environment, you can adjust the contents of the makefile or you can also use CMAKE.

Please refer to [section 6 on Compiling DualSPHysics](Compiling-DualSPHysics)

## How many particles can I simulate with the GPU code?

The amount of particles that can be simulated depends on (i) the memory space of the
GPU card and (ii) the options of the simulation.

## How should I start looking at the source code?

Section [DualSPHysics open-source code](DualSPHysics-open-source-code) of the guide introduces the source files including some call graphs for a better
understanding and it is also highly recommended that you read the documentation
generated with [Doxygen](www.doxygen.org).

## How can I create my own geometry?

Users can follow the provided example cases in the package. Those input XML files can
be modified following XML_GUIDE_v4.0.pdf. Different input formats of real
geometries can be converted using ExternalModelsConversion_GUIDE.pdf. This
manuscript also describes in detail the input files of the different test cases.

## How can I contribute to the project?

You can contribute to the DualSPHysics project by reporting bugs, suggesting new
improvements, citing DualSPHysics [See the answer to Question 24] in your paper if
you use it, submitting your modified codes together with examples.

To read more info on that, please refer to the [repository main page](https://github.com/DualSPHysics/DualSPHysics)

## How can I modify the code of the precompiled libraries?

Some code is provided in precompiled libraries to reduce the number of source files and
to facilitate the comprehension of only the SPH algorithms by the users. These
precompiled code covers secondary aspects during SPH simulations that are only used
in specific simulations so they are not used in most of the cases. If the user wants to
modify some of the codes included in the precompiled libraries, he can just replace that
library by his own implementation.

## How does the code define the limits of the domain?

In the input XML file, the parameters pointmin and pointmax only define the domain to
create particles beyond these limits fluid or boundary particles will not be created. The
limits of the computational domain are computed at the beginning of the DualSPHysics
simulation and use the initial minimum and maximum positions of the particles that
were already created with GenCase. In order to modify the limits automatically
computed by DualSPHysics, different execution parameters can be used:
-domain_particles[:xmin,ymin,zmin,xmax,ymax,zmax]
-domain_particles_prc:xmin,ymin,zmin,xmax,ymax,zmax
-domain_fixed:xmin,ymin,zmin,xmax,ymax,zmax
so that the limits can be specified instead of using initial particle positions.

## How can I define the movement of boundaries?

Examples of the different type of movements that can be described with DualSPHysics
are addressed in directory MOTION. Different kind of movements can be defined such
as rectilinear, rotational, sinusoidal or circular motion and they can be uniform or
accelerated, with pauses or with hierarchy of movements. And a final option is to load
the movement from an external file with a prescribed movement (info of time, X-
position, Y-position, Z-position and velocities) or with rotational movement (info of
time, angle) that will be interpolated at each time step during the simulation (see
CaseSloshingMotion).

## How can I include a new type of movement?

A new movement can be always defined by using an external file with mvfile or
mvrotfile where the desired movement can be computed in advance and loaded from
that file. However if a user wants to create the new type of movement in the source
code, this should be implemented in the functions JSphCpu::RunMotion() for CPU or
JSphGpu::RunMotion() for GPU, since the code implemented now is in the library
JSphMotion.

## How do I prevent the boundary particles from going outside of the domain limits when applying motion?

As explained in the previous question, the limits of the computational domain are
computed starting from the initial minimum and maximum positions of the particles.
Since these values use the initial configuration, any movement of boundaries that
implies positions beyond these limits will give us the error ‘boundary particles out the
domain’. The solutions to solve this problem and to avoid creating larger tanks or
domains are:
* defining boundary points <drawpoint> at the minimum and maximum positions
that the particles are expected to reach during the simulation. The option
<drawpoint> will create a particle at the given location x,y,z.
* using the parameters of DualSPHysics execution mentioned in the answer to
Question 9.


## Why do I observe a gap between boundaries, floating bodies and fluid in the solution?

The gap is a result of pressure overestimation across density discontinuities. It is
inherent to the boundary formulation used in DualSPHysics. The forces exerted by the
boundary particles create a small gap between them and fluid particles (1.5 times h).
Note that by increasing the resolution (i.e. using a smaller “dp”) the gap is reduced
however new boundary conditions are being developed and should be available in future
releases [Domínguez et al., 2015].

## How do I prevent the fluid particles from penetrating inside floating bodies?

Validation of floating using experimental data from [Hadzic et al., 2005], as shown in
http://dual.sphysics.org/index.php/validation/wavesfloatings/, has been performed only
for floating objects created with <setdrawmode mode="full" /> or <setdrawmode
mode="solid" />, therefore the use of these options is suggested. In this way, floating
particles are created in the faces of the object and inside the object so no particle
penetration will be observed.

## How do I numerically compute the motion and rotations of floating bodies?

The new code FloatingInfo allows to obtain different variables of interest of the floating
objects during the simulation; positions of the center, linear velocity, angular velocity,
motions (surge, sway and heave) and angles of rotation (pitch, roll and yaw). As shown
in http://dual.sphysics.org/index.php/validation/wavesfloatings/, the study of a floating
body subjected to a wave packet is validated with data from [Hadzic et al., 2005].

## When are fluid particles excluded from the simulation?

Fluid particles are excluded during the simulation: (i) if their positions are outside the
limits of the domain, (ii) when density values are out of a range (700-1300 by default),
(iii) when particles moves beyond 0.9 times the cell size during one time step.

## How do I create a 2-D simulation?

DualSPHysics can also perform 2-D simulations. To generate a 2-D configuration you
only have to change the XML file; imposing the same values in the Y-direction that
define the limits of the domain where particles are created (pointmin.y=1 and
pointmax.y=1).

## How can I solve the error “Constant 'b' cannot be zero”?

Constant ‘b’ appears in the equation of state (Eq. 14). Constant ‘b’ is zero when fluid
height (hswl) is zero (or fluid particles were not created) or if gravity is zero.
First, you should check that fluid particles have been created. Possible errors can appear
in 2-D simulations when the seed point of the option <fillbox> is not located at the
correct y-position. Other solution is to specify the value of ‘hswl’ in <constantsdef>
<hswl value="0.8" auto="false" />). When using gravity zero, the value of ‘b’ needs to
be specified in <constantsdef> (<b value="1.1200e+05" auto="false" />) as occurs in
CaseMovingSquare.

## How can I create a case without gravity?

When using gravity zero, the value of ‘b’ needs to be specified in <constantsdef> (<b
value="1.1200e+05" auto="false" />) as occurs in CaseMovingSquare. Otherwise, ‘b’ is
zero and gives the error shown in Question 18.

## How can I define the speed of sound?

By default, the speed of sound (speedofsound=coefsound*speedsystem) is calculated as
10∙sqrt(g*hswl). In order to calculate a more suitable ‘speedofsound‘ for a particular
case requires the user to set the parameters ‘coefsound‘ and ‘speedsystem‘.

## What is the recommended alpha value in artificial viscosity?

The value of α=0.01 has proven to give the best results in the validation of wave flumes
to study wave propagation and wave loadings exerted onto coastal structures [Altomare
et al., 2015a; 2015c]. However in the simulation of other cases such as dam-breaks, the
interaction between fluid and boundaries during dam propagation becomes more
relevant and the value of α should be changed according to the resolution (“dp”) to
obtain accurate results.

## How can I define new properties of the particles?

The file format XML offers several resources to define new general parameters or
specific properties for different type of particles. In order to load parameters from the
section <parameters>, the user can mimic how this is also carried out by DualSPHysics.
If different properties will be defined for different fluid volumes, section <properties>
can be used (that is also explained in the XML guide).

## How can I store new properties of the particles (e. g. Temperature)?

The new file format (.bi4) and the post-processing tools have been designed to include
new properties defined by the user for its own implementation. The function
JSph::SavePartData() already includes an example of how to store new particle data.
Then, the post-processing codes will automatically manage all variables included in the
.bi4 files.

## How must I cite the use of the code in my paper?

Please refer to the code if you use it in a paper with reference [Crespo et al., 2015].
