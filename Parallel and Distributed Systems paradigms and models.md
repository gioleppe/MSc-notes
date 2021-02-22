## Parallel and Distributed Systems: paradigms and models

---

University of Pisa, Computer Science MSc, AY 20/21.

Lecturer: **Professor Marco Danelutto.

Notes taken by Tommaso Colella.

\newpage

---

### Lecture 1

(Course introduction)

GPUs as accelerators --

---

### Lecture 2

#### Recap

GPU $\rightarrow$ GP-GPUs can be used as accelerators, they can speed up computations, being used as co-processors. They can be used mostly with arithmetic computations, which can be splitted: data parallel computations, where you can split some data into smaller datas. You can perform the same kind of function on all the members of the data structure.

#### FPGAs

GP-GPUs are not the same kind of accelerators, we also have **FPGAs**, that stands for Field Programmable Gate Arrays.  They're accelerators as well, they can talk with the CPU with a kind of I/O bus. The acceleration is much different wrt GPUs. 

FPGAs are like a matrix, with horizontally communication channels, and at each crossing there's a **cell** with a configurable hardware devices which has three configurations:

1. Boolean function (3-7 bit $\to$ 1bit). It's a configurable ROM memory with $2^k$ addresses
2. A bit of memory
3. Routing device

There's a very large number of these cells, $100K$ to $1000K$ for each chip. You can use the configurations to program a device, which replicates the ones you can actually print on silicon.

The catch is that because of this configurability, you have a lower clock speed in the order of the hundreds of MHz. 

What programming tools can you use with FPGAs?

- **RTL**: Register Transfer Languages, such as Verilog and VHDL.
- **High Level Synthesis Languages**: developed in order to address RTL languages' very hard syntax. They're converging towards **OpenCL and SyCL** languages, which are more or less the ones used to program GPUs.

The usual workflow with OpenCL and SyCL languages is something like this:

1. Define some buffers
2. Declare the kind of accesses needed to buffers
3. Declare some kernels
4. Declare a queue to the device (FPGA)
5. Post operations or data transfers to the queues

Functions can be pipelined inside the FPGA, we can achieve a throughput of 1 operation per clock cycle when fully operational, in the sense that with a single clock cycle we can obtain the result of the computation for a single element put in the queue.

This is quite different from the behaviour of GPUs, that will perform everything in a single compute unit.

FPGAs are also integrated inside CPUs by some vendors (such as Huawei), in order to make it easy to run neural networks on such CPUs.

In modern FPGAs we have **Cells + DSP + M**: each column in the matrix can be either cells, small memories (used to easily store intermediate results), or DSPs (that can be used to perform $+$ and $*$ operations). This "modern" design eases out the splitting of the computation in more phases in such a way that makes the clock cycle smaller.

Some traditional "cores" have been added to the FPGAs, so these FPGAs became a **SOC**: System On a Chip. As a reference, a FPGA could have an ARM processor at its center (let's say 4 cores), that could be used to talk to the main CPU in a much more efficient way than using an I/O bus.

To recap:

- Multicore Systems: Parallelism degree in the order of 10s to 100s of cores (general purpose cores)

- Accelerators: 
  - GPUs $\to$ 1000s of cores (only for data parallel code)
  - FPGA $\to$ larger number of small devices (can run small functions at high speed)

Of course, to exploit all this degree of parallelism we need to write parallel programs (or use libraries that use parallelism inside our "single threaded" code).

**TOP500**: Twice per year people runs some benchmarks on the biggest computers in the world in order to rank them on the TOP500 webpage. These supercomputers have a lot of cores and and a massive amout of memory. Of course all these supercomputers use a lot of power.

**Green500**: The list of the most power efficient supercomputers. 

**OpenMP**: standard used to parallelize a small amount of (simple) patterns with the Data Parallel approach.