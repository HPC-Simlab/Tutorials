# Table of Contents
1. [Description](#1)
2. [Python Example](#3)
    1. [Installing `numba` using `pip`](#4)
    2. [cuda_example.py example](#5)
    3. [Run the code on interactive mode](#6)

## Description <a name="1"></a>
Numba translates Python functions to optimized machine code at runtime using the industry-standard LLVM compiler library. Numba-compiled numerical algorithms in Python can approach the speeds of C or FORTRAN.
With support for both NVIDIA's CUDA and AMD's ROCm drivers, Numba lets you write parallel GPU algorithms entirely from Python.

## Python example using `numba` <a name="3"></a>

### Installing `numba` using pip <a name="4"></a>

- You first need to load Python version:
```sh
$ module load Python/3.8.6-GCCcore-10.2.0
```
- load CUDA Module:
```sh
$ module load CUDA/11.1.1-GCC-10.2.0
```
- Now you can install numba using `pip` command:
```sh
$ pip install numba
```
- Check the installed version:
```sh
$ pip show numba

Name: numba
Version: 0.53.0
Summary: compiling Python code using LLVM
[...]
```

### cuda_example.py example <a name="5"></a>

```sh
$ cat cuda_example.py

from numba import cuda

import numpy as np
from timeit import default_timer as timer

@cuda.jit
def increment_by_one(an_array):
    # Thread id in a 1D block
    tx = cuda.threadIdx.x
    # Block id in a 1D grid
    ty = cuda.blockIdx.x
    # Block width, i.e. number of threads per block
    bw = cuda.blockDim.x
    gd = cuda.gridDim.x
    # Compute flattened index inside the array
    index = tx + ty * bw
    stride = gd * bw
    if index < an_array.size:  # Check array boundaries
        for i in range(index, an_array.size, stride):
            an_array[i] = (an_array[i]/12)%3

if __name__=="__main__":
    n = 10000000

    a = np.random.rand(n)
    b = np.array(a)

    start = timer()
    increment_by_one[160, 32](a)
    print("without GPU:", timer()-start)

    start = timer()
    for i in range(n):
        b[i] = (b[i]/12)%3
    print("without GPU:", timer()-start)

    print("result check: ", np.allclose(a, b))
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
[<login>@node08 ~]$ python numba_example.py

without GPU: 2.9776507169008255
with GPU: 0.6109951017424464
```
