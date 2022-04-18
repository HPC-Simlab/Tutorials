# Table of Contents
1. [Some useful information](#1)
2. [Submit an MPI/OpenMP job in batch](#2)


## Some useful information <a name="1"></a>
The jobs are managed on all of the nodes by the  [Slurm](https://slurm.schedmd.com/documentation.html)  software.

## Submit an MPI/OpenMP job in batch <a name="2"></a>

***C and Fortran example are avaiable [here](https://github.com/HPC-Simlab/Website-utilities/tree/master/TESTS_LIBRARIES/tests_parallel/test_hybride).***

To submit an MPI/OpenMP job in batch on SIMLAB, it is necessary to: 

- Create a submission script:

```bash
$ cat run_omp_mpi.slurm

#!/bin/bash                                                                                                                                                                                                

#SBATCH --partition=shortq         # name of partition
#SBATCH --job-name=Hybrid          # name of job                                                                                                                                                           
#SBATCH --ntasks=1                 # name of the MPI process
#SBATCH --cpus-per-task=10         # number of OpenMP threads
# /!\ Caution, "multithread" in Slurm vocabulary refers to hyperthreading.
##SBATCH --hint=nomultithread      # 1 thread per physical core (no hyperthreading)
#SBATCH --time=00:10:00            # maximum execution time requested (HH:MM:SS)
#SBATCH --output=Hybride%j.out     # name of output file
#SBATCH --error=Hybride%j.out      # name of error file (here, common with the output file)                                                                                                                

# clean out the modules loaded in interactive and inherited by default
module purge

# use additional modules 
module use /cm/shared/modulefiles/

# loading modules
module load slurm OpenMPI/4.0.3-GCC-9.3.0


# number of OpenMP threads
export OMP_NUM_THREADS=$SLURM_CPUS_PER_TASK

# OpenMP binding
export OMP_PLACES=cores

# code execution                                                                                                                                                                                           
mpirun ./hello_omp_mpi
```

- Submit this script via the sbatch command:

```bash
sbatch run_openmp.slurm
```

- This script tells Slurm this is a MPI/OpenMP job, with 2 MPI process, and 4 OpenMP Threads in each process.


```bash
Hello World from thread 1, process 0 of 2, hostname node02
Hello World from thread 0, process 0 of 2, hostname node02
Thread 0 on process 0 of 2 reports: nthreads = 4
Hello World from thread 2, process 0 of 2, hostname node02
Hello World from thread 3, process 0 of 2, hostname node02
Hello World from thread 1, process 1 of 2, hostname node02
Hello World from thread 0, process 1 of 2, hostname node02
Thread 0 on process 1 of 2 reports: nthreads = 4
Hello World from thread 2, process 1 of 2, hostname node02
Hello World from thread 3, process 1 of 2, hostname node02
```
  
