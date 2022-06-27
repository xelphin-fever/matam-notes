# C++
# [] Overloading

```cpp
class Array {

  public:
    explicit Array(int n);
    Array(const Array&);
    ~Array();
    Array& operator=(const Array&);
    int size() const;
    // ------------------ INDEXING OPERATOR ------------------
    int& operator[](int index); 
    const int& operator[](int index) const;

  private:
    int* data;
    int size;
};

// The Indexing Operator for regular objects
int& Array::operator[](int index) {
  assert(index >= 0 && index < size);
  return data[index];
}

// The Indexing Operator for const objects
const int& Array::operator[](int index) const {
  assert(index >= 0 && index < size);
  return data[index];
}

// External Function
Array& doubleIt(Array& a) {
  for (int i = 0; i < a.size(); i++) {
  a[i] = 2 * a[i];
  }
  return a;
}
```