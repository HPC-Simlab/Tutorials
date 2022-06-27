# Table of Contents
1. [Description](#1)
2. [LAPACK on SIMLAB](#2)
3. [Linking phase](#3)

## Description <a name="1"></a>

LAPACK (Linear Algebra Package) is a library dedicated to dense linear algebra and depends on the BLAS (Basic Linear Algebra Subprograms) library. It provides functions for solving systems of linear equations, eigenvalue calculations and matrix decompositions (LU, QR, SVD, Cholesky). LAPACK is available via the Math Kernel Library (MKL) (recommended version) or in a free version (Netlib).

## LAPACK on SIMLAB <a name="2"></a>

- List available versions:
```sh
$ module avail LAPACK
----------------- /cm/shared/modulefiles ------------------
LAPACK/3.8.0-GCC-8.3.0  LAPACK/3.8.0-GCC-9.3.0  
```
- Load LAPACK (default version - 3.8.0 compiled with GCC-9.3.0):
```sh
$ module load LAPACK
```
- List modules loaded with LAPACK (dependencies):
```sh
$ module list
Currently Loaded Modulefiles:
 1) GCCcore/9.3.0                 4) GCC/9.3.0               
 2) zlib/1.2.11-GCCcore-9.3.0     5) LAPACK/3.8.0-GCC-9.3.0  
 3) binutils/2.34-GCCcore-9.3.0  
```

## Linking phase <a name="3"></a>
During the compilation, it is necessary to add the `-llapack` option: 

```sh
$ gcc example.c -llapack
```
please check the example below that is tested on simlab
https://gist.githubusercontent.com/erikzenker/c4dc42c8d5a8c1cd3e5a/raw/191a60f740b25d8639ce243c9821d760aaad6731/metis.cc
