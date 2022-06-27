# C++
# Namespaces

```cpp
#include <iostream>
using namespace std;
```

- Hierarchy: Organize large code into modules, sub-modules, etc.
- Name isolation: define a package (a set of classes, functions, constants, type definitions, etc.) in a namespace to ensure that the names it defines do not conflict with existing code
- Version control: maintain multiple versions of the code

## NameSpace Functions

**fast_math.h**
```cpp
namespace fast_math {
  double sqrt(double);
  double cos(double);
  double sin(double);
  double norm(double x, double y);
}
```
**fast_math.cpp**
```cpp
#include <cmath>
#include "fast_math.h"
```
```sqrt()``` exists also in ```std```, but if I want to use mine (from ```fast_math.h```)
then I can build a namespace

```cpp
namespace fast_math {
  double norm(double x, double y) {
    return sqrt(x*x + y*y);
  }
}
// OR
double fast_math::norm(double x, double y) {
  return sqrt(x*x + y*y);
}
```

## Using NameSpaces

There are various ways you can define which namespace you are using:

### Declaring NameSpaces

**main.cpp**
```cpp
namespace mtm {
  namespace ex4 {
    enum ErrorCode { OUT_OF_MEMORY, ... };
      printError(ErrorCode e);
    }
} 
```
OR
```cpp
using namespace mtm::ex4;
printError(OUT_OF_MEMORY);
```

- ❗ Do not write ````using```` in ```.h``` file
- ❗ If the functions from the namespaces you are using have the same names,
then you have to use prefix

```cpp
namespace linux_GUI {...}
namespace windows_GUI {...}
using namespace windows_GUI;
```

### Prefix

```cpp
x = 3;
cout << std::sqrt(x) << endl; // I explain I want sqrt() that is in std
cout << fast_math::sqrt(x) << endl; // I explain I want sqrt() that is in fast_math
```

Nested Namepsaces:

```cpp
mtm::ex4::printError(mtm::ex4::OUT_OF_MEMORY);
std::cout << "Error!" << std::endl;
```



