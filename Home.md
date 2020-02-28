<h1 align="center">
  <br>
  <a href="http://dual.sphysics.org/"><img src="http://design.sphysics.org/img/logo_dualsphysics.png" alt="DualSPHysics" width="300"></a>
</h1>

<h4 align="center"><a href="https://http://www.dual.sphysics.org" target="_blank">DualSPHysics</a> is based on the Smoothed Particle Hydrodynamics model named <a href="https://http://www.sphysics.org" target="_blank">SPHysics</a>.</h4>

<h4 align="center">The code is developed to study free-surface flow phenomena where Eulerian methods can be difficult to apply, such as waves or impact of dam-breaks on off-shore structures. DualSPHysics is a set of C++, <a href="https://developer.nvidia.com/cuda-zone" target="_blank">CUDA</a> and Java codes designed to deal with real-life engineering problems.</h4>


## Table of Contents
<div>
    <ul>
        <li>
            <a href="../1.-Introduction">1. Introduction</a>
        </li>
        <li>
            <a href="../2.-Developers-and-Institutions">2. Developers and Institutions</a>
        </li>
        <li>
            <a href="../3.-SPH-formulation">3. SPH formulation</a>
            <ul>
                <li><a href="../3.-SPH-formulation#31-smoothing-kernel">3.1 Smoothing kernel</a></li>
                <li><a href="../3.-SPH-formulation#32-momentum-equation">3.2 Momentum equation</a></li>
                <li><a href="../3.-SPH-formulation#33-continuity-equation">3.3 Continuity equation</a></li>
                <li><a href="../3.-SPH-formulation#34-equation-of-state">3.4 Equation of state</a></li>
                <li><a href="../3.-SPH-formulation#35-density-diffusion-term">3.5 Density diffusion term</a></li>
                <li><a href="../3.-SPH-formulation#36-shifting-algorithm">3.6 Shifting algorithm</a></li>
                <li><a href="../3.-SPH-formulation#37-time-stepping">3.7 Time stepping</a></li>
                <li><a href="../3.-SPH-formulation#38-boundary-conditions">3.8 Boundary conditions</a></li>
                <li><a href="../3.-SPH-formulation#39-wave-generation">3.9 Wave generation</a></li>
                <li><a href="../3.-SPH-formulation#310-passive-and-active-wave-absorption">3.10 Passive and active wave absorption</a></li>
                <li><a href="../3.-SPH-formulation#311-coupling-with-discrete-element-method-dem">3.11 Coupling with Discrete Element Method (DEM)</a></li>
                <li><a href="../3.-SPH-formulation#312-coupling-dualsphysics-with-project-chrono">3.12 Coupling with Project Chrono</a></li>
                <li><a href="../3.-SPH-formulation#313-coupling-with-wave-propagation-models">3.13 Coupling with wave propagation models</a></li>
                <li><a href="../3.-SPH-formulation#314-coupling-dualsphysics-with-moordyn">3.14 Coupling DualSPHysics with MoorDyn</a></li>
                <li><a href="../3.-SPH-formulation#315-open-boundary-conditions">3.15 Open boundary conditions</a></li>
                <li><a href="../3.-SPH-formulation#316-multi-phase-two-phase-liquid-gas-implementation-in-dualsphysics">3.16 Multi-phase: liquid-gas</a></li>
                <li><a href="../3.-SPH-formulation#317-multi-phase-two-phase-liquid-sediment-implementation-in-dualsphysics">3.17 Multi-phase: liqued-sediment</a></li>
            </ul>
        </li>
        <li>
            <a href="../4.-CPU-and-GPU-implementation">4.CPU and GPU implementation</a>
        </li>
   <li>
            <a href="../5.-Running-DualSPHysics">5.Running DualSPHysics</a>
            <ul>
                <li><a href="../5.-Running-DualSPHysics#51-directory-structure">5.1 Directory structure</a></li>
                <li><a href="../5.-Running-DualSPHysics#52-running-the-dualSPHysics-code">5.2 Running the DualSPHysics code</a></li>
                <li><a href="../5.-Running-DualSPHysics#53-preprocessing">5.3 Preprocessing</a></li>
                <li><a href="../5.-Running-DualSPHysics#54-processing">5.4 Processing</a></li>
                <li><a href="../5.-Running-DualSPHysics#55-postprocessing">5.5 Postprocessing</a></li>
                <li><a href="../5.-Running-DualSPHysics#56-graphical-user-interface">5.6 Graphical User Interface</a></li>
            </ul>
        </li>
       </ul>
</div>



## Suggestions and errors in the Wiki
If you have suggestions (a new section, corrections or contributions) please notify it using the [ISSUES section of the repository](https://github.com/DualSPHysics/DualSPHysics/issues). Please include something like [WIKI] into the title to help us to prioritize the work.
