# Table of Contents
1. [Some useful information](#1)
2. [OPENMP on SIMLAB](#2)
3. [Examples](#3)
    1. [C example](#4)
    3. [Fortran example](#5)

## Some useful information <a name="1"></a>

Multi-threading is a type of execution model that allows multiple threads to exist within the context of a process. Simply speaking, a Slurm multi-threading job is a single process, multi-core job. Many application can belong to this category, OpenMP programs are an example.

## OPENMP on SIMLAB <a name="2"></a>

You need to load either `ICC` or `GCC` to compile your code.

## Examples <a name="3"></a>
### C example <a name="4"></a>
 
```sh
$ cat hello_openmp.c

#include <omp.h>
#include <stdio.h>

int main (int argc, char *argv[])
{
  int nthreads, thread_id;

#pragma omp parallel private(nthreads, thread_id)
  {
    thread_id = omp_get_thread_num();
    printf("Thread %d says: Hello World\n", thread_id);

    if (thread_id == 0)
      {
	nthreads = omp_get_num_threads();
	printf("Thread %d reports: the number of threads are %d\n", 
	       thread_id, nthreads);
      }
  }

  return 0;
}
```
  
 
- Compile hello_openmp.c
 
```bash
# GCC compiler
gcc -o hello_openmp -fopenmp hello_openmp.c
```
or 
```bash
# Intel compiler
icc -o hello_openmp -fopenmp hello_openmp.c
```

- Run `hello_openmp` using 2 threads: <a name="exec"></a>

***Remark: Export the number of threads using `OMP_NUM_THREADS` (default number is all threads available)***
```sh
$ export OMP_NUM_THREADS=2
./hello_openmp

Thread 0 says: Hello World
Thread 0 reports: the number of threads are 2
Thread 1 says: Hello World
```
  
### Fortran example <a name="5"></a>
  
```sh
$ cat hello_openmp.f90

PROGRAM Parallel_Hello_World
USE OMP_LIB

!$OMP PARALLEL

    PRINT *, "Hello from process: ", OMP_GET_THREAD_NUM()

!$OMP END PARALLEL

END
```
  
- Compile hello_openmp.f90
 
```bash
# GCC compiler
gfortran -fopenmp hello_openmp.f90 -o hello_openmp
```
or 
```bash
# Intel compiler
ifort -fopenmp hello_openmp.f90 -o hello_openmp 
```

For running the `hello_openmp` use the same process described in the [C example](#exec)
