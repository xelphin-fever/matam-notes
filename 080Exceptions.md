# C++
# ❗ Exceptions

Example of using ```catch```/```throw```:
```cpp
void printGradesFile(string filename) {
  ifstream infile(filename);
  if (!infile) {
    // THROW
    throw string("cannot open file");
  }
  int grade;
  while (infile >> grade) {
    cout << grade << endl;
  }
}
```
```cpp
int main() {
  // TRY
  try {
    printGradesFile("grades.txt");
  } catch (string s) { // CATCH
    // Print Error
    cerr << s << endl;
  }
  return 0;
}
```

## Stack Unwinding

When a function throws an error, it releases all local variables (calls their d'tor).
- Don't have to worry about releasing memory.
- Suppose main() calls A calls B calls C and C throws an exception. Then if B doesn't catch it, it gets thrown to A and so on till main(); this is stack unwinding.


## Defining Exceptions

- You can throw an exception of any type
- You have to catch with the appropriate type accordingly


```cpp
class Stack {
	int* data;
	int size;
	int nextIndex;
 public:
	Stack(int size = 100);
	Stack(const Stack& stack);
	~Stack();
	Stack& operator=(const Stack& s);
	void pushint t);
	void pop();
	int top();
	const int top() const;
	int getSize() const;

  // MY EXCEPTIONS
	class Full {};
	class Empty {};
  OutOfRange(int index) : index(index) {}
};

void Stack::push(int& t) {
	if (nextIndex >= size) {
		throw Full();
    // OR
    throw OutOfRange(index); // I also can get index
	}
	data[nextIndex++] = t;
}
 
int Stack::top() {
	if (nextIndex <= 0) {
		throw Empty();
	}
	return data[nextIndex-1];
}
```

```cpp
void f(Stack<int>& s) {
	try {
		s.pop();
		for (int i = 0; i < 10; ++i) {
			s.push(i);
		}
	} catch (Stack<int>::Empty& e) {
		cerr << "No numbers";
	} catch (Stack<int>::Full& e) {
		cerr << "Not enough room";
	} catch (...) {
		cerr << "Oops";
		throw;
	}
}
```

## Throwing Objects

Complicated object that we will throw back:
```cpp
class String::BadIndex {
  public:
  	int index;
    // Constructor for BadIndex
  	BadIndex(int index) : index(index) {}
};
```
Usage:
```cpp
const char& String::operator[](int index) const {
	if (index >= size() || index < 0) {
		throw BadIndex(index);
    }
	return data[index];
}
  
char& String::operator[](int index) {
	if (index >= size() || index < 0) {
		throw BadIndex(index);
    }
	return data[index];
}
```

Us catching it:
```cpp
void f(String& s) {
	try {
		cout << s[50];
	} catch (const  String::BadIndex& e) {
		cerr << "Bad Index: "<< e.index;
  }
}
```
## Inheritance
Exceptions can be caught through their base class (just like function arguments). We can group several exceptions under one base class (This will allow handling all these exceptions at once).

```cpp
class GradesException {
public:
virtual ~GradesException() {}
};
```
```cpp
class NotEnrolled : public GradesException {};
//
class NoSuchStudent : public GradesException {};
```
```cpp
void GradesSystem::printGrade(string student, int course) {
  try {
    cout << "grade is: " << getGrade(student, course);
  } catch (const NotEnrolled&) {
    cerr << studentName << " is not registered";
  } catch (const GradesException&) {
    cerr << "Data not available";
  }
}
```



# Standard Libarary (std) Exceptions

The exception class from std
- **logic_error** represents errors that the function caller could
  have known about and avoided (e.g., index out of bounds)
- **runtime_error** represents errors that occur when the function
  runs, and couldn’t be known in advance (e.g., bad file format)

How it looks like:
```cpp
class exception {
  public:
    exception();
    exception(const exception&);
    exception& operator=(const exception&);
    virtual ~exception();
    virtual const char* what() const;
};
```

## Memory Exception

When ```new``` fails, an *std::bad_alloc* gets thrown
```cpp
int main() {
  try {
    while (true) {
      new int[10000];
    }
  } catch (const std::bad_alloc& e) {
    cerr << e.what() << endl;
  } 
  return 0;
}
```

## Constructors and Operators

```cpp
class Map {
public:
  class City;
  class Road;

  Map();
  ~Map();

private:
  City* cities;
  Road* roads;
  // ...
};
```
If a constructor throws an error, it stops building immediatley and the object isn't created.
```cpp
Map::Map() {
  cities = new City[INIT_CITY_VNUM];
  try {
    roads = new Road[INIT_ROAD_NUM];
  } catch (const bad_alloc&) {
    delete[] cities;
    throw;
  }
  // ...
}
```

> ❗ Never Throw from Destructor!

> ❗ Before deleting/creating/changing memory make sure to do the error catching
> first and only afterwards do those actions

```cpp
char* String::allocate_and_copy(const char* str, int size) {
	return strcpy(new char[size+1], str);
}
String& String::operator=(const String& str) {
	if (this == &str) {
		return *this;
  }
	delete[] data; // BAD!!!
  // What if the below throws an error?
	data = allocate_and_copy(str.data, str.size());
  // Then I would have deleted my data for nothing!
	length = str.length;
	return *this;
}
```

Therefore, you must write it like this:
```cpp
  // ...
	char* temp = allocate_and_copy(str.data, str.size());
  delete[] data;
	data = temp;
 	length = str.length;
	return *this;
```