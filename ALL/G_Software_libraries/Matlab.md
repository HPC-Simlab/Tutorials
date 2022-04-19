# Table of Contents
1. [Some useful information](#1)
2. [Matlab on SIMLAB](#2)
   1. [Use graphical mode on the frontend](#3)
   2. [Run Matlab with the graphical mode on interactive mode](#4)
   3. [Run Matlab without the graphical mode on batch mode](#5)

## Description <a name="1"></a>
MATLAB is a programming platform designed specifically for engineers and scientists to analyze and design systems and products that transform our world.

## Matlab on SIMLAB <a name="2"></a>

- List available versions:

```sh
$ module avail matlab
---------------------------- /cm/shared/modulefiles ----------------------------
matlab/gcc/R2019a  matlab/gcc/R2019b  
```
- Load matlab:
```sh
$ module load matlab
```
- List module loaded:

```sh
$ module list
Currently Loaded Modulefiles:
 1) matlab/gcc/R2019b  
```

### Use graphical mode on the frontend <a name="3"></a>

You need to connect using `-X` option, otherwise matlab will be runned as command line.

```sh
$ ssh -X <login>@simlab-cluster.um6p.ma 
```
***You can now load matlab if it's not loaded and run it on the frontend (It's not the recommanded way. Use the interactive or batch mode).***

### Run Matlab with the graphical mode on interactive mode <a name="4"></a>
- Matlab does not work on these nodes: node01, node02, node08, node15. Then you need to exclude them using `--exclude` option:
```sh
$ salloc -p shortq  -t1:00:00 --exclude=node01,node02,node08,node15 --exclusive -N 1 -n 1 
$ ssh -CY $SLURM_NODELIST
```
***You can now load matlab if it's not loaded and run it on the reserved node (**Be careful, if you session is broken the job will be killed**)***

**The best way to run matlab is to use the batch mode**

### Run Matlab without the graphical mode on batch mode <a name="5"></a>
```sh
$ cat matlab_job.slurm

#!/bin/bash

#SBATCH --partition=shortq
#SBATCH --ntasks=1
#SBATCH --mem-per-cpu=2GB
#SBATCH --time=1:00:00

module purge
module load matlab

matlab -nodisplay -r hello # The script name without .m
```
- Run the job:

```sh
$ sbatch matlab_job.slurm
```
