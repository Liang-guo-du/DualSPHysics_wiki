### SPH formulation
Smoothed Particle Hydrodynamics (SPH) is a Lagrangian meshless method. The
technique discretises a continuum using a set of material points or particles. When used
for the simulation of fluid dynamics, the discretised Navier-Stokes equations are locally
integrated at the location of each of these particles, according to the physical properties
of surrounding particles. The set of neighbouring particles is determined by a distance
based function, either circular (two-dimensional) or spherical (three-dimensional), with
an associated characteristic length or smoothing length often denoted as h. At each timestep
new physical quantities are calculated for each particle, and they then move
according to the updated values.

The conservation laws of continuum fluid dynamics are transformed from their partial
differential form to a form suitable for particle based simulation using integral equations
based on an interpolation function, which gives an estimate of values at a specific point.

Typically this interpolation or weighting function is referred to as the kernel function
(W) and can take different forms, with the most common being cubic or quintic. In all
cases however, it is designed to represent a function F(r) defined in r' by the integral
approximation

<p align="center">
<img src="https://i.imgur.com/4e3Yt3G.png"/> (1)
</p>

The smoothing kernel must fulfil several properties [Monaghan, 1992; Liu, 2003], such
as positivity inside a defined zone of interaction, compact support, normalization and
monotonically decreasing value with distance and differentiability. For a more complete
description of SPH, the reader is referred to [Monaghan, 2005; Violeau, 2013].

The function F in Eq. (1) can be approximated in a non-continuous, discrete form based
on the set of particles. In this case the function is interpolated at a particle (a) where a
summation is performed over all the particles that fall within its region of compact
support, as defined by the smoothing length h

<p align="center">
<img src="https://i.imgur.com/IdTUGJG.png"/> (2)
</p>

where the subscript denotes an individual particle, <img src="https://i.imgur.com/RGDPJWd.png" height="24"> is the volume of a neighbouring particle (b). If <img src="https://i.imgur.com/j1FPDqE.png" height="24">, with m and ρ being the mass and the density of particle b respectively then Eq. (2) becomes

<p align="center">
<img src="https://i.imgur.com/rqu0cyp.png"/> (3)
</p>

### The Smoothing Kernel
The performance of an SPH model depends heavily on the choice of the smoothing kernel. Kernels are expressed as a function of the non-dimensional distance between particles (q), given by <img src="https://i.imgur.com/WPAV5NO.png" height="24"> , where r is the distance between any two given particles a and b and the parameter h (the smoothing length) controls the size of the area around particle a in which neighbouring particles are considered. Within DualSPHysics, the user is able to choose from one of the following kernel definitions:

1. Cubic Spline
<p align="center">
<img src="https://i.imgur.com/jyEuS6x.png"/> (4)
</p>

where αD is equal to 10/7πh2 in 2-D and 1/πh3 in 3-D.

The tensile correction method, proposed by [Monaghan, 2000], is only actively used in
the cases of a kernel whose first derivative goes to zero with the particle distance q.

2. Quintic
<p align="center">
<img src="https://i.imgur.com/g0lkaup.png"/> (5)
</p>
where αD is equal to 7/4πh2 in 2-D and 21/16πh3 in 3-D.

In the text that follows, only kernels with an influence domain of 2h (q≤2) are
considered

### Momentum Equation
The momentum conservation equation in a continuum is

<p align="center">
<img src="https://i.imgur.com/5tlgjt0.png"/> (6)
</p>

where Γ refers to dissipative terms and g is gravitational acceleration. DualSPHysics
offers different options for including the effects of dissipation.

### Artificial Viscosity
The artificial viscosity scheme, proposed by [Monaghan, 1992], is a common method
within fluid simulation using SPH due primarily to its simplicity. In SPH notation, Eq. 6
can be written as

<p align="center">
<img src="https://i.imgur.com/6MwDAHJ.png"/> (7)
</p>

where Pk and ρk are the pressure and density that correspond to particle k (as evaluated
at a or b). The viscosity term <a src="https://i.imgur.com/jIBQoNg.png" /> is given by

<p align="center">
<img src="https://i.imgur.com/PNAdFht.png"/> (8)
</p>

where ab <img src="https://i.imgur.com/TBytuDT.png" /> and <img src="https://i.imgur.com/TBytuDT.png" /> with rk and vk being the particle position and velocity respectively. <img src="https://i.imgur.com/0WtDphK.png" /> is the mean speed of sound, <img src="https://i.imgur.com/z8fQyJ8.png"/> and α is a coefficient that needs to be tuned in order to introduce the proper dissipation. The value of α=0.01 has proven to give the best results in the
validation of wave flumes to study wave propagation and wave loadings exerted onto
coastal structures [Altomare et al., 2015a; 2015c].

### Laminar viscosity and Sub-Particle Scale (SPS) Turbulence
Laminar viscous stresses in the momentum equation can be expressed as [Lo and Shao,
2002]

<p align="center">
<img src="https://i.imgur.com/P7BXWYL.png"/> (9)
</p>

where υo is kinematic viscosity (typically 10-6 m2s for water). In SPH discrete notation
this can be expressed as

<p align="center">
<img src="https://i.imgur.com/UhXKZwz.png"/> (10)
</p>

The concept of the Sub-Particle Scale (SPS) was first described by [Gotoh et al., 2001]
to represent the effects of turbulence in their Moving Particle Semi-implicit (MPS)
model. The momentum conservation equation is defined as

<p align="center">
<img src="https://i.imgur.com/PrCkxCv.png"/> (11)
</p>

where the laminar term is treated as per Eq. 9 and <img src="https://i.imgur.com/GCGmUXz.png" /> represents the SPS stress tensor. Favre-averaging is needed to account for compressibility in weakly compressible SPH
[Dalrymple and Rogers, 2006] where eddy viscosity assumption is used to model the
SPS stress tensor with Einstein notation for the shear stress component in coordinate
directions i and <img src="https://i.imgur.com/EIcEFR6.png" /> where <img src="https://i.imgur.com/Ijsxbkq.png" /> is the sub-particle stress
tensor, <img src="https://i.imgur.com/cETvBL8.png" /> the turbulent eddy viscosity, k the SPS turbulence kinetic
energy, Cs the Smagorinsky constant (0.12), CI=0.0066, <img src="https://i.imgur.com/HS6vhQh.png" /> the particle to particle spacing and <img src="https://i.imgur.com/ogsos8j.png" /> where <img src="https://i.imgur.com/CaDoLwa.png" /> is an element of the SPS strain tensor. [Dalrymple and Rogers, 2006] introduced SPS into weakly compressible SPH using Favre averaging, Eq.11 can be re-written as

<p align="center">
<img src="https://i.imgur.com/RUG9SJF.png"/> (12)
</p>

### Continuity Equation
Throughout the duration of a weakly-compressible SPH simulation (as presented
herein) the mass of each particle remains constant and only their associated density
fluctuates. These density changes are computed by solving the conservation of mass, or
continuity equation, in SPH form:

<p align="center">
<img src="https://i.imgur.com/FiRiMTm.png"/> (13)
</p>

### Equation of State
Following the work of [Monaghan, 1994], the fluid in the SPH formalism defined in
DualSPHysics is treated as weakly compressible and an equation of state is used to
determine fluid pressure based on particle density. The compressibility is adjusted so that
the speed of sound can be artificially lowered; this means that the size of time step taken
at any one moment (which is determined according to a Courant condition, based on the
currently calculated speed of sound for all particles) can be maintained at a reasonable
value. Such adjustment however, restricts the sound speed to be at least ten times faster
than the maximum fluid velocity, keeping density variations to within less than 1%, and
therefore not introducing major deviations from an incompressible approach. Following
[Monaghan et al., 1999] and [Batchelor, 1974], the relationship between pressure and
density follows the expression

<p align="center">
<img src="https://i.imgur.com/zbT9A4G.png"/> (14)
</p>

where <img src="https://i.imgur.com/noiD8EZ.png" /> where <img src="https://i.imgur.com/b9ppfL9.png" /> is the reference density and <img src="https://i.imgur.com/xDA7oho.png" /> which is the speed of sound at the reference density.

### DeltaSPH
Within DualSPHysics it is also possible to apply a delta-SPH formulation, that
introduces a diffusive term to reduce density fluctuations. The state equation describes a
very stiff density field, and together with the natural disordering of the Lagrangian
particles, high-frequency low amplitude oscillations are found to populate the density
scalar field [Molteni and Colagrossi, 2009]. DualSPHysics uses a diffusive term in the
continuity equation, now written as

<p align="center">
<img src="https://i.imgur.com/DlqtjTc.png"/> (15)
</p>

This represents the original delta-SPH formulation by [Molteni and Colagrossi, 2009],
with the free parameter δΦ that needs to be attributed a suitable value. This modification
can be explained as the addition of the Laplacian of the density field to the continuity
equation. [Antuono et al., 2012] has presented a careful analysis of the influence of this
term in the system, by decomposing the Laplacian operator, observing the converge of
the operators and performing linear stability analysis to inspect the influence of the
diffusive coefficient. This equation represents exactly a diffusive term in the domain
bulk. The behaviour changes close to open boundaries such as free-surface. Due to
truncation of the kernel (there are no particles being sampled outside of an open
boundary), the first-order contributions are not null [Antuono et al., 2010], resulting in a
net force applied to the particles. This effect is not considered relevant for nonhydrostatic
situations, where this force is many orders of magnitude inferior to any
other force involved. Corrections to this effect were proposed by [Antuono et al., 2010],
but involve the solution of a renormalization problem for the density gradient, with
considerable computational cost. A delta-SPH (δΦ) coefficient of 0.1 is recommended
for most applications.

### Shifting algorithm
Anisotropic particle spacing is an important stability issue in SPH as, especially in
violent flows, particles cannot maintain a uniform distribution. The result is the
introduction of noise in the velocity and pressure field, as well as the creation of voids
within the water flow for certain cases.

To counter the anisotropic particle spacing, [Xu et al., 2009] proposed a particle shifting
algorithm to prevent the instabilities. The algorithm was first created for incompressible
SPH, but can be extended to the weakly compressible SPH model used in
DualSPHysics [Vacondio et al., 2013]. With the shifting algorithm, the particles are
moved (“shifted”) towards areas with fewer particles (lower particle concentration)
allowing the domain to maintain a uniform particle distribution and eliminating any
voids that may occur due to the noise.

An improvement on the initial shifting algorithm was proposed by [Lind et al., 2012]
who used Fick’s first law of diffusion to control the shifting magnitude and direction.
Fick’s first law connects the diffusion flux to the concentration gradient:

<p align="center">
<img src="https://i.imgur.com/N4Ufk40.png"/> (16)
</p>

where J is the flux, C the particle concentration, and DF the Fickian diffusion
coefficient.

Assuming that the flux, i.e. the number of particles passing through a unit surface in
unit time, is proportional to the velocity of the particles, a particle shifting velocity and
subsequently a particle shifting distance can be found. Using the particle concentration,
the particle shifting distance δrs is given by:

<p align="center">
<img src="https://i.imgur.com/UZtavpb.png"/> (17)
</p>

where D is a new diffusion coefficient that controls the shifting magnitude and absorbs
the constants of proportionality. The gradient of the particle concentration can be found
through an SPH gradient operator:

<p align="center">
<img src="https://i.imgur.com/c6fJZ7j.png"/> (18)
</p>

The proportionality coefficient D is computed through a form proposed by [Skillen et
al., 2013]. It is set to be large enough to provide effective particle shifting, while not
introducing significant errors or instabilities. This is achieved by performing a Von
Neumann stability analysis of the advection-diffusion equation:

<p align="center">
<img src="https://i.imgur.com/6d2cuqH.png"/> (19)
</p>

where Δtmax is the maximum local time step that is permitted by the CFL condition for a
given local velocity and particle spacing. The CFL condition states that:

<p align="center">
<img src="https://i.imgur.com/14FfvsR.png"/> (20)
</p>

Combining Eq. 19 and 20 we can derive an equation to find the shifting coefficient D:

<p align="center">
<img src="https://i.imgur.com/H42Ukai.png"/> (21)
</p>

where A is a dimensionless constant that is independent of the problem setup and
discretization and dt is the current time step. Values in the range of [1,6] are proposed
with 2 used as default.

The shifting algorithm is heavily dependent on a full kernel support. However, particles
at and adjacent to the free surface cannot obtain the full kernel support, which will
introduce errors in the free-surface prediction, potentially causing non-physical
instabilities. Applying Fick’s law directly would result in the rapid diffusion of fluid
particles from the fluid bulk, due to the large concentration gradients at the free surface.

To counter this effect, [Lind et al., 2012] proposed a free-surface correction that limits
diffusion to the surface normal but allow shifting on the tangent to the free surface.
Therefore, this correction is only used near the free surface, identified by the value of
the particle divergence, which is computed through the following equation, first
proposed by [Lee et al., 2008]:

<p align="center">
<img src="https://i.imgur.com/x6jnVya.png"/> (22)
</p>

This idea is applied to the DualSPHysics code by multiplying the shifting distance of
Equation (17) with a free-surface correction coefficient AFSC.

<p align="center">
<img src="https://i.imgur.com/o0itVZQ.png"/> (23)
</p>

where AFST is the free-surface threshold and AFSM is the maximum value of the particle
divergence. The latter depends on the domain dimensions:

<p align="center">
<img src="https://i.imgur.com/Yz8AusQ.png"/>
</p>

while the free surface threshold is selected for DualSPHysics as:

<p align="center">
<img src="https://i.imgur.com/SE2ii1z.png"/>
</p>

To identify the position of the particle relative to the free surface, the difference of the
particle divergence to AFST is used. Therefore, the full shifting equation (Eq. 17) with the
free surface correction is:

<p align="center">
<img src="https://i.imgur.com/QmCK73E.png"/> (24)
</p>

More information about the shifting implementation can be found in [Mokos, 2013].

### Time stepping
DualSPHysics includes a choice of numerical integration schemes, if the momentum
( a v ), density ( aρ ) and position ( ar ) equations are first written in the form

<p align="center">
<img src="https://i.imgur.com/6To5XZ6.png"/> (25a)
</p>

<p align="center">
<img src="https://i.imgur.com/nwaHq9H.png"/> (25b)
</p>

<p align="center">
<img src="https://i.imgur.com/rKZRGSy.png"/> (25c)
</p>

These equations are integrated in time using a computationally simple Verlet based
scheme or a more numerically stable but computationally intensive two-stage
Symplectic method.

### Verlet Scheme

This algorithm, which is based on the common Verlet method [Verlet, 1967] is split into
two parts and benefits from providing a low computational overhead compared to some
other integration techniques, primarily as it does not require multiple (i.e. predictor and
corrector) calculations for each step. The predictor step calculates the variables
according to

<p align="center">
<img src="https://i.imgur.com/wLSEvHM.png"/> (26)
</p>

where the superscript n denotes the time step, <img src="https://i.imgur.com/whgd5aw.png" /> and <img src="https://i.imgur.com/987U2FG.png"/> are calculated using Eq. 7 (or. 12) and Eq. 13 (or Eq. 14) respectively.
However, once every Ns time steps (where <img src="https://i.imgur.com/G7dLnjK.png" /> is suggested), variables are
calculated according to

<p align="center">
<img src="https://i.imgur.com/9kxzvgj.png"/> (27)
</p>

This second part is designed to stop divergence of integrated values through time as the
equations are no longer coupled. In cases where the Verlet scheme is used but it is
found that numerical stability is an issue, it may be sensible to increase the frequency at
which the second part of this scheme is applied, however if it should be necessary to
increase this frequency beyond Ns = 10 then this could indicate that the scheme is not
able to capture the dynamics of the case in hand suitably and the Symplectic scheme
should be used instead.

### Symplectic Scheme
Symplectic integration algorithms are time reversible in the absence of friction or
viscous effects [Leimkuhler, 1996]. They can also preserve geometric features, such as
the energy time-reversal symmetry present in the equations of motion, leading to
improved resolution of long term solution behaviour. The scheme used here is an
explicit second-order Symplectic scheme with an accuracy in time of O(Δt2) and
involves a predictor and corrector stage.

During the predictor stage the values of acceleration and density are estimated at the
middle of the time step according to

<p align="center">
<img src="https://i.imgur.com/0zYVbhV.png"/> (28)
</p>

During the corrector stage <img src="https://i.imgur.com/5Q2jRFx.png" /> is used to calculate the corrected velocity, and therefore position, of the particles at the end of the time step according to

<p align="center">
<img src="https://i.imgur.com/9DeYCq7.png"/> (29)
</p>

and finally the corrected value of density <img src="https://i.imgur.com/8L1BQ6U.png" /> is calculated using the
updated values of <img src="https://i.imgur.com/LRxMXgJ.png" /> and <img src="https://i.imgur.com/brH2R8E.png" /> [Monaghan, 2005].

### Variable Time Step
With explicit time integration schemes the timestep is dependent on the Courant-
Friedrichs-Lewy (CFL) condition, the forcing terms and the viscous diffusion term. A
variable time step Δt is calculated according to [Monaghan et al., 1999] using

<p align="center">
<img src="https://i.imgur.com/NphKClh.png"/> (30)
</p>

where Δtf is based on the force per unit mass (|fa|), and Δtcv combines the Courant and
the viscous time step controls.

### Boundary Conditions
In DualSPHysics, the boundary is described by a set of particles that are considered as a
separate set to the fluid particles. The software currently provides functionality for solid
impermeable and periodic open boundaries. Methods to allow boundary particles to be
moved according to fixed forcing functions are also present.

Dynamic Boundary Condition

The Dynamic Boundary Condition (DBC) is the default method provided by
DualSPHysics [Crespo et al., 2007]. This method sees boundary particles that satisfy the
same equations as fluid particles, however they do not move according to the forces
exerted on them. Instead, they remain either fixed in position or move according to an
imposed/assigned motion function (i.e. moving objects such as gates, wave-makers or
floating objects).

When a fluid particle approaches a boundary and the distance between its particles and
the fluid particle becomes smaller than twice the smoothing length (h), the density of
the affected boundary particles increases, resulting in a pressure increase. In turn this
results in a repulsive force being exerted on the fluid particle due to the pressure term in
the momentum equation.

Stability of this method relies on the length of time step taken being suitably short in
order to handle the highest present velocity of any fluid particles currently interacting
with boundary particles and is therefore an important point when considering how the
variable time step is calculated.

Different boundary conditions have been tested in DualSPHysics in the work of
[Domínguez et al., 2015]: Dynamic Boundary Condition (DBC), Local Uniform
STencil (LUST) and Boundary Integral (INTEGRAL). Validations with dam-break
flows and sloshing tanks highlighted the advantages and drawbacks of each method.

Periodic Open Boundary Condition

DualSPHysics provides support for open boundaries in the form of a periodic boundary
condition. This is achieved by allowing particles that are near an open lateral boundary
to interact with the fluid particles near the complimentary open lateral boundary on the
other side of the domain.

In effect, the compact support kernel of a particle is clipped by the nearest open
boundary and the remainder of its clipped support applied at the complimentary open
boundary [Gómez-Gesteira et al., 2012a].

Pre-imposed Boundary Motion

Within DualSPHysics it is possible to define a pre-imposed movement for a set of
boundary particles. Various predefined movement functions are available as well as the
ability to assign a time-dependant input file containing kinematic detail.
These boundary particles behave as a DBC described in Section 3.8.1, however rather
than being fixed, they move independently of the forces currently acting upon them.
This provides the ability to define complex simulation scenarios (i.e. a wave-making
paddle) as the boundaries influence the fluid particles appropriately as they move.

Fluid-driven Objects

It is also possible to derive the movement of an object by considering its interaction
with fluid particles and using these forces to drive its motion. This can be achieved by
summing the force contributions for an entire body. By assuming that the body is rigid,
the net force on each boundary particle is computed according to the sum of the
contributions of all surrounding fluid particles according to the designated kernel
function and smoothing length. Each boundary particle k therefore experiences a force
per unit mass given by

<p align="center">
<img src="https://i.imgur.com/KwwcVCU.png"/> (31)
</p>

where fka is the force per unit mass exerted by the fluid particle a on the boundary
particle k, which is given by

<p align="center">
<img src="https://i.imgur.com/SPQDcgI.png"/> (32)
</p>

For the motion of the moving body, the basic equations of rigid body dynamics can then
be used

<p align="center">
<img src="https://i.imgur.com/CiL3M8k.png"/> (33a)
</p>

<p align="center">
<img src="https://i.imgur.com/X8baOKr.png"/> (33b)
</p>

where M is the mass of the object, I the moment of inertia, V the velocity, Ω the
rotational velocity and R0 the centre of mass. Equations 33a and 33b are integrated in
time in order to predict the values of V and Ω for the beginning of the next time step.
Each boundary particle within the body then has a velocity given by

<p align="center">
<img src="https://i.imgur.com/UiKDdyy.png"/> (34)
</p>

Finally, the boundary particles within the rigid body are moved by integrating Eq. 34 in
time. The works of [Monaghan et al., 2003] and [Monaghan, 2005] show that this
technique conserves both linear and angular momentum. [Bouscasse et al., 2013]
presented successful validations of nonlinear water wave interaction with floating
bodies in SPH comparing with experimental data from [Hadzić et al., 2005] that
includes deformations in the free-surface due to the presence of floating boxes and the
movement of those objects during the experiment (heave, surge and roll displacements).
Several validations using DualSPHysics are performed in [Canelas et al., 2015] that
analyse the buoyancy-driven motion with solid objects larger than the smallest flow
scales and with various densities. They compared SPH numerical results with analytical
solutions, with other numerical methods [Fekken, 2004] and with experimental
measurements.

### Wave Generation

Wave generation is included in this version of DualSPHysics, for long-crested waves
only. In this way, the numerical model can be used to simulate a physical wave flume.
Both regular and random waves can be generated. The following sections refer only to
the piston-type wavemaker.

First order wave generation

The Biesel transfer functions express the relation between wave amplitude and
wavemaker displacement [Biesel and Suquet, 1951], under the assumption of
irrotational and incompressible fluid and constant pressure at the free surface. The
transfer function links the displacement of the piston-type wavemaker to the water
surface elevation, under the hypothesis of monochromatic sinusoidal waves in one
dimension in the x-direction:

<p align="center">
<img src="https://i.imgur.com/09DGr2k.png"/> (35)
</p>

where H is the wave height, d the water depth, x is distance and δ is the initial phase.
The quantity ω=2π/T is the angular frequency and k=2π/L is the wave number with T
equal to the wave period and L the wave length. The initial phase δ is given by a random
number between 0 and 2π.

Eq. 35 expresses the surface elevation at infinity that Biesel defined as the far-field
solution. The Biesel function can be derived for the far-field solution and for a pistontype
wavemaker as:

<p align="center">
<img src="https://i.imgur.com/SvRgilX.png"/> (36)
</p>

where S0 is the piston stroke. Once the piston stroke is defined, the time series of the
piston movement is given by:

<p align="center">
<img src="https://i.imgur.com/IrxhSZv.png"/> (37)
</p>

Second order wave generation

The implementation of a second order wavemaker theory will prevent the generation of
spurious secondary waves. The second order wave generation theory implemented in
DualSPHysics is based on [Madsen, 1971] who developed a simple second-order
wavemaker theory to generate long second order Stokes waves that would not change
shape as they propagated. The theory proposed by [Madsen, 1971] is straightforward,
controllable, computationally inexpensive with efficient results, and is accurate for
waves of first and second order.

The piston stroke S0 can be redefined from Eq. 36 as S0=H/m1 where:

<p align="center">
<img src="https://i.imgur.com/pMrwuHN.png"/> (38)
</p>

Following [Madsen, 1971], to generate a wave of second order, an extra term must be
added to Eq. 37. This term, for piston-type wavemaker, is equal to:

<p align="center">
<img src="https://i.imgur.com/HP1yidE.png"/> (39)
</p>

Therefore, the piston displacement, for regular waves, is the summation of Eq. 37 and
Eq. 39:

<p align="center">
<img src="https://i.imgur.com/vHigijQ.png"/> (40)
</p>

Madsen limited the application of this approximate second order wavemaker theory to
waves that complied with the condition given by HL2/d3 < 8π2/3. A specific warning is
implemented in DualSPHysics to inform the user whether or not this condition is
fulfilled.

First order wave generation of irregular waves

Monochromatic waves are not representative of sea states that characterise real wave
storm conditions. Sea waves are mostly random or irregular in nature. Irregular wave
generation is performed in DualSPHysics based on [Liu and Frigaard, 2001]. Starting from an assigned wave spectra, the Biesel transfer function (Eq. 36) is applied to each
component in which the spectrum is discretised. The procedure for the generation of
irregular waves is summarised as follows:

1. Defining the wave spectrum through its characteristic parameters (peak frequency,
spectrum shape, etc.).
2. Dividing the spectrum into N parts (N>50) in the interval (fstart, fstop), where generally
the values assumed by the spectrum (Sη) at the extremes of this interval are smaller
than the value assumed for the peak frequency, fp: Sη(fstart)≤0.01·Sη(fp) and
Sη(fstop) ≤ 0.01 · Sη(fp).
3. The frequency band width is so-defined as Δf=(fstop-fstart)/N. The irregular wave is
decomposed into N linear waves.
4. Determining the angular frequency ωi, amplitude ai and initial phase δi (random
number between 0 and 2π) of each i-th linear wave. The angular frequency ωi and
amplitude ai can therefore be expressed as follows:

<p align="center">
<img src="https://i.imgur.com/BX5XM7z.png"/> (41)
</p>

<p align="center">
<img src="https://i.imgur.com/RlBhsSH.png"/> (42)
</p>

5. Converting the time series of surface elevation into the time series of piston
movement with the help of Biesel transfer function:

<p align="center">
<img src="https://i.imgur.com/pE2Y1vl.png"/> (43)
</p>

6. Composing all the i-th components derived from the previous equation into the time
series of the piston displacement as:

<p align="center">
<img src="https://i.imgur.com/5XfBBNK.png"/> (44)
</p>

In DualSPHysics two standard wave spectra have been implemented and used to
generate irregular waves: JONSWAP and Pierson-Moskowitz spectra. The
characteristic parameters of each spectrum can be assigned by the user together with the
value of N (number of parts in which the spectrum is divided).

The user can choose among four different ways to define the angular frequency. It can
be determined assuming an equidistant discretization of the wave spectrum
(fi=fstart+iΔf-Δf/2), or chosen as unevenly distributed between (i-0.5)Δf and (i+0.5)Δf.
An unevenly distributed band width should be preferred: in fact, depending on N, an
equidistant splitting can lead to the repetition of the same wave group in the time series
that can be easily avoided using an unevenly distributed band width. The last two ways
to determine the angular frequency of each component and its band width consist of the
application of a stretched or cosine stretched function. The use of a stretched or cosine
stretched function has been proven to lead the most accurate results in terms of wave
height distribution and groupiness, even when the number of spectrum components N, is
relatively low. If there is a certain wave group that is repeating, finally the full range of
wave heights and wave periods is not reproduced and statistically the wave train is not
representing a real sea state of random waves.

A phase seed is also used and can be changed in DualSPHysics to obtain different
random series of δi. Changing the phase seed allows generating different irregular wave
time series both with the same significant wave height (Hm0) and peak period (Tp).

### Coupling with Discrete Element Method (DEM)
The discrete element method (DEM) allows for the computation of rigid particle
dynamics, by considering contact laws to account for interaction forces. The coupled
numerical solution, based on SPH and DEM discretisations, resolves solid-solid and
solid-fluid interactions over a broad range of scales.

Forces arise whenever a particle of a solid object interacts with another. In the particular
case of a solid-solid collision, the contact force is decomposed into Fn and Ft, normal
and tangential components respectively. Both of these forces include viscous dissipation
effects. This is because two colliding bodies undergo a deformation which will be
somewhere between perfectly inelastic and perfectly elastic, usually quantified by the
normal restitution coefficient

<p align="center">
<img src="https://i.imgur.com/FI6n4e6.png"/> (45)
</p>

The total forces are decomposed into a repulsion force, Fr, arising from the elastic
deformation of the material, and a damping force, Fd, for the viscous dissipation of
energy during the deformation.

Figure 3-1 generally illustrates the proposed viscoelastic DEM mechanism between two
interacting particles.

<p align="center">
<img src="https://i.imgur.com/Cf4aUv1.png"/>
</p>

<p align="center">
<strong>Figure 3-1.</strong> Schematic interaction between particles with viscoelastic DEM mechanism.
</p>

The normal force is given by

<p align="center">
<img src="https://i.imgur.com/JSWjteL.png"/> (46)
</p>

where the stiffness is given by

<p align="center">
<img src="https://i.imgur.com/E09Sbv7.png"/> (47)
</p>

and the damping coefficient is

<p align="center">
<img src="https://i.imgur.com/3SywlkB.png"/> (48)
</p>

where <img src="https://i.imgur.com/qJFoGej.png" /> is the unit vector between the centers of particles i and j.

The restitution coefficient ij e is taken as the average of the two materials coefficients, in
what is the only calibration parameter of the model. It is not a physical parameter, but
since the current method does not account for internal deformations and other energy
losses during contact, the user is given a choice to change this parameter freely in order
to control the dissipation of each contact. The reduced radius and reduced elasticity are
given by

<p align="center">
<img src="https://i.imgur.com/NFNi4cg.png"/> (49)
</p>

where Ri is simply the particle radius, Ei is the Young modulus and νp is the Poisson
coefficient of material i, as specified in the Floating_Materials.xml.

This results in another restriction to the time-step, adding

<p align="center">
<img src="https://i.imgur.com/CBkNVwo.png"/> (50)
</p>

to the existing CFL restrictions (Eq. 30), where vn is the normal relative velocity and M*
is the reduced mass of the system where there is a contact.

Regarding tangential contacts, friction is modelled using the same model:

<p align="center">
<img src="https://i.imgur.com/TEWT5wl.png"/> (51)
</p>

where the stiffness and damping constants are derived to be

<p align="center">
<img src="https://i.imgur.com/I0k85MJ.png"/> (52)
</p>

as to insure internal consistency of the time scales between normal and tangential
components. This mechanism models the static and dynamic friction mechanisms by a
penalty method. The body does not statically stick at the point of contact, but is
constrained by the spring-damper system. This force must be bounded above by the
Coulomb friction law, modified with a sigmoidal function in order to make it
continuous around the origin regarding the tangential velocity:

<p align="center">
<img src="https://i.imgur.com/KeEhBWb.png"/> (53)
</p>

where μIJ is the friction coefficient at the contact of object I and object J and is simply
taken as the average of the two friction coefficients of the distinct materials, indicated in
the Floating_Materials.xml.

More information about DEM implementation can be found in [Canelas, 2015; Canelas
et al., 2016].

Multi-phase: Two-phase liquid-sediment implementation in DualSPHysics

This guide provides a concise depiction of the multi-phase liquid-sediment model
implemented in DualSPHysics solver. The model is capable of simulating problems
involving liquid-sediment phases with the addition of highly non-linear deformations
and free-surface flows which are frequently encountered in applied hydrodynamics.
More specifically, the two-phase liquid-solid model is aimed at flow-induced erosion of
fully saturated sediment. Applications include scouring in industrial tanks, port
hydrodynamics, wave breaking in coastal applications and scour around structures in
civil and environmental engineering flows among others.

Description of the physical problem

A typical saturated sediment scour induced by rapid liquid flow at the interface
undergoes a number of different behavioural regime changes mostly govern by the
characteristics of the sediment and liquid phase rheology at the interface. These
sediment regimes are distinguishable as an un-yielded region of sediment, a yielded
non-Newtonian region and a pseudo Newtonian sediment suspension region where the
sediment is entrained by the liquid flow. These physical processes can be described by
the Coulomb shear stress τmc, the cohesive yield strength τc which accounts for the
cohesive nature of fine sediment, the viscous shear stress τv which accounts for the fluid
particle viscosity, the turbulent shear stress of the sediment particle τt and the dispersive
stress τd which accounts for the collision of larger fraction granulate. The total shear
stress can be expressed as

<p align="center">
<img src="https://i.imgur.com/3i7pXVb.png"/> (54)
</p>

The first two parameters on the right-hand side of the equation define the yield strength
of the material and thus can be used to differentiate the un-yielded or yielded region of
the sediment state according to the induced stress by the liquid phase in the interface.
The model implemented in DualSPHysics uses the Drucker-Prager yield criterion to
evaluate yield strength of the sediment phase and the sediment failure surface.

When the material yields the sediment behaves as a non-Newtonian rate dependent
Bingham fluid that accounts for the viscous and turbulent effects of the total shear stress
of Eq. 54. Typically, sediment behaves as a shear thinning material with a low and high
shear stress state of a pseudo-Newtonian and plastic viscous regime respectively.
Herein, the Herschel-Buckley-Papanastasiou model is employed as a power law Bingham model. This combines the yielded and un-yielded region using an exponential
stress growth parameter and a power law Bingham model for the shear thinning or
thickening plastic region.

Finally, the characteristics of the low concentration suspended sediment that has been
entrained by the liquid are modelled using a volumetric concentration based viscosity in
a pseudo-Newtonian approach by employing the Vand equation.

Sediment phase

The yield surface prediction is modelled using the Drucker-Prager (DP) model. The DP
can be written in a general form as [Fourtakas and Rogers, 2016]

<p align="center">
<img src="https://i.imgur.com/YTi6Wm0.png"/> (55)
</p>

The parameters a and κ can be determined by projecting the Drucker-Prager onto the
Mohr-Coulomb yield criterion in a deviatoric plane

<p align="center">
<img src="https://i.imgur.com/H4aCkE8.png"/> (56)
</p>

where φ is the internal friction and c the cohesion of the material. Finally, yielding will
occur when the following equation is satisfied

<p align="center">
<img src="https://i.imgur.com/AryWAwY.png"/> (57)
</p>

The multi-phase model uses the Herschel-Bulkley-Papanastasiou (HBP) [Papanastasiou,
1987] rheological characteristics to model the yielded region. The HBP model reads

<p align="center">
<img src="https://i.imgur.com/OJosS1C.png"/> (58)
</p>

where m controls the exponential growth of stress, n is the power law index and μ is the
apparent dynamic viscosity (or consistency index for sediment flows). Figure 3-2(a)
shows the initial rapid growth of stress by varying m whereas Figure 3-2(b) shows the
effect of the power law index n.

Note that as m → ∞ the HBP model reduces to the original Herschel-Bulkley model and
when n=1 the model reduces to a simple Bingham model. Consequently, when n=1 and
m=0 the model reduces to a Newtonian constitutive equation. Therefore, both phases
can be modelled using the same constitutive equation. Most importantly, since the HBP
parameters can be adjusted independently for each phase the current model is not
restricted to Newtonian/Non-Newtonian formulation but can simulate a variety of
combinations of flows (i.e. Newtonian/Newtonian, Non-Newtonian/Non-Newtonian
with or without a yield strength, etc.).

<p align="center">
<img src="https://i.imgur.com/wgeLepo.png"/>
</p>

<p align="center">
<strong>Figure 3-2.</strong> Initial rapid growth of stress by varying m and effect of the power law index n for the HBP model.
</p>

The rheological characteristics of the sediment entrainment by the fluid can be
controlled through the volume fraction of the mixture by using a concentration volume
fraction in the form of

<p align="center">
<img src="https://i.imgur.com/iRMnidK.png"/> (59)
</p>

where the summation is defined within the support of the kernel and jsat refers to the
yielded saturated sediment particles only.

We use a suspension viscosity based on the Vand experimental colloidal suspension
equation [Vand, 1948] of sediment in a fluid by

<p align="center">
<img src="https://i.imgur.com/DxHFbRQ.png"/> (60)
</p>

assuming an isotropic material with spherically shaped sediment particles. Eq. 60 is
applied only when the volumetric concentration of the saturated sediment particle
within the SPH kernel is lower than 0.3, which is the upper validity limit of Eq. 60.

More information about this multi-phase implementation can be also found in
[Fourtakas, 2014; Fourtakas and Rogers, 2016].