# Table of Contents
1. [Some useful information](#1)
2. [Submit a sequential job in batch](#2)


## Some useful information <a name="1"></a>
The jobs are managed on all of the nodes by the  [Slurm](https://slurm.schedmd.com/documentation.html)  software.

## Submit a sequential job in batch <a name="2"></a>

***C and Fortran example are avaiable [here](https://github.com/HPC-Simlab/Website-utilities/tree/master/TESTS_LIBRARIES/tests_sequentiel).***

To submit a sequential job in batch on SIMLAB, it is necessary to: 

- Create a submission script:

```bash
$ cat run.slurm

#!/bin/bash

#SBATCH --partition=shortq  # partition name 
#SBATCH --job-name=hello    # job name
#SBATCH --output=slurm.out  # output file name
#SBATCH --error=slurm.err   # error file name
#SBATCH --nodes=1           # number of nodes
#SBATCH --ntasks-per-node=1 # number of tasks

module purge                # unload all modules
module load slurm           # load slurm module 

./hello                     # execute the file hello
```

- Submit this script via the `sbatch` command:

```bash
sbatch run.slurm
```

- This script tells Slurm this is a sequential.

```bash
$ cat slurm.out

Hello World
```
