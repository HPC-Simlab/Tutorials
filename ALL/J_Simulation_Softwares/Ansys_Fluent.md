# Table of Contents
1. [Description](#1)
2. [Ansys Fluent on SIMLAB](#2)
3. [Running fluent models](#3)
    1. [Iterative mode](#4)
    2. [Batch mode (via slurm)](#5)

## Description <a name="1"></a>
Ansys Fluent is the industry-leading fluid simulation software known for its advanced physics modeling capabilities and industry leading accuracy.

## Ansys Fluent on SIMLAB <a name="2"></a>

- Connect on graphical mode using `-Y` option

```sh
ssh -Y <login>@simlab-cluster@um6p.ma
```
- List available versions:

```sh
$ module avail ansys
---------------------------- /cm/shared/modulefiles ----------------------------
ansys/2020.r1  ansys/2021.r1  ansys/v201   
```

- Now you can load `ansys/2020.r1` and run `runwb2` command to open Ansys:

```sh
$ module load ansys/2020.r1
$ runwb2
```

## Running fluent models <a name="3"></a>

### Iterative mode <a name="4"></a>

- For workbench usage under visualization node:

```sh
$ module load visualization/visTurboVNC
$ runTurboVNC.sh
```

- Connect to visualization node `visu01`:
```sh
$ ssh -CY visu01
```

- Now you can load `ansys/2020.r1` and run `runwb2` command to open Ansys:

```sh
$ module load ansys/2020.r1
```
- Run `fluent` and create/change the geometry:
```sh
$ fluent
```
- Or run directlu the fluent test (create the file `fluent-srun.sh`):

```sh
$ cat fluent-srun.sh

#!/bin/bash
fluent 3ddp -g -t${SLURM_NTASKS} -ssh -i test.jou -mpi=intel 
```

- Run the script file `fluent-srun.sh`:
```sh
$ srun -n <tasks> ./fluent-srun.sh
```

### Batch mode (via slurm) <a name="5"></a>

- Running `test.jou`

```sh
$ cat runfluent.slurm

#!/bin/bash

#SBATCH -J ANSYS_FLUENT # Job Name 
#SBATCH -N 1 # Number of Nodes to use 
# SBATCH -n 14 # Number of CPUs
#SBATCH --ntasks-per-node=14 
#SBATCH -o fluent_job.%j.%a.out # Output file name 
#SBATCH -e fluent_job.%j.%a.err # Error file name 
#SBATCH -p shortq # Partition to run on 
#SBATCH --verbose

# Remove all currently running modules and load Intel MPI and Ansys V2020.r1
module purge 
module load slurm
module load Intel_tools 
module add ansys/2020.r1

export FLUENT_GUI=off 
#Turns the Fluent GUI off

export I_MPI_ROOT=/cm/shared/apps/intel/compilers_and_libraries_2018.2.199/linux/mpi
#Tells fluent where Intel MPI is located 

export I_MPI_DEBUG=5 

#Checks number of tasks and sets number of processes 
if [ -z "$SLURM_NPROCS" ]; then N=$(( $(echo $SLURM_TASKS_PER_NODE | sed -r 's/([0-9]+)\(x([0-9]+)\)/\1 * \2/') )) 
else N=$SLURM_NPROCS 
fi 

# Prints number of processes to output file 
echo $SLURM_NPROCS 
echo -e "N: $N\n"; 

# run fluent in batch on the allocated node(s) 
srun hostname -s > hostfile 

# run Fluent 3d double precision without GUI on 1 node using 14 processors
fluent 3ddp -g -t${SLURM_NTASKS} -ssh -i test.jou -mpi=intel 

STATUS=$?

echo "================================================================" 
date
echo "================================================================" 
echo "" 

echo "STATUS = $STATUS" 
echo "" 
```
- Submit this script via the sbatch command:

```sh
$ sbatch runfluent.slurm
```
