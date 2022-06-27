# C++
# 🦊🐺🐶 Polymorphism

## Classes
```cpp
class Animal {

  	int age, weight;
   
  public:
  	Animal(int age, int weight);
  	int getAge() const;
  	virtual void makeSound() const {
  		cout << endl;
  	} // no sound by default;
   virtual ~Animal() {}
   
};
```
```cpp
class Dog: public Animal {

  public:
  	Dog(int age, int weight);
  	void makeSound() const override{
  		cout << "woof woof" << endl;
  	}
   
};
```
```cpp
class Cat: public Animal {
public:
	Cat(int age, int weight);
	void makeSound() const override{
		cout << "meow" << endl;
	}
};
```
```cpp
class Fish: public Animal {
public:
	Fish(int age, int weight);
}; // the default makeSound() is OK
```


### Static vs Dynamic
```cpp
Dog* d = new Dog(3,4);
Animal* a = d;
a->makeSound(); // woof woof (See Note)
d->makeSound(); // woof woof
```
> **Note:** If Animal didn't have ```virtual``` in ```makeSound()``` then ```a->makeSound()``` would have selected ```Animal::makeSound()``` and not ```Dog::makeSound()```.
- Static: Compilation Time (The address of the function that we jump to is decided in compilation time)
- Dynamic: RunTime (The address of the function that we jump to is decided in runtime, this characteristic can be replicated in C by using function pointers)


### Arrays

```cpp
void foo() {
	Animal* animals[3];
	animals[0] = new Dog(3,4);
	animals[1] = new Fish(1,1);
	animals[2] = new Cat(2,2);
	for (int i = 0; i < 3; ++i) {
		animals[i]->makeSound();

    // (See Note)
		delete animals[i];
	}
}
```
> **Note:** Were it not for the ```virtual``` d'tor then the delete will have called for each type of animal the ```~Animal()```. Meaning the static version instead of the dynamic.

### Copying Objects

```cpp
void foo(Animal& a) {
	Animal a2 = a;
	a.makeSound(); // [Animal Type]::makeSound()									
	a2.makeSound(); // Animal::makeSound()
}
```


