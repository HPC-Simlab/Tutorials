# Table of Contents
1. [Description](#1)
2. [LIGGGHTS on SIMLAB](#2)
3. [Run example on interactive mode](#3)

## Description <a name="1"></a>

LIGGGHTS is an Open Source Discrete Element Method Particle Simulation Software. see more in [docs](https://www.cfdem.com/liggghts-open-source-discrete-element-method-particle-simulation-code)

## LIGGGHTS on SIMLAB <a name="2"></a>

- Check available versions:

```sh
$ module avail liggghts
---------------------------- /cm/shared/modulefiles ----------------------------
liggghts/gcc/3.8.0  
```

- Load liggghts:
```sh
$ module load liggghts
```

- Check modules loaded (dependencies):
```sh
$ module list
Currently Loaded Modulefiles:
 1) gcc/7.2.0                           5) fftw3/openmpi/gcc/64/3.3.7  
 2) openmpi/gcc/64/3.1.4                6) vtk/gcc/v8.0.1              
 3) fftw2/openmpi/gcc/64/double/2.1.5   7) liggghts/gcc/3.8.0          
 4) boost/1.68.0                       
```

## Run example on interactive mode <a name="3"></a>
```sh
mpirun -np 4 lmp_auto < in.chute_wear
```

For more examples see [github](https://github.com/ParticulateFlow/LIGGGHTS-PFM)
