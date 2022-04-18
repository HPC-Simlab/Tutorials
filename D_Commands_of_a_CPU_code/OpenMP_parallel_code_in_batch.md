# Table of Contents
1. [Some useful information](#1)
2. [Submit an OpenMP job in batch](#2)

## Some useful information <a name="1"></a>
The jobs are managed on all of the nodes by the  [Slurm](https://slurm.schedmd.com/documentation.html)  software.

## Submit an MPI/OpenMP job in batch <a name="2"></a>

***C and Fortran example are avaiable [here](https://github.com/HPC-Simlab/Website-utilities/tree/master/TESTS_LIBRARIES/tests_parallel/test_openmp).***

To submit an OpenMP job in batch on SIMLAB, it is necessary to: 

- Create a submission script:

```bash
$ cat run_openmp.slurm

#!/bin/bash
#SBATCH --partition=shortq          # partition name
#SBATCH --job-name=omp              # name of the job
#SBATCH --nodes=1                   # number of nodes
#SBATCH --ntasks=1                  # number of tasks (a single process here)
#SBATCH --cpus-per-task=8           # number of OpenMP threads
# /!\ Caution, "multithread" in Slurm vocabulary refers to hyperthreading.
#SBATCH --hint=nomultithread        # reserve physical (not logical) cores
#SBATCH --time=00:01:00             # maximum execution time requested (HH:MM:SS)
#SBATCH --output=omp%j.out          # name of output file
#SBATCH --error=omp%j.out           # name of error file (here, in common with output)
 
# cleans out the modules loaded in interactive and inherited by default
module purge

# use additional modules 
module use /cm/shared/modulefiles/

# loads modules (slurm GCC9)
module load slurm GCC/9.3.0

# echo of launched commands
set -x
 
# number of OpenMP threads
export OMP_NUM_THREADS=$SLURM_CPUS_PER_TASK 
 
# Binding
export OMP_PLACES=cores
 
# code execution
./hello_openmp
```

- Submit this script via the `sbatch` command:


```bash
$ sbatch run_openmp.slurm
```

- This script tells Slurm this is a multi-threading job, with 1 process, and 8 OpenMP threads.

```bash
+ export OMP_NUM_THREADS=8
+ OMP_NUM_THREADS=8
+ export OMP_PLACES=cores
+ OMP_PLACES=cores
+ ./hello_openmp
Thread 0 says: Hello World
Thread 0 reports: the number of threads are 8
Thread 1 says: Hello World
Thread 7 says: Hello World
Thread 4 says: Hello World
Thread 2 says: Hello World
Thread 6 says: Hello World
Thread 5 says: Hello World
Thread 3 says: Hello World
```
