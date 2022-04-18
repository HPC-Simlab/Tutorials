# Table of Contents
1. [Description](#1)
2. [HDF5 on SIMLAB](#2)

## Description <a name="1"></a>

HDF signifies Hierarchical Data Format. This format was developed by the National Center for Supercomputing Applications (NCSA) and is now supported by The HDF Group. It facilitates the handling of files containing very large quantities of data through prioritisation in tree hierarchies.

## HDF5 on SIMLAB <a name="2"></a>

- Check available versions:
```sh
$ module avail HDF5
----------------- /cm/shared/modulefiles ------------------
HDF5/1.10.5-gompi-2019b  HDF5/1.10.6-gompi-2020a  HDF5/1.10.7-gompi-2020b  
```
- Load HDF5 (default - 1.10.7 compiled with GCC-10.2.0 and OpenMPI-4.0.5):
```sh
$ module load HDF5
```
- Check modules loaded (dependepencies):

```sh
$ module list
Currently Loaded Modulefiles:
 1) GCCcore/10.2.0                    10) libevent/2.1.12-GCCcore-10.2.0   
 2) zlib/1.2.11-GCCcore-10.2.0        11) UCX/1.9.0-GCCcore-10.2.0         
 3) binutils/2.35-GCCcore-10.2.0      12) libfabric/1.11.0-GCCcore-10.2.0  
 4) GCC/10.2.0                        13) PMIx/3.1.5-GCCcore-10.2.0        
 5) numactl/2.0.13-GCCcore-10.2.0     14) OpenMPI/4.0.5-GCC-10.2.0         
 6) XZ/5.2.5-GCCcore-10.2.0           15) gompi/2020b                      
 7) libxml2/2.9.10-GCCcore-10.2.0     16) Szip/2.1.1-GCCcore-10.2.0        
 8) libpciaccess/0.16-GCCcore-10.2.0  17) HDF5/1.10.7-gompi-2020b          
 9) hwloc/2.2.0-GCCcore-10.2.0        
```
