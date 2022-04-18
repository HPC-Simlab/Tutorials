# Table of Contents
1. [Some useful information](#1)
2. [Useful commands](#2)
   1. [Submitting a job using `sbatch`](#3)
   2. [Monitoring jobs using `squeue`](#4)
   3. [Resources and execution status using `scontrol`](#5)
   4. [Canceling a job using `scancel`](#6)

## Some useful information <a name="1"></a>

Jobs are managed on all the nodes by the software [Slurm](https://slurm.schedmd.com/documentation.html) .

## Useful commands <a name="2"></a>
## Submitting a job using `sbatch` <a name="3"></a>

```sh
 $ sbatch script.slurm 
```
### Monitoring jobs using `squeue` <a name="4"></a>

- To monitor jobs which are waiting or in execution

```sh
$ squeue -u $USER 
```
This command displays information in the following form:

```sh
JOBID  PARTITION  NAME  USER  ST   TIME  NODES  NODELIST(REASON)   
  235  part_name  test   abc   R  00:02      1  node01 
```
Where
JOBID: Job identifier
PARTITION: Partition used
NAME: Job name
USER: User name of job owner
ST: Status of job execution ( R=running, PD=pending, CG=completing )
TIME: Elapsed time
NODES: Number of nodes used
NODELIST: List of nodes used

Note: You can use the `--start` option to display an estimated start time for your jobs ("START_TIME" column). Slurm might not have a reliable estimation for the start time of some jobs, in this case the information will show as not available ("N/A"). Since the list of pending jobs is always evolving, it is important to note that the information given by Slurm is only an estimate which might change depending on the machine load.

### Resources and execution status using `scontrol` <a name="5"></a>

- To obtain complete information about a job

```sh
$ scontrol show job JOBID 
```

### Canceling a job using `scancel` <a name="6"></a>

- To cancel a job:

```sh
$ scancel JOBID 
```
For advanced use see [slurm-advanced](Advanced_slurm_commads.md) documentation.
