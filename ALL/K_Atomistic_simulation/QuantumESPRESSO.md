# Table of Contents
1. [Description](#1)
2. [Quantum Espresso on SIMLAB](#2)

## Description <a name="1"></a>

Quantum Espresso is an open-source software for electronic structure calculations and materials modeling at the nanoscale. It is based on density functional theory, plane waves, and pseudopotentials.

## Quantum Espresso on SIMLAB

- Check available versions:

```sh
$ module avail QuantumESPRESSO
----------------- /cm/shared/modulefiles ------------------
QuantumESPRESSO/6.7-foss-2020b  
```

- Load QuantumESPRESSO (version 6.7, compiled with GCC-10.2.0 and OpenMPI-4.0.5):
```sh
$ module load QuantumESPRESSO
```

- List all modules loaded with QuantumESPRESSO:
```sh
$ module list
Currently Loaded Modulefiles:
 1) GCCcore/10.2.0                    13) PMIx/3.1.5-GCCcore-10.2.0       
 2) zlib/1.2.11-GCCcore-10.2.0        14) OpenMPI/4.0.5-GCC-10.2.0        
 3) binutils/2.35-GCCcore-10.2.0      15) OpenBLAS/0.3.12-GCC-10.2.0      
 4) GCC/10.2.0                        16) gompi/2020b                     
 5) numactl/2.0.13-GCCcore-10.2.0     17) FFTW/3.3.8-gompi-2020b          
 6) XZ/5.2.5-GCCcore-10.2.0           18) ScaLAPACK/2.1.0-gompi-2020b     
 7) libxml2/2.9.10-GCCcore-10.2.0     19) foss/2020b                      
 8) libpciaccess/0.16-GCCcore-10.2.0  20) Szip/2.1.1-GCCcore-10.2.0       
 9) hwloc/2.2.0-GCCcore-10.2.0        21) HDF5/1.10.7-gompi-2020b         
10) libevent/2.1.12-GCCcore-10.2.0    22) ELPA/2020.11.001-foss-2020b     
11) UCX/1.9.0-GCCcore-10.2.0          23) libxc/4.3.4-GCC-10.2.0          
12) libfabric/1.11.0-GCCcore-10.2.0   24) QuantumESPRESSO/6.7-foss-2020b  
```
