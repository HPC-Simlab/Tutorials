# Table of Contents
1. [Description](#1)
2. [OpenBLAS on SIMLAB](#2)
3. [Linking phase](#3)

## Description <a name="1"></a>

BLAS (Basic Linear Algebra Subprograms) is a set of functions effectuating basic linear algebra operations such as vector addition, scalar products and matrix multiplication.

## OpenBLAS on SIMLAB <a name="2"></a>

Check and load OpenBLAS into your working environment:

- Check available versions:
```sh
$ module avail OpenBLAS
----------------- /cm/shared/modulefiles ------------------
OpenBLAS/0.3.7-GCC-8.3.0  OpenBLAS/0.3.9-GCC-9.3.0  OpenBLAS/0.3.12-GCC-10.2.0  
```
- Load OpenBLAS (default - version 0.3.12 compiled with GCC-10.2.0)
```sh
$ module load OpenBLAS
```

- Check modules loaded (dependencies):
```sh
$ module list
Currently Loaded Modulefiles:
 1) GCCcore/10.2.0                 4) GCC/10.2.0                  
 2) zlib/1.2.11-GCCcore-10.2.0     5) OpenBLAS/0.3.12-GCC-10.2.0  
 3) binutils/2.35-GCCcore-10.2.0  
```

## The linking phase <a name="3"></a>
During the compilation, it is necessary to add the `-lopenblas` option: 

```bash
$ gcc example.c -lopenblas
```
