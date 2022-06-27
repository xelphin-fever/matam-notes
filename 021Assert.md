# C
# Assert

Need to include the ```assert``` library.
```cpp
#include <assert.h>
```

If you don't want to run the ```assert()```s then you can write the following at the start of the code.

```cpp
#define NDEBUG
```

**Note:** You should only use the assert() for debugging.

## Basic Example

```cpp
int getInput() {
	int input;
	printf("Enter a positive number:"); // You need to trust the user to comply
	scanf("%d",&input);

	assert(input > 0); // Instead of trust you do this
  
  // Now when you run your code and come across bugs
  // You can be doubly sure it wasn't because of a non-positive input
	return input;
}
```

