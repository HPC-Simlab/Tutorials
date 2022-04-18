# Table of Contents
1. [Some useful information](#1)
2. [Matlab on SIMLAB](#2)
   1. [Use graphical mode](#3)
   2. [Run on interactive mode](#4)
   3. [Run on batch mode](#5)

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

### Use graphical mode <a name="3"></a>

You need to connect using `-X` option, otherwise matlab will be runned as command line.

```sh
$ ssh -X <login>@simlab-cluster.um6p.ma 
```

### Run on interactive mode <a name="4"></a>
```sh
$ srun -p shortq -n 10 -t1:00:00 --pty bash -i
```

### Run on batch mode <a name="5"></a>
```sh
$ cat matlab_job.slurm

#!/bin/bash
#SBATCH --ntasks=1
#SBATCH --mem-per-cpu=2GB
#SBATCH --time=1:00:00

module purge
module load matlab

matlab -nodisplay -r hello
```
- Run the job:

```sh
$ sbatch matlab_job.slurm
```
