# C
# Pointers


## Basic Pointers

```cpp
double my_value = 3.0;
double * my_value_address = &my_value; // I'm a pointer
double give_me_pointer_value = *my_value_address; // 3.0 (dereferencing)

printf("My value is: %.1f, and its address is %p\n", *my_value_address, my_value_address);
```

## NULL Address

Address 0 is NULL. You can't literally assign a pointer to address 0. However, you can assign an address to NULL. You do so when you want to show that the pointer isn't pointing at anything

```cpp
int * points_to_NULL = NULL;
```
You can't dereference!
```cpp
int a = *pointer; // -> Computer crashes
```
You HAVE TO initialize pointers to something.

## VOID* Pointers

Pointer **type** can be decided at runtime

```cpp
int int_value = 5;
double double_value = 3.14;

void* ptr = &int_value;
ptr = &double_value;
```

But you cannot dereference a void*
```cpp
double double_value_copy = *ptr;
```
Your options for dereferencing:
```cpp
// OPTION 1
double value_3 = *(double*)ptr;

// OPTION 2
double* double_value_ptr = ptr; // Implicit cast from void* to double*
double value_4 = *double_value_ptr; // O.K
```

## Pointer to a Pointer

```cpp
int some_value = 3;
int * ptr_some_value = &some_value;
int ** ptr_ptr_some_value = &ptr_some_value;

printf("Pointer of pointer points to: %d\n", **ptr_ptr_some_value);
```

### Example for Usage

```cpp
void swap_strings(char** str1, char** str2) {
	char* temp = *str1;
	*str1 = *str2;
	*str2 = temp;
}
```

A string is an array/pointer, hence: char** str1 is a pointer to a string

## Const Pointers

Notice the difference between the following two examples:

**Constant Pointer**
```cpp
int x = 5;
int * const x_ptr = &x;

// I can change the value of x
*x_ptr = 7;
// I CANNOT change who x_ptr is pointing to
int y = 7;
x_ptr  = &y; // ERROR

```
**Pointer to Constant**

```cpp
int x = 5;
const int* x_ptr = &x;

// I can change who x_ptr is pointing to
int y = 7;
x_ptr  = &y; 
// I CANNOT change the value of x
*x_ptr = 7; // ERROR
```

## Function Pointer

Useful for when you want to choose the function to use during runtime.

Functions:
```cpp
int cube(int num)
{
  return num*num*num;
}

void apply_to_array(int a[], int n, int (*operation)(int))
{
  // int (*operation)(int) --> function pointer
  for(int i=0; i<n; i++) {
    a[i] = operation(a[i]); // replaces a[i] with square(a[i])
  }
}

double derivative(int (*func)(int), int x)
{
  const double h = 1e-6;
  double diff = func(x+h) - func(x-h);
  return diff/(2+h);
}
```

Function Pointers:

```cpp
int (*function_ptr)(int);
function_ptr = cube; // function_ptr points to function cube()

int a[100], b[50];
apply_to_array(a, 100, square);
apply_to_array(b, 50, cube);

//

printf("use square %lf\n", derivative(square, 1));
printf("use cubed %lf\n", derivative(cube, 3));
```