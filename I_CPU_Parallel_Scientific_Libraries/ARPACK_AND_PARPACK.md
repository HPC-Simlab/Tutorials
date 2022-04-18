# Table of Contents
1. [Description](#1)
2. [PARPACK/ARPACK on SIMLAB](#2)
3. [Linking phase](#3)

## Description <a name="1"></a>

ARPACK (ARnoldi PACKage) is a library of Fortran77 subroutines for researching the eigenvalues and eigenvectors of large sparse matrices. The library is based on the iterative algorithms of Lanczos/Arnoldi.

PARPACK (Parallel ARnoldi PACKage) is a parallel version of the ARPACK library.

ARPACK and PARPACK are available in the ARPACK-NG package.

## PARPACK/ARPACK on SIMLAB <a name="2"></a>
- Check available versions:

```sh
$ module avail arpack-ng
----------------- /cm/shared/modulefiles ------------------
arpack-ng/3.7.0-foss-2020a  
```
- Load arpack-ng (version 3.7.0, compiled using GCC-9.3.0 and OpenMPI-4.0.3):

```sh
$ module load arpack-ng
```
- Check modules loaded (dependencies):

```sh
$ module list
Currently Loaded Modulefiles:
 1) GCCcore/9.3.0                    12) libfabric/1.11.0-GCCcore-9.3.0  
 2) zlib/1.2.11-GCCcore-9.3.0        13) PMIx/3.1.5-GCCcore-9.3.0        
 3) binutils/2.34-GCCcore-9.3.0      14) OpenMPI/4.0.3-GCC-9.3.0         
 4) GCC/9.3.0                        15) OpenBLAS/0.3.9-GCC-9.3.0        
 5) numactl/2.0.13-GCCcore-9.3.0     16) gompi/2020a                     
 6) XZ/5.2.5-GCCcore-9.3.0           17) FFTW/3.3.8-gompi-2020a          
 7) libxml2/2.9.10-GCCcore-9.3.0     18) ScaLAPACK/2.1.0-gompi-2020a     
 8) libpciaccess/0.16-GCCcore-9.3.0  19) foss/2020a                      
 9) hwloc/2.2.0-GCCcore-9.3.0        20) Eigen/3.3.7-GCCcore-9.3.0       
10) libevent/2.1.11-GCCcore-9.3.0    21) arpack-ng/3.7.0-foss-2020a      
11) UCX/1.8.0-GCCcore-9.3.0          
```

## Linking phase <a name="3"></a>

At the compilation, it is necessary to add `-larpack` to use the sequential version or `-lparpack -larpack` for the parallel version:

```sh
$ mpiifort appel_arpack.f90 -larpack  
```
or
```sh
$ mpiifort appel_parpack.f90 -lparpack -larpack 
```
