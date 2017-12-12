The code can be compiled for either CPU or CPU&GPU. Please note that both the C++
and CUDA version of the code contain the same features and options. Most of the
source code is common to CPU and GPU, which allows the code to be run on
workstations without a CUDA-enabled GPU, using only the CPU implementation.

To run DualSPHysics on a GPU using an executable, only an Nvidia CUDA-enabled
GPU card is needed and the latest version of the GPU driver must be installed.
However, to compile the source code, the GPU programming language CUDA and nvcc
compiler must be installed on your computer. CUDA Toolkit X.X can be downloaded
from Nvidia website http://developer.nvidia.com/cuda-toolkit-XX. CUDA versions
from 4.0 till 7.5 have been tested.

Once the C++ compiler (for example gcc) and the CUDA compiler (nvcc) have been
installed in your machine, you can download the relevant files from the repository:

## Windows compilation
The project file DualSPHysics4_vs2010.sln is provided to be opened with Visual Studio
2010 and DualSPHysics4_vs2013.sln to be opened with Visual Studio 2013.
Also different configurations can be chosen for compilation:

1. Release - For CPU and GPU
2. ReleaseCPU - Only for CPU

The result of the compilation is the dualsphysics executable.

The Visual Studio project is created including the libraries for OpenMP in the executable. To not include them, user can modify Props config -> C/C++ -> Language -> OpenMp and compile again

The use of OpenMP can be also deactivated by commenting the code line in Types.h:
`#define _WITHOMP ///<Enables/Disables OpenMP.`

## Linux compilation

Makefiles can be used to compile the code in linux:
1. `make –f Makefile` full compilation just using make command
2. `make –f Makefile_cpu` only for CPU

The result of the compilation is the dualsphysics executable.

To exclude the use of OpenMP you have to remove the flags `–fopenmp` and `-lgomp` in
the Makefile and comment line `#define _WITHOMP` in Types.h.

The user can modify the compilation options, the path of the CUDA toolkit directory,
the GPU architecture. The GPU code is already compiled (EXECS) for compute
capabilities sm20, sm30, sm35, sm37, sm50, sm52 and with CUDA v7.5.

## Alternative building method via CMAKE

A new building method is supported in the new version 4.0 of DualSPHysics using
CMAKE (https://cmake.org/). CMAKE is a cross-platform and an independent building
system for compilation. This software generates native building files (like makefiles or
Visual Studio projects) for any platform. The location of dependencies and the needed
flags are automatically determined. Note that this method is on trial for version 4.

### Compile instructions for Microsoft Windows with Cmake

The building system needs the following dependencies:

* CMake version 2.8.10 or greater
* Nvidia CUDA Toolkit version 4.0 or greater.
* Visual Studio 2010 or 2013 version.
* File `CMakeLists.txt`

The folder build will be created in DUALSPHYSICS/SOURCE/DualSPHysics_4.
This folder will contain the building files so it can be safely removed in case of
rebuilding, it can actually be placed anywhere where the user has writing permissions.
Afterwards, open the Cmake application, a new window will appear:

<p align="center">
<img src="https://i.imgur.com/t3oFLxO.png"/>
</p>

Paste the Source folder path in the textbox labeled as Where is the source code, and
paste the build folder path into the Where to build the binaries textbox. Once the
paths are introduced, the Configure button should be pressed. A new dialog will appear
asking for the compiler to be used in the project. Please, remember that only Visual
Studio 2010 and Visual Studio 2013 for 64bit are supported.

If the configuration succeeds, now press the Generate button. This will generate a
Visual Studio project file into the build directory.

In order to compile both CPU and GPU versions, just change configuration to Release
and compile. If the user only wants to compile one version, one can choose one of the
solutions dualsphysics4cpu or dualsphysics4gpu for CPU or GPU versions
respectively, and compile it.

The user can freely customize the Source/CMakeLists.txt file to add new source files
or any other modifications. For more information about how to edit this file, please,
refer to official Cmake documentation (https://cmake.org/documentation/).

### Compile instructions for Linux with Cmake
The building system needs the following dependencies:
* Cmake version 2.8.10 or greater.
* Nvidia CUDA Toolkit version 4.0 or greater.
* GNU G++ compiler 4.4 version or greater.
* File `CMakeLists.txt`

The folder build will be created in DUALSPHYSICS/SOURCE/DualSPHysics_4.
This folder will contain the building files so it can be safely removed in case of
rebuilding, it can actually be placed anywhere where the user has writing permissions.
To create this folder and run Cmake just type:
```
> cd DUALSPHYSICS/SOURCE/DualSPHysics_4
> mkdir build
> cd build
> cmake ../Source
-- The C compiler identification is GNU 4.4.7
-- The CXX compiler identification is GNU 4.4.7
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
Using cuda version <7.5
Using libraries for gcc version <5.0
-- Try OpenMP C flag = [-fopenmp]
-- Performing Test OpenMP_FLAG_DETECTED
-- Performing Test OpenMP_FLAG_DETECTED - Success
-- Try OpenMP CXX flag = [-fopenmp]
-- Performing Test OpenMP_FLAG_DETECTED
-- Performing Test OpenMP_FLAG_DETECTED - Success
-- Found OpenMP: -fopenmp
-- Configuring done
-- Generating done
-- Build files have been written to: /home/user/DUALSPHYSICS/SOURCE/DualSPHysics_v4/build
```

The command cmake ../Source will search for a Cmake file (CMakeLists.txt) in the
specified folder. As mentioned before, the user can freely customize this file to add new
source files or any other modifications. For more information about how to edit this file,
please, refer to Cmake official documentation (https://cmake.org/documentation/).

Once the cmake command runs without error, a Makefile can be found in the build
folder. To build both CPU and GPU versions of DualSPHysics just type make. If the
user only needs to build one of the executable files he can use the commands make
dualsphysics4cpu or make dualsphysics4gpu for CPU and GPU versions respectively.
In order to install the compiled binaries into the EXECS folder, the user can either copy
the executable files or type the command make install.
