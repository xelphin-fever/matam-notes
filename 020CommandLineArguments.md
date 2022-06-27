# C
# Command Line Arguments

### argc
```argc``` stands forr argument count. It counts the amount of arguments placed on the command line.

### argv
```argv``` The array of arguments
- (In char**argv, an array of strings)
- argv[0] == the name of the program that ran
- argv[argc] == NULL

## Basic Example

```cpp
#include <stdio.h>

int main( int argc, char *argv[] )  {

   if( argc == 2 ) {
      printf("The argument supplied is %s.\n", argv[1]);
   }
   else if( argc > 2 ) {
      printf("Too many arguments supplied.\n");
   }
   else {
      printf("One argument expected.\n");
   }
}
```

In the command line:
```
$./a.out oranges
The argument supplied is oranges.

$./a.out oranges and chocolate
Too many arguments supplied.

$./a.out
One argument expected.
```
