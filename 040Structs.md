# C++
# Structs

**Complex.h**
```cpp
#ifndef COMPLEX_H_
#define COMPLEX_H_

struct Complex {
  double re, im;

  // sets re and im to x and y
  void init(double x, double y) {
    // init(2,3) is safer than c1.re = 2; , c1.im = 3;
    re = x;
    im = y;
  }

  void add(Complex other);
}

void Complex::add(Complex other) {
  re += other.re;
  im += other.im;
}

#endif
```

**main.cpp**
```cpp
#include <iostream>
#include "Complex.h" 
using namespace std; 
```
```cpp
Complex c1;

cout << sizeof(c1) << endl; 
// prints 16 (size of) c1 

c1.init(4.0,1.0);
c1.re = 4;
c1.add(5.0);
```

## Encapsulate Struct

Can't access fields of struct declared inside of ```private:```

**Complex.h**
```cpp
#ifndef COMPLEX_H_
#define COMPLEX_H_

struct Complex {

  private:
    double re, im;

  public:
    void init(double x, double y);
    void add(Complex c);

  void add(Complex other);
}

void Complex::add(Complex c) {
  re+=c.re; // here we can access private fields
  im+=c.im; 
  // private members can be accessed by functions defined within the struct!
}

void Complex::changeReal(Complex c) {
  re=c.re; // here we can access private fields
}

#endif
```

**main.cpp**
```cpp
#include <iostream>
#include "Complex.h" 
using namespace std; 
```
```cpp
Complex c1;

❕ c1.re = 4; // ERROR - Now it's encapsulated so I can't access private fields
c1.changeReal(4);
```