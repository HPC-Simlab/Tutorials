# Table of Contents
1. [Some useful information](#1)
2. [FreeFem++ on SIMLAB](#2)
3. [Run example on interactive mode](#3)

## Some useful information <a name="1"></a>

- FreeFEM is free software: you can redistribute it and/or modify  it under the terms of the GNU Lesser General Public License as  published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.     
- FreeFEM is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU Lesser General Public License for more details.

## FreeFem on SIMLAB <a name="2"></a>

To setup your environment for working with FreeFem please follow these steps:

- Check available version:
```sh
$ module avail freefem++
---------------------------- /cm/shared/modulefiles ----------------------------
freefem++/gcc/3.61-1  
```
- Load freefem++:
```sh
$ module load freefem++
```
- Check loaded modules (dependencies):
```sh
$ module list
Currently Loaded Modulefiles:
 1) hdf5/1.10.1   3) openmpi/gcc/64/3.1.4  
 2) mesa/17.1.1   4) freefem++/gcc/3.61-1  
```

## Run example on interactive mode <a name="3"></a>

For Freefem++ examples see [github](https://github.com/FreeFem/FreeFem-sources/tree/master/examples)

- Run `test.edp` example:
```sh                                                                                                          
FreeFem++ test.edp
```
