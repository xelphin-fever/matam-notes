# C++
# Assignment Operator

- Automatically created by compiler

- In this case of the ```Complex``` class the ```=``` operator will work well
```cpp
Complex& Complex::operator=(const Complex& c) {
    im = c.im;
    re = c.re;
    return *this;
}
```

- However, it will not work well in all cases:

## Manually Create Assignment Operator

❗ You can't do this:
```cpp
Set& Set::operator=(const Set& s) {
    size = s.size;
    maxSize = s.maxSize;
    data = s.data; // BAD! - Will both point to the same data
    return *this;
}
```
✔️ You need to do this:
```cpp
Set& Set::operator=(const Set& s) {
    // I'm changin my current set to match the argument set 's'
    if (this == &s) {
        return *this; // Avoids bug in case of self assignment
    }
    delete[] data; // delete MY data
    data = new int[s.size];
    size = s.size;
    maxSize = s.size;
    for (int i = 0; i < size; i++) {
        data[i] = s.data[i] // copy 's' data into my data
    }
    return *this;
} 
```



