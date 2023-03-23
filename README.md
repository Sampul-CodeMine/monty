# 0x19. `C` - `Stacks`, `Queues` - `LIFO`, `FIFO`

## STACKS

A `Stack` in `C` is nothing but a linear data structure that follows the `LIFO` rule **(Last In First Out)**. In a stack, both insertion and deletion take place from just one end, that is, from the top. In order to better understand it, consider the following scenario: 

Imagine you have 5 plates that you have to keep on top of each other of distinct colors: Red, Green, Blue, White, and Orange. You start by placing the red plate on the table. This is the first element of the stack. Then, you place the green plate on top of the red plate. This is the second element of the stack. Similarly, you place the blue plate followed by white and then finally orange. Note that the first plate you inserted into the stack was the red one. Now, you want to remove the red plate. But, before that, you need to remove the rest of the plates that are on top of the red one.

We can implement a stack in C in 2 ways: 
- Statically: Array implementation of stacks allows the static memory allocation of its data elements. It is important to note that in this method, the stack acquires all the features of an array.
- Dynamically: Linked list implementation of stacks follow the dynamic memory allocation of its data elements. It is important to note that in this method, the stack inherits all the characteristics of a linked list in C. 

### Basic Operations performed on `Stacks`

The following are the basic operations served by stacks.
- `push()`: Adds an element to the top of the stack.
- `pop()`: Removes the topmost element from the stack.
- `isEmpty()`: Checks whether the stack is empty.
- `isFull()`: Checks whether the stack is full.
- `top`: Displays the topmost element of the stack.

### Array Implementation of `Stack` in `C`

```c
#include <stdio.h>
#include <stdlib.h>

#define LIMIT 100 /* Specifying the maximum limit of the stack */

/* Global declaration of variables */

int stack[LIMIT]; /* Array implementation of stack */
int top; /* To insert and delete the data elements in the stack */
int i; /* To traverse the loop to while displaying the stack */
int choice; /* To choose either of the 3 stack operations */
void push(void); /* Function used to insert the element into the stack */
void pop(void); /* Function used to delete the element from the stack */
void display(void); /* Function used to display all the elements in the stack according to LIFO rule */

int main(void)
{
	printf("Welcome to DataFlair tutorials!\n\n");
	printf("ARRAY IMPLEMENTATION USING STACKS\n\n");
	top = -1; /* Initializing top to -1 indicates that it is empty  */
	do
	{
		printf("1. Insert\n2. Delete\n3. Display\n4. Exit\n\n");
		printf("Enter your choice:");
		scanf("%d",&choice);
		switch(choice)
		{
		case 1:
			push();
			break;
		case 2:
			pop();
			break;
		case 3:
			display();
			break;
		case 4:
			exit(0);
			break;
		default:
			printf("Sorry, invalid choice!\n");
			break;
		}
	} while(choice!=4);
	return 0;
}

void push(void)
{
	int element;
	if(top == LIMIT- 1)
		printf("Stack underflow\n");
	else
	{
		printf("Enter the element to be inserted:");
		scanf("%d", &element);
		top++;
		stack[top]=element;
	}
}

void pop(void)
{
	int element;
	if(top == -1)
		printf("Stack underflow\n");
	else
	{
		element=stack[top];
		printf("The deleted item is %d\n",stack[top]);
		top--; /* The element below the topmost element is deleted */
	}
}

void display(void)
{
	if(top == -1)
		printf("Stack underflow\n"); // Stack is empty
	else if(top > 0)
	{
		printf("The elements of the stack are:\n");
		for(i = top; i >= 0; i--) // top to bottom traversal
			printf("%d\n",stack[i]);
	}
}
```

### Linked List Implementation of `Stack` in `C`

```c
#include <stdio.h>
#include <stdlib.h>

void push(void); /* Function used to insert the element into the stack */
void pop(void); /* Function used to delete the elememt from the stack */
void display(void); /* Function used to display all the elements in the stack according to LIFO rule */

struct node
{
	int data;
	struct node *next;
};

struct node *temp;

int main(void)
{
	printf("Welcome to DataFlair tutorials!\n\n");
	int choice;
	printf ("LINKED LIST IMPLEMENTATION USING STACKS\n\n");
	do
	{
		printf("1. Insert\n2. Delete\n3. Display\n4. Exit\n\n");
		printf("Enter your choice:");
		scanf("%d",&choice);
		switch(choice)
		{
		case 1:
			push();
			break;
		case 2:
			pop();
			break;
		case 3:
			display();
			break;
		case 4:
			exit(0);
			break;
		default:
			printf("Sorry, invalid choice!\n");
			break;
		}
	} while(choice!=4);
	return 0;
}

void push(void)
{
	int data;
	struct node *pointer = (struct node*)malloc(sizeof(struct node));
	
	if(pointer == NULL)
		printf("Stack overflow");
	else
	{
		printf("Enter the element to be inserted: ");
		scanf("%d",&data);
		if(temp == NULL)
		{
			pointer -> data = data;
			pointer -> next = NULL;
			temp = pointer;
		}
		else
		{
			pointer -> data = data;
			pointer -> next = temp;
			temp = pointer;
		}
	}
}

void pop(void)
{
	int item;
	struct node *pointer;
	
	if (temp == NULL)
		printf("Stack Underflow\n");
	else
	{
		item = temp -> data;
		pointer = temp;
		temp = temp -> next;
		free(pointer);
		printf("The deleted item is %d\n",item);
	}
}

void display(void)
{
	int i;
	struct node *pointer;
	
	pointer = temp;
	if(pointer == NULL)
		printf("Stack underflow\n");
	else
	{
		printf("The elements of the stack are:\n");
		while(pointer!= NULL)
		{
			printf("%d\n",pointer -> data);
			pointer = pointer -> next;
		}
	}
}
```

### Application of `Stack` in `C` 

The principle `LIFO` followed by stacks gives birth to the various applications of stacks. Some of the most popular applications of stacks are:

- Number reversal: A stack helps you reverse a number or a word entered as a sequence of digits or characters respectively.
- Undo operation: Implementation of a stack helps you perform the “undo” operation in text editors or word processors. Here, all the changes done in the text editor are stored in a stack.
- Infix to postfix conversion: Using stacks, you can perform the conversion of an infix expression to a postfix expression.
- Backtracking: Stacks are finding applications in puzzle or maze problem-solving.
- Depth-first search (DFS): Stacks allow you to perform a searching algorithm called the depth-first search.

## QUEUES

A `Queue` In contrast to a `Stack` in `C`, is nothing but a linear data structure that follows the `FIFO` rule **(First In First Out)**. Insertion is done from the back (the rear end) and deletion is done from the front.

In order to better understand the concept of queues in C, we can say that it follows the rule of “First Come First Serve”. Let us consider a simple scenario to help you get a clear picture of queues. Suppose you want to purchase a movie ticket. For that, you need to stand in a queue and wait for your turn, that is, you have to stand at the rear end of the queue. You can’t simply stand in the middle of the queue or occupy the front position.

We can implement a queue in 2 ways:
- Statically: Array implementation of queues allows the static memory allocation of its data elements. It is important to note that in this method, the queue acquires all the features of an array.
- Dynamically: Linked list implementation of queues follow the dynamic memory allocation of its data elements. It is important to note that in this method, the queue inherits all the characteristics of a linked list.

### Basic Operations Associated with `Queue`

A queue being an Abstract Data Structure provides the following operations for manipulation
on the data elements:

- `isEmpty()`: To check if the queue is empty
- `isFull()`: To check whether the queue is full or not
- `dequeue()`: Removes the element from the frontal side of the queue
- `enqueue()`: It inserts elements to the end of the queue
- `Front`: Pointer element responsible for fetching the first element from the queue
- `Rear`: Pointer element responsible for fetching the last element from the queue

### Array Implementation of `Queue` in `C`

```c
#include <stdio.h>
#include <stdlib.h>

#define LIMIT 100 /* Specifying the maximum limit of the queue */

/* Global declaration of variables */

int queue[LIMIT]; /* Array implementation of queue */
int front, rear; /* To insert and delete the data elements in the queue respectively */
int i; /* To traverse the loop to while displaying the stack */
int choice; /* To choose either of the 3 stack operations */
void insert(void); /* Function used to insert the element into the queue */
void delete(void); /* Function used to delete the elememt from the queue */
void display(void); /* Function used to display all the elements in the queue according to FIFO rule */

int main(void)
{
	printf("Welcome to DataFlair tutorials!\n\n");
	printf ("ARRAY IMPLEMENTATION OF QUEUES\n\n");
	front = rear = -1; /* Initialzing front and rear to -1 indicates that it is empty */
	do
	{
		printf("1. Insert\n2. Delete\n3. Display\n4. Exit\n\n");
		printf("Enter your choice:");
		scanf("%d",&choice);
		switch(choice)
		{
		case 1:
			insert();
			break;
		case 2:
			delete();
			break;
		case 3:
			display();
			break;
		case 4:
			exit(0);
			break;
		default:
			printf("Sorry, invalid choice!\n");
			break;
		}
	} while(choice!=4);
	return 0;
}

void insert(void)
{
	int element;
	
	if (rear == LIMIT - 1)
		printf("Queue Overflow\n");
	else
	{
		if (front == - 1)
			front = 0;
		printf("Enter the element to be inserted in the queue: ");
		scanf("%d", &element);
		rear++;
		queue[rear] = element;
	}
}

void delete(void)
{
	if (front == - 1 || front > rear)
		printf("Queue Underflow \n");
	else
	{
		printf("The deleted element in the queue is: %d\n", queue[front]);
		front++;
	}
}
void display(void)
{
	int i;
	if (front == - 1)
		printf("Queue underflow\n");
	else
	{
		printf("The elements of the queue are:\n");
		for (i = front; i <= rear; i++)
			printf("%d\n", queue[i]);
	}
}
```

### Linked-List Implementation of `Queue` in `C`

```c
#include <stdio.h>
#include <stdlib.h>

struct node
{
	int data;
	struct node *link;
};

struct node *front;
struct node *rear;

void insert(void); /* Function used to insert the element into the queue */
void delete(void); /* Function used to delete the elememt from the queue */
void display(void); /* Function used to display all the elements in the queue according to FIFO rule */

int main(void)
{
	int choice;
	
	printf("Welcome to DataFlair tutorials!\n\n");
	printf ("LINKED LIST IMPLEMENTATION OF QUEUES\n\n");
	do
	{
		printf("1. Insert\n2. Delete\n3. Display\n4. Exit\n\n");
		printf("Enter your choice:");
		scanf("%d",&choice);
		switch(choice)
		{
		case 1:
			insert();
			break;
		case 2:
			delete();
			break;
		case 3:
			display();
			break;
		case 4:
			exit(0);
			break;
		default:
			printf("Sorry, invalid choice!\n");
			break;
		}
	} while(choice!=4);
	return 0;
}

void insert(void)
{
	struct node *temp;
	
	temp = (struct node*)malloc(sizeof(struct node));
	printf("Enter the element to be inserted in the queue: ");
	scanf("%d", &temp->data);
	temp->link = NULL;
	if (rear == NULL)
	front = rear = temp;
	else
	{
		rear->link = temp;
		rear = temp;
	}
}

void delete(void)
{
	struct node *temp;
	
	temp = front;
	if (front == NULL)
	{
		printf("Queue underflow\n");
		front = rear = NULL;
	}
	else
	{
		printf("The deleted element from the queue is: %d\n", front->data);
		front = front->link;
		free(temp);
	}
}

void display(void)
{
	struct node *temp;
	
	temp = front;
	int cnt = 0;
	if (front == NULL)
		printf("Queue underflow\n");
	else
	{
		printf("The elements of the stack are:\n");
		while (temp)
		{
			printf("%d\n", temp->data);
			temp = temp->link;
			cnt++;
		}
	}
}
```

_**NOTE**: `Queues` can also be implemented using `Stacks`. Also there is another variant of the `Queue` which is the `Circular Queue`. The role of circular queue comes into play when we wish to avoid the loss of computer memory using arrays. It is based on the
principle that the rear end of the queue becomes equal to its front end._

### Applications of `Queue` in `C` 

The principle `FIFO` followed by queues gives birth to the various applications of queues. Some of the most popular applications of queues are:

- Round robin algorithm: The concept of queues finds a striking application in the round robin algorithm done in MBA.
- CPU Scheduling: In a queue, the data is not processed instantly, but processed according to the `FIFO` rule. Therefore, this feature of queues helps in the sharing of resources among multiple users at the same time.
- Input-Output Buffers: It helps in the transmission of asynchronous data (A condition where the retrieval of multiple data takes place at the user end at different rates) by converting it into synchronous data.
- Disk Scheduling
- Breadth-First Search Algorithm **(BFS)**

## The Project At Hand - `Monty Interpreter`

[Monty](http://montyscoconut.github.io/) Language interpreter made in the C programming language to manage stacks and queues (LIFO and FIFO). The aim is to interpret Monty bytecodes files. It is a language that aims to close the gap between scripting and programming languages.

### General Know-How
- What do LIFO and FIFO mean
- What is a stack, and when to use it
- What is a queue, and when to use it
- What are the common implementations of stacks and queues
- What are the most common use cases of stacks and queues
- What is the proper way to use global variables

### General Requirements
- Allowed editors: vi, vim, emacs
- All your files will be compiled on Ubuntu 20.04 LTS using gcc, using the options -Wall -Werror -Wextra -pedantic -std=c89
- All your files should end with a new line
- A README.md file, at the root of the folder of the project is mandatory
- Your code should use the Betty style. It will be checked using betty-style.pl and betty-doc.pl
- You allowed to use a maximum of one global variable
- No more than 5 functions per file
- You are allowed to use the C standard library
- The prototypes of all your functions should be included in your header file called monty.h
- Don’t forget to push your header file
- All your header files should be include guarded
- You are expected to do the tasks in the order shown in the project

### Compilation
To compile this project, you can use the following command:
`$ gcc -Wall -Werror -Wextra -pedantic -std=gnu89 *.c -o monty`

### Allowable opcodes and what they do

| opcode|functionality|
|---|---|
|push |	add element to the 'top' of stack and 'end' of queue |
|pop |	remove element from 'top' of stack and 'end' of queue |
|pall |	print every member of the structure |
|pint |	prints the member value at the top of stack |
|swap |	swaps the order of the 1st and 2nd elements in stack |
|add |	add top two member values |
|sub |	subtract the top element from the 2nd top element |
|div |	divide the 2nd element by the top element |
|mul |	multiply the top two elements of the stack |
|mod |	the remainder when the 2nd element is divided by the top element |
|comment |	there is the ability to parse comments found in bytecode ->'#' |
|pchar |	print character at the top of the stack |
|pstr |	print the character at the top of the stack |
|rotl |	moves element at the top to the bottom of the stack |
|rotr |	the bottom of the stack becomes the top |
|queue, stack |	toggles the doubly link list implementation style |
|nop	 |opcode should do nothing |



### Exit Status

Exits with status EXIT_FAILURE

### Styling

All files have been written in the Betty Style.

<div></div>

---

> Ehigboria Dukeson O.