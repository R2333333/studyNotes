<b>By __[Roy](https://github.com/r2333333)__</b>
from [Prof. Somayaji](https://homeostasis.scs.carleton.ca/wiki/index.php/Operating_Systems_(Fall_2019))'s notes

![R2333333](https://avatars2.githubusercontent.com/u/37459130?s=400&u=2e50a618e5e22e6d8b5a5009a66b5c5e483ef123&v=4)

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
# [Memory Management](/OS(from:%20Operation%20Systems:%20Three%20Easy%20Pices).md#address-space)

To get memory access:
  1. get virtual address
  2. mep address
  3. read memory from physical address

To access faster:
  * caches mapping

Since the memory is expensive, to save memory, we use the LRU(least recently used):
<br>`Throw something never get used out`
### [Page Table](/OS(from:%20Operation%20Systems:%20Three%20Easy%20Pices).md#paging-introduction)
* a structure that maps virtual to physical memory
* are stored in frames

Lecture 9
---
# Object File, Executable File, Dynamically Linked Library
Registers:
<dl>
  <dt>%rbp</dt>
    <dd>base pointer, points to the beginning of a function.<br>Can be used to store local variable. 
      <br>When funtions finished, the stack will copy the base pointer to stack pointer</dd>
  <dt>%rsp</dt>
    <dd>stack pointer, points to the current posisiton of the stack.
      <br>When entering a function, the rsp will be store in the rbp</dd>
  <dt>signal</dt>
    <dd> When the signal deliverd to a process, it will save current runing instruction to the stack.
      <br>Then change the instruction pointer's value to the signal handler location.</dd> 
</dl>

Lecture 10
---
# File Copy
<dl>
  <dt>Read & Write:</dt>
    <dd>read data to buffer and write the buffer to dest(by loops)</dd>
  <dt>mmap</dt>
    <dd>map a file or device to memory
      <br>(will not create space for mapped items, not to use lseek to offset the pointer if want to copy something)</dd>
</dl>
To copy a file using mmap: 

    1. map both file to memory
    2. use lseek to make space for the dest_file
    3. let the dest_file equal to the origin file
    4. (munmap)

Lecture 11
---
# 

