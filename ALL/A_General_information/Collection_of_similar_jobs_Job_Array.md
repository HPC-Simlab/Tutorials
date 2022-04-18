# Table of Contents
1. [Some useful information](#1)
2. [Variables specific to Job Arrays](#2)
3. [Examples of usage](#5)
4. [Job Array commands](#6)


## Some useful information <a name="1"></a>

- The SLURM Job Array mechanism offers the user the possibility of submitting a collection of similar jobs at one time.

- **Important**: At SIMLAB, job arrays must be submitted via the `sbatch` command as they can generate a very large number of jobs.

## 
Job arrays are differentiated by the usage of the SLURM `#SBATCH --array` directive which allows specifying the array index values, or a range of index values, as indicated below:


- For a job array whose index values go successively from 0 to NB_JOBS (i.e. 0, 1, 2, ... , NB_JOBS):
```sh
#SBATCH --array=0-NB_JOBS
```

- For a job array whose index values vary from 0 to NB_JOBS (maximum potential value) with STEP_SIZE (i.e. 0, STEP_SIZE, 2*STEP_SIZE, etc…):

```sh
#SBATCH --array=0-NB_JOBS:STEP_SIZE
```
- For an array of N jobs having the predefined index values of J_1, J_2, … , J_N :

```sh
#SBATCH --array=J_1,J_2,...,J_N
```

***Comment: To avoid saturating the waiting queue for SLURM jobs, the maximum number of jobs to be executed simultaneously from a job array can be specified by using the `%` separator. For example:***

- To execute all the jobs of an array by series of NB_MAX_RUNNING_JOBS, use the following syntax:
```sh
#SBATCH --array=0-NB_JOBS%NB_MAX_RUNNING_JOBS
```

## Variables specific to Job Arrays <a name="2"></a>

When using the Job Array mechanism, certain SLURM environment variables can be used in the script shell in order to personalize the different jobs in an array (for example, for each job of an array to use different input and/or output directories). The following environment variables are automatically set by SLURM:

- `SLURM_JOB_ID`: the job identifier
- `SLURM_ARRAY_JOB_ID`: the first job identifier of the array
- `SLURM_ARRAY_TASK_ID`: the index value belonging to each job of the array (can be seen as a job counter)
- `SLURM_ARRAY_TASK_COUNT`: the total number of jobs in the array which will be executed
- `SLURM_ARRAY_TASK_MIN`: the lowest index value of all the jobs in the array
- `SLURM_ARRAY_TASK_MAX`: the highest index value of all the jobs in the array

Moreover, with job arrays, in the `#SBATCH --output=...` and `#SBATCH --error=...` directives, two additional options are available to specify the names of input and output files for each job:

- `%A` will be replaced by the value of SLURM_ARRAY_JOB_ID
- `%a` will be replaced by the value of SLURM_ARRAY_TASK_ID.

***Comments:***

By default, the format of the output file name for a job array is `slurm-%A_%a.out`.

In Bash, job array variables can be obtained as follows:
```sh
echo ${SLURM_JOB_ID}
echo ${SLURM_ARRAY_JOB_ID}
echo ${SLURM_ARRAY_TASK_ID}
echo ${SLURM_ARRAY_TASK_COUNT}
echo ${SLURM_ARRAY_TASK_MIN}
echo ${SLURM_ARRAY_TASK_MAX}
```
For Python scripts, job array variables can be obtained as follows:

```python
import os
slurm_job_id=int(os.environ["SLURM_JOB_ID"])
slurm_array_job_id=int(os.environ["SLURM_ARRAY_JOB_ID"])
slurm_array_task_id=int(os.environ["SLURM_ARRAY_TASK_ID"])
slurm_array_task_count=int(os.environ["SLURM_ARRAY_TASK_COUNT"])
slurm_array_task_min=int(os.environ["SLURM_ARRAY_TASK_MIN"])
slurm_array_task_max=int(os.environ["SLURM_ARRAY_TASK_MAX"])
```

## Examples of usage <a name="3"></a>

Preliminary remark: the examples below concern executions on the CPU partition. The principle remains the same for executions on the GPU partitions.

**Example of a submission script for 20 identical jobs with a maximum of 5 jobs placed in the file (execution by series of 5 jobs):**

```sh
$ cat job_array_20.slurm

#!/bin/bash
#SBATCH --partition=shortq     # partition name
#SBATCH --job-name=job-array   # name of job
#SBATCH --ntasks=1             # total number of MPI processes
#SBATCH --ntasks-per-node=1    # number of MPI processes per node
# In Slurm vocabulary, "multithread" refers to hyperthreading. 
#SBATCH --hint=nomultithread   # 1 MPI process per physical core (no hyperthreading)
#SBATCH --time=00:01:00        # maximum execution time requested (HH:MM:SS)
#SBATCH --output=%x_%A_%a.out  # output file name contaning the ID and the index value
#SBATCH --error=%x_%A_%a.out   # name of error file (here common with the output)
#SBATCH --array=0-19%5         # total of 20 jobs but maximum of 5 jobs in the file 

# go into the submission directory
cd ${SLURM_SUBMIT_DIR}

# clean out modules loaded in interactive and inherited by default
module purge

# loas modules
module load ...

# echo of launched commands
set -x

# Execution of the "mon_exe" binary with different data for each job
# The value of ${SLURM_ARRAY_TASK_ID} is different for each job.
srun ./mon_exe < file${SLURM_ARRAY_TASK_ID}.in > file${SLURM_ARRAY_TASK_ID}.out
```
**Example of a submission script for 3 identical jobs, having the index values of 1, 3 and 8 respectively :**

```sh
$ cat job_array_3.slurm

#!/bin/bash
#SBATCH --partition=shortq     # partition name
#SBATCH --job-name=job-array   # name of job
#SBATCH --ntasks=1             # total number of MPI processes
#SBATCH --ntasks-per-node=1    # number of MPI processes per node
# In Slurm vocabulary, "multithread" refers to hyperthreading.
#SBATCH --hint=nomultithread   # 1 MPI process per physical core (no hyperthreading)
#SBATCH --time=00:01:00        # maximum execution time requested (HH:MM:SS)
#SBATCH --output=%x_%A_%a.out  # name of output file containing the ID and the index value
#SBATCH --error=%x_%A_%a.out   # name of error file (here common with the output)
#SBATCH --array=1,3,8          # total of 3 jobs having the index values 1, 3 and 8

# go into the submission directory
cd ${SLURM_SUBMIT_DIR}

# clean out modules loaded in interactive and inherited by default
module purge

# load modules
module load ...

# echo of launched commands
set -x

# Execution of the "mon_exe" binary with different data for each job
# The value of ${SLURM_ARRAY_TASK_ID} is different for each job.
srun ./mon_exe < file${SLURM_ARRAY_TASK_ID}.in > file${SLURM_ARRAY_TASK_ID}.out
```
**Example of a submission script for 6 identical jobs, having the index values 0 to 11 inclusive with step of 2 :**

```sh
$ cat job_array_0-11.slurm

#!/bin/bash
#SBATCH --partition=shortq     # partition name
#SBATCH --job-name=job-array   # name of job
#SBATCH --ntasks=1             # total number of MPI processes
#SBATCH --ntasks-per-node=1    # number of MPI processes per node
# In Slurm vocabulary, "multithread" refers to hyperthreading.
#SBATCH --hint=nomultithread   # 1 MPI process per physical core (no hyperthreading)
#SBATCH --time=00:01:00        # maximum execution time requested (HH:MM:SS)
#SBATCH --output=%x_%A_%a.out  # name of output file containing the ID and the index value
#SBATCH --error=%x_%A_%a.out   # name of error file (ihere common with the output)
#SBATCH --array=0-11:2         # 6 jobs having the index values 0, 2, 4, 6, 8, and 10

# go into the submission directory
cd ${SLURM_SUBMIT_DIR}

# clean out modules loaded in interactive and inherited by default
module purge

# load modules
module load ...

# echo of launched commands
set -x

# Execution of the "mon_exe" binary with different data for each job
# The value of ${SLURM_ARRAY_TASK_ID} is different for each job.
srun ./mon_exe < file${SLURM_ARRAY_TASK_ID}.in > file${SLURM_ARRAY_TASK_ID}.out
```

### Job Array commands <a name="4"></a>

- A job array must be executed via the sbatch command by reason of the large number of jobs it can generate:

```sh
$ sbatch job_array.slurm
```

Monitoring these jobs is done with the squeue command which returns the useful information. For example, for a job array with 7 jobs, executed by series of 2 jobs on the `shortq` partition:
- The first call to squeue returns :
```sh
$ squeue -j 2011
             JOBID PARTITION      NAME     USER ST       TIME  NODES NODELIST(REASON)
    2011_[2-6%2]     shortq job-array  mylogin PD       0:00      1 (JobArrayTaskLimit)
          2011_0     shortq job-array  mylogin  R       0:00      1 node01
          2011_1     shortq job-array  mylogin  R       0:00      1 node02
```
***Here, we see that the first 2 jobs are executing and the other 5 are waiting.***

- When the first 2 jobs are finished, a second call to squeue returns:

```sh
$ squeue -j 2011
             JOBID PARTITION      NAME     USER ST       TIME  NODES NODELIST(REASON)
      2011_[4-6%2]    shortq job-array  mylogin PD       0:00      1 (JobArrayTaskLimit)
          2011_2      shortq job-array  mylogin  R       0:05      1 node01
          2011_3      shortq job-array  mylogin  R       0:05      1 node02
```
Now we can see that the next 2 jobs are executing and there are only 3 which are still waiting. Note that we can no longer see the first 2 jobs which have finished.

To delete a job array, you should use the scancel command. However, there are different ways to proceed:

- To cancel the entire array, indicate its identifier `${SLURM_JOB_ID}`. With the above example, this is:

```sh
$ scancel 2011
```
- To cancel the execution of a particular job, indicate the array identifier `${SLURM_ARRAY_JOB_ID}` and the index value of the job `${SLURM_ARRAY_TASK_ID}`. With the above example, this is:

```sh
$ scancel 2011_2
```
- To cancel the execution of a series of jobs, indicate the array identifier `${SLURM_ARRAY_JOB_ID}` and a range of values (here, 4 to 6). With the above example, this is:
```sh
$ scancel 2011_[4-6]
```
