# C++
# Template Class

## Example: Set.h

> :exclamation: Note that there is no Set.cpp!

### Set.h
```cpp
#include <iostream>

template <class T>
class Set {
  public:
    Set();
    // ------------------ THE BIG THREE ------------------
    Set(const Set&);
    ~Set();
    Set& operator=(const Set&);
    // ------------------ SET FUNCTIONS ------------------
    bool add(const T& element);
    bool remove(const T& element);
    bool contains(const T& element) const;
    int getSize() const;
    Set& uniteWith(const Set&);
    Set& intersectWith(const Set&);
    // ------------------ ITERATOR ------------------
    class Iterator; 
    // Allows range -> for (int num : some_set)
    Iterator begin() const;
    Iterator end() const; 
  
  private:
    T* data;
    int size;
    int maxSize;
    int find(const T& element) const;
    void expand();
    static const int EXPAND_RATE = 2;
    static const int INITIAL_SIZE = 10;
    static const int ELEMENT_NOT_FOUND = -1;
};
```


```cpp

// Outside the class the <> decleration is needed
template<class T>
Set<T> unite(const Set<T>&, const Set<T>&);

template<class T>
Set<T> intersect(const Set<T>&, const Set<T>&);

template<class T>
std::ostream& operator<<(std::ostream& os, const Set<T>& set);

// SET ITERATOR CLASS
template<class T>
class Set<T>::Iterator {

  const Set<T>* set;
  int index;
  Iterator(const Set<T>* set, int index);
  friend class Set<T>;

  public:
    const T& operator*() const;
    const T* operator->() const;
    Iterator& operator++();
    Iterator operator++(int);
    bool operator==(const Iterator& iterator) const;
    bool operator!=(const Iterator& iterator) const;
    Iterator(const Iterator&) = default;
    Iterator& operator=(const Iterator&) = default;
};

// DEFAULT CONSTRUCTOR - has to have Set<T>
template<class T>
Set<T>::Set() :
  data(new T[INITIAL_SIZE]),
  size(0),
  maxSize(INITIAL_SIZE)
{}


// ------------------ THE BIG THREE ------------------


// DESTRUCTOR - has to have Set<T>
template<class T>
Set<T>::~Set() 
{
  delete[] data;
}

// COPY CONSTRUCTOR - has to have Set<T>
template<class T>
Set<T>::Set(const Set<T>& set) :
      data(new T[set.getSize()]),
      size(set.getSize()),
      maxSize(set.getSize())
{
  for(int i = 0; i < size; i++) {
    // must use assignment and not just memcpy
    data[i] = set.data[i];
    // must define operator "=()"!
  }
}

// =() OPERATOR - has to have Set<T>
template<class T>
Set<T>& Set<T>::operator=(const Set<T>& set) 
{
  if (this == &set) { // check if set is the same as me
    return *this;
  }
  delete[] data; // I know I'm not deleting myself
  data = new T[set.size];
  size = set.size;
  maxSize = set.size;
  for (int i = 0; i < size; ++i) {
    data[i] = set.data[i];
  }
  return *this; // ! dereferences pointer -> sends reference
  // y=(x=5); <- this is why you need to return *this
}


// ------------------ SET FUNCTIONS ------------------

// find() -> return index of element in set
template<class T>
int Set<T>::find(const T& elem) const 
{
  for(int i = 0; i < size; i++) {
    if (data[i] == elem) { // uses "==" operator
      return i;
    }
  }
  return ELEMENT_NOT_FOUND;
}

// contains() -> return if element in set
template<class T>
bool Set<T>::contains(const T& elem) const 
{
  return find(elem) != ELEMENT_NOT_FOUND;
}

// getSize() -> return size of set (till filled)
template<class T>
int Set<T>::getSize() const 
{
  return size;
}

// expand() -> make set maxSize bigger
template<class T>
void Set<T>::expand() 
{
  int newSize = maxSize * EXPAND_RATE;
  T* newData = new T[newSize];
  for (int i = 0; i < size; ++i) {
    newData[i] = data[i];
  }
  delete[] data;
  data = newData;
  maxSize = newSize;
}

// add() -> add element to set
template<class T>
bool Set<T>::add(const T& elem) 
{
  if (contains(elem)) {
    return false;
  }
  if (size >= maxSize) {
    expand();
  }
  data[size++] = elem;
  return true;
}

// remove() -> remove element from set
template<class T>
bool Set<T>::remove(const T& elem) 
{
  int index = find(elem);
  if (index == ELEMENT_NOT_FOUND) {
    return false;
  }
  data[index] = data[--size];
  return true;
}

// uniteWith() -> add all elements from other set to set
template<class T>
Set<T>& Set<T>::uniteWith(const Set<T>& other) 
{
  for (int i = 0; i < other.getSize(); ++i) {
    this->add(other.data[i]);
  }
  return *this;
}

// intersectWith() -> keep only elements that are also in other set
template<class T>
Set<T>& Set<T>::intersectWith(const Set<T>& other) 
{
  for (int i = 0; i < this->getSize(); ++i) {
    if (!other.contains(data[i])) {
      this->remove(data[i]);
    }
  }
  return *this;
}

// "<<" OPERATOR 
template<class T>
std::ostream& operator<<(std::ostream& os,const Set<T>& set) 
{
  os << "{";
  bool first = true;
  // when using a class that is defined within a template class we need to use "typename"
  // this is because without knowing T the compiler cannot know for sure if A<T>::B is a type or something else 
  for (typename Set<T>::Iterator it = set.begin();
    it != set.end(); ++it) {
    if (!first) {
      os << ",";
    }
    first = false;
    os << " " << (*it);
  }
  os << " }";
  return os;
}


// ------------------ ITERATOR ------------------
// Set s;
// Set::Iterator iterator = s.begin();

// BEGIN() -> send 

template<class T>
typename Set<T>::Iterator Set<T>::begin() const 
{
  return Iterator(this, 0);
}

// END()

template<class T>
typename Set<T>::Iterator Set<T>::end() const 
{
  return Iterator(this, size);
} 


// ------------------ ITERATOR IMPLEMENTATION ------------------

// CONSTRUCTOR
template<class T>
Set<T>::Iterator::Iterator(const Set<T>* set, int index) :
                  set(set), index(index)
{
  // my private:
    // set<T>* set
    // int index
}

// *iterator
template<class T>
const T& Set<T>::Iterator::operator*() const 
{
  assert(index >= 0 && index < set->getSize());
  return set->data[index]; 
}

// double x = iterator->x;  
// (returns referance to the specific set->data[x])
template<class T>
const T* Set<T>::Iterator::operator->() const 
{
  assert(index >= 0 && index < set->getSize());
  return &(set->data[index]);
} 

// ++iterator
template<class T>
typename Set<T>::Iterator& Set<T>::Iterator::operator++() 
{
  ++index;
  return *this;
}

// iterator++
template<class T>
typename Set<T>::Iterator Set<T>::Iterator::operator++(int) 
{
  Iterator result = *this;
  ++*this;
  return result;
} 

// iterator == iterator2
template<class T>
bool Set<T>::Iterator::operator==(const Iterator& i) const 
{
  assert(set == i.set); // need to belong to the same set
  return index == i.index;
} 

// iterator != iterator2
template<class T>
bool Set<T>::Iterator::operator!=(const Iterator& i) const {
  return !(*this == i);
}
```
- See ```054Iterators.md``` for Iterator implementation 
  - Although, in this case, everything is in the ```.h``` 


### main.cpp
```cpp
int main() {
  Set<int> set1;
  Set<int> set2;
  
  for (int j = 0; j < 20; j += 2) {
    set1.add(j);
  }
  
  for (int num : set1) { // can use ":" because Set<int> has begin() and end()
    set2.add(2*num);
  }
  
  cout << set1 << endl;
  cout << set2 << endl;
  cout << unite(set1, set2) << endl;
  cout << intersect(set1, set2) << endl;
  
  return 0;
}
```

## T must have the following implemented


- default c'tor ```T::T()```
- operator ```=()```
- operator ```==()```
- d'tor ```T::~T()```

### Conditional Template Compilation
- The compiler will only compile the template functions that are actually used by the user code
- A template parameter T must only satisfy the requirements of the functions that are compiled
- Thus, T might not need to satisfy all the template class requirements, if some of its functions are not used


- **Example**: what if we want to use Set with a type that does not have an ```operator<<()```

```cpp
template<class T>
std::ostream& operator<<(std::ostream& os, const Set<T>& set) {
  os << "{";
  bool first = true;
  for (const T& elem : set) {
    if (!first) { os << ","; }
    first = false;
    os << " " << (*it); // this line
  }
  os << " }";
  return os;
}
```

- To compile this line requires T to have an ```operator<<```.
- But even if T does not have this operator
- We can still create and use a Set\<T\>, we'll just not be able to use ```operator<<```.

