# First time at SIMLAB

## Table of Contents
1. [Step 0: Connect to Simlab using ssh](#Basic)
2. [Step 1: Change your password](#password)
3. [Step 2: Load module in Simlab](#load)
4. [Step 3: The available partitions](#partitions)
5. [Step 4: Run example using interactive mode](#interactive)
    1. [Run example on CPU node using iteractive mode](#interactivecpu)
    2. [Run example on GPU node using iteractive mode](#interactivegpu)
6. [Step 5: Advanced use](#advanced)

### Step 0: Connect to Simlab using ssh <a name="Basic"></a>
Connecting directly to the cluster frontends is restricted to networks within the university. So being connected to the university network is needed, or using a VPN, then you can connect via this command: 

```sh
$ ssh -CY <login>@simlab-cluster.um6p.ma
```

- For windows users you can use the command-line, or graphical interface third-party clients like [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/) and [mobaxterm](https://mobaxterm.mobatek.net)(recommended).
- To configure mobaxterm follow this [tuto](https://www.youtube.com/watch?v=s7xNGyG9GVc).


**For more detail see the [Access and shells](https://github.com/HPC-Simlab/Tutorials/blob/master/ALL/B_Computing_environment/Access_and_shells.md) documentation.**

### Step 1: Change your password <a name="password"></a>

You can change your password at any time by using the UNIX command `passwd` directly on front end. The change is taken into account immediately. 

```sh
$ passwd
Changement de mot de passe pour l'utilisateur $USER.
(current) LDAP Password: 
Nouveau mot de passe : 
Retapez le nouveau mot de passe : 
```
**In the case you forget you password, send an email to hpc-redmine@um6p.ma.**

### Step 2: Load module in Simlab <a name="load"></a>
- Load GCC module 

```bash
$ module purge
$ module load GCC
```
**For more detail see the [The module commands](https://github.com/HPC-Simlab/Tutorials/blob/master/ALL/B_Computing_environment/The_module_command.md) documentation.**

### Step 3: The available partitions  <a name="partitions"></a>

- `defq`: partition is automatically used if no partition is specified by all jobs. The execution time by default is 4 hours.
- `shortq`: partition used for short jobs (max. 12 hours), with max of two nodes per job (88 cores max.)
- `longq`: partition used for long jobs (max 30 days), with only one node per job (44 cores max.).
- `special`: used for running parallel jobs (max 30 minutes).
- `visu`: partition used for visualization.
- `gpu`: partition used for gpu computations (all nodes in this partition have gpu card P100 or P40), with max of two nodes per job (88 cores max.)

| Partition | Max. Cpu Time | Nodes available for the partition | Max nodes per job | Min-Max cores per job     |
|-----------|---------------|-------------------------------------------------------|-------------------|---------------------------|
| defq      | 4 hours       |              5 (node01, node02 node03, node14, node15)  |             1       |     1-44          |
| shortq    | 12 hours      |              5 (node01, node02 node03, node14, node15)  |             2       |     1-88          |
| longq     | 30 days       |              5 (node01, node02 node03, node14, node15)  |             1       |     1-44          |
| special   | 30 minutes    |              15 (all nodes)                             |            15       |     1-652         |
| visu      | 24 hours      |              1  (visu01)                                |             1       |     1-44          |
| gpu       | 48 hours      |              12 (node[06-17])                           |             2       |     1-88          |

##### Examples:
- You can reserve a job using `gpu` partition with max of two nodes (88 cores)
- You can reserve a job using `special` partition with max of 15 nodes (652 cores)
- ...
- 

### Step 4: Run example using interactive mode <a name="interactive"></a>

#### Run example on CPU node using iteractive mode <a name="interactivecpu"></a>

```sh
$ srun --pty --partition=shortq --ntasks=1 --cpus-per-task=4 bash
[team1337@node14 ~]$ ./cpu_exe
```
**For more detail see the [Interactive execution](https://github.com/HPC-Simlab/Tutorials/blob/master/ALL/D_Commands_of_a_CPU_code/Interactive_execution.md) documentation.**
***- This is not recommended because if your session is exited your job will be automatically killed, we recommend you to use `batch mode` (see the documentation of [Sequential job in batch](https://github.com/HPC-Simlab/Tutorials/blob/master/ALL/D_Commands_of_a_CPU_code/Sequential_job_in_batch.md)).***


You can verify that your reservation is active by using the `squeue` command. for more details you can see the [Basic slurm commands](https://github.com/HPC-Simlab/Tutorials/blob/master/ALL/A_General_information/Basic_Slurm_commands.md) or the [Advanced slurm commands](https://github.com/HPC-Simlab/Tutorials/blob/master/ALL/A_General_information/Advanced_slurm-commands.md).

```sh
$ squeue -u team1337
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
             32329    shortq     bash team1337  R       0:05      1 node14
```
- Jobid: 32329
- Partition: `shortq` choosed using the command `--partition=shortq`
- Node lists: `node14` is choosed by slurm to run the job

- To learn more about managing jobs and slurm commands, you can see the [Basic slurm commands](https://github.com/HPC-Simlab/Tutorials/blob/master/ALL/A_General_information/Basic_Slurm_commands.md) or the [Advanced slurm commands](https://github.com/HPC-Simlab/Tutorials/blob/master/ALL/A_General_information/Advanced_slurm-commands.md).


#### Run example on GPU node using iteractive mode <a name="interactivegpu"></a>

```sh
srun --pty --partition=gpu --nodes=1  --gres=gpu:1 bash
[team1337@node14 ~]$ ./gpu_exe
```
**For more detail see the [Interactive execution](https://github.com/HPC-Simlab/Tutorials/blob/master/ALL/F_Commands_of_a_GPU_code/Interactive_execution.md) documentation.**

***- This is not recommended because if your session is exited your job will be automatically killed, we recommend you to use `batch mode` (see the documentation of [Single-GPU code in a batch job](https://github.com/HPC-Simlab/Tutorials/blob/master/ALL/F_Commands_of_a_GPU_code/Single-GPU_code_in_a_batch_job.md)).***


You can verify that your reservation is active by using the `squeue` command. for more details you can see the [Basic slurm commands](https://github.com/HPC-Simlab/Tutorials/blob/master/ALL/A_General_information/Basic_Slurm_commands.md) or the [Advanced slurm commands](https://github.com/HPC-Simlab/Tutorials/blob/master/ALL/A_General_information/Advanced_slurm-commands.md).

```sh
$ squeue -u team1337
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
             32340       gpu     bash team1337  R       0:02      1 node09
```
- Jobid: 32340
- Partition: `gpu` choosed using the command `--partition=gpu`
- Node lists: `node09` is choosed by slurm to run the job

- To learn more about managing jobs and slurm commands, you can see the [Basic slurm commands](https://github.com/HPC-Simlab/Tutorials/blob/master/ALL/A_General_information/Basic_Slurm_commands.md) or the [Advanced slurm commands](https://github.com/HPC-Simlab/Tutorials/blob/master/ALL/A_General_information/Advanced_slurm-commands.md)

### Step 5: Advanced use <a name="advanced"></a>

For advanced use please see these [tutorials](https://github.com/HPC-Simlab/Tutorials).
