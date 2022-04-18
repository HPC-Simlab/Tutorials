# Table of Contents
1. [Description](#1)
2. [ParMETIS on SIMLAB](#2)
3. [Linking phase](#3)

## Description <a name="1"></a>

ParMETIS is an MPI-based parallel library which implements a variety of algorithms for partitioning unstructured graphs, meshes, and for computing fill-reducing orderings of sparse matrices.
 
## ParMETIS on SIMLAB <a name="2"></a>

- Check available versions:

```sh
$ module avail ParMETIS
----------------- /cm/shared/modulefiles ------------------
ParMETIS/4.0.3-gompi-2020a  
```
- Load ParMETIS (version 4.0.3, compiled with GCC-9.3.0 and OpenMPI-4.0.3):
```sh
$ module load ParMETIS
```
- Check modules loaded (dependencies):

```sh
$ module list
Currently Loaded Modulefiles:
 1) GCCcore/9.3.0                     9) hwloc/2.2.0-GCCcore-9.3.0       
 2) zlib/1.2.11-GCCcore-9.3.0        10) libevent/2.1.11-GCCcore-9.3.0   
 3) binutils/2.34-GCCcore-9.3.0      11) UCX/1.8.0-GCCcore-9.3.0         
 4) GCC/9.3.0                        12) libfabric/1.11.0-GCCcore-9.3.0  
 5) numactl/2.0.13-GCCcore-9.3.0     13) PMIx/3.1.5-GCCcore-9.3.0        
 6) XZ/5.2.5-GCCcore-9.3.0           14) OpenMPI/4.0.3-GCC-9.3.0         
 7) libxml2/2.9.10-GCCcore-9.3.0     15) gompi/2020a                     
 8) libpciaccess/0.16-GCCcore-9.3.0  16) ParMETIS/4.0.3-gompi-2020a      
```
## Linking phase <a name="3"></a>

The linking phase During the compilation, it is necessary to add the `-lparmetis` option.
