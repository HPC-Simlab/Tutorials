# Table of Contents
1. [Description](#0)
2. [Python on SIMLAB](#1)
3. [Install package using pip](#2)


## Description <a name="0"></a>
The Python ecosystem has many optimised tools for scientific computations and data processing. The most well known are available on SIMLAB via the modules.


## Python on SIMLAB <a name="1"></a>

- Check available versions:

```sh
$ module avail Python
----------------- /cm/shared/modulefiles ------------------
Python/2.7.16-GCCcore-8.3.0  Python/3.8.2-GCCcore-9.3.0   
Python/2.7.18-GCCcore-9.3.0  Python/3.8.6-GCCcore-10.2.0  
Python/3.7.4-GCCcore-8.3.0   
```

- Load Python (version 3.8.2 compiled with GCC9.3.0):

```sh
$ module purge
$ module load Python/3.8.2-GCCcore-9.3.0
```
- Check the loaded packages (python dependacies):

```sh
$ module list
Currently Loaded Modulefiles:
 1) slurm/17.11.12                6) ncurses/6.2-GCCcore-9.3.0      11) GMP/6.2.0-GCCcore-9.3.0     
 2) GCCcore/9.3.0                 7) libreadline/8.0-GCCcore-9.3.0  12) libffi/3.3-GCCcore-9.3.0    
 3) zlib/1.2.11-GCCcore-9.3.0     8) Tcl/8.6.10-GCCcore-9.3.0       13) Python/3.8.2-GCCcore-9.3.0  
 4) binutils/2.34-GCCcore-9.3.0   9) SQLite/3.31.1-GCCcore-9.3.0    
 5) bzip2/1.0.8-GCCcore-9.3.0    10) XZ/5.2.5-GCCcore-9.3.0
```

## Install package using pip <a name="2"></a>

After loading `Python` version, you can now install additional packages

- List packages:
```sh
$ pip list
```
- Install new package (For instance `pandas`):
```sh
pip install pandas
```

***be careful of what Python version you loaded, so you won't face any conflicts with the modules that you'll use with Python.***
