# Table of Contents
1. [Some useful information](#1)
2. [Example of Fortran functions](#2)
3. [Example of calling Fortran functions from C](#3)
4. [Compilation and execution](#4)


## Some useful information <a name="1"></a>
1. To pass a variable by value, we use the VALUE attribute, because in Fortran, parameter passing is done by address whereas in C it is done by value.
2. For multidimensional arrays, the indexes order is reversed as shown in the examples.

## Example of a Fortran subroutine <a name="2"></a>

```sh
$ cat average.f90

module ffromc 
  use ISO_C_BINDING, only : C_CHAR, C_INT, C_FLOAT
  contains
  SUBROUTINE average(T, res, l) bind(C,name='avrg')
    integer(kind=C_INT), VALUE              :: l
    real(kind=C_FLOAT)                      :: res 
    real(kind=C_FLOAT), dimension(l)        :: T
    do i=1,l
      res = res + T(i)
    end do
    res = res / l
  END SUBROUTINE average
end module ffromc
```

## Example of calling Fortran functions from C <a name="3"></a>

```sh
$ cat main.c

#include <stdio.h>
int main()
{
	float T[]={1.0, 2.0, 3.0, 4.0};
	float av;
	av = 0;

	avrg(T, &av, 4); /* Call Fortran subroutine */ 
	/* Note: Fortran indexes arrays 1..n */
	/* C indexes arrays 0..(n-1) */ 
	printf("the average = %f\n", av);

	return 0;
}
```

## Compilation and execution <a name="4"></a>

- Compile C and Fortran files:

```bash
$ gcc -c main.c
$ gcc -c average.f90
$ gfortran main.o average.o -o file.exe
```
- Execute `file.exe` file:

```sh
$ ./file.exe

the average = 2.500000
```
