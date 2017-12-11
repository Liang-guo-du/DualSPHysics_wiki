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

