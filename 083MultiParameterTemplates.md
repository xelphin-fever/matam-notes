# C++
#  Parameters of Templates

## Multi-Parameter

We can create templates that recieve more than one paramter

```cpp
template<class T, class S>
struct Pair {
  // fields are public (convention for simple objects that don't have functionality)
	T first;
	S second;
	Pair(const T& t, const S& s)
		: first(t), second(s) {}
};
```
```cpp
Pair<char, double> p('a', 15.0);
cout << "(" << p.first << "," << p.second << ")";

List<Pair<string, int>> phonebook;
phonebook.add(Pair<string, int>("Dani",8343434));
phonebook.add(Pair<string, int>("Rami",8252525));
```
### Shortcut

Sometimes it can be annoying to write the whole thing ```phonebook.add(Pair<string, int>("Dani",8343434));``` so instead we can do the following:

```cpp
template<class T, class S>
Pair<T, S> makePair(const T& t, const S& s) {
         return Pair<T, S>(t, s);
}
```
then:
```cpp
phonebook.add(makePair(string("Sammi"),8656565)); // Will create a Pair<string, int> and add it to the phonebook
```

## Template with Known Parameters

You can also explicitley write a paramter type in a template

```cpp
template<class T, int N>
class Vector {
	T data[N];
public:
	Vector();
	Vector& operator+=(const Vector& v);
	//...
};
```
Note that operations on these templates can only be done when they have the same template parameters.
```cpp
 void f(Vector<int, 3>& v) {
	Vector<int, 5> v5;
	Vector<int, 3> v3;
	v3 += v; // o.k.
	v5 += v; // error	- 5!=3
}
```
Also [I actually don't really understand why] but the N in the Vector class has to be a small number so as to avoid a stackoverflow.
