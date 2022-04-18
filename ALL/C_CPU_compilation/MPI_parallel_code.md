# Table of Contents
1. [Some useful information](#1)
2. [MPI on SIMLAB](#2)
   1. [Open MPI](#3)
   2. [Intel MPI](#4)
3. [Examples](#5)
    1. [C example](#6)
    2. [Fortran example](#7)
    3. [MPI using Python](#8)
       1. [Install mpi4py](#9)
       2. [Python example](#10)


## Some useful information <a name="1"></a>

The MPI libraries available on SIMLAB are Intel MPI and Open MPI. 

## MPI on SIMLAB <a name="2"></a>

To setup your environment for working with OpenMPI please follow these steps:

### Open MPI <a name="3"></a>

- Show available version:

```sh
$ module avail OpenMPI
----------------- /cm/shared/modulefiles ------------------
OpenMPI/3.1.4-GCC-8.3.0  OpenMPI/4.0.3-GCC-9.3.0  OpenMPI/4.0.5-GCC-10.2.0 
```

- Load OpenMPI (version 4.0.3 compiled with GCC 9.3.0):
```sh
$ module load OpenMPI/4.0.3-GCC-9.3.0
```

**You can now use the Open MPI commands `mpicc`, `mpic++`, `mpirun`, `mpif90`, etc...**

### Intel MPI <a name="4"></a>

- Show available version:

```sh
$ module avail Intel_tools 
---------------------------- /cm/shared/modulefiles -----------------------------
Intel_tools  
```

- Load Intel_tools (version 18.0.2):
```sh
$ module load Intel_tools
```
**You can now use the Intel MPI commands `mpiicc`, `mpiicpc`, `mpirun`, `mpiif90`, etc...**


## Examples <a name="5"></a>
### C example <a name="6"></a>

```bash
$ cat hello_mpi.c
  
#include <stdio.h>
#include <mpi.h>

int main (int argc, char *argv[])
{
  int nthreads, thread_id;
  int id, np;

  MPI_Init(&argc, &argv);

  MPI_Comm_size(MPI_COMM_WORLD, &np);
  MPI_Comm_rank(MPI_COMM_WORLD, &id);

  printf("I am process %d of %d\n", id, np);

  MPI_Finalize();

  return 0;
}
```

- Compile hello_mpi.c
 
```bash
#GCC compiler
mpicc -o hello_mpi hello_mpi.c
```
or 
```bash
#Intel compiler
mpiicc -o hello_mpi hello_mpi.c
```

- Run `hello_mpi` using 2 MPI cores:
```sh
$ mpirun -n 2 ./hello_mpi
I am process 1 of 2
I am process 0 of 2
```

  
### Fortran example <a name="7"></a>
  
```sh
$ cat hello_mpi.f90

Program hello

  use omp_lib

  IMPLICIT NONE

  include 'mpif.h'

  integer np, id, ierr, rc, len
  character*(MPI_MAX_PROCESSOR_NAME) name
  integer thread_id, nthreads

  call MPI_INIT(ierr)

  call MPI_COMM_SIZE(MPI_COMM_WORLD, np,ierr)
  call MPI_COMM_RANK(MPI_COMM_WORLD, id, ierr)

   write(*,*)" I am process ", id, "of ", np

  call MPI_FINALIZE(ierr)

end program hello
```
  
- Compile hello_mpi.f90
 
```bash
#GCC compiler
mpif90 -o hello_mpi hello_mpi.f90
```
or 
```bash
#Intel compiler
mpiifort -o hello_mpi hello_mpi.f90
```

- Run `hello_mpi` using 2 MPI cores:
```sh
$ mpirun -n 2 ./hello_mpi
I am process 1 of 2
I am process 0 of 2
```


## MPI using Python <a name="8"></a>
### Install mpi4py <a name="9"></a>

- First load both OpenMPI and Python
 ```sh
module load  OpenMPI/4.0.3-GCC-9.3.0 Python/3.8.2-GCCcore-9.3.0 
```
- Install mpi4py using pip
```sh
pip3 install mpi4py
```
### Python example <a name="10"></a>

```python
$ cat hello_mpi.py
from mpi4py import MPI

COMM = MPI.COMM_WORLD
np = COMM.Get_size()
id = COMM.Get_rank()

print("I am process", id, "of", np);
```

- Run `hello_mpi.py` using 2 MPI cores:

```sh
$ mpirun -n 2 python hello_mpi.py
I am process 1 of 2
I am process 0 of 2
```
