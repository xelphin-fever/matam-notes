# Automatic Software Testing 	:repeat::page_facing_up:

**How can we test our code?**
- **Manually**: run the program or the test code and look for bugs
    - Simple to implement
    - Takes a lot of time
    - Easier to make mistakes
    - Things will have to be checked repeatedly
- **Automatically**: Write testing code that will automatically verify the correctness of the code
    - Requires writing more code
    - Once written, can be run many times

**Conclusion**: We prefer to invest in automatic testing

- If good automatic tests are available, we can know that the code is correct with the touch of a button
    - With some probability, tests can always miss some things
- Allows effective regression testing – making sure things don’t break after a change
- Manual testing still has to be done
    - But we can minimize the time spent on it

## Configuration

Modern development environments can be **configured to periodically** (or whenever a change occurs) **do automatically** :
- A full build of the project to make sure it compiles
- A re-run of all (or part of) the tests to make sure no regressions have occurred
- A generation of a detailedtest report

## Example (Automatic Testing of Sort)

We‘ll write tests that automatically determine whether they succeeded or failed
- In case of failure, we will supply the reason

```cpp
#define ARRAY_SIZE(array) (sizeof((array)) / sizeof((array)[0]))
```
**sort_test.cpp**
```cpp
bool testSort() {
  
  int array[] = { 3, 4, 2, 1, 5 };

  // Expected Result
  int sorted[] = { 1, 2, 3, 4, 5 };
  
  // Call Sorting Function
  sort(array, ARRAY_SIZE(array), compare);

  // CHECK
  // CHECK - Success
  if (equalArrays(array, ARRAY_SIZE(array),
                  sorted, ARRAY_SIZE(sorted))) {
    return true;
  }
  // CHECK - Fail
  else {
    cout << "Test failed:" << endl;
    printArrayDiff(array, ARRAY_SIZE(array),
    sorted, ARRAY_SIZE(sorted));
    return false;
  }
}
```
```cpp
// CHECKS That the arrays are equal (returns true || false)
static bool equalArrays(int array1[], int size1,
  int array2[], int size2) {
  if (size1 != size2) {
    return false;
  }
  for (int i = 0; i < size1; ++i) {
    if (array1[i] != array2[i]) {
      return false;
    }
  }
  return true;
}
```
```cpp
// PRINTS Difference between arrays
static void printArrayDiff(int result[], int size1, int expected[], int size2) {
  cout << "expected: ";
  printArray(expected, size2);
  cout << " but received: ";
  printArray(result, size1);
}
```

We can use a few macros to help us with the testing code:
**test_utilities.cpp**
```cpp
#define ARRAY_SIZE(array) (sizeof((array)) / sizeof((array)[0]))
#define RUN_TEST(test) \
do { \
  cout << "Running " << #test << "... "); \
  if (test()) { \
    cout << "[OK]"; \
  } \
  cout << endl; \
} while(0)
```

**sort_test.cpp**
```cpp
int main() {
  // RUN TEST (Macro from test_utilities.cpp)
  RUN_TEST(testSort); // Macro used test from sort_test.cpp
  return 0;
}
```

### Note

- We should test boundary cases:
    - What happens if the array size is 0, 1 or negative?
    - What happens if a number appears in the array more than once?
- We should try different values for the function arguments
    - Maybe the code doesn't even use our compare function? (Verify this by using a different comparison function!)

### sort_test.cpp

```cpp
#include <iostream>
#include "test_utilities.h"
#include "sort.h"

// --------------------------------- ARRAY FUNCTIONS ---------------------------------

static bool equalArrays(int array1[], int size1, int array2[], int size2) {
  if (size1 != size2) {
    return false;
  }
  for (int i = 0; i < size1; ++i) {
    if (array1[i] != array2[i]) {
      return false;
    }
  }
  return true;
}

static void printArray(int array[], int size) {
  for (int i = 0; i < size; ++i) {
    cout << array[i] << ", ";
  }
}

static void printArrayDiff(int result[], int size1,
  int expected[], int size2) {
  cout << "expected: ";
  printArray(expected, size2);
  cout << " but received: ";
  printArray(result, size1);
}

// --------------------------------- ELEMENT FUNCTIONS ---------------------------------

static int compare(int a, int b) {
  return a - b;
}

static int compareReverse(int a, int b) {
  return b - a;
}

// FULL CHECK - Equivalent Arrays
#define VERIFY_EQUAL_ARRAYS(result, expected) \
  do { \
    if (!equalArrays(result, ARRAY_SIZE(result), \
                    expected, ARRAY_SIZE(expected))) { \
      cout << "Test failed at " << __FILE__ << " : " << __LINE__ << endl; \
      printArrayDiff(result, ARRAY_SIZE(result), \
                    expected, ARRAY_SIZE(expected)); \
      return false; \
  } while (0)

// --------------------------------- TESTS ---------------------------------

static bool testSortEmpty() {
  sort(nullptr, 0, compare);
  sort(nullptr, 1, nullptr);
  sort(nullptr, -1, compare);
  
  int a[] = { 3, 1, 2 }, b[] = { 3, 1, 2 };
  sort(a, 0, compare); // should not modify the array
  VERIFY_EQUAL_ARRAYS(a, b);
  return true;
}

static bool testSort() {
  int array[] = { 3, 4, 2, 1, 5 };
  int sorted[] = { 1, 2, 3, 4, 5 };
  
  sort(array, ARRAY_SIZE(array), compare);
  VERIFY_EQUAL_ARRAYS(array, sorted);
  return true;
}

static bool testSortWithDuplicates() {
  int array[] = { 3, 4, 3, 3, 4 };
  int sorted[] = { 3, 3, 3, 4, 4 };
  
  sort(array, ARRAY_SIZE(array), compare);
  VERIFY_EQUAL_ARRAYS(array, sorted);
  return true;
}

static bool testSortReverse() {
  int array[] = { 3, 4, 2, 1, 5 };
  int sorted[] = { 5, 4, 3, 2, 1 };
  
  sort(array, ARRAY_SIZE(array), compareReverse);
  VERIFY_EQUAL_ARRAYS(array, sorted);
  return true;
}

// --------------------------------- MAIN ---------------------------------

int main() {
  RUN_TEST(testSortEmpty);
  RUN_TEST(testSort);
  RUN_TEST(testSortInverse);
  RUN_TEST(testSortWithDuplications);
  
  return 0;
}
```