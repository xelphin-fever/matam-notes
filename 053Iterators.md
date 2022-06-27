# C++
# Iterators

## Usage

- Iterators allow range-based for loops.
- Allow various ways to iterate over elements in object.
- Costumizable iteration.

**main.cpp**
```cpp
int main() {
  Set set;
  for (int j = 0; j < 20; j += 2) {
    set.add(j);
  }
  int sum = 0;
  // ------------------ RANGE-BASED FOR LOOPS ------------------
  int sum = 0;
  for (int value : set) {
    sum += value;
  }
  // Range-based for loops work for any class with begin()
  // and end() methods that return a valid iterator


  // from Set.cpp
  Set::Iterator it1 = s.begin();
  it2 = it1++;
  it2 = ++it1;
}
```

## Implementation

**Set.h**
```cpp
class Set {
  public:
    // ...
    class Iterator; // declare a class Set::Iterator
    Iterator begin() const;
    Iterator end() const;

  private:
    int* data;
    int size;
    int maxSize;
    // ...
};
```
```cpp
class Set::Iterator {
  // Set has access to the private methods here
  const Set* set; // the set this iterator points to
  int index; // current index in the set
  // The constructor is private so that no one except Set can create a Set::Iterator
  Iterator(const Set* set, int index);
  friend class Set; // allow Set to call the constructor

  public:
    const int& operator*() const;
    Iterator& operator++(); // prefix (++it)
    Iterator operator++(int); // postfix (it++)
    bool operator==(const Iterator& it) const;
    bool operator!=(const Iterator& it) const;
    Iterator(const Iterator&) = default;
    Iterator& operator=(const Iterator&) = default;
};
```

**Set.cpp**
```cpp
// ITERATOR CONSTRUCTOR
Set::Iterator::Iterator(const Set* set, int index) :
  set(set),
  index(index)
{ }

// 
const int& Set::Iterator::operator*() const {
  assert(index >= 0 && index < set->getSize());
  return set->data[index];
  // Set::Iterator is inside the Set class, so it has access to the private section of set
}

Set::Iterator& Set::Iterator::operator++() {
  ++index;
  return *this;
}

Set::Iterator Set::Iterator::operator++(int) {
  Iterator result = *this;
  ++*this;
  return result;
}

bool Set::Iterator::operator==(const Iterator& i) const {
  assert(set == i.set); // comparing iterators of two different sets is a bug
  return index == i.index;
}

bool Set::Iterator::operator!=(const Iterator& i) const {
  return !(*this == i);
}
```

## Usage

```cpp
// ------------------ ITERATION ------------------
// USING OPERATOR OVERLOADING

void setSum(const Set& s) {
  int sum = 0;
  for (Set::Iterator it = s.begin(); it != s.end(); ++it) {
    // operator !=() -> to compare two iterators
    // prefix operator ++ -> implement it and make it so that it pushes 'it' further
    sum += *it;
    // operator *() -> returns the object currently pointed it
  }
  cout << "sum of set is " << sum << endl;
}


void func(const Set& s) {
  Set::Iterator it1 = s.begin();
  if (it1 == s.end()) {
    // operator ==() -> comparing iterators
    return;
  }
  cout << "first = " << *it1 << endl;
  it1++; // prefix operator ++() -> advancing the iterator
  Set::Iterator it2 = it1; // copy constructor and  operator =() -> advancing the iterator
  cout << "second = " << *it2 << endl;
  it1--; // post prefix operator -() -> moving the iterator backwards
  // iterators that support both back and forth are called bidirectional
  cout << "first again = " << *it1 << endl;
  cout << "second again = " << *it2 << endl;
}
```

