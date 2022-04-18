# Table of Contents
1. [Description](#desc)
2. [Singularity on SIMLAB](#1)
3. [Compiling a C program](#2)
4. [Compiling a Fortran program](#3)

## Description <a name="desc"></a>

## ICC on SIMLAB <a name="1"></a>

- List available versions:
```sh
$ module avail Intel_tools 
----------------------------- /cm/shared/modulefiles -----------------------------
Intel_tools  
```
- Load Intel-tools:
```sh
$ module load Intel-tools                  
```

## Compiling a C program <a name="2"></a>

```sh
$ cat hello.c

#include <stdio.h>

int main (int argc, char *argv[])
{
  printf("Hello world\n");

  return 0;
}
```

The standard way to compile the above program withou any optimization (recommended while debuging), is with the following command:

```sh
$ icc hello.c -o hello.exe
```
This command compiles `hello.c` into an executable program `"hello.exe"`
To run the executable use the command:

```bash
$./hello.exe

Hello world
```


## Compiling a Fortran program <a name="3"></a>

```Fortran
$ cat hello.f90

Program hello
  IMPLICIT NONE

  write(*,*)"Hello world"

end program hello
```

The standard way to compile the above program withou any optimization (recommended while debuging), is with the following command:

```sh
$ ifort hello.f90 -o hello
```

This command compiles `hello.f90` into an executable program `"hello.exe"`
To run the executable use the command:

```bash
$./hello.exe

Hello world
```


Thank you!
