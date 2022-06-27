# C
# Typedefs

## Basic Example

A ```typedef``` is a way to define your own costumized type. It is generally used to make clearer and cleaner code.

```cpp
typedef int Length;
```
```cpp
Length my_length = 4;
printf("My length is %d\n", my_length);
```

### With Enum

```cpp
// You could write:
enum Gender {MALE, FEMALE};
typedef enum Gender Gender;

// OR you could write
typedef enum {MALE, FEMALE} Gender;
```
```cpp
Gender my_gender = FEMALE;
```

### With Array
```cpp
typedef double Real;
typedef Real Point3D[3];
```
```cpp
Point3D p,q;
Real p_x = 4.8;
p[0] = p_x;
```

## Typedef to Self

```cpp
typedef struct node {
	int data;
	struct node* next;
} *Node;
```

```cpp
Node createNode(int d);
void destroyList(Node head);

int main(void) {

  Node node1 = malloc(sizeof(*node1)); // malloc because we don't know the length of NodeList
  Node node2 = malloc(sizeof(*node2));
  node1->data = 1;
  node1->next = node2;
  node2->data = 2;
  node2->next = NULL;
  
  return 0;
}
```
```cpp
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