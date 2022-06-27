# C++
# Templates

## Usage

- Sometimes, we will want to receive a parameter type at runtime.
- For example a ```sort()``` algorithm for different types of data.
  - Instead of ```sort()``` for ints, another for strings and so forth
  - We can make a generic one .

There are two new keywords in C++ that support templates ```template``` 
and ```typename``` (or ```class```)

## Template Syntax
```cpp
// -- Find max between two elements
template<class T>
T max(const T& a, const T& b) {
    return a > b ? a : b;
}
```
> In the class of ```T```, they did an operator overload for ```>```.
> This way, it does it accurately to whichever type it gets

```cpp
// -- Find max in array of elements
template<class T> // Template has one parameter
T max_element(const T* arr, int size) {
    T result = arr[0]; // Initialize using copy constructor
    for (int i = 1; i < size; ++i) {
        result = max(result, arr[i]);
    }
    return result;
}
```

## Calling Templates

```cpp
int a = 7, b = 5;
double d1 = 2.0, d2 = 3.0;
```

**Implicitley** Called:
```cpp
cout << max(a, b) << endl; // call max() with int
cout << max(d1, d2) << endl; // call max() with double
```
**Explicitley** Called:
```cpp
cout << max<int>(a, b) << endl;
cout << max<double>(d1, d2) << endl;
```

## Argument Deduction

- There are function templates where you **have to** call them **explicitley**
- the compiler will never use type conversion when deducing types

Template Functions:
```cpp
// -- Create new object of <type>
template<class T>
T* create() {
 return new T();
}

// --Covert object <S> into object <T>
template<class T, class S>
T convert(const S& s) {
 return T(s); // Copy Constructor
} 
```
Caling Template Functions:
```cpp
❕  int* ptr1 = create(); // ERROR
int* ptr1 = create<int>(); // has to be explicit
double int_to_double = convert<double, int>(n); // <explicit, deducible>
```

