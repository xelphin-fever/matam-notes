# Python
# Importing and Running Python Files

myfile1.py
```python
def getlanguageName():
    return 'Python'
print('Hello ' + who + '!')
```
```
$ python3 myfile1.py
Hello Python!
```

---

- The **interpreter** runs the commands line after line
- The ```import``` command includes a run on the file (module) to which we do the import
- Each declaration (variable, type, function) that appears in a file is saved under a namespace of the file name

---

myfile2.py
```python
import myfile1
print(myfile1.getlanguageName() + ' is cool!')
```
```
$ python3 myfile2.py
Hello Python!
Python is cool!
```

---

- ```import``` assumes that the file appears in the current folder or inside the PYTHONPATH
- We can also **import certain parts for a specific module**. Example:

myfile3.py
```python
from myfile1 import getlanguageName
print(getlanguageName() + 'is cool!')
```
```
$ python3 myfile3.py
Hello Python!
Python is cool!
```

## Running as a Script

- There are **two** mains ways to use a python file:
    - Can be run directly -> **Script**
    - Can apply ```import``` on it
- Occasionally, we'd like to use the file for both purposes (example: include in the same file functions that we use and tests for those same functions)
    - To run the tests, we'll run the file as a script
    - When we'll do ```import```, we'll import the functions without running the tests
- IF we'd want to run specific functions only when the run the file directly (not through ```import```) then we'll wrap the code with the following check:
```
if __ name__ == "__main__":
  <code>
```

### Example
We can add commands that are run when the file is run directlu from the line of command (not when imported)

myfile1.py
```python
who = 'Python'

if __name__ == "__main__":
    who = 'World'
    
print('Hello ' + who + '!')
```

The command under the condition will be run by direct activation of the file (but not in import time)

```
> python3 myfile1.py
Hello World!

> python3 myfile2.py
Hello Python!
Python is cool!
```

**Example**:

```python
def my_func():
    return 2

def test_my_func():
    return my_func() == 2

if __name__ == "__main__":
    if test_my_func:
	print(“TEST PASSED”)
    else:
	print(“TEST FAILED”)
```