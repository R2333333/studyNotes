
Cp4.	
-------------------------------------------------------		
# Processes(abstract):
(virtualizing the cpu, makes illusion for each process that they own the entire CPU)
	
	Time Sharing:
		Allow processes to share the same resource one while by one while	
	Space Sharing:
		Divide resouce in to parts for sharing purpose
		
	DataStructures:
	
Cp5.
-------------------------------------------------------
# ProcessAPI:
	
	System Calls:
    	<unistd.h>:
        	int execl(const char* path, const char* arg, const char* arg,.......)
        	int execv(const char *path, char *const argv[])
        	int execle(const char *path, const char *arg,..., char * const envp[])
        	int execvpe(const char *file, char *const argv[],char *const envp[])
        	fork()
        	wait()

    	<fcntl.h>:
        	open(const char* path, int Oflag, ...)
	
	CREATE: turn programs into processes, by loading codes into memory and address, 
		allocate memory for stack and heap, initializations like setting up file discriptors for std I/O.
		
		Lazily: load only when needed
			Paging, Swapping.
			
		Eagerly: load all before running
		
	
	DESTROY, WAIT, MISCELLANCE CONTROL 
	
	STATUS: Running, Ready, Blocked, Initial, Final(Zombie state: process finished but not cleaned up)
	
	
	Schedualer
	
Cp6.
-------------------------------------------------------
# Limited Direct Execution: Makes processes run efficiently and safely
	
	Direct Execution:
		Runs processes directly. Processes may have access to all files and memories
	User Mode:
		The mode processes run in
	Kernel Mode:
		The mode the OS runs in
	Trap:
		Processes use trap to swith control to the OS and get into the kernel mode
	Trap Table: 
		Used to store all syscall handler; initialized at booting system
	Return From Trap:
		Switch control back to process and get into user mode
	Switching Between Process:
		Cooperative Way:
			OS wait for syscalls from process
		Non-cooperative Way:
			OS sets up a timer when system boot, and will interrupt process by the time
		Schedualer:
			To decide wheather to switch to another process or keep running current process after the interruption

CP7.
-------------------------------------------------------
# CPU Schedualing:

	Schedualling Matric: used to measure something
  
	Turnaroud Time: Complete Time - Start Time
	
	Scheduling Matrices: There are two common matrices for scheduling, performance and fireness.(Preventing some process from running
		to increase performance may reduce fireness)

	FIFO: First in first out
		hase disadvantage when long task comes before short test, the average turnaroud time will be
		  much longer than the turnaroud time for just dealing the short task

		FIFO is optimal solution with the assumption that all jobs arrives at the sime time, but in reality
		  the jobs doesn't arrive at same time

	SJF: Shortest jobs first
		Not to run the jobs to completion, and when new jobs come, compute the running time of the all 
		  remaining jobs, and then run the job wit shortest time to complete.
          
      STCF: Shortest time-to-completion first
          For SJF, when a time-consuming job is running and then comes a short job, it cannot switch
          to the shorter job, which means the average turnaroud time will rise. In STCF, it can puse the 
          longer job and switch to the shorter one.
          
	A New Matric: Response Time

		Response Time: The time from when a job come to its first run

		Problems For SJF: not good for time sharing and responsitive(eg. need to wait 10 second for the terminal
			to response when executed a process)

	Round Robin: To do each jobs in the queen for a little while and swith between them
		improves response time of each jobs, but increased the turnaround time

	Incorporating with I/O: While one job is blocked waiting for I/O device, other jobs could be schedualed


Cp8.
---
# Muti-Level Feedback Queue

      In the SJF and STCF, we assume that the length/completion-time of the job is known, which is
      unrealistic in practice. The MLFQ relexes this assumption by using mutiple queues and approximating
      the length of the jobs.
      
      The Basic Rule and Changing Priority: (Attempt #1)
        The are several priority queues for the jobs to be running. The system only execute jobs in the queue that has highest priority. Every new arriving job will get highest priority and inserted to the highest-order queue. 
		The priority of a job gets reduced if the job runs over a time slice, and the job will be moved to the lowwer order queue. 
		If a job relinquishes the CUP or occurs an I/O request be for the end of current time slice, it will stay in the same queue.
        
        Problems: 
            Processes with I/O request at each end of time slices could control the CPU forever(gaming the scheduler).
            Processes in the lowest priority-queue have no change to be run(starvation) if any process existing in the first queue, 
			even that process have alot of I/O in the future.
            
        Atempt #2 and #3:
            To solve the starvation, we boost up all processes to the first queue after a period, 
			so that all processes have equal chances to run(increased fairness).
        
            To avoid any process gaming the scheduler, we coming up with better time-counting. 
			We keep tracking the total time a process used, no matter it relinquished the CUP or not.
        

Cp9.
---
# Scheduling: Propotional Share

        Lottery Scheduling:
            Gaving each process a number of tickets and coresponding numbers for those tickets.
            Generating a random number and choosing the process that has the coresponding ticket to run.
            
        Stide Scheduling:
            Each process has a stride and a pass(both a number) 
            Running a process by the length of its stride until it reaches other processes' pass;
            
        Completely Fair Scheduler:
            The length of time slice is not fixed.
            Using virtual run time to track and decide the process to be run.
            Preority can be set using a table and a constant called "sched_latency".
            Time slice is calculated by a fumular raleted to the weight.
            
        Red-Black Tree is used to store the process tree.
        Jobs awake from sleep will be assigned to the shortest vruntime in the system.

Cp10.
---
# Muti-processor Scheduling:


Cp13.
-------------------------------------------------------
# Address Space:
	
	Early Systems: 
		OS is a set of routains starting from address 0 in physical memmory
	
		Process is a running program sat in physical memmory that uses the rest of the memmory,
			starting from the end of the address space 

	Multiprogramming and Time Sharing:
		
		Address Space(abstraction): Contains all of the memory state of the running program
		  * all memory location showed to programmers are virtual

		    Code: 
			at top of the memory, as it won't grow 
		    Heap:
			sit after code, grows downward
		    Stack:
			sit at the bottom, grows upward
		    Virtualizing Memory:
			the OS maps virturl address into physical location

		Goal of Memory Virtualization:
		    Transperancy:
			to make software doesn't realize the memory virtualization
		    Efficiency:
			make processes run efficently both in time and space
		    Protection:
			protect processes from other processes and the OS itself, to make sure the process
			  doesn't effect or be effected by other processes
			  
CP14. 
-------------------------------------------------------
# Memory API

        malloc, calloc, realloc, free;
        
        tools: Purify, Valgrind
        



Cp15.
-------------------------------------------------------
# Mechanism: Address Translation

	Translate virtual address to physical address, and this process is transparent to all running processes.

	Use two pointers that point to base and bound.

	Virtual memmory starts and runs betweent base and limit.

	Start and bound could be changed, and need to be changed with kernal mode.

	The OS need to handle exception such as out of boundary, in order to keep user process running safely.

CP16.
---
# Segmentation

	
	
Cp18.
-------------------------------------------------------
# Paging: Introduction

	Two ways to solve space-management problems: 
		Varibale-sized pieces: Segmentation
		Fixed-Sized: Pages
		
	Page Table: To store address traslation for each page
	
	Vitual Page Number; Offset; Physical Frame Number;
	
	Where Pages store: somewhere in memory
	
	What's in Page Table:
	
		Valid bit: Indicates whether a translation is valid
		
		Protection bit: Indicates whether a page can be read or written
		
		Dirty bit: Indicates whether a page has been modified since brought to memory
		
		Reference bit: Indicates whether a page has been accessed
		
	Problems with paging:
	
		May be too slow: 
			It take one more memory access to find the table
		
		May cause memory waste: 
			The page tables may take up huge space in memory that should be used to store data


Cp39.
-------------------------------------------------------
# Files and Directories:
### Files: a linear array of bytes
	
		*each file has a low level name, usually a number
		
		Inode Number: low level name of a file
		
		File discriptor is an index, pointing to an array.
		
### Directory: 
	contains a list of pairs
		
	*also has low level name
	
### Open File Table:
	tracks files the fd points to, current offset, and details like readability, writeability
	
### Persistent Storage(hard disk drive)
	
### File System Interface:
#### Creatation:
			open("fileName", options, permission) with O_CREAT flag. (older way: creat())
#### Reading and Writing:
	read(fd,buffer,bufferSize): returns buffer size
	write(fd,buffer,bufferSize): returns buffer size
	usually be called directly in highly optimized files, or printf() will be called instead
			
### Reading and Writing but not Sequencially: to read or write from a specific position by offsetting the starting point
  		
		Offset the memory:
			off_t lseek(int fildes, off_t offset, int whence);
				fildes: file descriptor
				offset: offset bytes
				whence: flags imply how to offset		

### Shared File Entries: fork() and dup()
		
		forked process will have file discriptor shared with its parent and dup will creat a file discriptor pointing
			to the same file.

### Writing Immediately with fsync(): the write() call will not write immediately, instead it will keep content to be writen
					  for a while. If sysmtem crashes before the content been written to file, the data will
					  be lost.
#### fsync(int fd): forcing the system to store all dirty data immediately to a persistent file pointed by the fd.
		
### Renaming Files: 
	eg. when using "mv foo bar", rename("foo", "bar") will be called
		
#### rename(char *old, char *new) : rename old file to new file. This rename is an atomic operation, which means
			it will either rename the file succeessfully or failed with original file left, but no middle case 
			will ever happen.
	
### Getting Information About Files: stat() or fstat() syscall could be used to see the matadata
	
#### metadata: 
	information about the file the system is storing
		
#### inode: 
	the structure that each system keeps matadata in
		
### Removing Files: 
	when using rm in command, unlink() syscall will be called
	
		unlink();
		
### Creating Directories: 
	directory can not be written directly due to the file system
		
#### mkdir(): 
	the syscall used to create directory. An empty directory has two entities: . and ..
		
### Deleting Directories: 
	rmdir() can only detele empty directories, it will fail when tring to delete a nonempty directory
	
### Hard Link:
	a human readable name linking to the inode data stracture; not allowed for directory
		
#### unlink() removes the readable links, and when the link count goes to zero, the file file system can truely delete the file and its matadata
		
### Symbolic Link: 
	stores the path and file name of target file as its data, and its size depends on the path and name
			length of the target data
	
### Permission Bits and Control List;
	
### Making and Mounting File System:
#### mkfs : 
	makes a file system
#### mount :
	mount a file system to current file tree
		
Cp40.
-------------------------------------------------------
# File System Implementation (using vsfs(Very Simple File System) as example)

	Two Ways To Think A File System:
		
		Data Structure: How the data is structured on the disc
		
		Access Method: How does the file system maps the calls onto the structure
		
	The Overall Organizition:
		
		Inode: Structure used to store a file's metadata
		
		Inode Table: An array of on-disk inodes
		
		Data Region: A region of a file system used to store user data
		
		Bitmap: A structure that indicates if the corresponding object/block is free(0) or in-use(1) 
			data bitmap: used for data region 
			inode bitmap: used for inode region
		
		Super Block: A block that contains the information about the file system 
			     (like the how many inodes and data blocks are in the file system)
	
	File Organization: The Inode
		
		Inode: the short for index node
			including: file type, size, number of blocks, protection information, time information
	
		The Multi-Level Index: 
			Inodes need to point to the blocks. In case the block is too larger that needs
			too many pointers, which many excess the limits of the pointers. Using the pointer of an inode
			points to another block that contains mutiple pointers is called multi-level index, and the pointers
			are call indirect pointers.
	
	Directory Organization：A directory is a list of pairs(entry names, inode numbers).
		
		Record Length: total bytes of name pluse left over space(since every delinck will left an empty space)
		
	Free Space Management: Keeps tracking free space (by bitmap in the vsfs, or a free list in some OS)
	
	Access Paths: ("/foo/bar" for example)
		
		Reading From DisK:
			open("/foo/bar", O_RDONLY):
				1. Read root inode
				2. Traverse pointers inside the inode to find entry for foo (foo's inode number found this step)
				3. Traverse directory data of foo to find bar (bar's inode number found)
				4. Read bar's inode into memory
				5. Final permission check, allocate a file discriptor, return fd to user
				
			read():
				1. Consulting inode to find the first block to read (unlees used lseek)
				2. Update inode (atime, mtime...)
				3. Update open file table (offset)
				
		Writing To Disk:
			
			Writing without CREATE and file already opened:
				1. Read Bitmap;
				2. Write Bitmap;
				3. Read inode;
				4. Write inode;
				5. Write content;
				
			Create a file for write:
				1. Read root inode;
				2. Read root data;
				3. Read foo inode;
				4. Read foo data;
				5. Read inode bitmap;
				6. Write inode bitmap;
				7. Write foo data;
				8. Read bar inode;
				9. Write bar inode;
				10. Write foo inode;
			
	Caching an Buffering:
		
		Static Partitioning:
			Store some often used blocks in memory while boosting (may take up 10% of the memory)
		
		Dynamic Partitioning:
			Store the blocks after first usage(saves each finding or opening)
			
		Buffering:
			Store the write content in a buffer, and stores the buffer to persistent disk latter 
			(saves time by reducing write times). By schedual the operations, may skip some unnecessary steps.
			
Cp41.
-------------------------------------------------------			
# Locality And Fast File System
	The Problem: Poor Performance
	
		Old Unix File Systems
			
			Has three part, Super Block, Inodes, and Data Block
			
			Store data at next avilibal blocks
				The data may get spreaded into random block 
				(eg. amoung data a, b, c, d, remove small data b and d, then place large file e,
				 it becomes a, e(partial), c, e(partial));
	
	FFS: Disk Awareness Is The Solution(Fast File System)
		Has same API(open(), read(), write(), close()), but different implementation
		
	Oganizing Structure: The Cylinder Group
		The FFS divides the Disk into a Number of Cylinder Groups, and copies super blockes into each groups
		If one super block crupts, it can still mount the device using other replica
		
		Cyclinder: Tracks on different surface with same radius from the center of the disk
		
		Track: A curcular path on a disk surface
		
		----------------------------------------------
		|S|ib db|	Data			     |
		----------------------------------------------
		
	Policies: How to Allocate Directories and Files
		Keeps related directory and files close and irrelated far away.
		
		For Directory: Find groups with high number of free inodes and lownumber of directory allocated
		
		For Files:	
			1. Place in same groups with their inodes
			2. Place in same groups with their directory
		
		For example: the directory /, a, b, files /a/c, /a/d, /a/e, /b/f
		FFS:
		group 	inodes		data
		  0	 /		/---------
		  1	 acde		aabbccddee
		  2	 bf		bffff-----
		  ...
		  
		 Regular:
		 groups	 inodes		data
		   0	  /		/----------
		   1	  a		aa---------
		   2	  b		bb---------
		   3	  c		cc---------
		   4	  d		dd---------
		   5	  e		ee---------
		   6	  f		ffff-------
		   ...
		   
	File Locality:
		How Far away two files are. (eg. for /a/b, /a/c, /a/b/d, /a/c/e, b and c have difference 1, d and e have 2)
		
	The Large-File Exception:
		If put a Large File completely in one cylinder group, it may takes up all or most of the space in that group,
			since there will be no space for other files under the same path, which increases the locality of the
			file system and may break the structure. So FFS put a large file under few different groups, and this 
			leads to longer seeking time. Increase bolck size can reduce the seeking time but increase wasted space.
			
	Other Things About the FFS:
		
		Subblock: 
			In oder to reduce the waste when small files occupies the block that has larger size than the file,
			FFS uses subblock with size of 512b instead of 4Kb. With the file size growing, it allocates more
			subblocks to store the file, until the file grows to 4Kb, after which the file will be copied into
			a 4Kb block.
			
		Writting Buffer:
			In order to avoid the expensive cost of copying the files, the FFS use buffer to store data to be written.
			
		Parameterization:
			Since the disk spans, if data blocks were placed on continous chunck of the disk, when the system sets up
			the I/O and ready for reading next block, the disk could pass ahead the place. So the data was placed uncontinously
			with the exact distance for system to build up the next I/O. This process is called parameterization.
			
		Track Buffer:
			Stores the entire track's data in the cahe, so the system no longer need to wait the disk's rotation to get the data.
			data.
			
		Allowing Long File Names By Using Sym-Link.
		   
		  
		  
		  
	
		
		
		
	
		
		
