# Table of Contents
1. [Description](#1)
2. [MUMPS on SIMLAB](#2)
3. [Examples](#3)
   1. [C example](#4)
      1. [Linking phase](#5)
   3. [MUMPS using pymumps](#6)
      1. [Installing pymumps](#7)
      2. [Python example](#8)

## Description <a name="1"></a>

MUMPS (MUltifrontal Massively Parallel sparse direct Solver) is a software application for the solution of large sparse systems of linear algebraic equations on distributed memory parallel computers. see more in [wikipedia](https://en.wikipedia.org/wiki/MUMPS_(software)) and MUMPS [docs](http://mumps.enseeiht.fr/index.php?page=doc).

## MUMPS on SIMLAB <a name="2"></a>

- Check available versions:

```sh
$ module avail MUMPS
----------------- /cm/shared/modulefiles ------------------
MUMPS/5.2.1-foss-2020a-metis  
```
- Load MUMPS (5.2.1 compiled with GCC-9.3.0):
```sh
$ module load MUMPS
```
- List module loaded:

**All modules loaded are linked with the installed version (`metis`, `scotch`, `scalapack`, etc...)**
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
 9) hwloc/2.2.0-GCCcore-9.3.0        20) SCOTCH/6.0.9-gompi-2020a        
10) libevent/2.1.11-GCCcore-9.3.0    21) METIS/5.1.0-GCCcore-9.3.0       
11) UCX/1.8.0-GCCcore-9.3.0          22) MUMPS/5.2.1-foss-2020a-metis    
```

### Examples <a name="3"></a>

### C example <a name="4"></a>

C example is available [mumps_example.c](https://github.com/HPC-Simlab/Website-utilities/blob/master/TESTS_LIBRARIES/tests_mumps)

#### Linking phase <a name="5"></a>

The linking phase During the compilation, it is necessary to add the `-ldmumps` option.
 
```sh
$ mpicc mumps_example.c -o mumps_example -ldmumps
```
 
- Run C test:
 
```sh
$ mpirun -n 2 ./mumps_example
```
 
## Python example <a name="6"></a>

#### Install pymumps <a name="7"></a>
 
- Load Python:

```sh
module load Python/3.8.2-GCCcore-9.3.0
```
- Install pymumps using `pip` command:

```sh
$ pip3 install pymumps
```
#### Python example <a name="8"></a>

```python
import numpy as np
import mumps

# Set up the test problem:
n = 5
irn = np.array([1,2,4,5,2,1,5,3,2,3,1,3], dtype='i')
jcn = np.array([2,3,3,5,1,1,2,4,5,2,3,3], dtype='i')
a = np.array([3.0,-3.0,2.0,1.0,3.0,2.0,4.0,2.0,6.0,-1.0,4.0,1.0], dtype='d')

b = np.array([20.0,24.0,9.0,6.0,13.0], dtype='d')

# Create the MUMPS context and set the array and right hand side
ctx = mumps.DMumpsContext(sym=0, par=1)
if ctx.myid == 0:
    ctx.set_shape(5)
    ctx.set_centralized_assembled(irn, jcn, a)
    x = b.copy()
    ctx.set_rhs(x)

ctx.set_silent() # Turn off verbose output

ctx.run(job=6) # Analysis + Factorization + Solve

if ctx.myid == 0:
    print("Solution is %s." % (x,))

ctx.destroy() # Free memory
```

- Run Python test:

```sh
python mumps_example.py
```
