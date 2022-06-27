# C++
# Function Objects

An object of a class which overloads ```operator()``` is called a
**Function Object** or a **Functor**

- ```operator()``` can be overloaded for any number of parameters
  - In the below case, 1

```cpp
class DividesBy {

    int n;

    public:
        DividesBy(int n) : n(n) {}
        bool operator()(int number) const 
        {
            return number % n == 0;
        }
};
```

- With ordinary functions, we may need to create a new function for every parameter value
  - For example, DividesBy2(x), DividesBy3(x), ... 
- With function objects, we can simply pass the parameters to the object’s constructor 	:grin:

```cpp
int main() {
  
  DividesBy isEven(2); // c'tor call

  // operator ()
  cout << isEven(9) << endl;
  cout << isEven(8) << endl;
  
  DividesBy isTriple(3);
  
  cout << isTriple(9) << endl;
  cout << isTriple(8) << endl;
  
  return 0;
}
```

## Using Templates
Using templates, we can replace pointers to functions with
function objects.


```cpp
template <class T>
class Set {
  public:
    // ...
    template<class Condition> // yes, we defined a template inside a template
    Set filter(Condition myCondition) const;
    // ...
};

// Set filter(Condition myCondition) const:
template<class T>
template<class Condition>
Set<T> Set<T>::filter(Condition myCondition) const {
  Set<T> result;
    for (const T& elem : *this) {
      if (myCondition(elem)) {
        result.add(*it);
      }
  }
  return result;
}
```

```cpp
void test(const Set<int>& s) {
  DividesBy dividesByTwo(2);
  cout << s.filter(dividesByTwo) << endl;
}
```