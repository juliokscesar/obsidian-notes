https://web.stanford.edu/class/me200c/tutorial_77/

Fortran 77 foi a primeira linguagem de alto nível.

# Basic structure and informations
```fortran
program name

(declarations)

(statements)

stop
end
```
No variable can have the same name as the program `name`.

Example of a program to read a radius and calculate the circle area:
```fortran
	program circle
	
	real r, area

c This is a comment
c This program reas a real number r and prints
c the area of a circle with radius r
* this is also a comment

	write (*,*) 'Give radius r:'
	read  (*,*) r
	area = 3.14159*r*r
	write (*,*) 'Area = ', area
	
	stop
	end
```

## Column position rules
Fortran 77 is *not* a free-format language, but has a very strict set of rules for how the source code should be formatted. The most important rules are:
- Col. 1: Blank, or a 'c' or '\*' for comments
- Col. 1-5: Statement label (optional)
- Col. 6: Continuation of previous line (optional)
- Col. 7-72: statements
- Col. 73-80: Sequence number (optional, rarely used)

## Compiling
In linux, there is a package `gcc-fortran` with the compiler `gfortran`. It works the same as if using simple `gcc` with C files.

# Types and declarations
The main types are:
- `real`: floating point numbers (like `float`). 4 byte
- `integer`: no need to explain. 32 bit values.
- `character`: one char or strings. When declaring in statement the size needs to be passed
- `logical`: boolean (`.TRUE.` and `.FALSE.`)
- `double precision`: like `double` in C. 8 byte
- `complex`: equivalent to a pair of `reals`

Declaring variables look like (after the program name and before statements):
```fortran
	program name
	
	integer (list of variables)
	real (list of variables)
...
```

**Note**: when declaring character strings, the size of the string needs to be specified as well:
```fortran
	character*9 name, class
```
in this example `name` and `class` are both 9 characters long (not counting the terminator character `\0`).

Also, single quotes and double quotes can be used to declare strings:
```fortran
'ABC' => ABC
'It''s a nice day' => It's a nice day
```
### Naming variables
Fortran is not case-sensitive. Most common rules from other programming languages apply to Fortran too. 

There is only the strict standard of Fortran77 (which doesn't need to be followed) for naming variables:
- must start with letter of the alphabet
- must contain only upper case letters or digits
- must be at most 6 characters long

### Parameter statement and constants
There is no `const` qualifier in Fortran. The `parameter` statement does its job, for example:
```fortran
	program circle
	real r, area, pi
	parameter (pi = 3.14159)
```
Note that we first need to declare the variable name and then specify that it's a constant with the `parameter` statement.
The general syntax is:
```fortran
type name1, name2, ..., namen
parameter (name1 = constant, name2 = constant2, ..., namen = constantn)
```

***Real and Double constants***:
When declaring `real` or `double` constants, we can use the E-notation and the D-notation, respectively:
```fortran
	2.0E6
c ^ == 2 million with real type precision

	1D99
c ^ == double value 1 followed by 99 zeros
```

# Operators
## Arithmetic operators
- `+` 
- `-`
- `/`
- `*`
- `**` -> exponentiation

## Type conversion
The following functions are available for conversion (just like in Python):
```fortran
	int
	real
	dble
	char
	ichar
```
`ichar` takes a character and converts it to an integer. `char` does the opposite.

# Logical expressions
Logical expressions can yield the value `.TRUE.` or `.FALSE.`. There are the *relational* operators:
- `.LT.`: less than (<)
- `.GT.`: greater than (>)
- `.LE.`: <=
- `.GE.`: >=
- `.EQ.`: ==
- `.NE.`: !=

And the *logical operators* are:
- `.AND.`
- `.OR.`
- `.NOT.`

## `if` statements
`if` statements can be written in a single line if only one executable statement will be used:
```fortran
if (logical expression) executable statement
```

The most general form is:
```fortran
if (_logical expression_) then
	statements
elseif (_another logical expression_) then
	statements
.
.
.
else
	statements
endif
```

# Loops
