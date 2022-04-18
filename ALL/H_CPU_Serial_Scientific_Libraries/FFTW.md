# Table of Contents
1. [Description](#1)
2. [FFTW on SIMLAB](#2)

## Description <a name="1"></a>

The FFTW library is a set of C subroutines for calculating the discrete Fourier transform in one or many dimensions for real and complex data.

## FFTW on SIMLAB <a name="2"></a>

- Chech available versions:
```sh
$ module avail FFTW
----------------- /cm/shared/modulefiles ------------------
FFTW/3.3.8-gompi-2019b  FFTW/3.3.8-gompi-2020a  FFTW/3.3.8-gompi-2020b  
```
- Load FFTW (defautl - 3.3.8):
```sh
$ module load FFTW
```
- Check modules loaded:
```sh
$ module list
Currently Loaded Modulefiles:
 1) GCCcore/10.2.0                     9) hwloc/2.2.0-GCCcore-10.2.0       
 2) zlib/1.2.11-GCCcore-10.2.0        10) libevent/2.1.12-GCCcore-10.2.0   
 3) binutils/2.35-GCCcore-10.2.0      11) UCX/1.9.0-GCCcore-10.2.0         
 4) GCC/10.2.0                        12) libfabric/1.11.0-GCCcore-10.2.0  
 5) numactl/2.0.13-GCCcore-10.2.0     13) PMIx/3.1.5-GCCcore-10.2.0        
 6) XZ/5.2.5-GCCcore-10.2.0           14) OpenMPI/4.0.5-GCC-10.2.0         
 7) libxml2/2.9.10-GCCcore-10.2.0     15) gompi/2020b                      
 8) libpciaccess/0.16-GCCcore-10.2.0  16) FFTW/3.3.8-gompi-2020b           
```
