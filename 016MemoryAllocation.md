# C
# Dynamic Memory Allocation

```cpp
void* malloc(size_t num_bytes);
void* calloc(size_t num_elem, size_t elem_size); // zeroes allocated bytes
void* realloc(void* old_ptr, size_t new_size);
void free(void* ptr);
```

## Usage 

```cpp
typedef struct {
  double re, im;
} Complex;

const int initial_len = 10;
const int new_len = 20;
Complex* vec1 = malloc(initial_len * sizeof(Complex));

if (vec1 == NULL) {
  fprintf(stderr, "cannot allocate\n");
  exit(1);
}


Complex* vec2 = realloc(vec1, new_len * sizeof(Complex));
if (vec2 == NULL) {
  fprintf(stderr, "cannot allocate\n");
  exit(1); // note the code duplication here
  // use an inline function or macro to prevent this
}

// vec1 now points “nowhere” – do not free it
vec1 = NULL;
free(vec2); // return memory to heap – prevent memory leak
```

## Notice: For Strings
A string is saved in the following way:
```cpp
char* my_string = "oranges";
```
```['o','r','a','n','g','e','s','\0']```

Therefore, when allocating memory it is important to keep an extra slot for '\0'.

```cpp
char* str = "This is a string";
char* copy = malloc(sizeof(char)*(strlen(str)+1)); // notice the: +1
free(copy);
```