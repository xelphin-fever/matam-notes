# C
# Macros With Files

## Example

### MyFunctions.h 

```cpp
#ifndef MY_FUNCTIONS_H
#define MY_FUNCTIONS_H

int add_subtract (int num1, int num2, int calc);
int multiply (int num1, int num2);

#endif
```

### MyFunctions.c

```cpp
#include "MyFunctions.h"

int add_subtract (int num1, int num2, int calc)
{
  return num1 + calc*num2;
}

int multiply (int num1, int num2)
{
  return num1*num2;
}
```

### MyFile.c

```cpp
#include "MyFunctions.h"

// ...
```

## Explanation

This IFNDEF/DEFINE/ENDIF is used so that you don't copy paste the file twice
So if you've already copy pasted add_subtract() then you won't do it again


"Well I just wont include some_functions.h twice, dah"

### Example for why you need this method

```cpp
// file1.c
#include "MyFunctions.c"
```

```cpp
// file2.c
#include "MyFunctions.c"
```

```cpp
// Foo.c
#include "file1.c"
#include "file2.c"
```

I included MyFunctions.c twice inside of ```Foo.c```! This is bad because I defined ```add_subtract()``` and ```multiply()``` twice inside of ```Foo.c``` (this is the copy/pasting of the preprocessing)

### How does it work?

```cpp
// file1.c
#include "MyFunctions.h"
```

```cpp
// file2.c
#include "MyFunctions.h"
```

```cpp
// Foo.c
#include "file1.h"
#include "file2.h"
```

The first time ```Foo.c``` includes ```MyFunctions.h```, ```MY_FUNCTIONS_H``` is not defined and so it defines ```MY_FUNCTIONS_H``` and also includes ```add_subtract()``` and ```multiply()```

The second time it includes ```MyFunctions.h``` , ```MY_FUNCTIONS_H``` is already defined and so it skips to the ```endif``` and doesn't include ```add_subtract``` and ```multiply()``` again