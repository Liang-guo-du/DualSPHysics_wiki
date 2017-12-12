The codes provided within the DualSPHysics package present some important
improvements in comparison to the codes available within SPHysics. One of them is
related to the format of the files that are used as input and output data throughout the
execution of DualSPHysics and the pre-processing and post-processing codes. Different
format files for the input and the output data are involved in the DualSPHysics
execution: XML, binary and VTK-binary.

### XML File

The XML (EXtensible Markup Language) is a textual data format that can easily be read
or written using any platform and operating system. It is based on a set of labels (tags)
that organise the information and can be loaded or written easily using any standard text
or dedicated XML editor. This format is used for input files for the code.

### BINARY File
The output data in the SPHysics code is written in text files, so ASCII format is used.
ASCII files present some interesting advantages such as visibility and portability,
however they also present important disadvantages particularly with simulations with
large numbers of particles: data stored in text format consumes at least six times more
memory than the same data stored in binary format, precision is reduced when values
are converted from real numbers to text while reading and writing data in ASCII is more
expensive (two orders of magnitude). Since DualSPHysics allows performing
simulations with a high number of particles, a binary file format is necessary to avoid
these problems. Binary format reduces the volume of the files and the time dedicated to
generate them. These files contain the meaningful information of particle properties. In
this way, some variables can be removed, e.g., the pressure is not stored since it can be
calculated starting from the density using the equation of state. The mass values are
constant for fluid particles and for boundaries so only two values are used instead of an
array. Data for particles that leave the limits of the domain are stored in an independent
file (PartOut_000.obi4) which leads to an additional saving. Hence, the advantages can
be summarised as: (i) memory storage reduction, (ii) fast access, (iii) no precision lost
and (iv) portability (i.e. to different architectures or different operating systems).

The file format used now in DualSPHysics v4.0 is named BINX4 (.bi4) which is the
new binary format and can save particle position in single or double precision. This
format file is a container so the user can add new metadata and new arrays can be
processed in an automatic way using the current post-processing tools of the package.

### VTK File
VTK (Visualization ToolKit) files are used for final visualization of the results and can
either be generated as a pre-processing step or output directly by DualSPHysics instead
of the standard BINX format (albeit at the expense of computational overhead). VTK
not only supports the particle positions, but also physical quantities that are obtained
numerically for the particles involved in the simulations. VTK supports many data
types, such as scalar, vector, tensor, texture, and also supports different algorithms such
as polygon reduction, mesh smoothing, cutting, contouring and Delaunay triangulation.
The VTK file format consists of a header that describes the data and includes any other
useful information, the dataset structure with the geometry and topology of the dataset
and its attributes. Here VTK files of POLYDATA type with legacy-binary format is
used. This format is also easy for input-output (IO) or read-write operations.

