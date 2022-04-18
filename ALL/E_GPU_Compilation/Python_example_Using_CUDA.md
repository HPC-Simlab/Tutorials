# Table of Contents
1. [Description](#1)
2. [Python Example](#3)
    1. [Installing `numba` using `pip`](#4)
    2. [cuda_example.py example](#5)
    3. [Run the code on interactive mode](#6)

## Description <a name="1"></a>
CUDA is a parallel computing platform and application programming interface that allows software to use certain types of graphics processing unit for general purpose processing – an approach called general-purpose computing on GPUs.

## Python example using `numba` <a name="3"></a>

### Installing `numba` using pip <a name="4"></a>

- You first need to load Python version:
```sh
$ module load Python/3.8.6-GCCcore-10.2.0
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

from numba import jit, cuda

import numpy as np
from timeit import default_timer as timer

# To run on CPU
def func(a):
    for i in range(10000000):
        a[i]+= 1# To run on GPU

@jit
def func2(x):

    return x+1

if __name__=="__main__":
    n = 10000000

    a = np.ones(n, dtype = np.float64)    
    start = timer()
    func(a)
    print("without GPU:", timer()-start)    
    
    start = timer()
    func2(a)
    cuda.profile_stop()
    print("with GPU:", timer()-start)
```

### Run the code on interactive mode <a name="6"></a>

- You first need to be on GPU node: ***slurm module must be loaded to run this command***
```sh
$ srun -p gpu --gres=gpu:1 --mem=8g --constraint=V100 --pty bash
```

- Run the example:

```sh
[<login>@node08 ~]$ module load Python/3.8.6-GCCcore-10.2.0
[<login>@node08 ~]$ python cuda_example.py

without GPU: 2.9776507169008255
with GPU: 0.6109951017424464
```
