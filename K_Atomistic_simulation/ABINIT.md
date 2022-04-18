# Table of Contents
1. [Description](#1)
2. [ABINIT on SIMLAB](#2)

## Description <a name="1"></a>

Abinit is a materials modelling software using density functional theory.

## ABINIT on SIMLAB <a name="2"></a>
Setting up your envirement to work with HYPRE:

- Check available versions:
```sh
$ module avail ABINIT
----------------- /cm/shared/modulefiles ------------------
ABINIT/9.4.1-foss-2020b  
```
- Load ABINIT (version 9.4.1, compiled with GCC-10.2.0 and OpenMPI-4.0.5):
```sh
$ module load ABINIT
```

- List modules loaded (depenpencies):

```sh
$ module list
Currently Loaded Modulefiles:
 1) GCCcore/10.2.0                    15) OpenBLAS/0.3.12-GCC-10.2.0        
 2) zlib/1.2.11-GCCcore-10.2.0        16) gompi/2020b                       
 3) binutils/2.35-GCCcore-10.2.0      17) FFTW/3.3.8-gompi-2020b            
 4) GCC/10.2.0                        18) ScaLAPACK/2.1.0-gompi-2020b       
 5) numactl/2.0.13-GCCcore-10.2.0     19) foss/2020b                        
 6) XZ/5.2.5-GCCcore-10.2.0           20) libxc/4.3.4-GCC-10.2.0            
 7) libxml2/2.9.10-GCCcore-10.2.0     21) Szip/2.1.1-GCCcore-10.2.0         
 8) libpciaccess/0.16-GCCcore-10.2.0  22) HDF5/1.10.7-gompi-2020b           
 9) hwloc/2.2.0-GCCcore-10.2.0        23) cURL/7.72.0-GCCcore-10.2.0        
10) libevent/2.1.12-GCCcore-10.2.0    24) netCDF/4.7.4-gompi-2020b          
11) UCX/1.9.0-GCCcore-10.2.0          25) netCDF-Fortran/4.5.3-gompi-2020b  
12) libfabric/1.11.0-GCCcore-10.2.0   26) Wannier90/3.1.0-foss-2020b        
13) PMIx/3.1.5-GCCcore-10.2.0         27) ABINIT/9.4.1-foss-2020b           
14) OpenMPI/4.0.5-GCC-10.2.0          
```
