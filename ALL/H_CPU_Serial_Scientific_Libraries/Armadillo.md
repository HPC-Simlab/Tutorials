# Table of Contents
1. [Description](#1)
2. [Armadillo on SIMLAB](#2)
3. [C++ example](#3)
4. [Linking phase](#4)

## Description <a name="1"></a>

Armadillo is a high quality linear algebra library (matrix maths) for the C++ language, aiming towards a good balance between speed and ease of use.

## Armadillo on SIMLAB <a name="2"></a>

- Check available versions:

```sh
$ module avail Armadillo
----------------- /cm/shared/modulefiles ------------------
Armadillo/9.900.1-foss-2020a  
```
- Load Armadillo:
```sh
$ module load Armadillo
```

<details><summary>List modules loaded (dependencies)</summary>
<p>

```bash
$ module list
Currently Loaded Modulefiles:
 1) GCCcore/9.3.0                    13) PMIx/3.1.5-GCCcore-9.3.0      
 2) zlib/1.2.11-GCCcore-9.3.0        14) OpenMPI/4.0.3-GCC-9.3.0       
 3) binutils/2.34-GCCcore-9.3.0      15) OpenBLAS/0.3.9-GCC-9.3.0      
 4) GCC/9.3.0                        16) gompi/2020a                   
 5) numactl/2.0.13-GCCcore-9.3.0     17) FFTW/3.3.8-gompi-2020a        
 6) XZ/5.2.5-GCCcore-9.3.0           18) ScaLAPACK/2.1.0-gompi-2020a   
 7) libxml2/2.9.10-GCCcore-9.3.0     19) foss/2020a                    
 8) libpciaccess/0.16-GCCcore-9.3.0  20) bzip2/1.0.8-GCCcore-9.3.0     
 9) hwloc/2.2.0-GCCcore-9.3.0        21) Boost/1.72.0-gompi-2020a      
10) libevent/2.1.11-GCCcore-9.3.0    22) Eigen/3.3.7-GCCcore-9.3.0     
11) UCX/1.8.0-GCCcore-9.3.0          23) arpack-ng/3.7.0-foss-2020a    
12) libfabric/1.11.0-GCCcore-9.3.0   24) Armadillo/9.900.1-foss-2020a  
```

</details>
</p>

## C++ example <a name="3"></a>

```sh
$ cat example.cpp

#include <iostream>
#include <armadillo>

using namespace std;
using namespace arma;

int main()
{
mat A(4, 5, fill::randu);
mat B(4, 5, fill::randu);

cout << A*B.t() << endl;

return 0;
}
```
## Linking phase <a name="4"></a>

The linking phase During the compilation, it is necessary to add the `-larmadillo` option.

```sh
$ g++ example.cpp -o example -std=c++11 -O2 -larmadillo
```
