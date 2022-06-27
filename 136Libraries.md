# Python
# :books: Common Libraries

- Python has many Libraries (for: machine learning, data analysis, linear algebra, working with OS, networking, receiving arguments from command line and more...)
- Can install new libraries with ```pip```

The following are some basic built in libraries in the language:

## sys

- Allows access to variables and functions that connect to interpreter

```python
import sys

print('Error', file = sys.stderr) #prints to stderr

for arg in sys.argv: #prints the command line argument of a script
    print(arg) 
```

## os

- Allows access to many os methods

```python
import os
```

- Independent from os - Runs without dependency on them, run on Windows, Linux or any other os

- ```os.listdir(path)``` - Prints files from given directory
- ```os.sep``` - The character seperating between libraries in current os

```python
> path = 'home{}mtm{}top_secret_dir'.format(os.sep,os.sep)
#  path = 'home/mtm/top_secret_dir' in linux.
> os.listdir(path)
['tutorial13_python3.pptx', 'matam_exam_final.pdf', 'secret_nuclear_codes.txt']
```

- ```os.path.join(*path)``` - Receives elements of path and connects them into one path (as conventional in current os)
```python
> path = os.path.join('home’, 'mtm’, 'top_secret_dir')
# 'home/mtm/top_secret_dir' in linux.
```

- ```os.path.dirname(path)``` - Receives element of path and returns of parent directory
```python
> dir_path = os.path.dirname(path)
# dir_path = 'home/mtm'.
```

- ```os.path.basename(path)``` - Receives element of path and returns name of file/directory to which the path leads
```python
> dir_path = os.path.basename(path)
# dir_path = ‘top_secret_dir'.
```

- ```os.path.split(path)``` - Receives element of path and returns tuple with 2 elements: the start of path and its end
```python
> os.path.split(path)
('home/mtm', 'top_secret_dir')
```

- ```os.path.splittext(path)``` - Receives element of path and returns tuple with 2 elements: the path without end and its end
```python
> full_path = os.path.join(path, 'secret_nuclear_codes.txt’)
> os.path.splitext(full_path)
('home/mtm/top_secret_dir/secret_nuclear_codes', '.txt')
```

- ```os.mkdir(path)``` - Creates directory with given path
```python
> directory_name = 'cats_images’
> directory_path = os.path.join(path, directory_name)
> os.makedir(directory_path)
> os.listdir(path)
['tutorial13_python3.pptx', 'matam_exam_final.pdf', 'secret_nuclear_codes.txt', 'cats_images']
```

- ```os.path.isfile(path)``` - Returns True If the path belongs to a file (False if its a directory)
- ```os.path.isdir(path)``` - Returns True If the path belongs to a directory (False if its a file)

### Concluding Example

We'll write a program that prints the content of all files in the directory that are passed as a parameter in the script

```python
import os
import sys

if len(sys.argv) != 2:
    print('usage: script.py <path_to_dir>')

path = sys.argv[1]
for file in os.listdir(path):
    file_path = os.path.join(path,file)
    if os.path.isfile(file_path):
	 with open(file_path , 'r’) as f:
	     print(f.read())
```

```
> python3 script.py /home/mtm/top_secret_dir
Nuclear codes: 4, 8, 15, 25, 47, 42
Final exam: File too large
...
```

## Other Libraries (Built In)

### argparse

Advanced management of parameters from command line, including flags, optional parameters and more.

### shutil

Completing library for os that supplies functionality like copying/erasing files and libraries.

### math

Collection of common math functions.

### abc

Library for defining abstract classes.

### Itertools

Collection of function for working with iterators, like chaining iterators, repeating iterators a number of times and more.

### Random

Collection of functions for creating random.

### Time

Receiving current time, measuring time, containing program runtime to set amount and more.

### Pickle

Saving and loading python objects to files.

### Async

For working asynchronously.

## Other Libraries (External)

### Numpy

Mathematical library that treats matrices, vectors, static functions, mathematical calculations and more.

### Scipy

Library extending numpy with numerous numerical and lagorithmic calculation capabilities (integration, optimization and more).

### Matplotlib

Library fro interactive visualisation of two or multi dimensional graphs

### openCV

Library for working with photos and videos.

### Requests

Network management with internet sites and services (http): creatingconnections, passing data, secure communication and more.

### TensorFlow/PyTorch

Library for machine learning.

