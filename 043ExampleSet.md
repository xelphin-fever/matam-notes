# C++
# Set Example

**Set.h**
```cpp
#ifndef SET_H_
#define SET_H_
#include <string>

class Set {

  private:
    int* data; // the elements of the set
    int size; // the current number of elements in the set
    int maxSize; // the allocated size of the array

    int find(int number) const;
    void expand();

    /** The initial size of the set array */
    static const int EXPAND_RATE = 2;

    /** The factor by which to expand the array when needed */
    static const int INITIAL_SIZE = 10;

    /** Returned by 'find' when an element is not in the set */
    static const int NUMBER_NOT_FOUND = -1;

  public:
    Set();
    Set(const Set&);
    ~Set();
    bool add(int number);
    bool remove(int number);
    bool contains(int number) const;
    int getSize() const;
    Set& uniteWith(const Set&);
    Set& intersectWith(const Set&);

    std::string toString() const; // useful for debugging

    // …
};


Set unionH(const Set&, const Set&);
Set intersection(const Set&, const Set&);


#endif /* SET_H_ */
```

**Set.cpp**
```cpp
#include "Set.h"
#include <iostream>

using std::cout;
using std::endl;

#include <algorithm>
#define INITIAL_SIZE 50
#deine EXPAND_RATE 2

// ------------------ DEFAULT CONSTRUCTOR ------------------
Set::Set() :
  data(new int[INITIAL_SIZE]),
  size(0),
  maxSize(INITIAL_SIZE)
{ }

// ------------------COPY CONSTRUCTOR ------------------
Set::Set(const Set& set) :
  data(new int[set.getSize()]),
  size(set.getSize()),
  maxSize(set.getSize())
{
  for(int i = 0; i < size; ++i) {
    data[i] = set.data[i];
  }
}

// ------------------ DECONSTRUCTOR ------------------
Set::~Set() {
  delete[] data;
}

// ------------------ FUNCTIONS ------------------

// find index of element in set
int Set::find(int number) const {
  // const == won't change my object
  for(int i = 0; i < size; ++i) {
    if (data[i] == number) {
      return i;
    }
  }
  return NUMBER_NOT_FOUND;
}

// check if element in set
bool Set::contains(int number) const {
  return find(number) != NUMBER_NOT_FOUND;
}

// get: size
int Set::getSize() const {
  return size;
}

// add element to set (if not there)
bool Set::add(int number) {
  if (contains(number)) {
    return false;
  }
  if (size >= maxSize) {
    expand();
  }
  data[size++] = number;
  return true;
}

// make set bigger (make bigger data[] array and copy paste old elements)
void Set::expand() {
  int newSize = maxSize * EXPAND_RATE; // lol, maxSize = 0 in c'tor, what?
  int* newData = new int[newSize];
  for (int i = 0; i < size; ++i) {
    newData[i] = data[i];
  }
  delete[] data;
  data = newData;
  maxSize = newSize;
}

// remove element
bool Set::remove(int number) {
  // better implementation would also shrink the array
  int index = find(number);
  if (index == NUMBER_NOT_FOUND) {
    return false;
  }
  data[index] = data[--size];
  return true;
}

// unites elements of 'other' with my set 
Set& Set::uniteWith(const Set& other) {
  for (int i = 0; i < other.getSize(); ++i) {
    this->add(other.data[i]); // better to use public functions but whatevs
  }
  return *this;
}

//  only keep elements shared with 'other'
Set& Set::intersectWith(const Set& other) {
  for (int i = 0; i < this->getSize(); ++i) {
    if (!other.contains(data[i])) {
      this->remove(data[i]);
    }
  }
  return *this;
}

// ------------------ EXTERNAL FUNCTIONS ------------------
// why external?
// We prefer the syntax s3 = union(s1,s2) over s3 = s1.union(s2)
// External functions do not access the private section

Set unionH(const Set& set1, const Set& set2) {
  Set result = set1; // copy( constructor) set1 to result
  return result.uniteWith(set2);
}

Set intersection(const Set& set1, const Set& set2) {
  Set result = set1; // copy( constructor) set1 to result
  return result.intersectWith(set2);
}



```
**main.cpp**
```cpp
int main() {
  
  Set set1, set2;

  
  for (int j = 0; j < 20; j += 2) {
    set1.add(j);
  }
  for (int j = 0; j < 12; j += 3) {
    set2.add(j);
  }
  
  Set unionSet = union(set1,set2);
  Set intersectionSet = intersection(set1,set2);
  
  
  cout << set1.toString() << endl;
  cout << set2.toString() << endl;
  cout << unionSet.toString() << endl;
  cout << intersectionSet.toString() << endl;

  
  return 0;
}

```