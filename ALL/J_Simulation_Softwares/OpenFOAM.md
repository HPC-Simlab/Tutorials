# Table of Contents
1. [Description](#1)
2. [Useful commands](#2)
3. [Example of batch file using OpenFOAM8](#3)

## Description <a name="1"></a>
OpenFOAM is the free, open source CFD software developed primarily by OpenCFD Ltd since 2004. It has a large user base across most areas of engineering and science, from both commercial and academic organisations. OpenFOAM has an extensive range of features to solve anything from complex fluid flows involving chemical reactions, turbulence and heat transfer, to acoustics, solid mechanics and electromagnetics.

## OpenFOAM on SIMLAB <a name="2"></a>

- Check available version:
```sh
$ module avail OpenFOAM
----------------- /cm/shared/modulefiles ------------------
OpenFOAM/8-foss-2020a  

---------------------------- /cm/shared/modulefiles ----------------------------
OpenFOAM/6.0  OpenFOAM/intel/7.0  

- Load OpenFOAM (version 8 compiled with GCC-9.3.0):
```sh
$ module load OpenFOAM
```
- Source the OpenFoam environment:
```sh
# For OpenFoam8
$ source $FOAM_BASH
# For OpenFoam6 and OpenFoam7
$ source $FOAM_HOME/etc/bashrc
```
<details><summary>List modules loaded (dependencies)</summary>
<p>

```bash
$ module list
Currently Loaded Modulefiles:
 1) GCCcore/9.3.0                                 83) OpenFOAM/8-foss-2020a  
 2) zlib/1.2.11-GCCcore-9.3.0                     
 3) binutils/2.34-GCCcore-9.3.0                   
 4) GCC/9.3.0                                     
 5) numactl/2.0.13-GCCcore-9.3.0                  
 6) XZ/5.2.5-GCCcore-9.3.0                        
 7) libxml2/2.9.10-GCCcore-9.3.0                  
 8) libpciaccess/0.16-GCCcore-9.3.0               
 9) hwloc/2.2.0-GCCcore-9.3.0                     
10) libevent/2.1.11-GCCcore-9.3.0                 
11) UCX/1.8.0-GCCcore-9.3.0                       
12) libfabric/1.11.0-GCCcore-9.3.0                
13) PMIx/3.1.5-GCCcore-9.3.0                      
14) OpenMPI/4.0.3-GCC-9.3.0                       
15) OpenBLAS/0.3.9-GCC-9.3.0                      
16) gompi/2020a                                   
17) FFTW/3.3.8-gompi-2020a                        
18) ScaLAPACK/2.1.0-gompi-2020a                   
19) foss/2020a                                    
20) ncurses/6.2-GCCcore-9.3.0                     
21) libreadline/8.0-GCCcore-9.3.0                 
22) METIS/5.1.0-GCCcore-9.3.0                     
23) SCOTCH/6.0.9-gompi-2020a                      
24) bzip2/1.0.8-GCCcore-9.3.0                     
25) Tcl/8.6.10-GCCcore-9.3.0                      
26) SQLite/3.31.1-GCCcore-9.3.0                   
27) GMP/6.2.0-GCCcore-9.3.0                       
28) libffi/3.3-GCCcore-9.3.0                      
29) Python/3.8.2-GCCcore-9.3.0                    
30) Boost/1.72.0-gompi-2020a                      
31) MPFR/4.0.2-GCCcore-9.3.0                      
32) gzip/1.10-GCCcore-9.3.0                       
33) lz4/1.9.2-GCCcore-9.3.0                       
34) zstd/1.4.4-GCCcore-9.3.0                      
35) expat/2.2.9-GCCcore-9.3.0                     
36) libpng/1.6.37-GCCcore-9.3.0                   
37) freetype/2.10.1-GCCcore-9.3.0                 
38) util-linux/2.35-GCCcore-9.3.0                 
39) fontconfig/2.13.92-GCCcore-9.3.0              
40) xorg-macros/1.19.2-GCCcore-9.3.0              
41) X11/20200222-GCCcore-9.3.0                    
42) libdrm/2.4.100-GCCcore-9.3.0                  
43) libglvnd/1.2.0-GCCcore-9.3.0                  
44) libunwind/1.3.1-GCCcore-9.3.0                 
45) LLVM/9.0.1-GCCcore-9.3.0                      
46) Mesa/20.0.2-GCCcore-9.3.0                     
47) libGLU/9.0.1-GCCcore-9.3.0                    
48) double-conversion/3.1.5-GCCcore-9.3.0         
49) gettext/0.20.1-GCCcore-9.3.0                  
50) PCRE/8.44-GCCcore-9.3.0                       
51) GLib/2.64.1-GCCcore-9.3.0                     
52) PCRE2/10.34-GCCcore-9.3.0                     
53) DBus/1.13.12-GCCcore-9.3.0                    
54) NASM/2.14.02-GCCcore-9.3.0                    
55) libjpeg-turbo/2.0.4-GCCcore-9.3.0             
56) NSPR/4.25-GCCcore-9.3.0                       
57) NSS/3.51-GCCcore-9.3.0                        
58) snappy/1.1.8-GCCcore-9.3.0                    
59) JasPer/2.0.14-GCCcore-9.3.0                   
60) Qt5/5.14.1-GCCcore-9.3.0                      
61) CGAL/4.14.3-gompi-2020a-Python-3.8.2          
62) pybind11/2.4.3-GCCcore-9.3.0-Python-3.8.2     
63) SciPy-bundle/2020.03-foss-2020a-Python-3.8.2  
64) Szip/2.1.1-GCCcore-9.3.0                      
65) HDF5/1.10.6-gompi-2020a                       
66) cURL/7.69.1-GCCcore-9.3.0                     
67) netCDF/4.7.4-gompi-2020a                      
68) x264/20191217-GCCcore-9.3.0                   
69) LAME/3.100-GCCcore-9.3.0                      
70) x265/3.3-GCCcore-9.3.0                        
71) FriBidi/1.0.9-GCCcore-9.3.0                   
72) FFmpeg/4.2.2-GCCcore-9.3.0                    
73) ParaView/5.8.0-foss-2020a-Python-3.8.2-mpi    
74) pixman/0.38.4-GCCcore-9.3.0                   
75) cairo/1.16.0-GCCcore-9.3.0                    
76) libgd/2.3.0-GCCcore-9.3.0                     
77) ICU/66.1-GCCcore-9.3.0                        
78) HarfBuzz/2.6.4-GCCcore-9.3.0                  
79) Pango/1.44.7-GCCcore-9.3.0                    
80) libcerf/1.13-GCCcore-9.3.0                    
81) Lua/5.3.5-GCCcore-9.3.0                       
82) gnuplot/5.2.8-GCCcore-9.3.0                   
```
 
<p>
</details>
 
## Example of batch file using OpenFOAM8 <a name="3"></a>


```sh
$ cat foam.slurm

#!/bin/bash

#SBATCH --job-name=OpenFoam
#SBATCH --partition=shortq
#SBATCH --output=slurm.out
#SBATCH --error=slurm.err
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=8

#purge modules
module purge

#load modules
module load slurm OpenFOAM/8-foss-2020a

#source openfoam
source $FOAM_BASH             #(source $FOAM_HOME/etc/bashrc is used for OpenFoam6 and OpenFoam7)

#run example
decomposePar >log.decomposePar
mpirun simpleFoam  -parallel >log.simpleFoam
reconstructPar >log.reconstructPar
```
- Run the job
```sh
$ sbatch foam.slurm
```
