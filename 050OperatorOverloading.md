# C++
# Operator Overloading

A class can overload operators that are enacted on its object instances:
```cpp
Complex c1,c2;
Complex c3 = c1 + c2; // copy constructor on c3
```
In the example, we can define what ```+``` between two objects of type ```Complex```
will do.

### Binary Operator
- ```a.operator@(b)```  - Member function taking one argument
- or a nonmember function taking two arguments
- For any binary operator ```@```, the compiler interprets ```a@b``` as either
```a.operator@(b)``` or ```operator@(a,b)```

### Unary Operator
- ```a.operator@()```  - Member function taking no arguments
- As a nonmember function taking one argument
- For any prefix (left-side) unary operator ```@```,
the compiler interprets ```@a``` as either ```a.operator@()``` or ```operator@(a)```
- ```c2 = c1.operator-();``` or ```c2 = operator-(c1);```

### Friend
- Using a friend declaration we can grant an external function
access to the private section of a class



## Example

**Complex.h**
```cpp
#include <iostream>
class Complex {

  double re, im;
  
  // ------------------ FRIEND - ------------------
  friend bool operator==(const Complex& c1, const Complex& c2);
    
  // ------------------ OVERLOADING I/O OPERATIONS ------------------
  friend std::ostream& operator<<(std::ostream& os, const Complex& c);

  public:

    Complex();
    Complex(double x, double y);

    // ------------------ BINARY OPERATOR ------------------
    Complex operator+(const Complex& x) const;
    Complex& operator+=(const Complex& r);

    // ------------------ UNARY OPERATOR ------------------
    Complex operator- () const;
    

}

// ------------------ EXTERNAL FUNCTIONS ------------------
Complex operator+(const int realNumber, const Complex& other);
```


**Complex.cpp**
```cpp

// ------------------ CONSTRUCTOR ------------------

Complex::Complex(double x, double y) {
  re =x;
  im = y;
}

// ------------------ BINARY OPERATOR ------------------

// operator@(a,b)  <- Nonmember function taking two arguments

Complex& Complex::operator+=(const Complex& c) {
  re = re + c.real();
  im = im * c.imag();
  return *this;
}

Complex operator+ (const Complex& x, const Complex& y) {
  Complex result(x.real() + y.real(), x.imag() + y.imag());
  return result;
}


// ------------------ UNARY OPERATOR ------------------
// operator@(a)  <- Member function taking one argument
Complex operator- (const Complex& x);

// ------------------ FRIENDS - ------------------

bool operator==(const Complex& c1, const Complex& c2) {
  return c1.re == c2.re && c1.im == c2.im;
} 

// ------------------ OVERLOADING I/O OPERATIONS ------------------

std::ostream& operator<<(std::ostream& os, const Complex& c) {
  // std::ostream& os -> #include <iostream>
  os << c.re;
  os << "+ i" << r.im;
  return os;
}

// ------------------ EXTERNAL FUNCTIONS ------------------

Complex operator+(const int realNumber, const Complex& other)
{
  Complex newComplex= other;
  newComplex+=realNumber;
  return newComplex;
}
```

## Operator Overloading
- We'll be able to use ```+=``` , ```++``` , ```*```, ```/```,
```^```, ```!```, ```<```, ```&&```, ```()```, ```==```,```!=```  and 
 more with objects (see function f2())
- The overloaded operator must have at least one parameter which is a
user-defined type (a class, struct or enum)
- Can't overload ```::```, ```.```, ```.*```, ```?```, ```:```,
```sizeof```, ```typeid```
- The following operators can only be overloaded as member functions
(not external functions):
        ```=``` ```[]``` ```()``` ```->```
  - ```()``` can be overloaded with any number of parameters
  - ```->``` must return an object for which -> is a valid operator

```cpp
int main() {

  Complex c1, c2;
  
  // ------------------ BINARY OPERATOR ------------------  
  Complex c3 = c1 + c2; // copy constructor on c3
  Complex c3 = c1 + 2; 


  // ------------------ UNARY OPERATOR ------------------

  c2 = -c1;
  
  // ------------------ FRIEND ------------------
  
  bool areEqual = (c1 == c2);


  // ------------------ OVERLOADING I/O OPERATIONS ------------------

   cout << c1 << endl;
   
   // ------------------ EXTERNAL FUNCTIONS ------------------
   
   Complex c4 = 2 + c1;
    
    
  return 0;
}

```

## Convenience

```cpp
// without operator overloading == not convenient
void f1(Complex c1) {
  Complex c2(3.0, 2.0);
  Complex input;
  input.readFrom(cin);
  c2.multiply(input);
  c1.add(c2);
  c2.printTo(cout);
}

// with operator overrloading == convenient
void f2(Complex c1) {
  Complex c2(3.0, 2.0);
  Complex input;
  cin >> input;
  cout << (c1 + c2 * input);
}
```