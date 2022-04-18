# Table of Contents
1. [Description](#desc)
2. [EasyBuild on SIMLAB](#easyonsimlab)
3. [Searching for available easyconfigs files](#search)
4. [Install module](#install)
   1. [List new modules]("list)

## Description  <a name="desc"></a>

[EasyBuild](https://github.com/easybuilders/easybuild) is a software build and installation framework that allows you to manage (scientific) software on High Performance Computing (HPC) systems in an efficient way. For more information see [docs](https://docs.easybuild.io/en/latest/).

## EasyBuild on SIMLAB <a name="easyonsimlab"></a>

- List available versions:
```sh
$ module avail EasyBuild
---------------------------- /cm/shared/modulefiles ----------------------------
EasyBuild/4.4.2  
```
- Load EasyBuild (version 4.4.2):
```sh
$ module load EasyBuild
```
- List modules loaded with EasyBuild:
```sh
$ module list
Currently Loaded Modulefiles:
1) python/3.5.0   2) EasyBuild/4.4.2  
```

## Searching for available easyconfigs files <a name="search"></a>

```sh
$ eb --modules-tool EnvironmentModules --module-syntax Tcl -S gmsh
== found valid index for /cm/shared/apps/easybuild/4.4.2/lib/python3.5/site-packages/easybuild_easyconfigs-4.4.2-py3.5.egg/easybuild/easyconfigs, so using it...
CFGS1=/cm/shared/apps/easybuild/4.4.2/lib/python3.5/site-packages/easybuild_easyconfigs-4.4.2-py3.5.egg/easybuild/easyconfigs
* $CFGS1/g/gmsh/gmsh-3.0.6-foss-2017b-Python-2.7.14.eb
* $CFGS1/g/gmsh/gmsh-3.0.6-foss-2018b-Python-3.6.6.eb
* $CFGS1/g/gmsh/gmsh-4.2.2-foss-2018b-Python-3.6.6.eb
[...]
```

## Install module <a name="install"></a>

Install package with:
- ```--robot```  to enable dependency resolution.
- ```--detect-loaded-modules=error``` to print a clear error and stop when any (non-allowed) loaded modules are detected.
- ```--detect-loaded-modules=purge``` to run module purge if any (non-allowed) loaded modules are detected.
- ```--optarch=GENERIC``` to optimize for a generic processor architecture.

```sh
$ eb --modules-tool EnvironmentModules --module-syntax Tcl --prefix=/path/to/easybuild --robot --detect-loaded-modules=error --detect-loaded-modules=purge --optarch=GENERIC gmsh-4.7.1-foss-2020a-Python-3.8.2.eb
```

### List new modules <a name="list"></a>

```sh 
$ module avail
module avail gmsh-4.7.1-foss-2020a-Python-3.8.2.eb
---------------------------- /path/to/easybuild ----------------------------
gmsh/4.7.1-foss-2020a-Python-3.8.2
```
