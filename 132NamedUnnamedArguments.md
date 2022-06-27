# Python
# Named and Unnamed Arguments

- Similarlly to C++, we can define in python default arguments to fucntions.

- We can define the ```default``` values only to the last parameters of the function (like C++)

```python
def student(name, grade = 100):
	print('The student', name, 'got a grade of', grade)

# UNNAMED
student('Alice') # The student Alice got a grade of 100
student('Bob', 90) # The student Bob got a grade of 90.

# NAMED
student(name = 'Alice') # Named
student(name = 'Bob', grade = 90) # Named
student(grade = 90 , name = 'Bob') # Named

# NAMED & UNNAMED
student('Bob', grade = 90) # Both

```

**Notice**: When the paramters are identified using their names, there's no need to maintain their original order (from the function signature)

## Functions with Changing Amount of Parameters

- We can declare functions with an unknown amount of local parameters (unnamed). Optionally, after them you can receive named paramters.
- All local parameters will be received in the function as one ```list```, whose length is the size of the amount of parameters passed to it.

```python
def print_numbers(*numbers, separator=', '):
    for num in numbers[:-1]:
        print(num, end = '')
        print(separator, end = '')
    print(num)

print_numbers(1, 2, 3, 4)
# 1, 2, 3, 4
print_numbers(1, 2, 3, 4, 5, separator = ' ')
# 1 2 3 4 5
```

Another option is to define a function that receives an unknown (in advance) amount of named parameters that will received as a ```dictionary``` where:
- **keys** == names of parameters
- **values** == values of passed parameters
```python
def print_grades(**students):
    for student, grade in students.items():
        print(student, grade)

```
```python
print_grades(alex=100, bob=90, alice=95)
alex 100
bob 90
alice 95
```
