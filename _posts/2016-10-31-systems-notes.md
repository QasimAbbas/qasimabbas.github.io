---
layout: post
title: Ultimate Systems Programming Guide
---

# Ultimate Systems Programming Study Guide

* Final Study Material Links
    * [214 Final Review](https://docs.google.com/document/d/1d_AEYR8jUW9ILS8JSHiVsyhh_p7eHAEQg0qgGdAFFGo/edit)
    * [214 Copy of Final Spring 2016](https://docs.google.com/document/d/1fyS46wDSH8mIyp9ADojXjUc-kZyXig1by6K9oK0YATs/edit)
    * [Systems Programming Notes - Paul Jones](http://eden.rutgers.edu/~pmj34/?page=%2FNotes%2FComputer%20Science%2F%2FSystems%20Programming.md)
    * [Systems Programming Projects](https://github.com/iocat/cs214)

## Syntax

### Types

* For primitives there are different types in C with different sizes and uses
* Keep in mind these are all for a 32 bit architecture!!!
  * int
    * Integer 4 bytes long
  * double
    * More precise number with floating point 16 bytes looking
  * float
    * A number with a floating point half the size of a double 8 bytes long
  * char
    * A character that is 1 byte long

```c
//Integer
int i = 0;

//Double
double num1 = 1.0

//Float
float num2

//Character
int c = 'A';


```

### Typecasting
* As it is once a type is declared, it is allocated to a certain amount of bytes in memory.
  * What would we do if we wanted a variable of a different type though?

* Typecasting Allows us to 

### Declaration of Variables and Functions
* Primitives are declared normally
* Functions are still created in a similar way

* These are both placed on the Stack

```c

int i = 0;
char c = 'C';

int main(int argc, char * argv[]){
  char *message = Hello;
  printf(%s, message);

  return;
}

```
### Pointers
* Variables who are addresses to other Variables
 * Helps point to the same variable in memory
 * Helps with tasks such as Dynamic Memory Allocation



#### Creating and Dereferencing Pointers

```c


```

### Arrays
* There are different ways that Arrays are handled in C
* Arrays can be dereferenced in two different ways
  * [] brackts like a regular array
  *  using a pointer dereference

* If you have an Array:

```c
//Access Element in Double Array
s[0][0]

//Dereference Double Pointer
**s

//Deference Pointer of Element of an Array
*s[0]
```
* All do the same thing

### Addresses
* What is contained in &y?



### Union

* Store Different datatypes in the same location in memory
* Can be defined with different members but only one can be used at a time

```c
union money{
    char *currency;
    int dollars;
    double price;
};
```

* Allocates to the biggest size, in this case

```c
union money qasim;
qasim.money = "my money"    
qasim.dollars = 12
qasim.price = 12.46
```

* The only thing allocated is price
* Keep track of the datatypes!
### Structs
* Struct is a user defined data type to hold a collection of data types.
* When structs are initialized, they are stored contigiously in memory.
* All members of the struct are initialized and allocated the struct is initialized.

```c
struct person{
    int eyes;
    int nose;
    int mouth;
};
```
* Using a struct
```c
struct person qasim;
qasim.eyes = 2;
qasim.nose = 1;
qasim.mouth = 1;
```

### Enumerated Types
* Enumerated types (enum) are quite different from struct and unions. An enumerated type is a data type where every possible value is defined as a symbolic constant. Enumerations do not have members. Structures do not define lists of constants. A structure can contain enumerations, but an enumeration cannot contain structures.

```c
enum bool{
    false,
    true
}
```

*    Using the Enum
```c
    bool yes = true;
    if(yes){
        printf("IT WORKED :)");
    }
```
### Function Pointer
* Instead of referring to data values, a function pointer points to executable code within memory.

```c
int my_function(int a, int b)
{
    return a + b;
}
```
* Function to be pointed to

```c
int my_function(int a, int b)
{
    return a + b;
}
int main()
    {
    int (*intpointer)(int, int) = NULL;
    intpointer = &my_function;
    int ans = (*intpointer)(1, 2);
    printf("MY ANSWEEWEWWEWERRR %d", ans);

    return 0;
}

```

## Memory

### Dynamic Memory Allocation - Malloc
* Allocates requested size of bytes and returns a pointer to the first byte of allocated space
* Dyanmically allocates Memory in the Heap of a size that is allocated at runtime
```c
int *num = (int *)malloc(sizeof(int));
//Allocated a pointer of type int with a size of int
```
* When there is not enough memory, malloc fails and returns a null pointer
### Calloc
* Allocates space for an array of elements, initializes all the bytes to zero

```c
type *name = (type *)calloc([amount], [size]);
int *num = (int *)calloc(4, sizeof(int));
```
* When there is not enough memory, calloc fails and returns a null pointer
### Free
* Deallocates the amount of memory allocated dynamically

```c
int *num = (int *num)malloc(sizeof(int));
free(num);
```

### Realloc
* Change the size of previously allocated space(this will free the pointer that you give it while it reallocates the space--careful when using).
* Used for resizing previously allocated space

```c
int main()
{
   char *str;
   /* Initial memory allocation */
   str = (char *) malloc(15);

   /* Reallocating memory */
   str = (char *) realloc(str, 25);
   free(str);

   return(0);
}
```
* When there is not enough memory, realloc fails and returns a null pointer

### Segmentation Fault
* You should never free a pointer that has been freed
* Because then we’d have a dangling pointer which can result in unpredictable behavior. This can lead a lot of issues for example security issues or can cause your program to crash.

```c
char * name = (name *)malloc(sizeof(char));
free(name);
free(name);
GAHHH I DIED
```

### Memory Layout

| MEMORY LAYOUT |
|:-------------:|
|Kernel|
|Stack|
|Memory Map|
|Heap|
|BSS|
|Data|
|Text|

#### Kernel
* OS and Processes

#### Stack
* local variables, passing arguments

#### Heap
* dymnamically allocated variables

#### BSS
* undeclared global variables and what not

#### Data
* declared and initialized variables

#### Text
* instructions after compilation

#### Memory Alignment
* When variables are allocated they have padding
 Ex: Allocating a struct on 32bit architecture
```c
struct penguin{
    char name;
    int fish;
    float calories;
}
```
Allocated 13 bytes
Has 16 bytes
3 bytes added for padding
Order dependant


### Algorithms of Malloc

#### Implicit vs Explicit Lists

##### Implicit List
* Uses lengths to link blocks in memory
* Need to identify whether block is free of allocated
* Uses the length to move to the next free block
* Use size to traverse in memory
* list abstraction

##### Explicit List
* Node to the next free block
* Won't have free bit
* Will have pointer to the next free block
* Will have free blocks for look for sizes wanted

#### Metadata

* Information of the data in a block of memory that is dynamically allocated

#### Fits
*  First Fit
    * First Available block that fits malloc size
*  Best Fit
    * Block that fits best
*  Worst Fit
    * Opposite of Best Fit
*  Next Fit
    * After first space that fits is found, look for next space that fits
    * Saves you from looking at spaces you've already allocated in the beginning, forces you to look at space near the end

## Concurrent Programming

### Signal Handlers
*   Signal handlers let the user program know when an event occurs.
    * Conceptual examples: segmentation violation, message arrival, kill
    * Examples in real life: 
        * SIGABRT (abort)
        * SIGFPE (floating point exception)
        * SIGILL(illegal/invalid instruction)
        * SIGINT (interruption), SIGSEGV (segmentation violation)
        * SIGTERM (termination)
    * Inhibit the programming from procceeding
*   Signals - software interrupts delivered to a process by the operating system
    * Can also be issued by OS based on system or error conditions (i.e. a process is terminated when it receives an interrupt SIGINT signal by pressing ctrl-C)

```c
void (*signal(int, void (*)(int)))(int);

```


* **signal()** is a function that takes in two parameters and returns a pointer to a function. This function being returned takes in one argument, which is the signal handler, and returns nothing
* if signal() fails, the funciton will return SIG_ERR
* **int** in * signal(int, void (*)... is for the signal name
* int in void ( * )( **int** )))... is for a function that accepts an int argument and returns a signal handler
    * If you want to ignore a signal, use SIG_IGN as second argument
    * If you want to use default way of handling a signal, use SIG_DFL as second argument
    * The signals SIGKILL and SIGSTOP cannot be caught or ignored

 ```c
//EXAMPLES OF SIGNAL() USE

signal(SIGINT, SIG_IGN);    //ignores signal SIGNIT

signal(SIGALRM, SIG_DFL);   //defaults SIGALRM

signal(SIGINT, INThandler); /*calls function INThandler
                            as signal handler for SIGINT */

```

### Fork()
* What is forking?
    * fork() makes clones of current processes to create new processes
    * creates new processes by duplicating the state of the exisiting process from which it is copying from (with a few minor differences)
      * process id
      * parent is notified via a signal when the child process finishes but not vice versa
      * the child does not inherit pending signals or timer alarms
    * the child inherits from the parent
        * open filehandles
        * signal handlers
        * current working directory
        * environment variables
    * the process that invokes the fork() is the parent process
    * the new process is called the child process
    * when forking, the child process does not stem from main; it returns from the fork() of the parent process

*What is the fork-exec-wait pattern?
    *call fork -> create child process -> child process starts execution of a new program
    *meanwhile, parent waits (waitpid) to wait for child process to finish

* What is fork bomb?
    * an attempt to create an infinite number of processes
    * this will bring system to a near-standstill as it attempts to allocate CPU time and memory to the processes
    * not necessarily malicious

 ```c
//EXAMPLES OF FORK()

//EXAMPLE ONE - SIMPLEST EXAMPLE

    printf("I'm printed once!\n");
    fork();

    //now there are two processes running
    //that will print out the following line

    printf("You see this line twice!\n");
    
//EXAMPLE TWO - PRINT REPEATED

#include <unistd.h>
#include <stdio.h>
int main(){
    int answer = 84 >> 1;
    printf("Answer: %d, answer");       
    //printf is only executed once, 
    //HOWEVER printed contents have not
    //flushed to standard out (no newline, 
    //no call to fflush, or change in buffering mode)
 
    fork();
    //when fork() is executed, the process memory
    //is also duplicated and the child process start
    //with an nonempty buffer
    return 0;
}


//EXAMPLE THREE - DIFFERENTIATING PARENT AND CHILD

//check return value of fork()
// -1 = failed , 0 = in child process, 
//positive int = in parent process


//child can find parent with ppid(),
//but parent can only id child with
//return value

pid_t id = fork();
if(id == -1) exit (1);  //fork failed
if(id > 0) {
    //original parent created
    //child process with id 'id'
    //use waitpid to wait for child
    
} else {
    //newly created child
}
```

* How does parent wait for child process?
    * waitpid (or wait)

 ```c
pid_t child_id = fork();
if(child_id == -1){perror("fork"); exit(EXIT_FAILURE);}
if(child_id > 0){
    //child process! get exit code
    int status;
    waitpid(child_id, &status, 0);
    
    //code not shown to get exit status
    
    } else {
        //in child
        //start calculation
        exit(123);
    }
}
```

### Children, Orphans, and Zombies

* **Zombine Process** - created when a parent process does not wait on the child process, and the process continues to run even when the user has forgotten it
* **Orphan Process** - child process in which the parent process has finished running and did not wait for the child process
* What would be the effect of too many zombines?
    * Once a process completes, any of its children will be assigned to "init" (pid of 1)
    * Children will getppid() return value of 1
    * Orphans will finish and become zombies
    * init will wait for all children, thus removing zombies

*   How do I prevent zombies?
    * WAIT ON YOUR CHILD



## Networking

### Addresses

* There are millions of machines on the internet.  How do we know which one is ours?
* Hardware Address and IP Address
    * Hardware Address
        *  In a computer all the local parts have an address to help the machine and people identify what the parts are and what they are suppose to do.
        *  Hardware address is always unique to every single machine/
    * IP Address
        *   An IP Address is the Address used to identify your computer on the Internet.
        *   Can be relative to a router
            * (192.168.1.1)

#### IP Addresses
* Internet Protocol (IP)
    * higher-level address for accessing over internet
* We have learned that there is a way to identify the machine on the Internet
* 2 Different types of Addresses, both for same purpose
* Describes how to send packets from one machine to another

* IPV4
    * 32 split octets
    * 2^32 Addresses only
        * We are running out
    * 192.168.1.1
* IPV6
    * 128 bits
    * slow adoption
    * 2^128 addresses
    * 001:cdba:0000:0000:0000:0000:3257:9652

* DNS
    * Domain Name Service
    * match words to IPs
    * GoDaddy/Namecheap
    * http://google.com -> 192.223.232.3:6993

#### Ports

* To send a data to host on interent, need to specify exactly where the datagram is coming in
* unisgned 16 bit number
    * max port is 66535
* only root can listen to < 1024
* 192.138.1.1:8080

### Data Transfer
* Data is transferred from one computer to another through the use of packets
* Datagram
    * Also known as Packets
    * Bundles of Data
    * In IPV4 typically 20 bytes
    * Includes Source and Destination

#### Methods of Transfer
* UDP and TCP
* UDP
    * User Datagram Protocol
    * Unreliable
    * All packets are sent and recieved without discresion on whether they get to desitnation or not
    * Fast way of sending because no need to wait on packets being recieved
    * Not in order
* TCP
    * Creates simulated connection between machines
    * Sends packets and gets recieved in order
        * If packet is not recieved then client would send request and wait for it

#### Server vs Client

#### Basic Method Calls



##### Sockets
* Connection point on two links of a program over a network

```c
int socket(int domain, int type, int protocol);

// On success returns File Descriptor
// On fail -1/errno
```

* domain
    * connection type
        * AF_INET
            * reffers to IP Addresses specifically
* type
    * SOCK_STREAM
        * TCP
        * Provides sequenced, reliable, two-way, connection-based byte streams.  An out-of-band data transmission mechanism may be supported.
    * SOCK_DGRAM
        * UDP
            * Sends Datagrams connectionless, unreliable
                       messages of a fixed maximum length.

* protocol
    * default: 0
    * mapping more than 1 protocol

##### File Descriptor
* File Pointer
    * Gives information on file such as name, size, and memory address
* File Descriptors
    * int that Identifies a file at the Kernel Level
    * represent file and store information about a file
* File Handler
    * Uses File Descriptor and adds methods to it

```c
//File Descriptor Example

int fd = open("test.txt");
```

##### Connect
* connect file descriptor of socket given address specified

```c
int connect(int sockfd, const struct sockaddr *addr, socklen_t addrlen);

```
* sockfd
    * File Descriptor of socket
* addr
    * address of connction
* addrlen
    * length of the address 

##### Bind
* bind address to specific socket

```c
int bind(int sockfd, const struct sockaddr *addr, socklen_t addrlen);

//On success 0
//On fail -1/errno
```

* sockfd
    * File Descriptor of socket
* addr
    * address of connction
* addrlen
    * length of the address 

##### Listen
* marks a socket as a passive socket for connections

```c
int listen(int sockfd, int backlog);


```
* sockfd
    * File Descriptor of socket
* backlog
    * amount of connections want to have in queue

##### Accept
* The accept() system call is used with connection-based socket types (SOCK_STREAM, SOCK_SEQPACKET). It extracts the first connection request on the queue of pending connections for the listening socket, sockfd, creates a new connected socket, and returns a new file descriptor referring to that socket. The newly created socket is not in the listening state. The original socket sockfd is unaffected by this call.

```c

int accept(int sockfd, struct sockaddr *addr, socklen_t *addrlen, int flags);


```

* sockfd
    * File Descriptor of socket
* addr
    * address of connction
* addrlen
    * length of the address


##### GetAddrInfo
* Convert domain to IP Address




##### Files
* Files can be open(), read(), write, using File descriptors

```c
//Open returns fd
int open(const char *path, int oflags);

//Read returns size of file
size_t read(int fildes, void *buf, size_t nbytes);

//Write returns bytes written
size_t write(int fildes, const void *buf, size_t nbytes);



```

##### Block vs Nonblocking

##### Buffer
