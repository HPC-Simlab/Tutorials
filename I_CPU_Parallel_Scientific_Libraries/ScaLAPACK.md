# Table of Contents
1. [Description](#1)
2. [ScaLAPACK on SIMLAB](#2)
3. [Linking phase](#3)

## Description <a name="1"></a>

ScaLAPACK is available through the Intel MKL library (recommended version) or freely through netlib. ScaLAPACK is a library composed of a set of Fortran subroutines which allows the parallel solving of dense linear algebra problems by direct numerical methods. This library depends in particular on the PBLAS (Parallel BLAS) and BLACS (Basic Linear Algebra Communication Subprograms) parallel libraries on which it bases the realisation in parallel of the elementary matrix operations and the inter-process communications respectively, via MPI for example.

## ScaLAPACK on SIMLAB <a name="2"></a>

- Check available versions:

```sh
$ module avail ScaLAPACK
----------------- /cm/shared/modulefiles ------------------
ScaLAPACK/2.0.2-gompi-2019b  ScaLAPACK/2.1.0-gompi-2020b  
ScaLAPACK/2.1.0-gompi-2020a  
```
- Load ScaLAPACK (default - version 2.1.0 compiled with GCC-10.2.0 and OpenMPI-4.0.5):

```sh
$ module load ScaLAPACK
```
- Check modules loaded (dependencies):

```sh
$ module list
Currently Loaded Modulefiles:
 1) GCCcore/10.2.0                    10) libevent/2.1.12-GCCcore-10.2.0   
 2) zlib/1.2.11-GCCcore-10.2.0        11) UCX/1.9.0-GCCcore-10.2.0         
 3) binutils/2.35-GCCcore-10.2.0      12) libfabric/1.11.0-GCCcore-10.2.0  
 4) GCC/10.2.0                        13) PMIx/3.1.5-GCCcore-10.2.0        
 5) numactl/2.0.13-GCCcore-10.2.0     14) OpenMPI/4.0.5-GCC-10.2.0         
 6) XZ/5.2.5-GCCcore-10.2.0           15) gompi/2020b                      
 7) libxml2/2.9.10-GCCcore-10.2.0     16) OpenBLAS/0.3.12-GCC-10.2.0       
 8) libpciaccess/0.16-GCCcore-10.2.0  17) ScaLAPACK/2.1.0-gompi-2020b      
 9) hwloc/2.2.0-GCCcore-10.2.0        
```

## Linking phase <a name="3"></a>

The linking phase During the compilation, it is necessary to add the `-lscalapack` option.

