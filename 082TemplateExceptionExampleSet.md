# C++
# Template with Exceptions
## Example: Set

### Set.h
```cpp
template <class T>
class Stack {
	T* data;
	int maxSize;
	int nextIndex;
 
 public:
  // ------------------ CONSTRUCTOR ------------------
	explicit Stack(int maxSize = 100);
  // ------------------ THE BIG THREE ------------------
	Stack(const Stack& s);
	~Stack();
	Stack& operator=(const Stack&);
 // ------------------ FUNCTIONS ------------------
	void push(const T& t);
	void pop();
	T& top();
	const T& top() const;
	int getSize() const;
  // ------------------ EXCEPTION CLASSES ------------------
	class Full {};
	class Empty {};
	class InvalidSize {};
  // ------------------ OSTREAM ------------------
  // Because << is an external function we need to make it friend to give it access to our private
  // We have to declare with teample and not with T because it's taken
  template <class S>
	friend ostream& operator<<(ostream&, const Stack<S>&); 

};
```

```cpp

// ------------------ CONSTRUCTOR ------------------
template <class T>
Stack<T>::Stack(int size) :
   data(new T[size]),
   maxSize(size),
   nextIndex(0)
{
   if (size <= 0 ){
     delete[] data;
     throw InvalidSize();
   }
}

// ------------------ THE BIG THREE ------------------

// ASSUME: T has no-argument constructor
template <class T>
Stack<T>::Stack(const Stack<T>& s) :
   data(new T[s.maxSize]), // if bad_alloc is sent then the object isn't constructed
   maxSize(s.maxSize),
   nextIndex(s.nextIndex)
{
  try {
    for (int i = 0; i < nextIndex; ++i) {
     data[i] = s.data[i];
	  }
  } catch (…) {
    delete[] data;
    throw;
	}
}

// ASSUME: T has no-argument constructor
        // T has =operator
template <class T>
Stack<T>::Stack(const Stack<T>& s) :
   data(new T[s.maxSize]), maxSize(s.maxSize), nextIndex(s.nextIndex) {
   try {
     for (int i = 0; i < nextIndex; ++i) {
       data[i] = s.data[i];
	   }
   } catch (…) {
     delete[] data;
     throw;
	 }
}

// ASSUME: T has no-argument constructor
        // T has =operator
template <class T>
Stack<T>& Stack<T>::operator=(const Stack<T>& s) {
	if (this == &s) {
		return *this;
	}
	T* tempData = new T[s.maxSize];
	try {
  	maxSize = s.maxSize;
  	nextIndex = s.nextIndex;
  	for (int i = 0; i < nextIndex; ++i) {
  		data[i] = s.data[i];
  	}
	} catch (…) {
    delete[] tempData;
    throw;
	 }
	delete[] data;
	data = tempData;
	return *this;
}

template <class T>
Stack<T>::~Stack() {
	delete[] data;
}

// ------------------ FUNCTIONS ------------------

// ASSUME: T has =operator
template <class T>
void Stack<T>::push(const T& t) {
	if (nextIndex >= size) {
		  throw Full();
	}
	data[nextIndex++] = t;
}

template <class T>
void Stack<T>::pop() {
	if (nextIndex <= 0) {
		  throw Empty();
	}
	nextIndex--;
}

template <class T>
T& Stack<T>::top() {
	if (nextIndex <= 0) {
		  throw Empty();
  }
	return data[nextIndex - 1];
}

template <class T>
const T& Stack<T>::top() const {
	if (nextIndex <= 0) {
		     throw Empty();
	}
	return data[nextIndex - 1];
}

template <class T>
int Stack<T>::getSize() const {
	return nextIndex;
}

// ------------------ OSTREAM ------------------
template <class S>
ostream& operator<<(ostream& os, const Stack<S>& s) {
           for (int i = 0; i < nextIndex; ++i) {
       		os << data[i] << endl;
			   }
	return os;
}
```