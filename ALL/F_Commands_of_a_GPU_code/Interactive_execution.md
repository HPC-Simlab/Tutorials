# Table of Contents
1. [Connection on the front end](#1)
2. [Obtaining a terminal on a GPU compute node](#2)
3. [Interactive execution on the GPU partition](#3)
4. [Interactive execution on the GPU partition](#4)
5. [Connect to the node using graphical mode](#5)


## Some useful information <a name="1"></a>
The jobs are managed on all of the nodes by the  [Slurm](https://slurm.schedmd.com/documentation.html)  software.

## Connection on the front end <a name="2"></a>

```sh
ssh login@simlab-cluster@um6p.ma
```

The interactive node resources are shared between all the connected users: As a result, the interactive on the front end is reserved exclusively for compilation and script development.

All interactive executions of your codes must be done on the GPU compute nodes by using one of the two following commands:

- The `srun` command :
    - to obtain a terminal on a GPU compute node within which you can execute your code,
    - or to directly execute your code on the GPU partition.
- Or, the salloc command to reserve GPU resources which would allow you to do more than one execution.

**However, if the computations require a large amount of GPU resources (in number of cores, memory, or elapsed time), it is necessary to submit a batch job.**

## Obtaining a terminal on a GPU compute node <a name="3"></a>

It is possible to open a terminal directly on a compute node on which the resources have been reserved for you (here 4 cores) by using the following command:
```sh
$ srun --pty --partition=gpu --nodes=1  --gres=gpu:1 [--other-options] bash
```

**Comments:** <a name="6"></a>

- An interactive terminal is obtained with the `--pty` option.
- By default, the allocated GPU memory is proportional to the number of reserved cores. For example, if you request 1/4 of the cores of a node, you will have access to 1/4 of its memory. You can consult our documentation on this subject : [Memory allocation on GPU partitions](#mem.md).
- `--other-options` contains the usual Slurm options for job configuration (`--time=`, etc.): See the documentation on batch submission scripts in the index section [Commands of a GPU code](https://github.com/HPC-Simlab/Tutorials/tree/master/ALL/F_Commands_of_a_GPU_code).
- The reservations have all the resources defined in Slurm by default, per partition and per QoS (Quality of Service). You can modify the limits of them by specifying another partition and/or QoS as detailed in our documentation about the partitions and QoS.
- `--partition=gpu` required to use the GPU nodes.

The terminal is operational after the resources have been granted: 

```sh
$ srun --pty --partition=gpu --ntasks=1 --cpus-per-task=4 bash
[team1337@node09 ~]$ 
```
### NVIDIA-GPU process viewer
- `nvitop` is a tool for enriching the output of `nvidia-smi` (installed on Python/3.8.2-GCCcore-9.3.0).

```sh
$ module load Python/3.8.2-GCCcore-9.3.0
$ nvitop 
Thu Apr 21 01:03:14 2022
╒═════════════════════════════════════════════════════════════════════════════╕
│ NVIDIA-SMI 460.32.03    Driver Version: 460.32.03    CUDA Version: 11.2     │
├───────────────────────────────┬──────────────────────┬──────────────────────┤
│ GPU  Name        Persistence-M│ Bus-Id        Disp.A │ Volatile Uncorr. ECC │
│ Fan  Temp  Perf  Pwr:Usage/Cap│         Memory-Usage │ GPU-Util  Compute M. │
╞═══════════════════════════════╪══════════════════════╪══════════════════════╪════════════════════╕
│   0  Tesla P40           On   │ 00000000:3B:00.0 Off │                    0 │ MEM: ▏ 0.0%        │
│ MAX   20C    P8     9W / 250W │        0B / 22.38GiB │      0%      Default │ UTL: ▏ 0%          │
╘═══════════════════════════════╧══════════════════════╧══════════════════════╧════════════════════╛
[ CPU: █▌ 2.9%                                                ]  ( Load Average:  1.08  1.03  0.79 )
[ MEM: █▉ 3.8%                                                ]  [ SWP: █████████████▋ 62.1%       ]

╒══════════════════════════════════════════════════════════════════════════════════════════════════╕
│ Processes:                                                                       team1337@node15 │
│ GPU     PID      USER  GPU-MEM %SM  %CPU  %MEM  TIME  COMMAND                                    │
╞══════════════════════════════════════════════════════════════════════════════════════════════════╡
│  No running processes found                                                                      │
╘══════════════════════════════════════════════════════════════════════════════════════════════════╛

```

You can verify if your interactive job has started by using the `squeue` command. 
Complete information about the status of the job can be obtained by using the scontrol show job `<job identifier>` command.

After the terminal is operational, you can launch your executable files in the usual way: `./your_executable_file`. 
For an MPI execution, you should again use `srun` : `srun ./your_mpi_executable_file`. 

To leave the interactive mode :

```sh
[team1337@node09 ~]$ exit
```

Caution: If you do not yourself leave the interactive mode, the maximum allocation duration 
(by default or specified with the `--time` option) is applied and this amount of hours is then counted for the project you have specified.

## Interactive execution on the GPU partition <a name="4"></a>

If you don't need to open a terminal on a compute node, it is also possible to start the interactive execution of a code on the compute nodes directly from the front end by using the following command (here with 4 tasks) :
```sh
$ srun --ntasks=4 --partition=gpu [--other-options] ./my_executable_file
```
**Comments:**
Same as comments above in [section](#6)

## Connect to the node using graphical mode <a name="5"></a>


Reserving resources (here for 4 tasks) is done via the following command:
```sh
$ salloc --partition=gpu --ntasks=4 [--other-options]
```

**Comments:**
Same as comments above in [section](#6)

The reservation becomes usable after the resources have been granted:

```sh
salloc: Granted job allocation 32339
```

You can verify that your reservation is active by using the `squeue` command. 
```sh
$ squeue -u team1337
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
             32340       gpu     bash team1337  R       0:02      1 node09
```
Complete information about the status of the job can be obtained by using the scontrol show job `<job identifier>` command.

You can connect to the node `node09` using the `ssh` command:

```sh
$ ssh -CY $node09
```

Important:

- `-CY` for the graphical mode (for example, you can run graphical mode of matlab, ...)

- Exit the node
```sh
$ exit
déconnexion
Connection to node09 closed.
```

- Therefore, to cancel the reservation, it is necessary to manually enter:

```sh
$ exit
exit
salloc: Relinquishing job allocation 32340
```

