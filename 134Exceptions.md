# Python
# :exclamation: Exceptions

- In python you can throw objects of type ```Exception``` or from a type that inherits from it.

- Common python exceptions: ```ValueError```, ```TypeError```, ```RuntimeError```

### raise

```python
def print_pos_number(num):
    if num < 0:
       raise ValueError(num)
    print(num)
```

## Built In Exceptions

- ```IndexError```/```KeyError```: Trying to access non-existent index in list or non-existent key in dict
- ```TypeError```: Trying to operate on a type an operation that doesn't suit it
- ```ValueError```: Function recieves parameter of correct type but the value doesn't suit the function
- ```ZeroDivisionError```: Dividing by zero
- ```IOError```: Error connected in file treatment

## :adhesive_bandage: Treating Exceptions

### try ... except

```python
def print_pos_number(num):
    if num <= 0:
       raise ValueError(num)
    print(num)

try:
    print_pos_number(int(input('Enter a positive number: ')))
except ValueError:
    print('This was not a positive number…')
except KeyboardInterrupt:
    print(‘exiting…’) # Thrown when user presses ctrl+C
```

```
> python3 print_positive_number.py
Enter a positive number: -1
This was not a positive number…

> python3 print_positive_number.py
Enter a positive number: aaaa
This was not a positive number… 
```

## as

```python
def print_pos_number(num):
    if num <= 0:
       raise ValueError(num)
    print(num)

try:
    print_pos_number(int(input('Enter a positive number: ')))
except ValueError as err:
    print('This was not a positive number… exception:', err)

```

```
> python3 print_positive_number.py

Enter a positive number: -1
This was not a positive number… exception: -1
```

### try ... else

```python
def print_pos_number(num):
    if num < 0:
       raise ValueError(num)
    print(num)

try:
    print_pos_number(int(input('Enter a positive number: ')))
except ValueError as err:
    print('This was not a positive number… exception:', err)
else:
    print('That was a positive number, good job!')
```

```
> python3 print_positive_number.py
Enter a positive number: 5
5
That was a positive number, good job!
```

### try ... finally

```python
def print_pos_number(num):
    if num < 0:
       raise ValueError(num)
    print(num)

try:
    print_pos_number(int(input('Enter a positive number: ')))
except ValueError as err:
    print('This was not a positive number… exception:', err)
finally:
    print('All in all, a learning experience')
```

```
> python3 print_positive_number.py
Enter a positive number: 5
5
All in all, a learning experience
```

## 	:file_cabinet::outbox_tray: Stack Unwinding

- Simmilarly to C++, also in python the exception unwinds upwards in the stack.
- If an exception isn't caught in the function/main script then the program finishes its run and prints ```Traceback``` of the call stack.

```python
def print_pos_number(num):
    if num < 0:
       raise ValueError(num)
    print(num)

print_pos_number(int(input('Enter a positive number: ')))
```

```
Enter a positive number: -1
Traceback (most recent call last):
  File "test.py", line 5, in <module>
    print_pos_number(int(input('Enter a positive number: ')))
  File "test.py", line 3, in print_pos_number
    raise ValueError(num)
ValueError: -1
```

### print_stack

**test.py**

```python
from traceback import print_stack

def print_pos_number(num):
    if num < 0:
       raise ValueError(num)
    print_stack()
    print(num)

print_pos_number(int(input('Enter a positive number: ')))
```

```
Enter a positive number: 1
 File "test.py", line 9, in <module>
    print_pos_number(int(input('Enter a positive number: ')))
 File "test.py", line 6, in print_pos_number
    traceback.print_stack()
1
```

### assert

```python
x = "hello"
#if condition returns False, AssertionError is raised:
assert x == "goodbye"
```
```
Traceback (most recent call last):
  File "<string>", line 3, in <module>
AssertionError
```
> When ```assert``` criteria isn't fulfilled, ```AssertionError``` is thrown

Can also add error messages
```python
x = "hello"
assert x == "goodbye", "x should be goodbye'"
```
```
Traceback (most recent call last):
  File "<string>", line 2, in <module>
AssertionError: x should be 'goodbye'
```