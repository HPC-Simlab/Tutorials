# Table of Contents
1. [Some useful information](#1)
2. [Example of C functions](#2)
3. [Example of calling C functions from Fortran](#3)
4. [Compilation and execution](#4)


## Some useful information <a name="1"></a>

1. In C a string is a NUL-terminated array of characters while in Fortran each string has a length associated with it and is thus not terminated,
in the following examples we NUL-terminate fortran strings.
2. To pass a variable by value, we use the VALUE attribute, because in Fortran, parameter passing is done by address whereas in C it is done by value.
3. For multidimensional arrays, the indexes order is reversed as shown in the examples.

## Example of C functions <a name="2"></a>

```sh
$ cat file.c

#include <stdio.h>

void print_C(char *string)
{
	printf("%s\n", string);
}

int power(int n, int m)
{
	int i;
	int result;

	i = 0;
	result = 1;
	while (i < m)
	{
		result = result * n;
		i++;
	}
	return result;
}

void print_table(int T[][3], int n, int m)
{
	for (unsigned i = 0; i < n; ++i)
		for (unsigned j = 0; j < m; ++j)
            printf("tab[%u][%u] = %d\n", i, j, T[i][j]);
}
```

## Example of calling C functions from Fortran <a name="3"></a>

```sh
$ cat file.f90 
module cfromf 
  use ISO_C_BINDING, only : C_INT, C_CHAR
  interface
    INTEGER(kind=C_INT) function pow(n , m) bind(C, name='power')
        import C_INT
        INTEGER(kind=C_INT), VALUE :: n
        INTEGER(kind=C_INT), VALUE :: m
    end function pow
    subroutine cprint(string) bind(C, name="print_C")
        use iso_c_binding, only: C_CHAR 
        CHARACTER(kind=C_CHAR) :: string(*)
    end subroutine cprint
    subroutine cprint_table(T, n, m) bind(C, name="print_table")
        use iso_c_binding, only: C_INT
        INTEGER(kind=C_INT), VALUE :: n
        INTEGER(kind=C_INT), VALUE :: m
        INTEGER(kind=C_INT), dimension(3,2) :: T
    end subroutine cprint_table
  end interface
end module cfromf
!
PROGRAM c_from_f 
  use ISO_C_BINDING, only : C_NULL_CHAR
  use cfromf
  IMPLICIT NONE
  CHARACTER(len = 20)   :: hw = 'hellow world from c'//C_NULL_CHAR
  INTEGER               :: n = 2
  INTEGER               :: m = 2
  INTEGER               :: result
  INTEGER, dimension(3,2) :: T
  INTEGER :: i, j
  do i = 1, 3 
    do j = 1, 2
        T(i, j) = i+j
    end do
  end do

  call cprint(hw)
  result = pow(n, m)
  PRINT '(a, i0)', 'result = ', result
  call cprint_table(T, 2, 3)
END PROGRAM c_from_f
```

## Compilation and execution <a name="4"></a>

- Compile C and Fotran files:
```bash
$ gcc -c file.c
$ gfortran file.f90 file.o -o file.exe
```
- Execute `file.exe` file:
```sh
$ ./file.exe

hellow world from c
result = 4
tab[0][0] = 2
tab[0][1] = 3
tab[0][2] = 4
tab[1][0] = 3
tab[1][1] = 4
tab[1][2] = 5
```
