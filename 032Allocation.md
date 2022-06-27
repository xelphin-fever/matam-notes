# C++
# Allocation

- ```new``` initializes the object
- ```delete``` calls its destructor

Syntax: ```type* name = new type(value);```
```cpp
int* ptr = new int(5); // In C: -> int* ptr = malloc(sizeof(*ptr));  -> *ptr = 5;
int* array = new int[10](); // In C: -> int* array = malloc(sizeof(*array) * 10); 
// ...
delete ptr; // In C: -> free(ptr);
delete[] array; // In C: -> free(array);
```
