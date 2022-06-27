# Python
# Conditions

## If

```python
x = 9
y = 7
if x > y:
    print("x is greater than y")
    x -= 1
print(x)
# x is greater than y
# 8
```

### If - Elif - Else

```python
if x > y:
    print("x is greater than y")
elif x == y:
    print("x is equal to y")
else:
    print("y is greater than x")
```

### Boolean

```python
x = 3
y = -3
if x >= 2 and y <= -2:
    print("True")
if x > 3 or y < -3:
    print("True")
if not x == y: # also: x != y
    print("True")

if x > y or not (x >= 3 and y <= -3):
    print("True")
```

```python
x = True
y = False
x and y
# False

type(x)
# <class 'bool'>
```

## while

```python
count = 0
while count < 3:
    print("count:", count)
    count += 1
print("Done")
# count: 0 
# count: 1 
# count: 2 
# Done
```

## for

```python
elements = [3, 'a', 5.5]
for element in elements:
    print(element)
print("Done")
# 3
# a
# 5.5
# Done
```

### Range
Returns an **iterable object** that represents the requested **range** *of elements* of **type int**.

```python
list(range(6,10))
# [6,7,8,9]

list(range(5))  # same as range(0,5)
# [0,1,2,3,4]

list(range(4,2))
# []

list(range(10, 0, -2))
# range(start, stop, step)
# [10,8,6,4,2]

type(range(10))
# <class 'range'>

list(range(10)) 
# [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

### for with range

```python
elements = [3, 'a', 5.5]
for i in range(3):
    print("iteration:", i)
    print("element:", elements[i])
print("Done")
# iteration: 0
# element: 3
# iteration: 1
# element: a
# iteration: 2
# element: 5.5
# Done
```


### for with enumerate

Using enumerate you can iterate over an iterable object. In eah iteration, receiving both the element and its index.

```python
elements = [3, 'a', 5.5]
for i, e in enumerate(elements):
    print("iteration:",i)
    print("element:", e)
Print("Done")
# iteration: 0
# element: 3
# iteration: 1
# element: a
# iteration: 2
# element: 5.5
# Done
```

**Note**: enumerate returns an iteration of tuples that represent pairs of (index, element)

### zip (command)

To iterate over a number of lists simultaneously, we'll use the ```zip``` command

```python
l1, l2 = ['We', 'Rock'], ['will', 'you']
for e1, e2 in zip(l1, l2):
    print(e1, e2)
# We will
# Rock you

l1, l2 = ['C', 'for'], ['is', 'Cookie']
print(zip(l1, l2))
# [('C', 'is'), ('for', 'Cookie')]

# Implementing 'enumerate' using 'zip' and 'range'
list(zip(range(len(l1)), l1))
# [(0, 'C'), (1, 'for')]
```

### List Comprehensions

**Method of creating a new list** by activating a calculation on each element in an existing list.

```[elem**2 for elem in myList if type(elem) is int]```

- ```myList``` is the **Input**
- ```elem``` is the **Name for the Element**
- ```type(elem) is int``` is the **Condition Expression** (optional)
- ```elem**2 is int``` is the **Output Expression**

Note: Can convert ```[]``` to ```()``` to get a tuple

```python
myList = [1, 4, 9, 'a', 'b', 0, 4]
squared_ints = [elem**2 for elem in myList if type(elem) is int]
# [1, 16, 81, 0, 16]
```

### Examples of 'for' Usage

**Iterating over a String**
```python
str_mtm = 'mtm'
for letter in str_mtm:
    print(letter)
# m
# t
# m
```

**Counting appearances of a 'char' in a String**

```python
seq = 'supercalifragilisticexpialidocious'

count = 0
for letter in seq:
    if letter == 's':
        count += 1   # count = count + 1
print(count)
# 3
```

## Dictionaries (or dict)

Dictionary is a datastructure that maps between  **keys** and **values**.

```python
new_dict = {
  'a': 1, 'b': 2, 'c': [3]
}
print(new_dict)
# {'a': 1, 'b': 2, 'c': [3]}
```

**Notice**: keys have to be of an immutable type

```python
d = {[3]: 4}
# TypeError: unhashable type: 'list'

d = {(3): 4} # okay
```

### Operations on dictionaries

```python
d = {'one': 1, 'two': 2, 'three': 3}

d['two']
# 2

d['two'] = [2]
print(d)
# {'one': 1, 'two': [2], 'three': 3}

d['four'] = 'quattro'
# {'one': 1, 'four': 'quattro', 'two': [2], 'three': 3}

del d['two']
# {'one': 1, 'four': 'quattro', 'three': 3}

'four' in d
# True
```

### for on dictionary

- ```items()```: returns iterators
- ```values()```: returns keys
- ```keys()```: returns pairs (key,value)

```python
d = {'C': 'cookie', 'B': 'Big bite', 'A': 'Apple'} 

# .items()
for k, v in d.items():
    print(k + ' is for ' + v)
# C is for cookie
# B is for Big bite
# A is for Apple

# .values()
for v in d.values():
    print(v)
# cookie
# Big bite
# Apple
  
# .keys()
for k in d.keys(): # also "for k in d:" 
    print(k)
# C
# B
# A
```

### Dictionary Comprehension

**Mechanism that creates a dictionary** by activating a calculation on each element in a sequence of existing elements. (very simmilar to list comprehensions)

```{elem: elem**2 for elem in myList if type(elem) is int}```

- ```myList``` is the **Input** (existing dictionary/list/iterable object)
- ```elem``` is the **Name for the Element**
- ```type(elem) is int``` is the **Condition Expression** (optional)
- ```elem**2 is int``` is the **Output Expression** of form (key : value)

```python
a_dict = {'a': 'Alfa', 'b': 'Bravo', 'c': 'Charlie', 'd': 'Delta'}

result = {letter: code.lower() for (letter, code) in a_dict.items()}
# {'a': 'alfa', 'b': 'bravo', 'c': 'charlie', 'd': 'delta'}

result = {'-'+letter+'-': code for (letter, code) in a_dict.items()
                               if len(code) >= 5}
# {'-b-': 'Bravo', '-c-': 'Charlie', '-d-': 'Delta'}
```
