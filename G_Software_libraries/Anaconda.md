# Table of Contents
1. [Some useful information](#1)
2. [Anaconda on SIMLAB](#2)
3. [Make environment](#3)
4. [Useful Commands](#4)


## Some useful information <a name="1"></a>
- Anaconda is a distribution of the Python and R programming languages for scientific computing (data science, machine learning applications, large-scale data processing, predictive analytics, etc.), that aims to simplify package management and deployment.
- It is mainly used to maintain python versions and packages in separate environments so that they don’t conflict with system versions or with each other.

## Anaconda on SIMLAB <a name="2"></a>

- Check available versions:
```sh
$ module avail Anaconda
---------------------------- /cm/shared/modulefiles ----------------------------
Anaconda3/2020.11    
```
- Load Anaconda3:
```sh
$ module load Anaconda3
```

## Make environment <a name="3"></a>

After loading anaconda now you can start by either use an already made environment.

- You can get some basic information about the loaded version by typing:
```sh
$ conda info
``` 

- you can see the available environments with the command:

```sh
$ conda env list
# conda environments:
#
eb                       /home/<login>/.conda/envs/eb
jup                      /home/<login>/.conda/envs/jup
pyccel_env               /home/<login>/.conda/envs/pyccel_env
base                  *  /home/team1337/.local/easybuild_new/software/Anaconda3/2020.11
```

- you can create your own environement `new_env` with the command:

```sh
$ conda create -n new_env
```

- to activate the desired environment you need to use:

```sh
$ source activate new_env
```  
(for more options follow this [link](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-with-commands)).  

- Now you have the ability to install your desired packages in your environment with the command:

```sh
$ conda install "package name"
```  

NOTE: you should be in a personal environment to install new packages.

## Useful Commands <a name="4"></a>

- Create a new environment named myenv, install Python 3.8: ```conda create --name myenv python=3.8```
- Activate a conda environment: ```conda activate ENVIRONMENT_NAME```
- Deactivate a conda environment: ```conda deactivate ENVIRONMENT_NAME```
- Get a list of all my environments, active environment is shown with *: ```conda env list```
- List all packages and versions installed in active environment: ```conda list```
- Install a package included in Anaconda: ```conda install PACKAGENAME ```

Check [cheat-sheet](https://docs.conda.io/projects/conda/en/4.6.0/_downloads/52a95608c49671267e40c689e0bc00ca/conda-cheatsheet.pdf) for more commands.
