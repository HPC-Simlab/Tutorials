# Table of Contents
1. [Description](#1)
2. [HYPRE on SIMLAB](#2)
3. [Linking phase](#3)

## Description <a name="1"></a>
The Parallel High Performance Preconditioners (hypre) is a library of routines for scalable (parallel) solution of linear systems. The built-in BLOPEX package in addition allows solving eigenvalue problems. See more in [wikipedia](https://en.wikipedia.org/wiki/Hypre) and HYPRE [docs](https://computing.llnl.gov/projects/hypre-scalable-linear-solvers-multigrid-methods).

## HYPRE on SIMLAB <a name="2"></a>
Setting up your envirement to work with HYPRE:

- Check available versions:
```sh
$ module avail Hypre
----------------- /cm/shared/modulefiles ------------------
Hypre/2.18.2-foss-2020a  
```
- Load Hypre (version 2.18.2 compiled with GCC-9.3.0):
```sh
$ module load Hypre
```
- Check modules loaded (dependencies):
```sh
$ module list
Currently Loaded Modulefiles:
 1) GCCcore/9.3.0                    11) UCX/1.8.0-GCCcore-9.3.0         
 2) zlib/1.2.11-GCCcore-9.3.0        12) libfabric/1.11.0-GCCcore-9.3.0  
 3) binutils/2.34-GCCcore-9.3.0      13) PMIx/3.1.5-GCCcore-9.3.0        
 4) GCC/9.3.0                        14) OpenMPI/4.0.3-GCC-9.3.0         
 5) numactl/2.0.13-GCCcore-9.3.0     15) OpenBLAS/0.3.9-GCC-9.3.0        
 6) XZ/5.2.5-GCCcore-9.3.0           16) gompi/2020a                     
 7) libxml2/2.9.10-GCCcore-9.3.0     17) FFTW/3.3.8-gompi-2020a          
 8) libpciaccess/0.16-GCCcore-9.3.0  18) ScaLAPACK/2.1.0-gompi-2020a     
 9) hwloc/2.2.0-GCCcore-9.3.0        19) foss/2020a                      
10) libevent/2.1.11-GCCcore-9.3.0    20) Hypre/2.18.2-foss-2020a         
```
## Linking phase <a name="3"></a>

The linking phase During the compilation, it is necessary to add the `-lHYPRE` option.
