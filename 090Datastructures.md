# 🧮 DataStructures

## 📃 List

- Order: Exists
- Duplication: Allows

## ♠️♥️♣️♦️ Set

- Order: Doesn't Exist
- Duplication: Doesn't Allow

## 🗄️ Stack

- Order: Exists
- Duplication: Allows
- Pop: Last Entered
- Push: To End

## 🧍🧍🧍‍️Queue

- Order: Exists
- Duplication: Allows
- Pop: First Entered
- Push: To End

# Standard Library

## Vector

The most widely used container is std::vector.
- Dynamic array
- Has fast random access (uses indeces)
- Pop/Push elements to the END of the vector quickly
- (doing so from the middle of the vector can be much slower)

```cpp
#include <vector>
```
Example:
```cpp
void read_and_print() {
  vector<int> numbers;
  int input;
  while (cin >> input) {
    numbers.push_back(input);
  }
  for (int i = 0; i < numbers.size(); ++i) {
    cout << numbers[i] << " ";
  }
}
```

### Constructing
```cpp
vector<int> v1;
vector<double> v2(5, 3.0); 
vector<double> v3(5); 
vector<double> v4(v2);

vector<string> words = {"Hello", "World"};

int array[] = { 1, 2, 3 };
vector<int> v5(array, array + 3);
vector<int> v6(v2.begin(), v2.end());
```

### Popular Actions

- ```.push_back(<variable>)``` Adds element to then end of the vector
- ```.pop_back()``` Removes element from the end of the vector
- ```.size()``` Returns amount of elements in vector
-  ```.at(<index>)``` Element at index

Iteration:
```cpp
vector<int> v = { 2, 3, 4, 1, 2, 4 }
for (vector<int>::iterator it = v.begin(); it != v.end(); ++it) {
    cout << *it << " ";
  }
}
// OR
for (int num : vec) {
  // ... do something with num
}
```

### Object Requirements
Objects that can be elements of vector need to have implemented:
- Copy Constructor
- =operator

## List

std::list is a collection that implements a two directional node list
- Can quickly add elements anywhere in the array
- Access to random locations is not quick
- Usually better to use vector unless you'll often be adding/removing elements from the middle of the collection

### Popular Actions

- ```.push_back(<variable>)``` Adds element to then end of the vector
- ```.pop_back()``` Removes element from the end of the vector
- ```.push_front(<variable>)``` Adds element to the start of the vector
- ```.pop_front(<variable>)``` Removes element from the start of the vector
- ```.size()``` Returns amount of elements in vector
-  ```.at(<index>)``` Element at index

## Iterators

- begin() returns an iterator to the start of the structure
- end() returns an iterator to the place one after the last element in the structure

### Const Iterator
Can iterate over a structure but can't modify the structure, only read from it.
```cpp
const vector<int> v(10, 3);
vector<int>::const_iterator i = v.begin();
*i = 7; // error! *i is a const int&
```
You can also iterate with a const_iterator over a non const structure (but not the opposite)
```cpp
vector<int> v(10, 3);
vector<int>::const_iterator i = v.begin();
*i = 7; // error! *i is a const int&
```

### Biderectional Iterator
The list iterator is biderectional as it can move forward and back with ++/--.

### Random Access Iterator
The vector iterator is a random access iterator. Allows biderectional capabilities, accessing elements with [] and jumping forward/back with an integer.

