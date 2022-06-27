# Python :snake:

- Programming language
- Popular and a wide range of available packages
- Easy usability for development and testing of new code
- Works with interpreter
- Simple syntax
- Supports wide range of operating systems
- Free and Open Source

C++:
```cpp
#include <stdio.h>
int main() {
  printf("hello world!\n");
  return 0;
}
```
Python:
```python
print("hello world!");
```

## Interpreter vs Compiler

**Compiler**: Translates full program into efficient machine code (exe file), that can be operated and ran directly from CPU.

**Interpreter**: Interactively runs line after line in code

Runtime of program that used compiler is usually shorter than that used with interpreter.

## Running Python Code

- Install python
- In CS server use ```python3.6``` command

### Interactively on Terminal

```
python 3.6
```
Python commands such as:
```
print("Hello World!")
```
Exit using:Ctrl+d

### Using Script

- Create python file

hello.py
```python
print("Hello World!")
```

- Run file in terminal

```
python hello.py
```

### Unix
- Create python file

hello.py
```python
#! /usr/local/bin/python3.6
print("Hello World!")
```
- Run in terminal
```
chmod u+x hello.py
./hello.py
```
