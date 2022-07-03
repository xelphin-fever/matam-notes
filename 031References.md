# C++
# References

```cpp
#include <iostream>
using namespace std;
```

A reference variable is an alias, that is, another name for an already existing variable.

```cpp
int i = 1;
int& i_ref = i; 
int i_copy = i_ref;
i_ref = 2; 
cout << "i is: " << i << endl; // 2
cout << "i_ref is: " << i_ref << endl; // 2
cout << "i_copy is: " << i_copy << endl; // 1
```
> ❗ Reference must be initialized to some value

> ❗ Reference can't be changed to refer to a different variable

## Const

```cpp
int norm_int = 7; // int
const int const_int = 5; // const int
const int* ptr_to_const_int = &const_int; // pointer to const int
❕  int* const const_ptr_to_int = &const_int; // Error - because n is 'const int' and not 'int'
int* const const_ptr_to_int = &norm_int;
const int* const const_ptr_to_const_int = &const_int; // a const pointer to a const int
```
```cpp
❕ int& nc_x = 1; // Error
const int& c_x = 1;
```

## References as Function Parameters

```cpp
int firstValue = 5;
int secondValue = 3;
swap(firstValue, secondValue); 
```
> ❗ Can't do ```swap(4,5)```, you can't refer to local values or constants
```cpp
void swap(int& a, int& b) {
  int temp = a;
  a = b;
  b = temp;
}
```
> ❗ Never return a reference to a local value !!! (value declared inside function)
## Const Reference

A const reference CAN refer to a temp value, but can't be changed inside a scope its not
defined in.
```cpp
int a = 5;
print(a)
print(3);
print(3 + a);
```

```cpp
void print(const int& r) {
  cout << r << endl;
}
```
- The given r doesn't need to come from a constant variable.
- Only means it won't be changed here
- Avoids duplication of large structs in memory

## Pointer to Array

```cpp
int array[5] = { 1, 2, 3, 4, 5 };
getMax(array,5) = 0 ; // array[4] = 0 <- weird, don't do this
```
```cpp
int& getMax(int array[], int size) {
	int max_id = 0;
	for (int i = 1; i < size; ++i) {
		if (array[i] > array[max_id]) {
			max_id = i;
		}
	}
	return array[max_id]; // return reference to 
}
```

## Reference v.s Pointer 

- Can't refer to NULL
- Don't need to use & * (of course when you declare & for first time you need to use it)
- Can't change the variable you're pointing to
- In pointers you can use [] (to find values before and after pointer)

## Overloading

```cpp
void print(int); // (1)
void print(double); // (2)
void print(const char*); // (3)
void print(char); // (4)

void h(char c, int i, float f, double d, long l) {
	print(c); // 4
	print(f); // 2
	print(d); // 2
	print(i); // 1
	// print(l); // none
	
	print('a'); // 4
	print(49); // 1
	print(0); // 1
	print("Hello"); // 3
}
```
### Default Value
```cpp
printNumbers(5);
printNumbers(); // printNumbers(10);
```

```cpp
static void printNumbers(int n = 10) {
  for (int i = 0; i < n; ++i) {
    cout << i << " ";
  }
  cout << endl;
}
```

