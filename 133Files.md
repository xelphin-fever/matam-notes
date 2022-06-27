# Python
# Files

## :book: Read

**file.txt**
```
1. Sunday
2. Monday
3. Tuesday
```

### read

Returns full file as a single string

```python
f  = open ('file.txt', 'r’)
           
f.read()
# '1. Sunday\n2. Monday\n3.Tuesday'
```

### readlines

Returns list where each element is a string containing a single line from file

```python
f  = open ('file.txt', 'r’)
           
f.readlines()
# ['1. Sunday\n', 2. Monday\n', '3.Tuesday']
```

### readline

Returns single line from file. In each call the line returned is the proceeding line in the file.

```python
f  = open ('file.txt', 'r’)
           
f.readline()
# '1. Sunday'

f.readline()
# '2. Monday'

f.close()
```

You can read with a loop in the following way:

```python
f = open("file.txt", 'r')

for line in f:
	print(line)

f.close()
```
> :exclamation: Must ```close()``` every file that has been ```open()```ed
>
## :pencil2: Write

### write
The function receives as a paramter a string and writes it into the file.

```python
f = open("new_file.txt", 'w')
s1 = "Hello World\n"
s2 = "End of file"

f.write(s1)
f.write(s2)

f.close()
```
**new_file.txt**
```
Hello world
End of file
```
> :exclamation: Must ```close()``` every file that has been ```open()```ed

> :heavy_check_mark: Recommended to use ```with```

## with

The file closes automatically in the end of ```with```s scope. No need to worry about manually closing the file.

**file.txt**
```
1. Sunday
2. Monday
3. Tuesday
```

```python
file_name = 'new_file.txt'

with open(file_name, 'r') as f:
    lines = f.readlines()

print(lines[0])

# '1. Sunday\n'
```

## :bookmark_tabs: Writing Dictionary Into File

```JSON``` - Javascript Object Notation: Conventional way of representing information using a simple ```.txt``` file. Supported by many programming languages.

> :exclamation: The ```keys``` have to be ```strings```

```python
import json

my_dict = {'key_1': 17, 
           'key_2': ['a', 'list']}

# Write my_dict to json
with open('myfile.json', 'w') as f:
   json.dump(my_dict, f, indent=4)

# Read myfile.json
with open('myfile.json', 'r') as f:
   loaded_dict = json.load(f)

print(loaded_dict)

# {'key_1': 17, 'key_2': ['a', 'list']}
```
**myfile.json**
```
{
    "key_1": 17,
    "key_2": [
        "a",
        "list"
    ]
}
```

> ```json.dumps``` and ```json.loads``` used for reading/writing directly from strings