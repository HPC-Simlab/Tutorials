# Table of Contents
1. [Connection on the front end](#1)
2. [Obtaining a terminal on a CPU compute node](#2)
3. [Interactive execution on the CPU partition](#3)
4. [Interactive execution on the CPU partition](#4)
5. [Connect to the node using graphical mode](#5)


## Some useful information <a name="1"></a>
The jobs are managed on all of the nodes by the  [Slurm](https://slurm.schedmd.com/documentation.html)  software.

## Connection on the front end <a name="2"></a>

```sh
ssh login@simlab-cluster@um6p.ma
```

The interactive node resources are shared between all the connected users: As a result, the interactive on the front end is reserved exclusively for compilation and script development.

All interactive executions of your codes must be done on the CPU compute nodes by using one of the two following commands:

- The `srun` command :
    - to obtain a terminal on a CPU compute node within which you can execute your code,
    - or to directly execute your code on the CPU partition.
- Or, the salloc command to reserve CPU resources which would allow you to do more than one execution.

**However, if the computations require a large amount of CPU resources (in number of cores, memory, or elapsed time), it is necessary to submit a batch job.**

## Obtaining a terminal on a CPU compute node <a name="3"></a>

It is possible to open a terminal directly on a compute node on which the resources have been reserved for you (here 4 cores) by using the following command:
```sh
$ srun --pty --ntasks=1 --cpus-per-task=4  [--other-options] bash
```

**Comments:** <a name="6"></a>

- An interactive terminal is obtained with the `--pty` option.
- By default, the allocated CPU memory is proportional to the number of reserved cores. For example, if you request 1/4 of the cores of a node, you will have access to 1/4 of its memory. You can consult our documentation on this subject : [Memory allocation on CPU partitions](#mem.md).
- `--other-options` contains the usual Slurm options for job configuration (`--time=`, etc.): See the documentation on batch submission scripts in the index section [Commands of a CPU code](https://github.com/HPC-Simlab/Tutorials/tree/master/ALL/D_Commands_of_a_CPU_code).
- The reservations have all the resources defined in Slurm by default, per partition and per QoS (Quality of Service). You can modify the limits of them by specifying another partition and/or QoS as detailed in our documentation about the partitions and QoS.

The terminal is operational after the resources have been granted: 

```sh
$ srun --pty --ntasks=1 --cpus-per-task=4 bash
[team1337@node14 ~]$ 
```

You can verify if your interactive job has started by using the `squeue` command. 
Complete information about the status of the job can be obtained by using the scontrol show job `<job identifier>` command.

After the terminal is operational, you can launch your executable files in the usual way: `./your_executable_file`. 
For an MPI execution, you should again use `srun` : `srun ./your_mpi_executable_file`. 

To leave the interactive mode :

```sh
[team1337@node14 ~]$ exit
```

Caution: If you do not yourself leave the interactive mode, the maximum allocation duration 
(by default or specified with the `--time` option) is applied and this amount of hours is then counted for the project you have specified.

## Interactive execution on the CPU partition <a name="4"></a>

If you don't need to open a terminal on a compute node, it is also possible to start the interactive execution of a code on the compute nodes directly from the front end by using the following command (here with 4 tasks) :
```sh
$ srun --ntasks=4 [--other-options] ./my_executable_file
```
**Comments:**
Same as comments above in [section](#6)

## Connect to the node using graphical mode <a name="5"></a>


Reserving resources (here for 4 tasks) is done via the following command:
```sh
$ salloc --ntasks=4 [--other-options]
```

**Comments:**
Same as comments above in [section](#6)

The reservation becomes usable after the resources have been granted:

```sh
salloc: Granted job allocation 32318
```

You can verify that your reservation is active by using the `squeue` command. 
```sh
$ squeue -u team1337
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
             32329      defq     bash team1337  R       0:05      1 node14
```
Complete information about the status of the job can be obtained by using the scontrol show job `<job identifier>` command.

You can connect to the node `node14` using the `ssh` command:

```sh
$ ssh -CY $node14
Last login: Wed Apr 20 23:40:18 2022 from frontend02.cm.cluster
```

Important:

- `-CY` for the graphical mode (for example, you can run graphical mode of matlab, ...)

- Exit the node
```sh
$ exit
déconnexion
Connection to node14 closed.
```

- Therefore, to cancel the reservation, it is necessary to manually enter:

```sh
$ exit
exit
salloc: Relinquishing job allocation 32323

```

