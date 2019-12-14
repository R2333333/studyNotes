Lecture 1  
---
# What is an operating system?
  Code that turns the computer into what you want to program on
 # Two key task (Three in the book)
  * resource allocation
  * abstraction
  * (concurrency)
  # Key Abstractions
  * files & directories (__persistance__)
  * GUI elements
  * network sockets
  * processes & threads (__virtualization & concurrency__)
  
  `The OS is the boss process, since it gets to the hardware first, and the hardware is the enforcer` 

Lecture 2
---
# The Shell
  An interface (a thin layer) between the user and OS(the kernel)

Lecture 3
---
# The Fuction Calls and System Calls
The Function Calls:
*  are stored on the stack 
* when load (to the register) will jump to a location 
* will be poped when done 

System Calls:
* the process use syscall to get the kernel perform some function calls

Lecture 4
---
# Files, Syscalls, I/O, Directory Access
What nomally can be done to a file:
* open (add the file descriptor to the [open file table](/OS(from:%20Operation%20Systems:%20Three%20Easy%20Pices).md#open-file-table), for performance reason to store some info and check permission of that file)
* read 
* write
* close 

Lecture 5
---
# Signal, Memory and Background Process
Signals:
* Can interupt a process at any time.
* The flag of restart will restart the syscall that was interupted by the signal(if we don't restart, the read() will retrun as failed when it was interupted)


Memory:
* can be allocated:
<br>`Statically(at compile time)` 
<br>`Dynamically(on stack or in the heap)`

* command line argument resides at the top, stack resides below it; code resides at the bottom, heap resides above it

* allocating memory uncontinuously on the disk may cause fragmentation (between them)
<br>`Solutions:`<br> `using pointers pointing to pointers (handler)`<br>`allocating with same size`([pages](/OS(from:%20Operation%20Systems:%20Three%20Easy%20Pices).md#paging-introduction))

Lecture 8
---
# Memory Management


