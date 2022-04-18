# Table of Contents
1. [Description](#desc)
2. [GCC on SIMLAB](#1)
3. [Compiling a C programs](#2)
    1. [Compiling a single source file](#3)
    2. [Compiling multiple files](#4)
    3. [More gcc options](#5)
4. [Compiling a Fortran programs](#6)

## Description <a name="desc"></a>

GCC is the GNU C compiler, below are some examples that show how to use gcc to compile C programs.


## GCC on SIMLAB <a name="1"></a>
- List available versions:
```sh
$ module avail GCC
----------------- /cm/shared/modulefiles ------------------
GCC/8.3.0  GCC/9.3.0  GCC/10.2.0  GCCcore/8.3.0  GCCcore/9.3.0  GCCcore/10.2.0  
```
- Load GCC (version 9.3.0):
```sh
$ module load GCC/9.3.0
```
- List modules loaded with GCC9.3.0:
```sh
$ module list
Currently Loaded Modulefiles:
1) GCCcore/9.3.0   2) zlib/1.2.11-GCCcore-9.3.0   3) binutils/2.34-GCCcore-9.3.0   4) GCC/9.3.0                   
```

## Compiling a C programs <a name="2"></a>
### Compiling a single source file <a name="3"></a>

```c
$cat hello.c

#include <stdio.h>

int main()
{
  printf("Hello world")
}

```
The standard way to compile the above program withou any optimization (recommended while debuging), is with the following command:

```bash
gcc hello.c -o -o hello.exe
```
This command compiles `hello.c` into an executable program `"hello.exe"`
To run the executable use the command:

```bash
$./hello.exe

Hello world
```
When `gcc` is invoked, it normally does preprocessing, compilation, assembly and linking, we can stop this process at intermediate stage, in the following example
we will compile the the file hello.c into bytecode and then link it

```bash
gcc -c hello.c
gcc hello.o -o hello.exe
```
- `gcc -c hello.c`          : creates the object file hello.o(contains machine code)
- `gcc hello.o -o hello.exe`: takes the object file and links it to system libraries(or other object files if any)

### Compiling multiple files <a name="4"></a>

```sh
$cat main.c

void print_tab(int (*)[2], int, int);

int main()
{
	int T[][2] = {{1,2},{3,4}};
	print_tab(T, 2, 2);
	return 0;
}
```
```sh
$cat print_tab.c

#include <stdio.h>

void print_tab(int (*T)[2], int n, int m)
{
	for (unsigned i = 0; i < n; i++)
		for (unsigned j = 0; j < m; j++)
			printf("T[%u][%u] = %d\n", i, j, T[i][j]);
}
```

We can compile the above two files into a single executable using the following command:

```bash
$gcc main.c print_tab.c -o exec
$./exec

T[0][0] = 1
T[0][1] = 2
T[1][0] = 3
T[1][1] = 4

```

Or we can create object files first, and then link, as follows:

```bash
$gcc -c main.c print_tab.c
$gcc main.o print_tab.o -o exec
$./exec

T[0][0] = 1
T[0][1] = 2
T[1][0] = 3
T[1][1] = 4

```

*Note that the second method is much more optimal when dealing with many source files.*

### More gcc options <a name="5"></a>

- Compile a C program that uses *math.h* library functions
```bash
gcc prog.c -lm -o exec
```
- Optimize compilation

```bash
gcc -O prog.c -o exec
```
*Note: `-O<level>` to customize the optimization to your liking(reduce compilation time, reduce output binary code size ...)*  

- generate more warnings about syntactically correct but questionable looking code

```bash
gcc -Wall prog.c -o exec
```

- produce symbolic informations for gdb debugger, more on gdb [here](gdb.md)

```sh
gcc -g prog.c -o exec
```

## Compiling a Fortran programs <a name="6"></a>
```sh
$ cat hello.f90
Program hello
  IMPLICIT NONE

  write(*,*) "Hello world"

end program hello
```
The standard way to compile the above program withou any optimization (recommended while debuging), is with the following command:

```bash
gfortran hello.f90 -o hello.exe
```

This command compiles `hello.f90` into an executable program `"hello.exe"`
To run the executable use the command:

```bash
$./hello.exe

Hello world
```
