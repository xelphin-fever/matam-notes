# C++
# Classes

```cpp
#include <iostream>
using namespace std; //using standard library
```

```cpp
// ------------------ CLASS------------------

class Complex {

  // ------------------ PRIVATE------------------
  // methods get secret parameter "this" which points at object

  double re, im;

  // STATIC VARIABLES - single copy for all objects
  static int initCounter;



  // ------------------ PUBLIC------------------

  public:

    // CONSTRUCTOR - creates object
    Complex(); // Default constructor
    Complex(double x, double y);

    // void init(double x, double y); // <- use constructor instead

    void add(Complex c);

    // CHAINING MEMBER FUNCTION CALLS - return object
    Complex& add_v2(Complex c);

    // CONST - won't change object
    double abs() const;

    // GETTERS & SETTERS - get/change object attributes
    double Complex::getReal() const;
    double Complex::setReal(double x);

    // STATIC - Can call without object
    // 1 shared by all objects
    static const double pi = 3.14159;
    static Complex conjugate(const Complex&);
    static Complex I();

    
  

}

//////////////////////////////////////////////////////

// ------------------ CONSTRUCTOR ------------------
// Create object

Complex::Complex(double x, double y) {
  re =x;
  im = y;
}


// ------------------ THIS POINTER ------------------


void Complex::add(Complex c) {
  // you can write like the way it's commented but it's !unecessary!
  re+= c.re; // this->re += c.re;
  im+= c.im; // this->im += c.im;
}
// c1.add(c2)  --> add(&c1,c2);


// ------------------ CHAINING MEMBER FUNCTION CALLS ------------------
// Return Object

// Complex& is a pointer (reference) to -> *this
Complex& Complex::add_v2(Complex c) {
  re += c.re;
  im += c.im;
  return *this; // return our Complex !
}

// ------------------ CONST ------------------
// Wont change object

double Complex::abs() const {
  return sqrt(re * re + im * im); 
  // return sqrt(this->re * this->re + this->im*this->im)
}
 

// ------------------ GETTERS AND SETTERS ------------------

double Complex::getReal() const {
  return re;
}
double Complex::setReal(double x) {
  re = x;
}

// ------------------ STATIC VARIABLE------------------
int Complex::initCounter = 0; // = 0 is optional because it's done by default

// ------------------ STATIC FUNCTION------------------
// Can call without object (and has access to private parts of class)
// Static function doesn't have access to 'this'

Complex Complex::conjugate(const Complex& c) {
  Complex result;
  result.init(c.re, -c.im);
  return res;
} // Complex c1 = Complex::conjugate(c1);

Complex Complex::I() {
  Complex result;
  result.init(0, 1);
  return res;
}

```

```cpp

// ------------------ MAIN ------------------

int main() {


  // ------------------ CHAINING MEMBER FUNCTION CALLS ------------------
  cout << "\n-- CHAINING MEMBER FUNCTION CALLS --\n" ;

  Complex c1, c2, c3;
  c1.add(c2).add(c3);

  // ------------------ STATIC ------------------
  cout << "\n-- STATIC --\n" ;

  // can access static public variables
  Complex c;
  c.init(Complex::pi / 2.0, 0.0);
  Complex c1 = Complex::I(); // Don't need an object to call!

  

  // ------------------ CONSTRUCTOR ------------------
  cout << "\n-- CONSTRUCTOR --\n" ;
  Complex c4(1.0, 0.0);
  Complex* pc5 = new Complex(1.0, 0.0);
  Complex default_c; // default constructor

  
  // ------------------ CONST ------------------
  const Complex const_c = new Complex(1,2);
  // can only access const functions!!
  
  
  return 0;
}

```

```cpp

// ------------------ USING CONST ------------------
void f(Complex& c, const Complex& c2) {
  c.add(c2);
  c2.add(c); // ERROR - c2 is const (in f())
  cout << c2.abs() << endl; // ok
}


//////////////////////////////////////////////////////


// ------------------ INIT ------------------


// BAD WRITING!! (can be called twice, not called...) Instead use constructor!
void Complex::init(double re, double im) {
  // !Have to! write like this
  this->re = re;
  this->im = im;
  initCounter++; // Access STATIC class
}
```