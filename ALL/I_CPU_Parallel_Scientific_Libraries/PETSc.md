# Table of Contents
1. [Description](#1)
2. [PETSc on SIMLAB](#2)
3. [Examples](#3)
   1. [C example](#4)
      1. [Linking phase](#5)
   3. [PETSc using petsc4py](#6)
      1. [Use  petsc4py](#7)
      2. [Python example](#8)

## Description <a name="1"></a>

The Portable, Extensible Toolkit for Scientific Computation (PETSc), is a suite of data structures and routines developed by Argonne National Laboratory for the scalable (parallel) solution of scientific applications modeled by partial differential equations. see more in [wikipedia](https://en.wikipedia.org/wiki/Portable,_Extensible_Toolkit_for_Scientific_Computation) and PETCs [docs](https://petsc.org/release/docs/).

## PETSc on SIMLAB <a name="2"></a>

before working with PETSc we need to see the avaiable version and load what we wont to work with by the following steps:

- Check available versions:

```sh
$ module avail PETSc
----------------- /cm/shared/modulefiles ------------------
PETSc/3.16.1-GCC-9.3.0-Python-3.8.2  
```

```sh
$ module load PETSc
```

**PETSc configuration**

```sh
--with-mpi=1 --with-debugging=0 --with-zlib=1 --with-fortran-bindings=0 --with-parmetis=1 --with-metis=1 --with-hdf5=1 --with-hypre=1 --download-fblaslapack=1 --download-ptscotch --with-scalapack=1 --with-mumps=1 --with-petsc4py
```

<details><summary>- List modules loaded (dependencies)</summary>
<p>

```sh
$ module list

Currently Loaded Modulefiles:
 1) GCCcore/9.3.0                    19) OpenMPI/4.0.3-GCC-9.3.0              
 2) zlib/1.2.11-GCCcore-9.3.0        20) gompi/2020a                          
 3) cURL/7.69.1-GCCcore-9.3.0        21) SCOTCH/6.0.9-gompi-2020a             
 4) Xerces-C++/3.2.3-GCCcore-9.3.0   22) OpenBLAS/0.3.9-GCC-9.3.0             
 5) ncurses/6.2-GCCcore-9.3.0        23) FFTW/3.3.8-gompi-2020a               
 6) bzip2/1.0.8-GCCcore-9.3.0        24) ScaLAPACK/2.1.0-gompi-2020a          
 7) CMake/3.16.4-GCCcore-9.3.0       25) foss/2020a                           
 8) binutils/2.34-GCCcore-9.3.0      26) METIS/5.1.0-GCCcore-9.3.0            
 9) GCC/9.3.0                        27) MUMPS/5.2.1-foss-2020a-metis         
10) numactl/2.0.13-GCCcore-9.3.0     28) ParMETIS/4.0.3-gompi-2020a           
11) XZ/5.2.5-GCCcore-9.3.0           29) libreadline/8.0-GCCcore-9.3.0        
12) libxml2/2.9.10-GCCcore-9.3.0     30) Tcl/8.6.10-GCCcore-9.3.0             
13) libpciaccess/0.16-GCCcore-9.3.0  31) SQLite/3.31.1-GCCcore-9.3.0          
14) hwloc/2.2.0-GCCcore-9.3.0        32) GMP/6.2.0-GCCcore-9.3.0              
15) libevent/2.1.11-GCCcore-9.3.0    33) libffi/3.3-GCCcore-9.3.0             
16) UCX/1.8.0-GCCcore-9.3.0          34) Python/3.8.2-GCCcore-9.3.0           
17) libfabric/1.11.0-GCCcore-9.3.0   35) Hypre/2.18.2-foss-2020a              
18) PMIx/3.1.5-GCCcore-9.3.0         36) PETSc/3.16.1-GCC-9.3.0-Python-3.8.2  
 ```

</p>
</details>

## Examples <a name="3"></a>

### C example <a name="4"></a>

C examples are available [here](https://www.mcs.anl.gov/petsc/petsc-3.5/src/ksp/ksp/examples/tutorials/)

#### Linking phase <a name="5"></a>
 
The linking phase During the compilation, it is necessary to add the `-lpetsc` option.

***This example use hybrid parallelization***

```sh
$ mpicc -fopenmp petsc_example.c -o petsc_example -lpetsc -lm
```

- Run C test

```sh
$ mpirun -n 4 ./petsc_example -pc_type jacobi -ksp_monitor_short -ksp_gmres_cgs_refinement_type refine_always 
```

### PETSc using petsc4py <a name="6"></a>

#### Use petsc4py <a name="7"></a>
Petsc4py is installed in `SciPy-bundle` module

- Load SciPy-bundle to use petsc4py:

```sh
$ module load SciPy-bundle/2020.03-foss-2020a-Python-3.8.2
```
***Now you can use petsc4py***

#### Python example <a name="8"></a>
Python examples are available [here](https://github.com/JesseLu/petsc4py-tutorial)

```sh
$ cat petcs_example.py
 
import petsc4py
import sys
petsc4py.init(sys.argv)
from petsc4py import PETSc
[...]
```

- Run Python example:

```sh
$ python petcs_example.py
```
