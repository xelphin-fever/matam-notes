# Python
# Functions

## Syntax

```python
def function_name(arg1, arg2, ...):
    statements
```

- We **don't define** the return value, type of argument, decleration of function
- We can **use the function** starting from the line **after its initialization**
- The command ```pass``` indicates an empty command
- Return value of function that does not have a ```return``` command is ```None```
- Unlike C++, there's no function overriding

## Examples

```python
def sumTwo(a,b) :
  return a + b

sumTwo(1,5)
# 6
sumtwo('Hello', 'World')
# 'Hello World'
```

```python
def avg(elements):
    sum = 0
    for elem in elements:
        sum += elem
    return sum / len(elements)
```

## Type

```python
type(sumTwo)
# <class 'function’>
```

## Passing a function as a parameter

```python
def map(seq, f):
    return [f(elem) for elem in seq]

def square(x):
  return x**2
map(square, [1, 2, 3])
# [1, 4, 9]
```

### Example

```python
def derivative(f, x, epsilon): 
    assert epsilon > 0
    dy = f(x + epsilon) – f(x – epsilon)
    dx = 2 * epsilon
    return dy / dx
```
```python
from math import sin, cos, pi

derivative(sin, pi/4, 0.001)
0.707106663335455

cos(pi/4)
0.7071067811865475
```
