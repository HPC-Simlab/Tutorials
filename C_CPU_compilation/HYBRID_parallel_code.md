# Table of Contents
1. [Some useful information](#1)
2. [Hybrid MPI/OpenMP on SIMLAB](#2)
3. [Examples](#3)
    1. [C example](#4)
    2. [Fortran example](#5)


## Some useful information <a name="1"></a>

## Hybrid MPI/OpenMP on SIMLAB <a name="2"></a>

To use the hybrid parallelization you need to load either Intel or Open MPI using see [MPI on SIMLAB](MPI_parallel_code.md)

## Examples <a name="3"></a>
### C example <a name="4"></a>

```bash
$ cat hello_omp_mpi.c

#include <stdio.h>
#include <omp.h>
#include <mpi.h>

int main (int argc, char *argv[])
{
  int nthreads, thread_id;
  int id, np;
  char processor_name[MPI_MAX_PROCESSOR_NAME];
  int processor_name_len;

  MPI_Init(&argc, &argv);

  MPI_Comm_size(MPI_COMM_WORLD, &np);
  MPI_Comm_rank(MPI_COMM_WORLD, &id);
  MPI_Get_processor_name(processor_name, &processor_name_len);

#pragma omp parallel private(nthreads, thread_id)
  {
    thread_id = omp_get_thread_num();
    
    // print output only for thread 0
    if (thread_id == 0)
      {
        nthreads = omp_get_num_threads();
        printf("Thread %d on process %d of %d reports: nthreads = %d\n",
               thread_id, id, np, nthreads);
      }
  }

  MPI_Finalize();
  return 0;
}
```
  
 - Compile hello_omp_mpi.c

```bash
#GCC compiler
mpicc -fopenmp hello_omp_mpi.c -o hello_omp_mpi
```
or 
```bash
#Intel compiler
mpiicc -fopenmp hello_omp_mpi.c -o hello_omp_mpi
```
- Run `hello_omp_mpi` using 2 MPI cores and 3 threads (The output is printed only for thread 0):

***Remark: Export the number of threads using OMP_NUM_THREADS (default number is all threads available)***

```sh
$ export OMP_NUM_THREADS=3
$ mpirun -n 2 ./hello_omp_mpi 
Thread 0 on process 1 of 2 reports: nthreads = 3
Thread 0 on process 0 of 2 reports: nthreads = 3
```
### Fortran example <a name="5"></a>
  
```sh
$ cat hello_omp_mpi.f90
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
  call MPI_GET_PROCESSOR_NAME(name, len,ierr)

  !$OMP PARALLEL PRIVATE(thread_id)
  thread_id=OMP_GET_THREAD_NUM()

   if (thread_id == 0) then
      nthreads = OMP_GET_NUM_THREADS()
      write(*,*) "Thread ", thread_id, "on process ", id, "of ", np, " reports: nthreads = ", nthreads
   endif
  !$OMP END PARALLEL

  call MPI_FINALIZE(ierr)

end program hello
```
  
- Compile hello_omp_mpi.f90
 
```bash
#GCC compiler
mpif90 -fopenmp hello_omp_mpi.f90 -o hello_omp_mpi
```
or 
```bash
#Intel compiler
mpiifort -fopenmp hello_omp_mpi.f90 -o hello_omp_mpi
```

- Run `hello_omp_mpi` using 2 MPI cores and 3 threads (The output is printed only for thread 0):

***Remark: Export the number of threads using OMP_NUM_THREADS (default number is all threads available)***

```sh
$ export OMP_NUM_THREADS=3
$ mpirun -n 2 ./hello_omp_mpi 
Thread 0 on process 1 of 2 reports: nthreads = 3
Thread 0 on process 0 of 2 reports: nthreads = 3
```
