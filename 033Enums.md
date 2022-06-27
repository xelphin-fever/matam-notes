# C++
# Enums

```cpp
#include <iostream>
using namespace std;
```


```cpp
enum Color {RED, GREEN, BLUE};
```
In C++ we don't need to use typedef
```cpp
Color my_color = GREEN;
```

## Enum Class

```cpp
enum class PowerState {
  Off,
  Hibernate,
  Sleep,
  On
};

enum class FlashMode {
  Off, // also PowerState has this -> Oh uh, name clash?
  On,
  Auto,
  RedEye
};
```
- Encloses its constants inside a scope
- Avoids name clashes
```cpp
PowerState state = PowerState::Off;
FlashMode mode = FlashMode::Off; 
```


## Conversions

### enum -> int
```cpp
int enum_color = GREEN;
```
### int -> enum
```cpp
❕  Color int_color = 2; // ERROR
Color int_color = (Color)2;
```
### enum class -> int
They do not auto-convert to int
```cpp
int x = (int) state;
```
### int -> enum class
```cpp
PowerState newState = (PowerState) 2;
```