# C
# Structs

## Basic Example

```cpp
struct complex {
  double re;
  double im;
};
typedef struct complex Complex;

// OR

typedef struct complex {
  double re;
  double im;
} Complex;
```

```cpp
// (doesn't use the typedef)
struct complex my_complex;

my_complex.re = 4;
my_complex.im = 2;

// (as typedef)

Complex my_complex_2;
my_complex_2.re = 2;
my_complex_2.im = 3;

Complex my_complex_3 = {6,7};
// not very safe because i can mess up the input


// Using a Struct Creator Function

Complex my_new_complex = complexCreate(2,3);

printf("complex z= %.1f + %.1fi\n",my_new_complex.re, my_new_complex.im);
```
```cpp
Complex complexCreate(double real, double imaginary)
{
  Complex number;
  number.re = real;
  number.im = imaginary;

  return number;

  // You can't get complexCreate(Complex num) and then do num.re = 3;
  // Because it won't change it outside of the function
}
```
You can't do ```complexCreate(my_complex)``` and then do ```num.re = 3; ```because it won't change it outside of the function.

## Complicated Example

```cpp
// -- STUDENT --

typedef double Grade;
typedef Grade GradesJournal[2];

typedef struct Address {
  char* street_address; // street and number
  char* city;
  unsigned int zip;
} Address;

struct student {
  int age;
  unsigned int id;
  Gender gen;
  char * name;
  Address address;
  GradesJournal matam;
  GradesJournal modernit;
  GradesJournal physics;
  GradesJournal combi;
  GradesJournal cyber;
  GradesJournal infi2;
};
```

## Simple Datastructure Example

```cpp
// -- NODELIST --

typedef struct node {
	int data;
	struct node* next; // has a pointer to its own type
} *Node; // Node is a pointer

Node createNode(int d) {
	Node ptr = malloc(sizeof(*ptr));
	if(!ptr) {
		return NULL;
	}
	ptr->data = d;
	ptr->next = NULL;
	return ptr;
}

void destroyList(Node head) {
	while(head) {
		Node toDelete = head; // Node is a pointer
		head = head->next; // head = head.next
		free(toDelete); // erase toDelete
	}
}
```