## Parallel and Distributed Systems: paradigms and models

---

University of Pisa, Computer Science MSc, AY 20/21.

Lecturer: **Professor Marco Danelutto**.

Notes taken by Tommaso Colella.

\newpage

---

### Lecture 1 - Setting up the Scenario: Evolution from single to multi core and GPU accelerators

(Course introduction)

GPUs as accelerators --

---

### Lecture 2 - Scenario: FPGA as accelerators, TOP500 and GREEN500

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

---

### Lecture 3 - Sample Parallel Computations

**Sequential**: 

- $A \to B \to C$

- $| - | - | - |$ (time = $T_A + T_B + T_C$)

**Parallel**: 

- $A$
- $B$
- $|-|$ (time = $max(T_A, T_B,...)$)

We're interested into moving from sequential computations to parallel ones, and to achieve some kind of speedup in doing this. Of course we need some workers to compute the single tasks.

**Speedup** = $\frac{T_{seq}}{T_{par}} = \frac{T_A + T_B + T_C}{max(T_A, T_B, T_C)}$

in our case  $speedup = \frac{3T_A}{T_A} = 3$, assuming the three operations take the same amount of time (more or less) and assuming to employ three workers.

#### Some Examples 

- **Translate a book** (eng $\to$ ita)
  - We have m pages
  - $T_P$ time to translate 1 page

A single person (sequential worker), may spend a total time $T_{seq} = m*T_P$  translating the book by herself.

 Let's now assume to make the same job together:

- $760$ pages
- $76$ students = n
- $\frac{760pp}{76}$ 

What I can hope is that $T_{par}(76)\simeq \frac{m}{n} * tp$, that is $speedup(n) \simeq \frac{m*T_p}{m/n*T_P} \simeq n$

At the beginning, I have to pay a splitting time, which is proportional to the number of workers/students taking up the job. We also have to count for the merginng time at the end, which is needed in order to collect the job done so the formula becomes:

 $T_{par} = T_{split} \times n + \frac{m}{n}T_p + T_{merge} \times n$

$T_{split}$ and $T_{merge}$ are only needed because we want to make the computation parallel, we don't have such overhead if we're using a simple sequential computation.

So speedup becomes: 

$Speedup(n) = \frac{m*T_p}{n(T_{split} + T_{merge}) + \frac{m}{n}T_p}$

If we work in a regime where $m \gg n$, the time in splitting and merging can be omitted, and the formula comes close to the linear speedup that we saw earlier, but if we take $T_{split}$ and $T_{merge}$ into account, we will **always** achieve a worse result than the ideal speedup of n. 

We could never achieve a speedup that is superlinear, if $\frac{T_{seq}}{T_{par}} > n$ we would find out that the sequential time would be smaller than the parallel one, but it is clearly a contradiction, so, normally, this is impossible.

If I increase too much the number of students/workers, the time in splitting the job would increase. The overhead becomes more and more important, and at a certain point the speedup function will actually begin to decrease.

Going back to the book translation example, we could have different kind of pages:

- pages with a small amount of pictures, where $T_p = \frac12h$
- pages with a great amount of pictures, where $T_p = \frac14h$

If the pages which take longer to translate are clustered, some student could get a lot of those, and take much more time than another student that only gets pages with great amount of pictures. There's some kind on inefficiency taking place, which could be solved if workers who already finished translating their pages were able to ask more work proactively to the workers struggling to finish the job. Another approach would be to give out pages in smaller batches, this would make each task smaller and easier/faster to complete, but would also increase the overhead involved with assigining the tasks. As with everything, there's a tradeoff to consider.

**Embarassingly parallel computation**: once a worker gets a task, the task can go on without being synchronized with the other workers at all. 

**Data parallel computation**: there's a task which I can split in parts, once I have the set of parts, each item in the set can be processed in order to get a set of partial results which I can then combine to form the global result.

Task $\to$ Parts set $\to$ Results set $\to$ Global result

There are data parallel computations that are not embarassingly parallel. For example summing the rows in a matrix.

Key point: counting, counting means computing sums, and "+" is an associative and commutative operator

Another possibility is to split a computation in various steps (let's say 3) to be carried out by a number of workers each specializing in the single step (let's say 3, again). This forms a kind of pipeline that lets us output one element for time unit, when fully operational. In this case $T_{par} = m*max(T_i) + \sum{T_i} - max(T_i) = (m-1)max(T_f, T_g, T_h) + (T_f + T_g + T_h)$

This case that we just mentioned is called **Stream Parallel Computation**

Translating a book $\to$ **MAP parallel computation** 

Counting devices $\to$ **REDUCE parallel computation**

assembling bags $\to$ **PIPELINE parallel computation**

These are the three main kinds of parallelism that we will consider.

---

### Lecture 4 - 

Let's consider a bank. You have a number of employees, and people line up in order to get services from them. Let's say we have **e employees** and let $T_e$ be the average time needed by an employee to serve a single client. Let's also assume to have $Ta$, the time taken for a new client coming to the bank.

Inter arrival rate = $\frac{1}{T_a}$

Service rate = $\frac{1}{T_e} \times e$

If the inter arrival rate is small, and $T_e$ is big, the queue starts to grow. I can imagine to increase the number of the employees, of course. We should strive to reach a point where $T_a \simeq \frac{T_e}{e}$.

Let's suppose $T_e = avg(T_{e1}, T_{e2}, T_{e3},..., T_{ek})$, this means that we have employees working at diferent speeds.

**Farm Pattern**: it is a stream parallel pattern

**Fair scheduling**: $T_{schedule} + T_{ei}$, of course $T_{schedule}$ is an overhead

1. Map
2. Reduction
3. Pipeline
4. Farm

Map and Reduction are Data Parallel patterns, while Pipeline and Farm are Stream Parallel patterns.

#### Measures of interest

#### **Latency (L)**

- Time from the start of a task to the computation of the the final result
- $L = T_{stop} - T_{start}$ 

**Service Time**

- Time in between the delivery of two consecutive results
- makes sense only for stream parallel computations
- it is equivalent to the time in between accepting two consecutive input tasks to compute
- For sequential computations, $T_S = L$
- In some sense, it is the same for data parallel computations, $T_S = L$, this makes sense only for Data Parallel computations on a stream of input tasks.

**Throughput** 

- amount of tasks computed per unit of time
- $\frac{1}{T_S}$

Base (non derived) measures include: 

- Latency
- One among Service Time and Throughput

**Derived measures** are functions of the base measures and of the parallelism degree.

- $speedup(n) = \frac{best\ sequential\ time}{parallel\ time\ with\ n} = \frac{T_{seq}}{T_{par}}$ (measures how much I improve wrt the sequential state of the art)
- $scalability(n) = \frac{T_{par}(1)}{T_{par}(n)}$ (how much I can improve when using higher parallelism degrees)

**Speedup and Scalability** can be given both in terms of Latency (main interest wrt DP computations) or Service Time (main interest wrt ).

**Efficiency**: it is a measure of the capacity to work with the available resources. It tells me "how much far" I am from the ideal parallel computation.

$ideal\ parallel\ time(n) = T_{id} = \frac{T_{seq}}{n}$

$Efficiency = \epsilon(n) = \frac{T_{id}}{T_{par}(n)} = \frac{T_{seq}}{n \times T_{par}(n)} = \frac{speedup(n)}{n}$

The maximum possible efficiency is 1. Values of efficiency > 90% are considered good. Ideal efficiency is quite impossible to achieve, since there's always some overhead involved with parallel computation.

$\epsilon(n) = \frac{T_{id}}{\frac{t_{seq}}{n} + overhead} = \frac{T_{id}}{T_{id} + overhead}$

$\epsilon(1) = \frac{T_{seq/1}}{T_{par}(1)} = \frac{T_{seq}}{T_{seq}} = 1$

Of course, $T_{par}(1)$ is not really equal to $T_{seq}$ (it features some overhead introduced by the parallel computation), but we can simplify it considering the time for $T_{seq}$ in cases such as the previous equation.

---

### Lecture 5

**Completion time**: time from the beginning of the first input to the end of the last output

- $T_C = \sum{L_i} + (m-1)max(L_i)$

- $T_S = max(T_{S_i})$

- $T_C$ can be rewritten as $T_C = \sum{L_i} + (m-1)T_S$, and can be approximated to $T_C \simeq mT_S$

Three forms of farm.

**Amdahl law**: a tentative to compute an upper bound for the speedup that can be achieved via parallel computation.

Divide the computation in a serial fraction (that cannot be parallelized) and a non-serial fraction (which can be made parallel)

$\lim_{n \to \infty}T_C = serial\ fraction$

$speedup(n) = \frac{T_{seq}}{T_{par}} = \frac{T_{seq}}{(fT_{sec)} + (1-f)T_{seq}/n}$

so, $\lim_{n\to \infty}speedup(n) = \frac{T_{seq}}{fT_{seq}} = \frac1f$

let's try with an example:

10% of the code is sequential $\implies f = \frac{1}{10} \implies max\ speedup = 10$ 

$1h = 60m, 10h = 600m, 1m\ sequential, \frac{1}{600} \implies max\ speedup = 600$

This means I will not be able to achieve a speedup greater that 600, so I would not benefit from the supercomputers in the TOP500, for example.

So Amdahl's law is pretty harsh, but there are some ways to surpass Amdahl's law, notably Gustafson's Law. Basically it is about the fact that the data which can be parallelized continues to grow and can be addressed with a greater amount of resources and greater parallelism, while the serial part of the program is more or less stable over time for the same kind of problem. 