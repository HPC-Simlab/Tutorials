# Table of Contents
1. [Some useful information](#1)
2. [Submit an MPI job in batch](#2)


## Some useful information <a name="1"></a>
The jobs are managed on all of the nodes by the  [Slurm](https://slurm.schedmd.com/documentation.html)  software.

## Submit an MPI job in batch <a name="2"></a>

***C and Fortran example are avaiable [here](https://github.com/HPC-Simlab/Website-utilities/tree/master/TESTS_LIBRARIES/tests_parallel/test_mpi).***

To submit an MPI job in batch on SIMLAB, it is necessary to: 

- Create a submission script:
 
```bash
$ cat run_mpi.slurm

#!/bin/bash

#SBATCH --partition=shortq          # partition name
#SBATCH --job-name=mpi              # name of the job
#SBATCH --nodes=2                   # number of nodes
#SBATCH --ntasks-per-node=4         # number of MPI processes per node
# /!\ Caution, "multithread" in Slurm vocabulary refers to hyperthreading.
#SBATCH --hint=nomultithread        # 1 MPI process per physical core (no hyperthreading)
#SBATCH --time=00:01:00             # maximum execution time requested (HH:MM:SS)
#SBATCH --output=mpi%j.out          # name of output file
#SBATCH --error=mpi%j.out           # name of error file (here, in common with output)

# cleans out the modules loaded in interactive and inherited by default
module purge

# use additional modules 
module use /cm/shared/modulefiles/

# load modules
module load slurm OpenMPI/4.0.3-GCC-9.3.0

# echo of launched commands
set -x

mpirun ./hello_mpi
# for Python example: mpirun python hello_mpi.py
```
- Submit this script via the `sbatch` command:

```bash
$ sbatch run_mpi.slurm
```

- This script tells Slurm this is a MPI job, using 4 processes on two nodes.

```bash
$ cat mpi<jobid>.out

+ mpirun ./hello_mpi
I am process 3 of 8, hostname node01
I am process 0 of 8, hostname node01
I am process 1 of 8, hostname node01
I am process 2 of 8, hostname node01
I am process 4 of 8, hostname node02
I am process 5 of 8, hostname node02
I am process 6 of 8, hostname node02
I am process 7 of 8, hostname node02
```
