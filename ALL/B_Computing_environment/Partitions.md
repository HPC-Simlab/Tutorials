# Table of Contents
1. [Simlab partitions](#1)

## The available partitions  <a name="1"></a>

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

### Examples:
- You can reserve a job using `gpu` partition with max of two nodes (88 cores)
- You can reserve a job using `special` partition with max of 15 nodes (652 cores)
- ...

**To see examples for jobs reservation on CPU compute nodes, you to use `batch mode` (see the documentation of [Sequential job in batch](https://github.com/HPC-Simlab/Tutorials/blob/master/ALL/D_Commands_of_a_CPU_code/Sequential_job_in_batch.md)).**

**To see examples for jobs reservation on GPU compute nodes, you to use `batch mode` (see the documentation of [Single-GPU code in a batch job](https://github.com/HPC-Simlab/Tutorials/blob/master/ALL/F_Commands_of_a_GPU_code/Single-GPU_code_in_a_batch_job.md)).**


