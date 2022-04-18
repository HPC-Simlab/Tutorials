# Table of Contents
1. [Description](#desc)
2. [Displaying the installed modules](#display)
   1. [Default modules](#default)
2. [Module commads](#commands)
   1. [Load module](#load)
   2. [List loaded modules](#list)
   3. [Load more than module](#loadmore)
   4. [Unload module](#unload)

## Description <a name="desc"></a>

 To load the products installed on SIMLAB, it is necessary to use the `module` command. 

## Displaying the installed modules <a name="display"></a>

### Default modules <a name="default"></a>

```sh
$ module avail
----------------------------------------- /cm/local/modulefiles -----------------------------------------
cluster-tools-dell/8.1  dot             intel/mic/sdk/3.8.4  module-git   openldap                      
cluster-tools/8.1       freeipmi/1.5.7  ipmitool/1.8.18      module-info  openmpi/mlnx/gcc/64/3.1.1rc1  
cmd                     gcc/7.2.0       lua/5.3.4            null         shared                        

---------------------------------------- /cm/shared/modulefiles -----------------------------------------
ABINIT/8.10.1                           libpng/1.6.37-GCCcore-9.3.0                     
ABINIT/9.4.1-foss-2020b                 libpng12/gcc/1.2.56                             
abinit/gcc/64/8.10.1                    libreadline/8.0-GCCcore-8.3.0                   
acml/gcc-int64/64/5.3.1                 libreadline/8.0-GCCcore-9.3.0                   
acml/gcc-int64/fma4/5.3.1               libunwind/1.3.1-GCCcore-9.3.0                   
acml/gcc-int64/mp/64/5.3.1              libxc/4.3.4-GCC-10.2.0                          
acml/gcc-int64/mp/fma4/5.3.1            libxml2/2.9.9-GCCcore-8.3.0                     
acml/gcc/64/5.3.1                       libxml2/2.9.10-GCCcore-9.3.0                    
acml/gcc/fma4/5.3.1                     libxml2/2.9.10-GCCcore-10.2.0                   
acml/gcc/mp/64/5.3.1                    liggghts/gcc/3.8.0                              
acml/gcc/mp/fma4/5.3.1                  LLVM/9.0.1-GCCcore-9.3.0                        
anaconda/3-5.2.0                        Lua/5.3.5-GCCcore-9.3.0                         
anaconda/3-5.3.1                        lz4/1.9.2-GCCcore-9.3.0                         
Anaconda3/2020.11                       M4/1.4.17                                       
ansys/2020.r1                           magma/intel/2.4.0                               
ansys/2021.r1                           maple/2018                                      
ansys/v201                              matlab/gcc/R2019a                               
Armadillo/9.900.1-foss-2020a            matlab/gcc/R2019b                       
[...]
```

## Module commands <a name="commands"></a>

`module purge`: used to unload all loaded modules

### Load module <a name="load"></a>
```bash
$ module purge
$ module load GCC
```

### List loaded modules <a name="list"></a>
```sh
$ module list
Currently Loaded Modulefiles:
 1) GCCcore/10.2.0               3) binutils/2.35-GCCcore-10.2.0  
 2) zlib/1.2.11-GCCcore-10.2.0   4) GCC/10.2.0   
```

### Load more than module <a name="loadmore"></a>
```bash
$ module purge
$ module load GCC UCX
$ module list
Currently Loaded Modulefiles:
 1) GCCcore/10.2.0                 4) GCC/10.2.0                     
 2) zlib/1.2.11-GCCcore-10.2.0     5) numactl/2.0.13-GCCcore-10.2.0  
 3) binutils/2.35-GCCcore-10.2.0   6) UCX/1.9.0-GCCcore-10.2.0      
```

### Unload module <a name="unload"></a>

- Unload a specific module:
```sh
$ module unload UXC
$ module list
Currently Loaded Modulefiles:
 1) GCCcore/10.2.0                 4) GCC/10.2.0                     
 2) zlib/1.2.11-GCCcore-10.2.0     5) numactl/2.0.13-GCCcore-10.2.0  
 3) binutils/2.35-GCCcore-10.2.0 
```
- You can unload all modules loaded: 

```sh
$ module purge
$ module list
No Modulefiles Currently Loaded.
```


**Remark**
You need to unload modules when trying to load new ones to avoid the conflicts.

***Example***

- Load GCC (version 9.3.0):
```sh 
$ module load GCC/9.3.0
```
- List the modules loaded:
```sh
$ module list
Currently Loaded Modulefiles:
 1) GCCcore/9.3.0               3) binutils/2.34-GCCcore-9.3.0  
 2) zlib/1.2.11-GCCcore-9.3.0   4) GCC/9.3.0   
```
- Load module GCC (version 10.2.0): 
```sh
$ module load GCC/10.2.0 
WARNING: GCC/10.2.0 cannot be loaded due to a conflict.
HINT: Might try "module unload GCC" first.
```
**You first need to unload `GCC/9.3.0` (dependencies also) and load `GCC/10.2.0`** 

- Unload all modules depending on GGC/9.3.0
```sh
$ module unload GCCcore/9.3.0 zlib/1.2.11-GCCcore-9.3.0 binutils/2.34-GCCcore-9.3.0 GCC/9.3.0 
```
or 
```sh
$ module purge
```

- Now you can load GCC/10.2.0:
```sh
$ module load GCC/10.2.0
```
