# C++
# 🤙 Unique and Shared Pointers

## Smart Pointers

RAII means using an object with a destructor for any
type of operation that requires a clean up.

Instead of using a simple C pointer, we will use smart pointer. It's pretty much a class costuming as a pointer. Meaning that it has the functionaliy of a pointer but it also has a d'tor for example and so, is automatically deleted when it reaches the end of its scope.

```cpp
void good() {
  smart_ptr<Employee> emp(new Engineer("David"));
  // safe to use code that throws exceptions!!
  emp->giveRaise(500); // our smart_ptr has operator->()
  f(); // no problem if this throws an exception
  // the engineer will be automatically deleted
}
```

Employee's d'tor will automatically delete our engineer whenever good() terminates - whether normally or due to an exception

### Null Pointer
You can use ```nullptr``` as you would ```NULL```. It can be converted to any type of pointer (it can't be converted to an int value like NULL though).


### Creating a Smart Pointer
Implementation of a smart pointer.
```cpp
template<class T>
class smart_ptr {
  T* data;
  public:
  
    explicit smart_ptr(T* ptr = NULL);
    
    // UNIQUE
    smart_ptr(const smart_ptr&) = delete; // can't copy a pointer
    smart_ptr& operator=(const smart_ptr&) = delete; // can't be assigned to another pointer
    
    ~smart_ptr();
    T& operator*() const;
    T* operator->() const;
    
};
```
```cpp

// ACTS LIKE A POINTER, data is a pointer to the address
template<class T>
smart_ptr::smart_ptr(T* ptr)
  : data(ptr) {
}

// DELETES data (hooray! Now we don't need to free it manually.)
template<class T>
smart_ptr::~smart_ptr() {
  delete data;
}

template<class T>
T& smart_ptr::operator*() const {
  return *data;
}
template<class T>
T* smart_ptr::operator->() const {
  return data;
}
```
The automatic deletion
- Solve a lot of memory leaks like forgetting to
  delete.
- Solve ownership problems. An object can be allocated from one place and passed to another. Who deletes the object? Now there is no need to.

## std::unique_ptr

std::unique_ptr represents a smart pointer that
uniquely owns its object
- It is clear who owns the object, who is responsible for
  destroying it, and when it will be destroyed (when its
  owner is destructed!)
- It’s a highly efficient smart pointer that has no overhead
  compared to a C pointer

```cpp
#include <memory>
void f() {
  std::unique_ptr<Employee> emp(new Engineer("David"));
  emp->giveRaise(500);
  // ... safe to return or to use code that can throw exceptions
}
```
- std::unique_ptr cannot be copied or assigned. (They will both be pointing at the same thing, so if one is deleted and frees the memory it is pointing at, the other one is also deleted and is left pointing at garbage, and freeing the same memory block twice will cause a crash).
- However, we can transfer ownership between two
  unique_ptrs if needed (original pointer will point to NULL)

```cpp
unique_ptr<int> p1(new int(5));
unique_ptr<int> p2 = p1; // compilation error
unique_ptr<int> p3 = std::move(p1); // OK!
```
- A function can also allocate an object and return
  a unique_ptr to it
```cpp
unique_ptr<Employee> createEngineer(const char* name, int salary) {
  unique_ptr<Engineer> eng(new Engineer(name));
  eng->setSalary(salary);
  return eng;
}

unique_ptr<Employee> emp = createEngineer("David", 10000);
// No need for std::move() ownership is passed automatically
```
- We can't pass a unique_ptr to a function by value since it does not have a copy c'tor
- A function will typically just need to access the object, not own it
- We can just use ordinary C pointers for this!

An ordinary pointer that just points to an
object but is not responsible for it is called a **non-owning pointer**

```cpp
// This function can be used with any smart pointer or standard C pointer

void printEmployee(const Employee* emp) {
  cout << "Name: " << emp.getName() << endl;
  // ...
}
```
```cpp
unique_ptr<Employee> emp = createEngineer("David", 10000);
printEmployee(emp.get()); // get() returns a standard C pointer to the object
```
unique_ptr may be used as a member variable
(However, the object will not be copyable or
assignable since unique_ptr does not have those
operations, We can implement those manually if needed (and
duplicate the unique member for each object)

```cpp
class ChessGame {
  vector<Piece> m_whitePieces;
  vector<Piece> m_blackPieces;
  unique_ptr<ChessBoard> m_gameBoard;
  ...
}
```

## std::shared_ptr

std::shared_ptr is a smart pointer that allows multiple
smart pointers to point to the same object
- They all share ownership of that object
- Uses reference counting (It maintains a counter of all pointers referring to the same object, that way only once 0 are pointers are pointing to the object is it realeased)
- It has more overhead than unique_ptr so do not use it without a reason!

> std::shared_ptr is useful when we need multiple
objects to refer to the same object, and do not know
which of them will be destroyed last

Implementation:
```cpp
// ...
shared_ptr(const smart_ptr& other) : data(nullptr), counter(nullptr) {
	if (other.data) { 
    this->data = other.data; 
    this->counter = other.counter;
    *counter++;
  }
}
~shared_ptr() {
  *counter--;
	if (*this->counter==0) { 
    delete this->data; 
    delete this->counter;
	}
}
// ...
```

```cpp
shared_ptr<Employee> f() {
  shared_ptr<Employee> ptr1(new Engineer("Dave"));
  shared_ptr<SalesPerson> ptr2(new SalesPerson(…));
  shared_ptr<Employee> ptr3(new Manager("John"));
  
  ptr3 = ptr2;
  
  cout << ptr3->getYearlyCost() << endl;
  
  Employee& emp = *ptr1;
  return ptr3;
}
```
