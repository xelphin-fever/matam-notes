# C
# Macros

Notation ```#<the rest>```.

What macros do is copy/paste (this happens during the preprocessing).

## File Inclusions

```cpp
#include "MyHFile.h"
```
Copy/Pastes the ```MyHFile.h``` content inside of the file.

## Define

```cpp
#define literally_anything :)&&&84834
#define PI 3.1415
```
This will copy/paste ```:)&&&84834``` or ```3.1415``` accordingly inside of the file where it appears (note that if some other file ```include```s this file then it will also copy/paste there).

This is what you wrote:
```cpp
printf("Pi is %f\n", PI);
```
This is what it sees after preprocessing:
```cpp
printf("Pi is %f", 3.1415);
```


## Macro Functions


```cpp
#define MAX(a,b) a>b ? a:b 

#define SQR(x) x*x
#define SQR_SAFER(x) ((x)*(x))
double sqr_safest(double x) {
  return x*x;
}
```
MAX is great because it can support a bunch of types (char/int/enum...). But there are a couple things to keep in mind when using Macro Functions.

This is what you wrote:
```cpp
double res1 = SQR(5); 
double res2 = MAX(7,9);

double res3 = SQR(5+3);
double res4 = SQR_SAFER(5+3);
```

This is what it sees after preprocessing:
```cpp
double res1 = 5*5;
double res2 = 7>9 ? 7:9;

// But beware, it's rather dumb copy/pasting
double res3 = 5+3*5+3; // BAD!
double res4 = (5+3)*(5+3); // Good :)
```

## Common and Correct Usage

```cpp
#define MAX_STR_LEN 20

#define IS_UPPER(c) ((c) >= 'A' && (c) <= 'Z')

#define TO_LOWER(c) (IS_UPPER(c) ? (c)-'A': (c))

#define SWAP(type, a, b) { type t = a; a=b; b=t}
```

## Macro Functions with String Literals

Writing ```#``` inside of a Macro will make the variable a string literal

```cpp
#define PRINT_INT(a) printf("%s = %d", #a, a)
```
This is what you wrote:
```cpp
PRINT_INT(5);
```
This is what it looks like after preprocessing:
```cpp
printf("%s = %d", "5", 5);
```

## Conditional Compilation

```cpp
#define LOW 1
#define MEDIUM 2
#define HIGH 3

# define LOGGING_LEVEL HIGH

#if LOGGING_LEVEL >=MEDIUM
#define LOG_MEDIUM(message) printf(message);
#else
#define LOG_MEDIUM(message) ((void)0)
#endif

#ifdef DEBUG_ON
#define DEBUG_PRINT(MSG) printf("%s", MSG)
#else
#define DEBUG_PRINT(MSG) ((void)0)
#endif
```

This is what you wrote:

```cpp
#if LOGGING_LEVEL > MEDIUM
  printf("Configuration is high \n");
#endif

LOG_MEDIUM("I only get printed IF configuration is HIGH\n");

int arr[4];
#ifdef DEBUG_ON // CAN DEBUG when I want it to
if (arr[0] == NULL) {
  DEBUG_PRINT("BUG: arr[0] is null\n");
}
#endif
```

This is what it looks like after preprocessing:

```cpp
printf("Configuration is high \n");

printf("I only get printed IF configuration is HIGH\n");

((void)0);
```

## Assert Macros (For Debugging)

Note that __LINE\_\_ and __FILE\_\_ are predefined macros.

```cpp
#include <assert.h>

#ifdef NDEBUG // I DONT want to debug
#define assert(x) ((void)0) 
#else // I DO want to debug
void _assert (const char* condition, const char* filename, int line);
// #define assert(e) ((e) ? (void)0 : _assert(#e, __FILE__, __LINE__))
#endif
```

