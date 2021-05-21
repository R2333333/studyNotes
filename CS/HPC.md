# Parallel Performance
## Measurement
1. Speed-up: S<sub>N</sub> = T<sub>0</sub>/T<sub>N</sub>
2. Efficiency: E<sub>N</sub> = S<sub>N</sub>/N
3. Strong Scaling: 

	* Keeps the total task size same, and increase the processes
	* Amdahl's Law: 
	
		* S<sub>N</sub> = 1 / ( s + p<sub>N</sub>)
		* S<sub>Max</sub> = 1 / s = 1 / (1 - p)
	
4. Weak Scaling: 

	* Keeps task per process same, and inscrease the total size of problem
	* Gustafson's Law:

		* S<sub>N</sub> = s + pN

## Loop Schedualing & Load Balancing
* Static: iterations divided into pieces of size chunk and distributed round robin between threads
* Dynamic: iterations divided into pieces of size chunk, when a thread finishes its chunk it is given another
* Guided: dynamic with decreasing chunk size

## Interconnect & Message
* Network Topolygies:

	* Too complete interconnect isn't practical
	* Too simple interconnect will raise latency

* Ideal Transmission Time: t = L + M / B

## Domain Docomposition overhead
* Strong scale a domain decomposition increases the communication to computation ratio
* We can get a super-linear speed-up if data fits into cache

## Parallel Overhead & Amdahl's law
* Can't be estimated, but need to be minimized
* Can be added in Amdahl's law:

	+ Parallel Run Time: T<sub>N</sub> = sT<sub>0</sub> + pT<sub>0</sub> / N + n<sub>p</sub>v
	+ Parallel Speed-up: S<sub>N</sub> = 1 / (s + p / N + n<sub>p</sub>v / T<sub>0</sub>)

## Task parallelism and manager-worker parallelism
* manager-worker: one process send work to other process upon the requests from other processes.
## OpenMP Work Sharing Contructs
* parallel for:

	* parallelize a for loop
* sections:

	* loops in a section are run iteratively
	* all sections run concurrently
* single:

	* only one thread execute this section
## OpenMP tasks
* Similar to manager-worker in OpenMPI
* Use a single struct to generate tasks
* Other thread in the parallel region carry out the tasks
* Use firstprivate to take a prive variable from outside the task construct

# Linear Algebra
## Matrices
* Dense Matrices: Most or all of elements fare non-zero
* Sparse Matrices: Most of the elements are zeros
*  BLAS: Basic Linear Algebra Subprograms
	
	* Arithmetic Intensity: O(1)
		
		1. Level 1: vector-vector
		2. Level 2: matrix-vector

	* Arithmetic Intensity: O(N)
	
		3. Level 3: matrix-matrix
* Compressed Sparse Row Format:

	* Space for storing: 2N<sub>NZ</sub> + N<sub>row</sub> + 1

## Benchmarks
* HPL: measures performance on dense matrices
* HPCG: mearsures performance on sparse matrices
## Accelerator & GPU
* GPU is energy efficient
* Most of the HPC in the Top 500 uses gpu as accelerator
* GPU connects to other pieces via PCI.E, which has large latency
* Pascal GPU architecture:

	1. contains up to 60 SMs
	2. hight bandwidth memmory (720Gb/s)
	3. threads divided into blocks and wraps
	4. threads within the same block are executed by same SM and can access same shared memory
	5. threads in blocks are divided in wraps (32 threads / wrap)

* GPUs don't have branch prediction


