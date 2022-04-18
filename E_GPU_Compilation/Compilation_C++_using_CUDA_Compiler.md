# Table of Contents
1. [Description](#1)
2. [CUDA on SIMLAB](#2)
3. [C++ Example](#3)
    1. [cuda_example.cu example](#4)
    2. [Compiling the example](#5)
    3. [Running CUDA on interactive mode](#6)

## Description <a name="1"></a>
CUDA is a parallel computing platform and application programming interface that allows software to use certain types of graphics processing unit for general purpose processing – an approach called general-purpose computing on GPUs.

## CUDA on SIMLAB <a name="2"></a>

- Check available versions:
```sh
$ module avail CUDA
----------------- /cm/shared/modulefiles ------------------
CUDA/11.1.1-GCC-10.2.0  CUDA/11.3.1  CUDAcore/11.1.1  
```
- Load CUDA/11.1.1-GCC-10.2.0 (version 11.1.1, compiled with GCC-10.2.0):
```sh
$ module load CUDA/11.1.1-GCC-10.2.0
```
- Check modules loaded (dependencies):
```sh
$ module list
Currently Loaded Modulefiles:
1) GCCcore/10.2.0                 4) GCC/10.2.0              
2) zlib/1.2.11-GCCcore-10.2.0     5) CUDAcore/11.1.1         
3) binutils/2.35-GCCcore-10.2.0   6) CUDA/11.1.1-GCC-10.2.0  
```
- after loading the module you can get some basic information about the loaded version by typing:

```sh
$ nvcc --version
``` 

## C++ Examples <a name="3"></a>
### cuda_example.cu example <a name="4"></a>

```sh
$ cat cuda_example.cu

#include <iostream>
#include <math.h>

// function to add the elements of two arrays
__global__
void add(int n, float *x, float *y)
{
    int index = blockIdx.x * blockDim.x + threadIdx.x;
    int stride = blockDim.x * gridDim.x;
    for (int i = index; i < n; i += stride)
        y[i] = x[i] + y[i];
}

 int main(void)
{
    int N = 1<<20; // 1M elements

    int blockSize = 256;
    int numBlocks = (N + blockSize - 1) / blockSize;
    
    float *x, *y;
    //variable allocation on GPU memory
    cudaMallocManaged (&x, N*sizeof(float));
    cudaMallocManaged (&y, N* sizeof(float));

    // initialize x and y arrays on the host
    for (int i = 0; i < N; i++) {
        x[i] = 1.0f;
        y[i] = 2.0f;
    }

     add<<<numBlocks, blockSize>>>(N, x, y);

     cudaDeviceSynchronize();

    float maxError = 0.0f;
    for (int i = 0; i < N; i++)
        maxError = fmax(maxError, fabs(y[i]-3.0f));
    std::cout << "Max error: " << maxError << std::endl;

    // Free GPU memory
    cudaFree(x);
    cudaFree(y);

    return 0;
}
```
### Compiling the example <a name="5"></a>

- Now you can compile the example using `nvcc`:
```sh
$ nvcc cuda_example.cu
```
### Running CUDA on interactive mode <a name="6"></a>

- You first need to be on GPU node:
***`slurm` module must be loaded to run this command***

```sh
$ srun -p gpu --gres=gpu:1 --mem=8g --constraint=V100 --pty bash
```

- Run the example:

```sh
[<login>@node10 ~]$ module load CUDA/11.1.1-GCC-10.2.0 
[<login>@node10 ~]$ ./a.out 
Max error: 0
```
