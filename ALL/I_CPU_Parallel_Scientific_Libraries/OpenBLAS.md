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
- Let's try a simple level-1 routine e.g. `dscal` (Multiplies each element of a vector `x` by a constant (double-precision)`alpha`.)
refer to the [Blas documentation](https://www.netlib.org/blas/index.html)
for more information:
```c
#include <stdio.h>
#include "cblas.h"

int main(int argc, char **argv) {
  double x[3] = {1.0, 2.0, 3.0};
  double alpha = 2.0;

  printf("Pre dscal\t: %g %g %g\n", x[0], x[1], x[2]);

  cblas_dscal(3, alpha, x, 1);

  printf("Post dscal\t: %g %g %g\n", x[0], x[1], x[2]);
  return 0;
}
```
- To compile our example, it is necessary to add the `-lopenblas` option:
```bash
$ gcc example.c -lopenblas
```
- You can run the executable to see the result:
```bash
$ ./a.out
Pre dscal       : 1 2 3
Post dscal      : 2 4 6
```
