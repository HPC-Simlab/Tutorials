# Table of Contents
1. [Description](#desc)
2. [Singularity on SIMLAB](#singsimlab)
3. [Singularity Examples](#singexample)
    1. [Create your own image](#singown)
        1. [Create and build singularity image on your laptop](#singcreate)
        2. [Run the singularity image on interactive mode](#singsinteractive)
        3. [Run the singularity image on batch mode](#singbatch)
    4. [Use existing image on SIMLAB](#singsexist)


## Description <a name="desc"></a>

Singularity is a multi-platform open source container system developed by Sylabs. One of the principal advantages of Singularity is the reproducibility of scientific computations. This system is effective and well adapted to both high performance and artificial intelligence computations. Reproducibility requires the use of containers in order to port applications from one system to another. By using Singularity containers, users can work in reproducible environments of their choice and design. These complete environments can be easily copied and executed on the SIMLAB supercomputer.

## Singularity on SIMLAB <a name="singsimlab"></a>

- List available versions
```sh
$ module avail singularity
---------------------------- /cm/shared/modulefiles ----------------------------
singularity/3.2.1-rc1                           
singularity/images/caffe2_18.08-py2             
singularity/images/caffe2_18.08-py3             
singularity/images/caffe_19.04-py2              
singularity/images/centos-7.5_osu-ompi-3.1.4    
singularity/images/cntk_18.08-py3               
[...]
```

- Load singularity:
```sh
$ module load singularity
```
- To obtain information about the Singularity module, you simply need to use the following command:
```sh
$ module show singularity
```

## Singularity Examples <a name="singexample"></a>
### Create your own image <a name="singown"></a>

#### Create and build singularity image on your laptop <a name="singcreate"></a>

- To create singularity image `<name_container>.def`:

```sh
$ cat <name_container>.def

Bootstrap: docker
From: ubuntu:16.04

%post
    apt-get -y update
    apt-get -y install fortune cowsay lolcat

%environment
    export LC_ALL=C
    export PATH=/usr/games:$PATH

%runscript
    fortune | cowsay | lolcat
```

- To build the container one use `build` commad ([build](https://sylabs.io/guides/2.6/user-guide/build_a_container.html#build-a-container)):
```sh
$ sudo singularity build <name_container>.simg <container>.def
```

- Copy the image on the cluster:
```sh
$ scp -r <name_container>.simg <login>@simlab-cluster.um6p.ma
```

#### Run the singularity image on interactive mode <a name="singsinteractive"></a>

- Load singularity module:
```sh
$ module load singularity/3.2.1-rc1
```
- Example: run on V100 node:
```sh
$ srun -p gpu --gres=gpu:1 --mem=8g --constraint=V100 --pty bash
```
- Run the singularity image:

```sh
$ singularity exec <name_container>.simg sh
```

- You can now start working on your image:
```sh
Singularity>
```

#### Run the singularity image on batch mode <a name="singbatch"></a>

```sh
$ cat Job_Singularity.slurm

#!/bin/sh
#SBATCH --job-name=Singularity-Test
#SBATCH -p gpu
#SBATCH --gres=gpu:1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=4
# SBATCH --gres-flags=enforce-binding
#SBATCH --output=Deep-%j.out
#SBATCH --error=Deep-%j.err

module purge
module load slurm
module load singularity/3.2.1-rc1

singularity exec <name_container>.simg sh
```

- Run the job:
```sh
$ sbatch Job_Singularity.slurm
```

### Use existing image on SIMLAB <a name="singsexist"></a>

- Use `tensorflow_19.04-py3` image:
```sh
$ module load singularity/images/tensorflow_19.04-py3
```

- Run the image:
```sh
$SING_EXEC sh
```

- You can now start working on your image:
```sh
Singularity>
```
