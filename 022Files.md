# C
# Files

## File Operations

MODES: r: read, w: write, a: append

## Commands

```cpp
// OPEN FILE
FILE* fopen (const char* filename, const char* mode);

// CLOSE FILE
int fclose (FILE* my_file);

//  my_file needs to be open for printf/scanf to work

// PRINTF - prints my_text into my_file
int fprintf(FILE* my_file, const char* my_text);

// SCANF
int fscanf(FILE* my_file, const char* my_text);

// FGETS
// put first [size] text from [my_file] into [str] -> return str
char* fgets (char* str, int size, FILE* my_file);

// FPUTS
// put [str] inside [my_file]
int fputs (const char* str, FILE* my_file);

// PUTS
int puts (const char* str);

// GETS
char* gets (char* buffer);
```

## Basic Examples

FPRINTF
```cpp
// FPRINTF
FILE* my_file = fopen("hello.txt", "w");
fprintf(my_file, "Hello world!\n"); // write "Hello world!\n" into my_file
fclose(my_file);
```

FGETS
```cpp
#define BUFFER_SIZE 10
```
```cpp
// FGETS
// Reads a line from my_file
char buffer[BUFFER_SIZE] = "";
fgets(buffer, BUFFER_SIZE, my_file);
printf("Line is: %s",buffer);
```