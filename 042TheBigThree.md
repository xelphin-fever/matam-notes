# C++
# Big Three

- A class that has a field that allocates memory needs to be released
in its destructor.
- If the class uses pointers or allocates resources (such as dynamic memory),
a user-defined copy constructor is probably needed
- Similarly with an assignment operator (more information in later chapters)

```cpp
#include <iostream>
using namespace std; //using standard library
```
```cpp
class Array {
  int* data; // Array with unknown size -> Needs to be destroyed later
  int size;

  public:
    // CONSTRUCTOR
    Array(int size);
    // METHODS
    int& atIndex(int index);
    
    // ------------------ COPY CONSTRUCTOR ------------------
    
    Array(const Array&);
    
    // ------------------ ASSIGNMENT OPERATOR ------------------
    
    Array& operator=(const Array&);
    
    // ------------------ DESTRUCTOR ------------------
    
    ~Array();
    
}

// CONSTRUCTOR
Array::Array(int n) :
  data(new int[n]), size(n)
{}

// METHODS
int& Array::atIndex(int index) {
  assert(index >= 0 && index < size);
  return data[index];
}

// ------------------ COPY CONSTRUCTOR ------------------

Array::Array(const Array& arr) : 
  data(new int[arr.size]),
  size(arr.size)
{
  for (int i = 0; i < size; ++i) {
    data[i] = arr.data[i];
  }
} 

// ------------------ ASSIGNMENT OPERATOR ------------------

Array& Array::operator=(const Array& other)
{
  if (this == &other) {
    return *this;
  }

  int* tempData = new int[other.size()];
  try {
    for(int i=0; i<other.size(); i++) {
      tempData[i] = other.data[i];
    }
  } catch(...) {
      delete[] tempData;
      throw;
	}

  delete[] data;
  size = other.size();
  data = tempData;

  return *this;
}

// ------------------ DESTRUCTOR ------------------

// DECONSTRUCTOR
Array::~Array() {
  delete[] data;
}

```



```cpp
int main() {
  
  // ------------------ THE BIG THREE ------------------
  Array a(10);
  
  // ------------------ COPY CONSTRUCTOR ------------------
  Array b(a);
  Array c = a;
  
  // ------------------ ASSIGNMENT OPERATOR ------------------
  
  Array d(20);
  Array d = a;

  // ------------------ DESTRUCTOR------------------
  
  a.atIndex(3) = 2;
  cout << a.atIndex(3) << endl;

  Array* ptr = new Array(20);
  delete ptr; // calls ptr->~Array()
  
  return 0;
}
```