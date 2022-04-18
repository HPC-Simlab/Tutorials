# Table of Contents
1. [Some useful information](#1)
2. [Submit Single-GPU job in batch](#2)
    1. [C++ example](#3)
    2. [Python example](#4)


## Some useful information <a name="1"></a>

The jobs are managed on all of the nodes by the  [Slurm](https://slurm.schedmd.com/documentation.html)  software.

## Submit Single-GPU job in batch <a name="2"></a>

#### Remark:
- **To submit a job under GPU partition you need to add `--partition=gpu` to your job file.**
- **`--gres=gpu:1`: is used to activate the GPU card, otherwise GPU is not used.**

### C++ example <a name="3"></a>

- Create the job file `cuda.slurm`:

```bash
$ cat cuda.slurm

#!/bin/bash

#SBATCH --partition=gpu              # partition name
#SBATCH --job-name=single_gpu        # name of job 
#SBATCH --nodes=1                    # we request one node   
#SBATCH --ntasks-per-node=1          # with one task per node
#SBATCH --gres=gpu:1                 # number of GPUs (only one GPU per node is allowed for the `gpu` partition)
#SBATCH --cpus-per-task=1            # number of cores per task (>1 if multi-threaded tasks)
#SBATCH --hint=nomultithread         # hyperthreading is deactivated
#SBATCH --time=00:10:00              # maximum execution time requested (HH:MM:SS)
#SBATCH --output=gpu_single%j.out    # name of output file
#SBATCH --error=gpu_single%j.out     # name of error file (here, in common with the output file)

module purge
module load CUDA/11.1.1-GCC-10.2.0
nvcc cuda_example.cu
```
- Run the job;

```sh
$ sbatch cuda.slurm
```

## Python example 

- Create the job file `cuda.slurm`:

```bash
$ cat cuda.slurm

#!/bin/bash

#SBATCH --partition=gpu              # partition name
#SBATCH --job-name=single_gpu        # name of job 
#SBATCH --nodes=1                    # we request one node   
#SBATCH --ntasks-per-node=1          # with one task per node
#SBATCH --gres=gpu:1                 # number of GPUs (only one GPU per node is allowed for the `gpu` partition)
#SBATCH --cpus-per-task=1            # number of cores per task (>1 if multi-threaded tasks)
#SBATCH --hint=nomultithread         # hyperthreading is deactivated
#SBATCH --time=00:10:00              # maximum execution time requested (HH:MM:SS)
#SBATCH --output=gpu_single%j.out    # name of output file
#SBATCH --error=gpu_single%j.out     # name of error file (here, in common with the output file)

module purge
module load Python/3.8.6-GCCcore-10.2.0
python cuda_example.py
```

- Run the job:

```sh
$ sbatch cuda.slurm
```
