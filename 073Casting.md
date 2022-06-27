# C++
# 🪄 Casting

```s
Type(var)
// same thing
(Type)var
```

- Casting between two different objects can cause unwanted behaviour expecially when the objects don't have a clear overlap.
- Casting between pointers that have an inheritance connection
- Cast that removes const (usually done accidentally)

To solve these issues, C++ defines a collection of operations to differentiate
between the different types of casts and to allow the compiler to ensure the cast.

## Types of Cast

- **static_cast**: Casts between objects with a defined cast operation between them , or between pointers/references that have an inheritance connection
- **dynamic_cast**: Casts between pointers/references that have an inheritance connection
- **const_cast**: Removes const from the type (requires caution)
- **reinterpret_cast**: Casts between two different types by redefining their bit representations

### static_const
Assume ```class B: public A``` and class C doesn't inherit from A:
```cpp
void f(int n, A& base) {
  
  // Pointers/References that have an inheritance connection
	double d = static_cast<double>(n);
	B& derived = static_cast<B&>(base);
	B* ptr = static_cast<B*>(&base);
  
	// The following will not compile:
  // int* -> double* is not safe
	double* ptr2 = static_cast<double*>(&n);
  // A and C are unrelated
	C& unrelated = static_cast<C&>(base);
  
}
```
> static_const maintains const, so the compiler won't allow its removal


## dynamic_cast - Data on Objects in Runtime

Imagine the following:
```cpp
class Engineer : public Employee {
  // ...
public: 
  // UNIQUE to Engineer
  void printDegrees() const;
}; 
```
```cpp
void printDegrees(const Employee* employees[], int n) 
{
  for (int i = 0; i < n; ++i) {
    if (/** employees[i] is an Engineer **/) {
      cout << employees[i]->getName() << endl;
      employees[i]->printDegrees();
      // BUT this won't compile because printDegree() is not defined in Employee
    }
  }
}
```
SOLUTION
```cpp
void printDegrees(const Employee* employees[], int n)
{
  for (int i = 0; i < n; ++i) {
    // Turn Employee to Engineer
    const Engineer* eng = dynamic_cast<const Engineer*>(employees[i]);
    // If it was possible to turn it:
    if (eng != nullptr) {
      eng->printDegrees();
    }
  }
}
```

### Another Example
```cpp
void g(int n, A& base) 
{
	B* ptr = dynamic_cast<B*>(&base);
	if (ptr == nullptr) {
		cerr << "base is not a B";
	}
	try {
		B& derived = dynamic_cast<B&>(base);
	} catch (const std::bad_cast&) {
		cerr << "base is not a B";
	}
  // the following will not compile
	double* ptr2 = dynamic_cast<double*>(&n);
	C& unrelated = dynamic_cast<C&>(base);
}

```
> dynamic_const maintains const, so the compiler won't allow its removal


