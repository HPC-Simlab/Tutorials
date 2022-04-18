# Table of Contents
1. [Description](#1)
2. [METIS on SIMLAB](#2)
3. [Linking phase](#3)

## Description <a name="1"></a>

METIS is a graph partitioning tool. It can be used for partitioning finite element meshes and reducing induced fill-in during the sparse matrix factorization. The algorithms implemented in METIS are based on the multilevel recursive, multilevel k-way and multi-constraint partitioning schemes.

## METIS on SIMLAB <a name="2"></a>

- List available versions:

```sh
$ module avail METIS
----------------- /cm/shared/modulefiles ------------------
METIS/5.1.0-GCCcore-9.3.0  
```
- Load METIS (5.1.0 compiled with GCC-9.3.0):
```sh
$ module load METIS
```
- Check modules loaded (dependencies):

```sh
$ module list
Currently Loaded Modulefiles:
 1) GCCcore/9.3.0   2) METIS/5.1.0-GCCcore-9.3.0  
```

## Linking phase <a name="3"></a>
During the compilation, it is necessary to add the `-lmetis` option: 

```sh
$ gfortran appel_metis.f90 -lmetis
```
