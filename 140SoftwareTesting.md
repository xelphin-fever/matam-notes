# Software Testing

## Why Test Software
- Need a way to be sure our program is giving us the **correct result**
- Need a way to make sure a **programmers’ changes did not degrade the performance** of the full system
- The **end client** needs to be able to **correct bugs** on his own
- Fact: Software is becoming increasingly complex (Testing methods must be able to handle very large projects)
- Investment in testing has dramatically increased over the years
- The **code has to be tested all the time** (Saves time when mistakes occur)

## Testing Categories

- Black Box Testing v.s White Box Testing (When the two are mixed it's called gray box testing)
- Static Testing v.s Dynamic Testing

## Black Box Testing :black_large_square:
**Behavioural Testing**
- Test input-output relationships
- Advantages:
    - This is what the product is about
    - Independent of implementation
    - Easier to decide what to check
- Disadvantages:
    - Identifying erroneous output may be hard
    - Difficult to choose the right inputs to test
        - Most likely inputs?
        - Most problematic inputs?
    - Hard to test a wide spectrum of system functionality

### Example
We’ll create a simple black box test for a sorting function:

**sort.h**
```cpp
void sort(int array[], int size, int (*compare)(int, int));
```
```cpp
void printArray(int array[], int size) {
  for (int i = 0; i < size; ++i) {
    printf("%d, ", array[i]);
  }
}
```
```cpp
int compare(int a, int b) {
  return a - b;
}
```
**sort_test.cpp**
```cpp
#define TEST_SIZE 100
void testSort() {
  int array[TEST_SIZE];
  cout << "Enter " << TEST_SIZE << " integers:";
  for (int i = 0; i < TEST_SIZE; ++i) {
    cin >> array[i];
  }
  sort(array, TEST_SIZE, compare);
  printArray(array, TEST_SIZE);
}
```

## White Box Testing :white_large_square:
**Operational Testing**
- Test how input becomes output
    - Test the code itself
    - Also called “glass box” testing
- Advantages:
    - Easier to detect weaknesses of the program
    - The only way to check all execution paths
      and ensure good code coverage
- Disadvantages:
    - Implementation dependent: more work to maintain
    - The product might have weaknesses which are hard to notice from within the code

### Example
White box test code may (but does not have to) appear withinthe code itself:

**sort.cpp**
```cpp
void sort(int array[], int size, int (*compare)(int, int)) {
  if (array == nullptr) return;
  assert(size >= 0);
  
  int num_swapped;
  do {
    num_swapped = 0;
    for (int i = 0; i < size-1; ++i) {
      if (compare(array[i], array[i+1]) > 0) {
        swap(array+i, array+i+1);
        num_swapped++;
      }
    }
#ifdef DEBUG_ON
    cout << "\nSwapped " << num_swapped << " numbers\n";
    printArray(array, size);
#endif
  } while (num_swapped > 0);
}
```

## Static v.s Dynamic Testing
- Static testing (:white_medium_square:):
    - Code reviews
        - Time-consuming, but very effective
    - Using code analysis tools
        - Will look for suspicious code without running it
          (uninitialized objects, unused values, unreachable code, …)
        - Limited capabilities, but constantly improving
- Dynamic testing (:white_medium_square::black_medium_square:):
    - Preprocessor-controlled code (:white_medium_square:)
        - Typically used to print or verify the status of internal objects
    - Writing test drivers (:white_medium_square::black_medium_square:)
        - Code for running the program and checking its behavior

