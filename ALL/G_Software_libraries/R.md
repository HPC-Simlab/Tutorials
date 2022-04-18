# Table of Contents
1. [Description](#1)
2. [R on SIMLAB](#2)
3. [Example of batch file using R](#3)

## Description  <a name="1"></a>

[R](https://en.wikipedia.org/wiki/R_(programming_language)) is a programming language and free software environment for statistical computing and graphics. It is supported by the R Core Team and the R Foundation for Statistical Computing. It is widely used among statisticians and data miners for developing statistical software and data analysis.

## R on SIMLAB  <a name="2"></a>

- Check available versions:
```sh
$ module avail R (version 4.0.0):
----------------- /cm/shared/modulefiles ------------------
R/4.0.0-foss-2020a  
``
- Load R:
```sh
$ module load R:
```
<details><summary>List modules</summary>
<p>

```sh 
$ module list
Currently Loaded Modulefiles:
 1) GCCcore/9.3.0                     35) LLVM/9.0.1-GCCcore-9.3.0            
 2) zlib/1.2.11-GCCcore-9.3.0         36) Mesa/20.0.2-GCCcore-9.3.0           
 3) binutils/2.34-GCCcore-9.3.0       37) libGLU/9.0.1-GCCcore-9.3.0          
 4) GCC/9.3.0                         38) pixman/0.38.4-GCCcore-9.3.0         
 5) numactl/2.0.13-GCCcore-9.3.0      39) libffi/3.3-GCCcore-9.3.0            
 6) XZ/5.2.5-GCCcore-9.3.0            40) gettext/0.20.1-GCCcore-9.3.0        
 7) libxml2/2.9.10-GCCcore-9.3.0      41) PCRE/8.44-GCCcore-9.3.0             
 8) libpciaccess/0.16-GCCcore-9.3.0   42) GLib/2.64.1-GCCcore-9.3.0           
 9) hwloc/2.2.0-GCCcore-9.3.0         43) cairo/1.16.0-GCCcore-9.3.0          
10) libevent/2.1.11-GCCcore-9.3.0     44) libreadline/8.0-GCCcore-9.3.0       
11) UCX/1.8.0-GCCcore-9.3.0           45) Tcl/8.6.10-GCCcore-9.3.0            
12) libfabric/1.11.0-GCCcore-9.3.0    46) SQLite/3.31.1-GCCcore-9.3.0         
13) PMIx/3.1.5-GCCcore-9.3.0          47) PCRE2/10.34-GCCcore-9.3.0           
14) OpenMPI/4.0.3-GCC-9.3.0           48) NASM/2.14.02-GCCcore-9.3.0          
15) OpenBLAS/0.3.9-GCC-9.3.0          49) libjpeg-turbo/2.0.4-GCCcore-9.3.0   
16) gompi/2020a                       50) LibTIFF/4.1.0-GCCcore-9.3.0         
17) FFTW/3.3.8-gompi-2020a            51) Java/11.0.2(11)                     
18) ScaLAPACK/2.1.0-gompi-2020a       52) Tk/8.6.10-GCCcore-9.3.0             
19) foss/2020a                        53) cURL/7.69.1-GCCcore-9.3.0           
20) bzip2/1.0.8-GCCcore-9.3.0         54) GMP/6.2.0-GCCcore-9.3.0             
21) expat/2.2.9-GCCcore-9.3.0         55) NLopt/2.6.1-GCCcore-9.3.0           
22) libpng/1.6.37-GCCcore-9.3.0       56) libsndfile/1.0.28-GCCcore-9.3.0     
23) freetype/2.10.1-GCCcore-9.3.0     57) ICU/66.1-GCCcore-9.3.0              
24) ncurses/6.2-GCCcore-9.3.0         58) Szip/2.1.1-GCCcore-9.3.0            
25) util-linux/2.35-GCCcore-9.3.0     59) HDF5/1.10.6-gompi-2020a             
26) fontconfig/2.13.92-GCCcore-9.3.0  60) UDUNITS/2.2.26-foss-2020a           
27) xorg-macros/1.19.2-GCCcore-9.3.0  61) GSL/2.6-GCC-9.3.0                   
28) X11/20200222-GCCcore-9.3.0        62) Ghostscript/9.52-GCCcore-9.3.0      
29) gzip/1.10-GCCcore-9.3.0           63) JasPer/2.0.14-GCCcore-9.3.0         
30) lz4/1.9.2-GCCcore-9.3.0           64) LittleCMS/2.9-GCCcore-9.3.0         
31) zstd/1.4.4-GCCcore-9.3.0          65) ImageMagick/7.0.10-1-GCCcore-9.3.0  
32) libdrm/2.4.100-GCCcore-9.3.0      66) GLPK/4.65-GCCcore-9.3.0             
33) libglvnd/1.2.0-GCCcore-9.3.0      67) R/4.0.0-foss-2020a                  
34) libunwind/1.3.1-GCCcore-9.3.0     
```

</p>
</details>

## Example of batch file using R  <a name="3"></a>

```bash
#!/bin/bash
#SBATCH --job-name=R-job      # create a short name for your job
#SBATCH --nodes=1                # node count
#SBATCH --ntasks=1               # total number of tasks across all nodes
#SBATCH --cpus-per-task=1        # cpu-cores per task (>1 if multi-threaded tasks)
#SBATCH --time=00:01:00          # total run time limit (HH:MM:SS)

module purge
module load R
Rscript myscript.R
```
