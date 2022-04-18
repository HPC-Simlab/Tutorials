# Table of Contents
1. [Description](#1)
2. [Jupyter-notebook/Jupyter-lab on SIMLAB](#2)
    1. [Jupyter-notebook/Jupyter-lab on interactive mode](#3)
        1. [Running the Jupyter-notebook/Jupyter-lab](#4)
        2. [Create the ssh tunnel from you local machine](#5)
    2. [Jupyter-notebook/Jupyter-lab on batch mode](#6)
    4. [Installing a specific jupyter notebook version on the simlab cluster](#7)

## Description <a name="1"></a>

The notebook extends the console-based approach to interactive computing in a qualitatively new direction, providing a web-based application suitable for capturing the whole computation process: developing, documenting, and executing code, as well as communicating the results. The Jupyter notebook combines two components:

A web application: a browser-based tool for interactive authoring of documents which combine explanatory text, mathematics, computations and their rich media output.

Notebook documents: a representation of all content visible in the web application, including inputs and outputs of the computations, explanatory text, mathematics, images, and rich media representations of objects.
[read more](https://jupyter-notebook.readthedocs.io/en/stable/notebook.html)

## Jupyter-notebook/Jupyter-lab on SIMLAB <a name="2"></a>

### Jupyter-notebook/Jupyter-lab on interactive mode <a name="3"></a>

- Get access to compute node with GPU access
```sh
$ srun -p gpu --gres=gpu:1 --time=1:00:00 --pty bash
```
- Get access to compute node without GPU access
```sh
$ srun -p longq --time=1:00:00 --pty bash
```
#### Running the jupyter-notebook/jupyter-lab <a name="4"></a>

You first need to load Anaconda.

- Check Anaconda versions:
```sh
$ module avail Anaconda
---------------------------- /cm/shared/modulefiles ----------------------------
Anaconda3/2020.11  
```

- Load the Anancoda:
```sh
$ module load Anaconda3
```

- Running the jupyter-notebook command (need to put a port > than 1024)
```sh
$ jupyter-notebook --ip localhost --port <port> --no-browser
```
or
```sh
$ jupyter-lab --ip localhost --port <port> --no-browser
```
#### Create the ssh tunnel from you local machine <a name="5"></a>

- After running the notebook you need to run the following command from your local machine to create the ssh tunnel
```sh
$ ssh -t -L <port>:localhost:<port> <login>@simlab-cluster.um6p.ma ssh -N -L <port>:localhost:<port> <node name>
```

**Example using port 4456:**

- From SIMLAB run (****Reservation of node in `gpu` partition for 1 hour****):

```sh
$ srun -p gpu --gres=gpu:1 --time=1:00:00 --pty bash

node06~$
```
Now you can run jupyter notebook from `node06`

```sh
[<login>@node06 ~]$ jupyter-notebook --ip localhost --port 4456 --no-browser
```

- From your local machine run:

```sh
$ ssh -t -L 4456:localhost:4456 <login>@simlab-cluster.um6p.ma ssh -N -L 4456:localhost:4456 node06
```

- Go back to SIMLAB and run the link provided:

***link eg: ```http://localhost:4456/?token=rh4efcde6216a5f274cf0b17f1bakl351fe872dc834277e4```***

## Jupyter-notebook/Jupyter-lab on batch mode <a name="6"></a>

```sh
$ cat jupyter-example.slurm

#!/bin/bash

# If your job will need to use the gpu ressource, add this two lines
#SBATCH -p gpu                             # partition name
#SBATCH --gres=gpu:1                       # Necessary to activate the gpu card (The number of GPUs allowed by node is 1)
#SBATCH -N 1                               # number of nodes (for gpu partition you can use 2 nodes max)
#SBATCH -n 1                               # number of cores ( max 44 per node)
#SBATCH --time=00:05:00                    # wall time to finish the job
#SBATCH --job-name jupyter-notebook        # job name
#SBATCH --output jupyter-notebook-%j.log   # output file

# get tunneling info
XDG_RUNTIME_DIR=""
node=$(hostname -s)
user=$(whoami)
cluster="simlab-cluster"
port=$(( 4456 ))


# print tunneling instructions jupyter-log
echo -e "
Command to create ssh tunnel:
ssh -N -f -L ${port}:${node}:${port} ${user}@${cluster}.um6p.ma
Use a Browser on your local machine to go to:
localhost:${port}  (prefix w/ https:// if using password)
"

# If your job will need to use the gpu ressource, add this line also
module load CUDA

# load modules or conda environments here (you can use your own conda environment)
module load Anaconda3

# Run Jupyter lab
jupyter-lab --no-browser --port=${port} --ip=${node} 
```

- Run the job:
```sh
$ sbatch jupyter-example.slurm
```

- Check the job in the queue:
```sh
$ squeue -u <login>
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
             28728       gpu jupyter- <login>   R       0:12      1 node10
```
- Check the log file `jupyter-notebook<JOBID>.log` ***(in this case JOBID is 28728)***:

```sh
$ cat jupyter-notebook-28728.log 
 
Command to create ssh tunnel:
ssh -N -f -L 4456:node10:4456 <login>@simlab-cluster.um6p.ma

Use a Browser on your local machine to go to:
localhost:4456  (prefix w/ https:// if using password)

[...]
[I 13:51:01.790 LabApp] http://node10:4456/?token=ba70ffae079fe0266db4f0611433f0d2330dd9a4b7d2a3e8
[I 13:51:01.790 LabApp]  or http://127.0.0.1:4456/?token=ba70ffae079fe0266db4f0611433f0d2330dd9a4b7d2a3e8
[I 13:51:01.790 LabApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
[C 13:51:01.800 LabApp] 
[...]    
```

- Copy the command `ssh -N -f -L 4456:node10:4456 <login>@simlab-cluster.um6p.ma` and paste in on your local machine to create the ssh tunnel

- Now you can run copy the link `http://127.0.0.1:4456/?token=ba70ffae079fe0266db4f0611433f0d2330dd9a4b7d2a3e8` and paste it on you browser.

## Installing a specific jupyter notebook version on the simlab cluster <a name="7"></a>

- Check available Python versions:

```sh
$ module avail Python
---------------------------- /cm/shared/modulefiles ----------------------------
Python/3.7.4-GCCcore-8.3.0  Python/3.8.2-GCCcore-9.3.0  
```

- Load a Python (version 3.8.2):
```sh
$ module load Python/3.8.2-GCCcore-9.3.0
```
- Install jupyter-notebook
```sh
$ pip install notebook=="6.4.7"
```

- Check the juyter-notebook version installed
```sh
$ jupyter notebook --version
6.4.7
```
***After installing jupyter-notebook the first time you can use it by loading the same Python version used for the installation.***

