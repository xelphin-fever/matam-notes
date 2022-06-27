# Testing Large Software Process :iphone::page_facing_up:

## How

Must test at different levels
- :mountain: High Level:
    - Overall system functionality
- :evergreen_tree: Intermediate Level:
    - High level functionality
    - Interactions between modules
- :rabbit2: Low Level:
    - Modules and classes
    - Basic Functions


## :mountain: High Level
- System testing
    - Tests the overall system in a specific usage scenario
    - Writing automatic tests for this is usually very challenging
    - If it works, gives confidence in the system
    - However, it probably misses a lot of boundary cases
    - Hard to pinpoint the bug when a test fails
    - Slow – this means it will not be run very often
- Acceptance testing
    - Performed by an external entity – typically the client
    - Tests the overall system performance in a real environment

## :evergreen_tree: Intermediate Level
- Integration testing
    - Test the functionality of a large sub-system
    - Test the interactions between several modules
    - Irrelevant or non-implemented modules can be replaced
      with stubs
    - Dependencies can sometimes be replaced (for example, instead of contacting a real server, use a dummy server)

## :rabbit2: Low Level
- Unit testing
    - Test one unit at a time
    - A unit in our code is a module – usually a class
- A unit test is simple
    - Only tests one part of the code
    - When it breaks, the bug is easily tracked
    - Smaller, more simple and therefore faster
    - Can be run after every change to the file
- A unit test covers a small part of the system
    - We will need a lot of these
    - Does not test interactions between modules or overall behavior

## Writing Unit Tests :pencil2:
- Test one module – in our case a single class
- Divide the unit test into several tests
    - A good rule of thumb:
      Write a test for every function in the interface
- In each test:
1. Call the module with some input
   (Make sure to cover the error cases, not just the happy paths)
2. Assert that the returned values are correct

## Example

**set_test.cpp**
```cpp
int main() {
  
  RUN_TEST(testSetConstruct);
  RUN_TEST(testSetCopy);
  RUN_TEST(testSetAssign);
  RUN_TEST(testSetAdd);
  RUN_TEST(testSetRemove);
  RUN_TEST(testSetContains);
  RUN_TEST(testSetGetSize);
  RUN_TEST(testSetUnite);
  RUN_TEST(testSetIntersect);
  RUN_TEST(testSetFilter);
  RUN_TEST(testSetIsEmpty);
  RUN_TEST(testSetOutput);
  RUN_TEST(testSetIterator);
  RUN_TEST(testSetIteratorEmptySet);
  RUN_TEST(testSetIteratorOneElement);
  return 0;
  
}
```
```cpp
static bool testSetCopy() {
  Set<int> empty;
  Set<int> emptyCopy = empty;
  VERIFY_EQUAL_SETS(empty, emptyCopy);
  
  Set<string> set;
  set.add("joey");
  set.add("chandler");
  set.add("monica")
  Set copy = set;
  VERIFY_EQUAL_SETS(set, copy);
  set.add("ross");
  VERIFY_NOT_EQUAL_SETS(set, copy);
  
  return true;
}

static bool testSetGetSize() {
  Set<string> empty;
  Set<string> colors;
  colors.add("orange");
  colors.add("red");
  colors.add("magenta");
  
  VERIFY_TRUE(empty.getSize() == 0);
  VERIFY_TRUE(colors.getSize() == 3);
  
  Set<string> colorsCopy = colors;
  colors.remove("orange");
  VERIFY_TRUE(colors.getSize() == 2);
  VERIFY_TRUE(colorsCopy.getSize() == 3);
  return true;
}

// MORE TESTS...
```

**set.cpp**
```cpp
// FAULT INJECTION
template<class T>
bool Set<T>::add(const T& elem) {
  if (contains(elem)) {
    return false;
  }
  if (size >= maxSize) {
    expand();
  }
  
  // Use special code to simulate a specific error 
#ifdef FORCE_FAILED_COPY
  throw std::bad_alloc();
#endif
  data[size++] = elem;
  return true;
}
```

**set_test_failed_add.cpp**
```cpp
// Produces a compilation error
#ifndef FORCE_FAILED_COPY
  #error "This test requires FORCE_FAILED_COPY to be defined"
#endif

static bool testSetAddCopyError() {
  Set<double> set;
  // VERIFIES that the exception is thrown or else the test fails
  VERIFY_THROWS(set.add(3.14));
  VERIFY_TRUE(set.getSize() == 0);
  return true;
}

int main() {
  RUN_TEST(testSetAddCopyError);
}
```
> gcc –DFORCE_FAILED_COPY set.cpp set_test_failed_add.cpp

## Writing Testable Code :keyboard::heavy_check_mark:

- The real challenge is writing code that can be easily tested
    - Write modules with little or no dependencies
        - Isolate class members with private and protected
        - Do not use modifiable global objects
- Write short functions that perform a single task
- Minimize side-effects of functions
- Reduce code duplication through helper functions and class inheritance
