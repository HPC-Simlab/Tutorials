# Table of Contents
1. [Description](#1)
2. [Python Example](#3)
    1. [Installing `Cupy` using `pip`](#4)
    2. [Cupy_example.py example](#5)
    3. [Run the code on interactive mode](#6)

## Description <a name="1"></a>
CuPy is an open-source NumPy/SciPy-compatible array library for GPU-accelerated computing with Python. CuPy utilizes CUDA Toolkit libraries including cuBLAS, cuRAND, cuSOLVER, cuSPARSE, cuFFT, cuDNN and NCCL to make full use of the GPU architecture.

## Python example using `Cupy` <a name="3"></a>

### Installing `Cupy` using pip <a name="4"></a>

- load Python Module:
```sh
$ module load Python/3.8.6-GCCcore-10.2.0
```
- load CUDA Module:
```sh
$ module load CUDA/11.1.1-GCC-10.2.0
```
- install Cupy using `pip` command using the CUDA version:
```sh
$ pip install cupy-cuda111
```
- Check the installed version:
```sh
$ pip show cupy-cuda111
Name: cupy-cuda111
Version: 10.5.0
Summary: CuPy: NumPy & SciPy for GPU
Home-page: https://cupy.dev/
Author: Seiya Tokui
Author-email: tokui@preferred.jp
License: MIT License
Requires: fastrlock, numpy
Required-by: 
```

### Cupy_example.py example <a name="5"></a>

```sh
$ cat Cupy_example.py

from timeit import default_timer as timer

# Using numpy
import numpy as np

arr_c1= np.random.rand(10000,10000)
arr_c2= np.random.rand(10000,10000)

start = timer()
r1 = arr_c1 * arr_c2
print("without GPU:", timer()-start)    



# Using Cupy
import cupy as cp
arr_g1= cp.random.rand(10000,10000)
arr_g2= cp.random.rand(10000,10000)
start = timer()
r1 = arr_g1 * arr_g2
print("with GPU:", timer()-start)

```

### Run the code on interactive mode <a name="6"></a>

- You first need to be on GPU node: ***slurm module must be loaded to run this command***
```sh
$ srun -p gpu --gres=gpu:1 --mem=8g --pty bash
```

- Run the example:

```sh
[<login>@node08 ~]$ module load Python/3.8.6-GCCcore-10.2.0
[<login>@node08 ~]$ module load CUDA/11.1.1-GCC-10.2.0
[<login>@node08 ~]$ python Cupy_example.py


```
