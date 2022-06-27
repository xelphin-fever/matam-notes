# Python
# Python Language

## Variables

```<varname> = <value>```
```python
x = 7  # Create a new variable with the value 7

x = 5  # Change the value of x to 5

x = (4*9)/6 # Change the value of x to 6

y = 3
x = y*4 # Change the value of x to 12
```

Attempting to access a variable that has not been declared will cause a runtime error that will cause the program to exit (if running script) or stopping the running of the code (if interactively running python)

### Variable Types

```python
x = 3.14
type(x)
# <class 'float'>
```

### Print

```python
n = 3
print(n)
# 3
```

### Arithmetic Operators

- \+ addition
- \- subtraction
- \* multiplication
- \** power
- / division
- % modulo
- // integer division

## strings

strings are written with ```"```...```"```
```python
print ("Hello World!")
# Hello World!

s = "Hello"
print(s)
# Hello

type(s)
# <class ‘str’>

s = 'Hello'
print(s)
# Hello
```

Can be accessed like an array:

```python
print(s[0])
# H
print(s[4])
# o
print(s[-1])
# o
print(s[-3])
# l
```

### Concatenation

```
> s1 = "Hello"
> s2 = "World"
> print(s1+' '+s2)
Hello World
```

### Editing

Can't edit individual characters
```python
s = "Dog"
s[0] = "d"
# TypeError: 'str' object does not support item assignment
```
But can change the string entirely
```python
s = "Dog"
s = "Cat"
```

### Slicing

```python
s = "Some String"
```
```s[start:end]```
Returns new string
```python
sub_s = s[1:6]
print(sub_s)
# ome S
```

Can also use step_size
```s[start:end:step_size]```

```python
s[5:]
# String
s[5::2]
# Srn
```

### More Operations on Strings

```python
mystr = “Hello”
len(mystr)
# 5

mystr = “Hello”
mystr.startswith(“He”)
# True

mystr = “    Hello   ”
mystr.strip()
# Hello

mystr = “Hello”
mystr.upper()
# HELLO

mystr = “021334”
mystr.isdigit()
# True

mystr = “hello”
mystr.find(“lo”)
# 3

mystr = “Hello”
mystr.replace(“el”, “ro”)
# Hrolo

mystr = “     ”
mystr.ispace()
# True
```

### print()

```python
print(3, 5, 6)
# 3 5 6

print(3, 5, 6, sep=“;”)
# 3;5;6

print(3, 5.4, “Cat”)
# 3 5.1 Cat
```

### string.format()

```python
s = “My number is {} and twice my number is {}”.format(5, 10)
print(s)
# My number is 5 and twice my number is 10
```

## Lists

```python
new_list = [ 1, 2, 3, 4, 5 ]
print(new_list)
# [1,2,3,4,5]

empty_list = []
print(empty_list)
# []

zeros = [0]*5
print(zeros)
# [0, 0, 0, 0, 0]

mixed_types = [7, 'dog', [7], 3.14]
print(mixed_types)
# [7, ‘dog’, [7], 3.14]

```

### Indexing

```python
my_list = ["Eran", "Efrat", "Tal", "Lotem"]

my_list[0]
# "Eran"

my_list[3]
# "Lotem"

my_list[4]

# Traceback (most recent call last):
#   File "<stdin>", line 1, in <module>
# IndexError: list index out of range

my_list[-1]
# "Lotem"
```

### Slicing

```python
my_list = ['a','b','c','d','e','f','g','h','i','j']
my_list[1:5] # Slicing
# ['b', 'c', 'd', 'e']

# Slicing does NOT change the original list
my_list 
# ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j']

# Slicing using an arithmetic progression
my_list[0:9:2]
# ['a', 'c', 'e', 'g', 'i']

# We can omit any of these
my_list[0::2]
# ['a', 'c', 'e', 'g', ‘i’]

my_list[1::2]
# [‘b', ‘d', ‘f', ‘h', ‘j']
```

### Adding Elements

```python
new_list = [ 1, 2, 3, 4, 5 ]
print(new_list)
# [1,2,3,4,5]

new_list.append(8)
print(new_list)
# [1,2,3,4,5,8]
```

```python
new_list = [ 1, 2, 3, 4, 5 ]
print(new_list)
# [1,2,3,4,5]

new_list.insert(1, 'one')
print(new_list)
# [1,'one',2,3,4,5]

new_list[1] = 10
# [1,10,2,3,4,5]
```
```python
new_list = [ 1, 2, 3, 4, 5 ]
new_list.extend([23, 22])
# [1,2,3,4,5,23,22]

new_list.append([55, 56])
# [1,2,3,4,5,23,22, [55, 56]]
```
```python
new_list = [1,2,3] + [4,5]

new_list += [23, 22]
# [1,2,3,4,5,23,22]
```

### Changing Existing Elements

```python
new_list = [ 1, 2, 3, 4, 5 ]

new_list[3] = 77

# [1, 2, 3, 77, 5]

new_list[0:3] = [90, 100, 10]

# [90, 100, 10, 77, 5]
```

### Deleting Elements

```python
new_list = [ 1, 2, 3, 4, 2, 5 ]

new_list.remove(2)
# [ 1, 3, 4, 2, 5 ]

del new_list[2]
# [ 1, 3, 2, 5 ]

x = new_list.pop(2) 
# [ 1, 3, 5 ]
```

### copy

```python
a = [1, 2, 3]
b = a
b[1] = 5
print(a)
# [ 1, 5, 3]    

b = a.copy()
b[1] = 5
print(a, b)
# [ 1, 2, 3] [ 1, 5, 3]    
```

Deep Copy:
``` > from copy import deepcopy```
```python
a = [17, [1, 'dog'], ['bog', 5.3]]
b = a.copy()
b[1] = 5
b[2][0] = 5

print(b)
# [17, 5, [5, 5.3]]
print(a)
# [17, [1, 'dog'], [5, 5.3]]
```

### Comparing

```python
a = [1, 2, 3]
b = a 
c = a.copy()
a is b
# True
print(a is c, a == c)
# False True
```
```python
a = 3
b = 3
c = a
print(a is b, a is c)
# ?? (depends on implementation)
```
```python
a = 3
b = a
a = 4
print(a is b, b)
# False 3
```

### More Operations on Lists

```python
my_list = [1, 3, 2, 0, -1, 1, 1]
len(my_list)
# 7

my_list = [1, 3, 2, 0, -1, 1, 1]
max(my_list)
# 3

my_list = [1, 3, 2, 0, -1, 1, 1]
my_list.count()
# 3

my_list = [1, 3, 2, 0, -1, 1, 1]
my_list.index(1)
# 0

my_list = [1, 3, 2, 0, -1, 1, 1]
my_list.sort()
print(my_list)
# [-1, 0, 1, 1, 1, 2, 3]

my_list = [1, 3, 2, 0, -1, 1, 1]
sorted(my_list)
# [-1, 0, 1, 1, 1, 2, 3]

my_list = [1, 3, 2, 0, -1, 1, 1]
my_list.reverse()
# [1, 1, -1, 0, 2, 3, 1]

my_list = [1, 3, 2, 0, -1, 1, 1]
4 in my_list
# False
```

## Tuples
Tuples are immutable (can't be changed, but can be copied).

```python
new_tuple = ( 1, 2, 3, 4, 5 )
print(new_tuple)
# (1,2,3,4,5)

new_tuple[2] = 0
# Type Error: ‘tuple’ object does not support item assignment

empty_tuple = ()
print(empty_tuple)
# ()

zeros = (0, )*5
print(zeros)
# (0, 0, 0, 0, 0)

mixed = (7, 'dog', [7], 3.14)
mytuple = (5, 3) + mixed
print(mytuple)
# (5,3,7,’dog’,[7],3.14)
```

## * Operator

The * operator operates on sequences (list, tuples, strings...).

Converts the sequence's elements into comma seperated values.![image](image.png)

```python
mixed = (5, 'dog', [7], 3.14)
print(mixed)
# (5, 'dog', [7], 3.14)

mytuple = (3, mixed)
print(mytuple)
# (3, (5, 'dog', [7], 3.14))

mytuple = (3, *mixed) # like (3, 5, ‘dog’, [7], 3.14)
print(mytuple)
# (3, 5, 'dog', [7], 3.14)

mytuple = (3, *mixed) # like print(3, 5, ‘dog’, [7], 3.14)
print(*mytuple)
# 3 5 dog [7] 3.14
```

## Unpacking

```python
my_tuple = (1, 2)
a, b = my_tuple
print(a, b)
# 1 2

my_tuple = (1, 2, 3)
a, _, b = my_tuple
print(a, b)
# 1 3
```