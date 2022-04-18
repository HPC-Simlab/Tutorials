# Table of Contents
1. [Some useful information](#1)
2. [SLURM Concepts](#2)
3. [SLURM useful commands](#3)
4. [SLURM partitions and nodes](#4)
5. [Submitting a job to the cluster](#5)
    1. [Submit a job using `srun`](#6)
        1. [Usage](#7)
    3. [Submit a job using `sbatch`](#8)
        1. [Usage](#9)
        2. [Batch scripts rules](#10)
    4. [Execution parameters](#11)
        1. [Parameters for log](#12)
        2. [Parameters to control the job](#13)
        3. [Parameters for multithreading](#14)
    5. [Job information](#15)
    6. [Manage jobs](#16)

## Some useful information <a name="1"></a>

SLURM is the queue manager used on SIMLAB cluster, it is an open-source workload manager designed for Linux clusters, it provides three key functions:
1. It allocates exclusive and/or non-exclusive access to resources (computer nodes) to users for some duration of time so they can perform work.
2. It provides a framework for starting, executing, and monitoring work on a set of allocated nodes.
3. t arbitrates contention for resources by managing a queue of pending work.

The following material will explain how to use SLURM.
Some of the content is exclusive to simlab cluster, and to be used from the host simlab-cluster.um6p.ma

## SLURM Concepts <a name="2"></a>

| Term      | Description                                                                                                                     |
|-----------|---------------------------------------------------------------------------------------------------------------------------------|
| Task      | A task under SLURM is a synonym for a process, and is often the number of MPI processes                                         |
| Success   | A job completes and terminates well (with exit status 0) (cancelled jobs are not considered successful)                         |
| Socket    | A socket contains one processor                                                                                                 |
| Node      | A node contains one or more sockets                                                                                             |
| Resource  | A mix of CPUs, memory and time                                                                                                  |
| Processor | A processor contains one or more cores                                                                                          |
| Partition | SLURM groups nodes into sets called partitions. Jobs are submitted to a partition to run.<br>SIMLAB default partition is (defq) |
| Failure   | Anything that lacks success                                                                                                     |
| Core      | A processor core                                                                                                                |
| Batch job | A chain of commands in a script file                                                                                            |

## SLURM useful commands <a name="3"></a>

| command | Description                                                                                                                                                                                        |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| salloc  | allocate resources for a job in real time (typically used to allocate resources and spawn a shell, in which the srun<br>command is used to launch parallel tasks                                   |
| sbatch  | submit a job script for later execution (the script typically contains one or more srun commands to launch parallel tasks)                                                                          |
| scancel | cancel a pending or running job                                                                                                                                                                    |
| sinfo   | reports the state of partitions and nodes managed by Slurm (it has a variety of filtering, sorting, and formatting options)                                                                        |
| squeue  | reports the state of jobs (it has a variety of filtering, sorting, and formatting options), by defaul reports the running<br>jobs in priority order followed by the pending jobs in priority order |
| srun    | used to run application on requested/allocated resources in real time on command line (interactive job) or inside batch<br>job                                                                     |
| sacct   | report job accounting information about active or completed jobs                                                                                                                                   |
|         |                                                                                                                                                                                                    |

## SLURM partitions and nodes <a name="4"></a>

The SIMLAB cluster is organized into several SLURM partitions.
Each partition gathers a set of compute nodes, you can check SIMLAB partitions [here](slurm_at_simlab.md).

The default partition used by SLURM (defq).

- To view all the partitions available on the cluster and the nodes available on each partition:

```bash
$ sinfo

PARTITION AVAIL  TIMELIMIT  NODES  STATE NODELIST
defq*        up    1:00:00      3    mix node[01,03-04]
defq*        up    1:00:00      2  alloc node[02,05]
gpu          up 2-00:00:00      1   drng node06
gpu          up 2-00:00:00      1  drain node07
gpu          up 2-00:00:00      4    mix node[09-10,14,16]
gpu          up 2-00:00:00      2  alloc node[08,17]
gpu          up 2-00:00:00      4   idle node[11-13,15]
[...]
```

- To see available nodes run:

```bash
$sinfo -Nl

Tue Jan  8 11:48:21 2019
NODELIST   NODES PARTITION       STATE CPUS    S:C:T MEMORY TMP_DISK WEIGHT AVAIL_FE REASON
node01         1     longq        idle   40   2:20:1 128823    51175      1 broadwel none
node01         1    shortq        idle   40   2:20:1 128823    51175      1 broadwel none
node01         1     defq*        idle   40   2:20:1 128823    51175      1 broadwel none
node02         1     longq        idle   40   2:20:1 128823    51175      1 broadwel none
node02         1    shortq        idle   40   2:20:1 128823    51175      1 broadwel none
node02         1     defq*        idle   40   2:20:1 128823    51175      1 broadwel none
node03         1     longq    drained*   44   2:22:1 385483    51175      1  skylake 'Drained by cmdaemon
node03         1    shortq    drained*   44   2:22:1 385483    51175      1  skylake 'Drained by cmdaemon
node03         1     defq*    drained*   44   2:22:1 385483    51175      1  skylake 'Drained by cmdaemon
[...]
```


## Submitting a job to the cluster <a name="5"></a>

There are two commands to submit a job to the cluster:

`srun` to run jobs interactively
`sbatch` to submit a batch job

### Submit a job using `srun` <a name="6"></a>

To learn more about the `srun` command, see [the official documentation](https://slurm.schedmd.com/srun.html)

#### Usage <a name="7"></a>

The job will start immediately after you execute the srun command, and it will use the ressources specified to **srun**, or already allocated with **salloc** if any.
The outputs are returned to the terminal.
You have to wait until the job has terminated before starting a new job.
This works with ANY command.

Example:

1. Allocate resources:

```bash
$ salloc --nodes=1 -p shortq

salloc: Pending job allocation 26364
salloc: job 26364 queued and waiting for resources
salloc: job 26364 has been allocated resources
salloc: Granted job allocation 26364
```

- `--nodes=1`: specify the desired number of nodes
- `-p shortq`: specify the desired partition


2. Run job in the allocated resources:

```bash
$srun hostname
```

3. Check the status of the job:

```bash
$squeue --user $(whoami)

JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
26364    shortq     bash rmahjoub  R       7:09      1 no
```

- `squeue --user $(whoami)`: shows status of jobs that belongs to the current user

4- Example if an interaction is needed: 

```bash
$ module load R
$ salloc --nodes=1 -p shortq
$ srun --pty R
$ demo(graphics)
$ q()
```
- `--pty`: will keep the interaction possible
- `q()`: to quit R

- To run  a job in a specific category of nodes, for example to run the job in a node with <em>skylake</em> cpu: <a name="11"></a>

```bash
$ srun -p gpu --constraint=skylake --pty bash
```

- `-p gpu`: specify the desired partition
- `--pty`: keeps the interaction possible

### Submit a job using `sbatch` <a name="8"></a>

To learn more about the `sbatch` command, see [the official documentation](https://slurm.schedmd.com/sbatch.html)

#### Usage <a name="9"></a>

The job starts when resources are available.
The command only returns the job id.
The outputs are sent to file(s).
This works ONLY with shell scripts. The batch script may be given to sbatch through a file name on the command line, or if no file name is specified, sbatch will read in a script from standard input.

Exemple of submission file:

```bash
$ cat test.slrm

#!/bin/sh
#SBATCH --nodes=2           # number of nodes
#SBATCH --partition shortq  # partition
#SBATCH -o slurm.out        # STDOUT

# print the number of the allocated nodes
echo number of nodes: $SLURM_JOB_NUM_NODES

# launch a command or an application (in this case it's the system command "hostname")
srun hostname

```

```bash
$sbatch test.slrm
Submitted batch job 5256

$cat slurm.out
number of nodes 2
node01
node03
```

#### Batch scripts rules <a name="10"></a>

1. The script can contain srun commands. Each srun is a job step. 
The script must start with shebang (#!) followed by the path of the interpreter

```bash
#!/bin/bash
```

2. The execution parameters can be set within the terminal as for the previous examle or At runtime in the command `sbatch`, for example we can set the number of nodes:

```bash
$ sbatch --nodes=1 test.slrm
```

```bash
$ sbatch test.slrm
Submitted batch job 5257

$ cat slurm.out
number of nodes 1
node03
```

3. The scripts can contain slurm options just after the shebang but before the script commands `#SBATCH`

**Note** that however the number of nodes is specified in the script, it was overided by the command line.

**Advice:** We recommend to set as many parameters as you can in the script to keep a track of your execution parameters for a future submission.

**Note** that the syntax `#SBATCH` is important and doesn't contain any `!` (as in the Shebang)

### Execution parameters <a name="11"></a>

These parameters are common to the commands `srun` and `sbatch`.

#### Parameters for log <a name="12"></a>

```bash
#!/bin/bash
#
#SBATCH -o slurm.%N.%j.out  # STDOUT file with the Node name and the Job ID
#SBATCH -e slurm.%N.%j.err  # STDERR file with the Node name and the Job ID
```

#### Parameters to control the job <a name="13"></a>

**`--partition=<partition_names>`, `-p`**

Request a specific partition for the resource allocation. Each partition (queue) have their own limits: time, memory, nodes ...

Cf: `sinfo` to know which partitions are available.

**`--mem=<size[units]>`**

Specify the real memory required per node. The default units is `MB`

The job is killed if it exceeds the limit

**`--time=<time>`, `-t`**

Set a limit on the total run time of the job allocation.

Acceptable time formats include "minutes", "minutes:seconds", "hours:minutes:seconds", "days-hours", "days-hours:minutes" and "days-hours:minutes:seconds".

#### Parameters for multithreading <a name="14"></a>

**`--cpus-per-task=<ncpus>`, `--cpus`, `-c`**

Request a number of CPUs (default 1)

Note that you can use the variable `$SLURM_CPUS_PER_TASK` in the command line to avoid mistake between the resource allocated and the job.

```bash
#!/bin/bash

#SBATCH --cpus-per-task=8

srun bowtie2 --threads $SLURM_CPUS_PER_TASK -x hg19 -1 sample_R1.fq.gz -2 sample_R2.fq.gz -S sample_hg19.sam
```

### Job information <a name="15"></a>

- List a user's current jobs:

```bash
$ squeue -u <username>
```

- List a user's running jobs:

```bash
$ squeue -u <username> -t RUNNING
```

- List a user's pending jobs:

```bash
$ squeue -u <username> -t PENDING
```

- View accounting information for all user's job for the current day:

```bash
$ sacct --format=JobID,JobName,User,Submit,ReqCPUS,ReqMem,Start,NodeList,State,CPUTime,MaxVMSize%15 -u <username>
```

- View accounting information for all user's job for the 2 last days:

```bash
$ sacct -a -S $(date --date='2 days ago' +%Y-%m-%dT%H:%M) --format=JobID,JobName,User%15,Partition,ReqCPUS,ReqMem,State,Start,End,CPUTime,MaxVMSize -u <username>
```

- List detailed job information:

```bash
$ scontrol show -dd jobid=<jobid>
```

### Manage jobs <a name="16"></a>

- To cancel/stop a job:

```bash
$ scancel <jobid>
```

- To cancel all jobs for a user:

```bash
$ scancel -u <username>
```

- To cancel all pending jobs for a user:

```bash
$ scancel -t PENDING -u <username>
```
