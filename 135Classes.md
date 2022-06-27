# Python
# :woman_mechanic: Classes

- Define class with ```class```
- Class methods are defined within the class
    - To notify that they are class methods we use the ```self``` parameter (like ```this``` from C++)

```python
class Dog:
  def bark(self):
    print('Woof')

dog = Dog()
dog.bark() # Woof
```

## :wrench: Fields

- Can access fields using ```<object>.<field>```
- No access control (everything is public)
- Conventional to initialize

```python
class Dog:
  def __init__(self, name):
  	self.name = name

  def bark(self):
    print('Woof, says', self.name)

dog = Dog('Rexy')
print(dog.name) # Rexy
dog.bark() # Woof, says Rexy
```

> :grey_exclamation: No need for destructor (automatic memory release in python)
> :exclamation: Can't access class fields without ```self``` Example: ```print('Woof, says', name) # must use self.name```

## :family_man_woman_girl: Inheritance

```python
class Dog:
  def __init__(self, name):
  	self.name = name

  def bark(self):
    print('Woof, says', self.name) # must use self.name

class Chiwawa(Dog):
  def bark(self):
    print(‘Weef, says’, self.name) # must use self.name

dogs = [Dog("Tino"), Chiwawa("Toy")[
[dog.bark() for dog in dogs]
```
```
woof, says Tino
weef, says Toy
```