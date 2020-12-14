---
layout:     post
title:      Summary of Concurrency for Software Development
date:       2020-12-20
summary:    Summary notes of Concurrency for Software Development
categories: Software Concurrency
---

- [Complexity Model](#complexity-model)
  - [Speedup](#speedup)
    - [Examples](#examples)
  - [Amdahl's Law for fixed problem size](#amdahls-law-for-fixed-problem-size)
    - [Examples](#examples-1)
  - [Gustafson's Law for scaled problem size](#gustafsons-law-for-scaled-problem-size)
    - [Examples](#examples-2)
  - [Karp-Flatt Metric](#karp-flatt-metric)
    - [Examples](#examples-3)
  - [Isoefficiency](#isoefficiency)
    - [Examples](#examples-4)
- [Memory Hierarchies](#memory-hierarchies)
- [Locality](#locality)
  - [Temporal Locality](#temporal-locality)
  - [Spatial Locality](#spatial-locality)
  - [Examples](#examples-5)
- [False Sharing vs True Sharing](#false-sharing-vs-true-sharing)
  - [True sharing](#true-sharing)
  - [False sharing](#false-sharing)
- [Process](#process)
  - [Fork](#fork)
  - [Zombie Process](#zombie-process)
  - [Communication Between Process](#communication-between-process)
- [Threads](#threads)
  - [Detached Mode](#detached-mode)
  - [Unintended Sharing](#unintended-sharing)
  - [Data Race](#data-race)
  - [Race Condition](#race-condition)
- [Thread vs Process](#thread-vs-process)
  - [Process Pros](#process-pros)
  - [Process Cons](#process-cons)
  - [Thread Pros](#thread-pros)
  - [Thread Cons](#thread-cons)
- [Synchronisation](#synchronisation)
  - [Semaphores](#semaphores)
    - [Producer-Consumer with Semaphore](#producer-consumer-with-semaphore)
  - [Mutex Locks](#mutex-locks)
    - [Types of Mutex](#types-of-mutex)
    - [Overheads of Locking](#overheads-of-locking)
  - [Conditional Variables](#conditional-variables)
    - [Producer-Consumer using Condition Variable](#producer-consumer-using-condition-variable)
  - [Atomic Operation](#atomic-operation)
    - [Lock vs Atomic](#lock-vs-atomic)
    - [Sequentially Consistent Ordering](#sequentially-consistent-ordering)
  - [Spinlock](#spinlock)
    - [CAS (Compare-and-swap)](#cas-compare-and-swap)
  - [Read-Write Locks](#read-write-locks)
  - [Barrier](#barrier)
  - [Deadlocks](#deadlocks)

# Complexity Model

## Speedup

-   Inherently sequential computations: $$\sigma(n)$$
-   Potentially parallel computations: $$\phi(n)$$
-   Communication operations: $$\kappa(n,p)$$

$$
\begin{align*}
    \psi &= \frac{\text{sequential execution time}}{\text{parallel execution time}} \\
    &\leq \frac{\sigma(n) + \phi(n)}{\sigma(n) + \frac{\phi(n)}{p} + \kappa(n,p)}
\end{align*}
$$

### Examples

1.  A computer animation program generates feature movies frame-by frame. Each frame can be generated and written to its own file independently. If it takes 90 seconds to render a frame and 10 second to write a frame into a file, what is the maximum speedup you can achieve if you have 100 single-processor computers to use?
    $$
    \begin{align*}
        \psi \leq \frac{\sigma(n) + \phi(n)}{\sigma(n) + \frac{\phi(n)}{p} + \kappa(n,p)} = \frac{1}{0 + \frac{1}{100} + 0} = 100
    \end{align*}
    $$

2.  Your program has an execution time of $n^3$ and uses $n^2$ bytes space when the problem size is n. You have worked very hard to make it fully parallel and reduced the communication time to $24n^2 \log^p_2$ on p cores.
    1.  If you want to achieve a speed up of 1000 with 1024 cores, what is the minimum memory each core must have?
        -   $$\psi = 1000, p = 1024, M(n) = n^2, \kappa(n,p) = 24n^2 \log^p_2$$
        -   $$\psi = \frac{\sigma(n) + \phi(n)}{\sigma(n) + \frac{\phi(n)}{p} + \kappa(n,p)} = \frac{n^3}{\frac{n^3}{1024} + 24n^2 \log^{1024}_2} = \frac{1}{\frac{1}{1024} + \frac{240}{n}} = 1000$$
        -   Hence, $$n = 10240000$$
        -   So the minimum memory each core must have $$\frac{n^2}{p} = \frac{1024 \cdot 10^8}{1024} = 10^8 KB = 100GB$$
    2.  If you have 1024 cores with 1 GB ($$2^{30}$$ bytes) memory per core, what is the maximum speedup you can achieve?
        -   $$\frac{M(n)}{p} = \frac{n^2}{1024} = 2^{30}$$, hence $$n = \sqrt{2^{30} \cdot 1024} = 1048576$$
        -   $$\psi = \frac{\sigma(n) + \phi(n)}{\sigma(n) + \frac{\phi(n)}{p} + \kappa(n,p)} = \frac{n^3}{\frac{n^3}{1024} + 24n^2 \log^{1024}_2} = \frac{1}{\frac{1}{1024} + \frac{240}{n}} =.  \frac{1}{\frac{1}{1024} + \frac{240}{1048576}} \cong 929.57$$

## Amdahl's Law for fixed problem size

Strong scaling concerns the speedup for a fixed problem size with respect to the number of processors.
$$
\begin{align*}
    \psi(n,p) \leq \frac{1}{f + \frac{1-f}{p}} \, \text{ where sequence $f$ part is fixed}
\end{align*}
$$

### Examples

1.  95% of a program’s execution time occurs inside a loop that can be executed in parallel. What is the maximum speedup we should expect from a parallel version of the program executing on 8 CPUs?
    $$
    \begin{align*}
        \psi \leq \frac{1}{0.05+ \frac{1-0.05}{8}} \cong 5.9
    \end{align*}
    $$

2.  20% of a program’s execution time is spent within inherently sequential code. What is the limit to the speedup achievable by a parallel version of the program?
    $$
    \begin{align*}
        \lim _{p \rightarrow \infty} \frac{1}{0.2+\frac{1-0.2}{p}}=\frac{1}{0.2}=5
    \end{align*}
    $$

3.  If 99.9% of your sequential program execution time is spent inside a loop that can be paralleled, what is the maximum speedup you can achieve via parallelising this loop?
    $$
    \begin{align*}
        \lim _{p \rightarrow \infty} \frac{1}{0.1\% +\frac{1- 0.1\%}{p}}=\frac{1}{0.001}=1000
    \end{align*}
    $$

## Gustafson's Law for scaled problem size

Weak scaling concerns the speedup for a scaled problem size with respect to the number of processors.
$$
\begin{align*}
    \psi \leq p + (1 - p)s \, \text{ where parallel $s$ part is fixed}
\end{align*}
$$

### Examples

1.  An application running on 10 processors spends 3% of its time in serial code. What is the scaled speedup of the application?
    $$
    \begin{align*}
        \psi = 10 + (1 - 10) \cdot 0.03 = 10 - 0.27 = 9.73
    \end{align*}
    $$

2.  What is the maximum fraction of a program’s parallel execution time that can be spent in serial code if it is to achieve a scaled speedup of 7 on 8 processors?
    $$
    \begin{align*}
        &7 = 8 + (1 - 8)s \\
        &7s = 1 \\
        &s = 0.14
    \end{align*}
    $$

3.  If a two-hour parallel program running on one thousand cores spends one hour in its parallel portion, what is the scaled speedup of the program on one thousand cores?
    $$
    \begin{align*}
        \psi = 1000 + (1 - 1000) \cdot \frac{1}{2} = 500.5
    \end{align*}
    $$

## Karp-Flatt Metric

$$
\begin{align*}
    e = \frac{\frac{1}{\psi} - \frac{1}{p}}{1 - \frac{1}{p}}
\end{align*}
$$

### Examples

1.  What is the primary reason of the following table for speedup of only 4.7 on 8 CPUs?

    | $$p$$    | 2    | 3    | 4    | 5    | 6    | 7    | 8    |
    | ------ | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
    | $$\psi$$ | 1.8  | 2.5  | 3.1  | 3.6  | 4.0  | 4.4  | 4.7  |

    -   $$p = 2, e = \frac{1/1.8 - 1/2}{1 - 1/2} = 0.1$$
    -   $$p = 3, e = \frac{1/2.5 - 1/3}{1 - 1/3} = 0.1$$
    -   $$p = 4, e = \frac{1/3.1 - 1/4}{1 - 1/4} = 0.1$$
    -   $$p = 5, e = \frac{1/3.6 - 1/5}{1 - 1/5} = 0.1$$
    -   $$p = 6, e = \frac{1/4.0 - 1/6}{1 - 1/6} = 0.1$$
    -   $$p = 7, e = \frac{1/4.4 - 1/7}{1 - 1/7} = 0.1$$
    -   $$p = 8, e = \frac{1/4.7 - 1/8}{1 - 1/8} = 0.1$$

    Since e is constant, i.e. e is not affected by the paralleled overhead, so that serial part of code is dominated.

2.  What is the primary reason of the following table for speedup of only 4.7 on 8 CPUs?

    | $$p$$    | 2    | 3    | 4    | 5    | 6    | 7    | 8    |
    | ------ | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
    | $$\psi$$ | 1.9  | 2.6  | 3.2  | 3.7  | 4.1  | 4.5  | 4.7  |

    -   $$p = 2, e = \frac{1/1.9 - 1/2}{1 - 1/2} = 0.053$$
    -   $$p = 3, e = \frac{1/2.6 - 1/3}{1 - 1/3} = 0.077$$
    -   $$p = 4, e = \frac{1/3.2 - 1/4}{1 - 1/4} = 0.083$$
    -   $$p = 5, e = \frac{1/3.7 - 1/5}{1 - 1/5} = 0.088$$
    -   $$p = 6, e = \frac{1/4.1 - 1/6}{1 - 1/6} = 0.092$$
    -   $$p = 7, e = \frac{1/4.5 - 1/7}{1 - 1/7} = 0.0.092$$
    -   $$p = 8, e = \frac{1/4.7 - 1/8}{1 - 1/8} = 0.100$$

    Since e is steadily increasing, parallel overhead is the primary reason.

3.  Is this program likely to achieve a speedup of 10 on 12 processors?

    | $$p$$    | 4     | 8     | 12    |
    | ------ | ----- | ----- | ----- |
    | $$\psi$$ | 3.9   | 6.5   | ?     |
    | $$e$$    | 0.008 | 0.032 | 0.018 |

    No, because $$e_3 \geq e_2$$, which means the parallel overhead has increase on 12 processors.

4.  A parallel program achieves a speedup of 2 on 4 cores. Is it likely to achieve a speedup of 4 on 8 cores?
    $$
    \begin{align*}
        &e_1=\frac{1 / \psi-1 / p}{1-1 / p} = \frac{1 / 2-1 / 4}{1-1 / 4} \cong 0.33 \\
        &e_2=\frac{1 / \psi-1 / p}{1-1 / p} = \frac{1 / 4-1 / 8}{1-1 / 8} \cong 0.14 \\
    \end{align*}
    $$
    Since $$e_1 > e_2$$, so it is not likely to achieve a speedup of 4 on 8 cores.

## Isoefficiency

![graph](https://i.loli.net/2020/12/12/VWD6ejUm2RakpcY.png)

-   $$T_0(n,p)$$ is parallel overhead
-   $$T(n,1)$$ is sequential execution time
-   $$M(n)$$ is to maintain same level of efficiency, how must n increase when p increases

$$
\begin{align*}
    &T(n,1) \geq CT_0(n, p) \Rightarrow n \geq f(p) \\
    &\text{scalability function} = \frac{M(f(p))}{p}
\end{align*}
$$

### Examples

1.  Let $$n > f(p)$$ denote the Isoefficiency relation of a parallel system and $$M(n)$$ denote the amount of memory for a problem of size n. Use the scalability function to rank the following parallel systems from most to least scalable:

    -   $$f(p) = p$$ and $$M(n)=n$$
    -   $$f(p)=p$ and $M(n)=n^2$$
    -   $$f(p)=p\cdot \log(p)$$ and $$M(n)=n$$
    -   $$f(p)=p \cdot \log(p)$$ and $$M(n)=n^2$$

    $$
    \begin{align}
    &\frac{M(f(p))}{p} = \frac{Cp}{p} = C \\
    &\frac{M(f(p))}{p} = \frac{(Cp)^2}{p} = C^2p \\
    &\frac{M(f(p))}{p} = \frac{Cp \cdot \log(p)}{p} = C \cdot \log(p) \\
    &\frac{M(f(p))}{p} = \frac{(Cp \cdot \log(p))^2}{p} = C^2 \cdot p \cdot log^2(p) \\
    \end{align}
    $$

    Hence a > c > b > d.

2.  Assume a parallel program takes 1000 seconds to finish when using 1 core and 600 seconds to finish when using 2 cores.

    1.  Is it possible to finish the program within 400 seconds when using 4 cores?
        -   When using 2 cores, speedup is $$\frac{1000}{600} = \frac{5}{3}$$
        -   When using 2 cores, serial fraction is $$e = \frac{\frac{1}{5/3} - \frac{1}{2}}{1 - \frac{1}{2}} = \frac{1}{5}$$
        -   When using 4 cores, speedup is $$\frac{1}{f + \frac{1 - f}{p}} = \frac{1}{\frac{1}{5} - \frac{1 - \frac{1}{5}}{4}} = 2.5$$
        -   When using 4 cores, execution time is $$\frac{1000}{2.5} = 400$$
        -   So, it’s possible to finish the program within 400 seconds when using 4 cores.
    2.  If your experiment actually takes 500 seconds when using 4 cores, what is the minimum execution time when using 6 cores?
        -   When using 4 cores, speedup is $$\frac{1000}{500} = 2$$
        -   When using 4 cores, serial fraction is $$e = \frac{\frac{1}{2} - \frac{1}{4}}{1 - \frac{1}{4}} = \frac{1}{3}$$
        -   Since serial fraction of 6 cores should be \textbf{larger} than serial fraction of 4 cores in order to achieve speedup, so $$e_6 > \frac{1}{3}$$
        -   When using 6 cores, serial fraction is $$e_6 = \frac{\frac{1}{\psi} - \frac{1}{6}}{1 - \frac{1}{6}} \geq \frac{1}{3}$$, thus $$\psi \leq \frac{4}{9}$$
        -   Hence, minimum execution time is $$\text{Parallel execution time} = \frac{\text{sequential execution time}}{\text{speedup}} = \frac{1000}{\frac{9}{4}} = 444.4$$ seconds.

3.  If sequential algorithm complexity is. $$T(n,1) = \Theta(n)$$, computational complexity is $$\Theta(\frac{n}{p})$$, communication complexity is $$\Theta(\log p)$$, parallel overhead is $$T_0(n, p) = \Theta(p \log p)$$ and $$M(n) = n$$. Does this system has good scalability?
    $$
    \begin{align*}
        &T(n,1) \geq CT_0(n,p) \Rightarrow n \geq C p \log p \\
        % &\text{computational complexity is $\Theta(\frac{n}{p})$} \Rightarrow M(n) = n \\
        &\frac{M(C p \log p)}{p} = \frac{Cp \log p}{p} = C\log p
    \end{align*}
    $$
    Hence this system has good scalability. (reduction)

4.  If sequential time complexity is $$T(n, 1)=\Theta\left(n^{3}\right)$$, parallel computation time is $$\Theta\left(n^{3} / p\right)$$, parallel communication time is $$\Theta\left(n^{2} \log p\right)$$, parallel overhead is $$T_{0}(n, p)=\Theta\left(p n^{2} \log p\right)$$ and $$M(n) = n^2$$. Does this system has good scalability?
    $$
    \begin{align*}
        &T(n,1) \geq CT_0(n,p) \Rightarrow n^3 \geq C pn^2 \log p \Rightarrow n \geq Cp \log p \\
        &\frac{M(C p \log p)}{p} = \frac{(Cp \log p)^2}{p} = \frac{C^2 p^2 \log^2p}{p} = C^2 p \log^2p
    \end{align*}
    $$
    Hence this system has poor scalability. (Floyd's algorithm)

5.  If sequential time complexity is $$T(n, 1)=\Theta\left(n^{2}\right)$$, parallel communication complexity per iteration is $$\Theta\left(\frac{n}{\sqrt{p}}\right)$$, parallel overhead is $$T_{0}(n, p)=\Theta(n \sqrt{p})$$ and space complexity $$M(n) = n^2$$. Does this system has good scalability?
    $$
    \begin{align*}
        &T(n,1) \geq CT_0(n,p) \Rightarrow n^2 \geq C n \sqrt{p} \Rightarrow n \geq C \sqrt{p} \\
        &\frac{M(C \sqrt{p})}{p} = \frac{(C \sqrt{p})^2}{p} = \frac{C^2 p}{p} = C^2
    \end{align*}
    $$
    Hence this system has perfect scalability.

# Memory Hierarchies

![image-20201213162030556](https://i.loli.net/2020/12/13/6T82juSR9eHiFId.png)

-   Cycle number (notes: CPU has 4 or 8 operations per cycle)
    -   Register access, ~1 cycle (0.376 ns)
    -   L1 Cache access, ~4 cycles
    -   L2 Cache access, ~10 cycles
    -   L3 Cache access, line unshared, ~40 cycles
    -   L3 Cache access, shared line in another core, ~65 cycles
    -   L3 Cache access, modified in another core, ~75 cycles
    -   DRAM access, ~150 cycles
    -   Disk access, ~10,000 cycles
-   Based on idea of spatial and temporal data locality
    -   Cache hit: data found in cache
    -   Cache miss: data not found in cache and must be copied from a lower level
        -   Compulsory miss: first reference miss
        -   Capacity miss: cache runs out of room for new data
        -   Conflict miss: many data items map to same location in cache
        -   True sharing miss: Occurs when a thread in another processor wants the same data. Cure: Minimize sharing
        -   False sharing miss: Occurs when another processor uses different data in the same cache line. Cure: Pad data.

# Locality

Principle of Locality: Programs tend to use data and instructions with addresses near or equal to those they have used recently.

## Temporal Locality

<img src="https://i.loli.net/2020/12/13/Iy7rCbZqh6zRix1.png" alt="image-20201213161634698" style="zoom:50%;" />

Recently referenced items are likely to be referenced again in the near future.

## Spatial Locality

<img src="https://i.loli.net/2020/12/13/Z7ibUDuv6wSzrX9.png" alt="image-20201213161657961" style="zoom:50%;" />

Items with nearby addresses tend to be referenced close together in time

## Examples

1.  State the locality of the following examples

    ```c
    sum = 0;
    for (i = 0; i < n; i++)
        sum += a[i];
    return sum;
    ```

    1.  Reference array elements in succession (spatial)
    2.  Reference variable `sum` each iteration (temporal)
    3.  Reference instructions in sequence. (spatial)
    4.  Cycle through loop repeatedly. (temporal)

# False Sharing vs True Sharing

![image-20201214131733232](https://i.loli.net/2020/12/14/taxB4G3qzSN16iD.png)

-   True sharing occurs when multiple threads on different cores access overlapping bytes on the same cache line (e.g. multiple threads accessing a shared lock object).
-   False sharing, on the other hand, occurs when multiple threads access disjoint bytes on the same cache line.

## True sharing

-   Require programmatic synchronisation constructs to ensure ordered data access.
-   One core accessing multiple nearby memory addresses that have been loaded into a single cache line.
-   Occur when a processor writes some words into a cache block, invalidating the block in another processor's cache, after which the other processor reads one of the modified words.
-   Cause
    -   One core accessing multiple nearby memory addresses that have been loaded into a single cache line.
    -   Occur when a processor writes some words into a cache block, invalidating the block in another processor's cache, after which the other processor reads one of the modified words.

## False sharing

-   The frequent coordination required between processors when cache lines are marked `invalid` requires cache lines to be written to memory and subsequently loaded.

-   Increases this coordination and can significantly degrade application performance.

-   Cause

    -   Occurs when threads on different processors modify variables that reside on the same cache line. This invalidates the cache line and forces a memory update to maintain cache coherency, which hurts performance.
    -   Shared data is modified by multiple processors.
    -   Multiple processors update data within the same cache line.
    -   This updating occurs very frequently (for example, in a tight loop).

-   Fixing

    The goal is to ensure that variables causing false sharing are spaced far enough apart in memory that they cannot reside on the same cache line.

    -   Use compiler directives to force individual variable alignment, pad the structure to the end of a cache line to ensure that the array elements begin on a cache line boundary. If you cannot ensure that the array is aligned on a cache line boundary, pad the data structure to twice the size of a cache line. If the array is dynamically allocated, you can increase the allocation size and adjust the pointer to align with a cache line boundary.
    -   It is also possible to reduce the frequency of false sharing by using thread-local copies of data. The thread-local copy can be read and modified frequently and only when complete, copy the result back to the data structure. The following source code demonstrates using a local copy to avoid false sharing.
    -   making use of private data as much as possible
    -   utilising the compiler's optimization features to eliminate memory loads and stores.

-   Examples

    ```c
    double sum=0.0, sum_local[NUM_THREADS];
    #pragma omp parallel num_threads(NUM_THREADS)
    {
    	int me = omp_get_thread_num();
        sum_local[me] = 0.0;

        #pragma omp for
        for (i = 0; i < N; i++)
            sum_local[me] += x[i] * y[i];

        #pragma omp atomic
        sum += sum_local[me];
    }
    ```

    There is a potential for false sharing on array `sum_local`. This array is dimensioned according to the number of threads and is small enough to fit in a single cache line. When executed in parallel, the threads modify different, but adjacent, elements of `sum_local`, which invalidates the cache line for all processors.

    The compiler eliminates false sharing using thread-private temporal variables. Run-time false sharing from the above code will be only an issue if the code is compiled with optimisation disabled.

# Process

<img src="https://i.loli.net/2020/12/12/7pGJ6x3VPiHabvI.png" alt="iShot2020-12-12 20.43.11" style="zoom: 33%;" />

-   Process
    -   = memory state + machine state
    -   = context + code, data, and stack
    -   = thread + code, data, and kernel context
-   a process is in one of three states
    -   In the running state it is either executing on the CPU or is waiting to be executed and eventually scheduled by the kernel
    -   In the stopped state the execution of the process is suspended and will not be scheduled. A process stops if it receives a `SIGSTOP`, `SIGTSTP`, `SIGTTIN`, or `SIGTTOU` signal
    -   In the terminated state the process is stopped permanently. A process becomes terminated for one of three reasons
        -   receiving a signal to terminate
        -   returning from main
        -   calling the exit function

## Fork

-   Examples

    What is the output of the program?

    A. acbc

    B. bcac

    C. abcc

    D. bacc

    E. A or  C or D √

    ```c
    #include <stdio.h>
    #include <stdlib.h>
    #include <unistd.h>
    #include <sys/wait.h>

    void main() {
        if (fork() == 0) {
            printf("a");
        } else {
            printf("b");
            waitpid(-1, NULL, 0);
        }

        printf("c");
        exit(0);
    }
    ```

    ![image-20201214152645532](https://i.loli.net/2020/12/14/LsJlARwefTCdozW.png)

## Zombie Process

-   Examples on reap a zombie process

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

int N = 5;

int main() {
    pid_t pid[N];
    int i;
    int child_status;
    for (i = 0; i < N; i++) {
        if ((pid[i] = fork()) == 0) {
            exit(100+i);
        }
    }

    for (i = 0; i < N; i++) {
        pid_t wpid = wait(&child_status);
        if (WIFEXITED(child_status)) {
            printf("Child %d terminated with exit status %d\n", wpid, WEXITSTATUS(child_status));
        }  else {
            printf("Child %d terminated abnormally\n", wpid);
        }
    }
}

// output
// Child 39926 terminated with exit status 101
// Child 39925 terminated with exit status 100
// Child 39927 terminated with exit status 102
// Child 39928 terminated with exit status 103
// Child 39929 terminated with exit status 104
```

**Notes**: `int waitpid(01, &status, 0)` is the same as `int wait(&status)`

## Communication Between Process

A signal is an event of some type that has occurred in the system.

-   It allows the OS to communicate to a process
    -   If a process tries to divide by 0, OS sends it a SIGFPE signal
    -   If a process executes an illegal instruction, OS sends it a SIGILL signal
    -   If a process makes illegal memory reference: OS sends it a SIGSEGV signal
-   User processes to communicate to each other
    -   If you type ctrl-‐c during process exec, OS sends it a SIGINT signal
    -   A process can kill another process, P1 sends P2 a SIGKILL signal
    -   When a child terminates, OS sends the parent a SIGCHLD signal
-   A signal is pending if sent but not yet received
    -   There can be at most 1 pending signal for a type
    -   Important: signals are **not queued** - If a process has a pending signal of type k, then subsequent signals of type k that are sent to that process are discarded.

-   A process can block the receipt of certain signals
    -   Blocked signals can be delivered, but will not be received until the signal is unblocked.

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <signal.h>

void sig_alarm(int signal) {
    printf("Receive alarm signal =  %d\n", signal);
}

int main(int argc, char* argv[]) {
    signal(SIGALRM, sig_alarm);
    alarm(1);
    printf("program end!\n");
    return 0;
}
```

# Threads

<img src="https://i.loli.net/2020/12/13/hwBVdjSrna3KZ96.png" alt="image-20201213183706335" style="zoom:50%;" />

```c
#include <stdio.h>
#include <pthread.h>

void* thread(void* vargp) {
    printf("Hello, world!\n");
    return NULL;
}

int main() {
    pthread_t tid;
    pthread_create(&tid, NULL, thread, NULL);
    pthread_join(tid, NULL);
    return 0;
}
```

![image-20201214160641600](https://i.loli.net/2020/12/14/odeFx2Q94HgIUSj.png)

## Detached Mode

```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>

void* thread(void* vargp) {
    pthread_detach(pthread_self());
    printf("hello from thread world.\n");
    return NULL;
}

int main()  {
    pthread_t tid;

    printf("Main thread creating peer thread.\n");
    pthread_create(&tid, NULL, thread, NULL);

    pthread_exit(NULL);
    return 0;
}
```

```c
todo
```

-   Runs independently of other threads
-   Reaped automatically (by kernel) when it terminates
-   without the need for another thread to join with the terminated thread

## Unintended Sharing

-   Unintended sharing examples

    ```c
    #include <stdio.h>
    #include <stdlib.h>
    #include <pthread.h>

    // unintended sharing
    void* thread(void* vargp) {
        pthread_detach(pthread_self());
        // run into segmentation fault, once the lifetime of i is expired
        int arg = *((int*) vargp);
        printf("hello from thread %d.\n", arg);
        return NULL;
    }

    int main()  {
        pthread_t tid;

        for (int i = 0; i < 10; i++) {
            // the address of i is shared within all the threads, so that you cannot predicate the  conteent in i
            pthread_create(&tid, NULL, thread, &i);
        }

        pthread_exit(NULL);
        return 0;
    }
    ```

-   Fix unintended sharing

    ```c
    #include <stdio.h>
    #include <stdlib.h>
    #include <pthread.h>

    // fix unintended sharing
    void* thread(void* vargp) {
        pthread_detach(pthread_self());
        int arg = *((int*) vargp);
        printf("hello from thread %d.\n", arg);
        free(vargp);
        return NULL;
    }

    int main()  {
        pthread_t tid;
        int* argp;

        for (int i = 0; i < 10; i++) {
            argp = malloc(sizeof(int));
            *argp = i;
            pthread_create(&tid, NULL, thread, argp);
        }

        pthread_exit(NULL);
        return 0;
    }
    ```

## Data Race

A data race occurs when two or more threads can access shared data and one of them is a write. Because the thread scheduling algorithm can swap between threads at any time, you don't know the order in which the threads will attempt to access the shared data.

```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>

long cnt = 0;

// data race
void* thread(void* vargp) {
    long i, niters = *((long*) vargp);
    for (i = 0; i < niters; i++) {
        cnt++;
    }
    return NULL;
}

int main(int argc, char** argv) {
    long niters;
    pthread_t tid1, tid2;

    niters = atoi(argv[1]);
    pthread_create(&tid1, NULL, thread,  &niters);
    pthread_create(&tid2, NULL, thread, &niters);
    pthread_join(tid1, NULL);
    pthread_join(tid2, NULL);

    // check result
    if (cnt != (2 * niters)) {
        printf("BOOM! cnt = %ld\n", cnt);
    } else {
        printf("OK cnt = %ld\n", cnt);
    }

    return 0;
}
```

## Race Condition

A race condition is a semantic error. It is a flaw that occurs in the timing or the ordering of events that leads to erroneous program behavior.

Many race conditions can be caused by data races, but this is not necessary. For example, the following simple example where x is a shared variable:

```c
// thread 1
lock(1);
x = 1;
unlock(1);
```

```c
// thread 2
lock(1);
x = 2;
unlock(1);
```

# Thread vs Process

![image-20201214154639164](https://i.loli.net/2020/12/14/3Ftxamlv6fogKkT.png)

<img src="https://i.loli.net/2020/12/14/HmZkDjFhCt89nxP.png" alt="image-20201214154749810" style="zoom:50%;" />

-   How threads and processes are similar
    -   Each has its own logical control flow
    -   Each can run concurrently with others
    -   Each is context switched
-   How threads and processes are different
    -   Threads share code and some data
        -   Processes (typically) do not
    -   Threads are somewhat less expensive than processes
        -   Process control is twice as expensive as thread control
        -   Linux numbers:
            -   ~20K cycles to create and reap a process
            -   ~10K cycles (or less) to create and reap a thread

## Process Pros

-   Clean Sharing Model
    -   Global variables (address spaces) are not shared
    -   File tables (file descriptors) are shared
-   Simple and straightforward
    -   Forking a child process is easy
    -   Reaping child processes is simple
    -   Processes are isolated for protection

## Process Cons

-   Forking a process is expensive
    -   Need to clone parent’s memory space
    -   Need to setup a separate context for child
-   Non-trivial to share data between processes
    -   Need to use files/pipes to share data
    -   Can use shared memory
    -   Lots of overhead!

## Thread Pros

-   Threads can share common data, they do not need to use interprocess communication.

-   Threads are cheap in the sense that
    -   They only need a stack and storage for registers therefore, threads are cheap to create.
    -   Threads use very little resources of an operating system in which they are working. That is, threads do not need new address space, global data, program code or operating system resources.
    -   Context switching are fast when working with threads. The reason is that we only have to save and/or restore PC, SP and registers.

## Thread Cons

-   There is no protection between threads.
    -   If the kernel is single threaded, a system call of one thread will block the whole process and CPU may be idle during the blocking period.
    -   Since there is, an extensive sharing among threads there is a potential problem of security. It is quite possible that one thread over writes the stack of another thread (or damaged shared data) although it is very unlikely since threads are meant to cooperate on a single task.

# Synchronisation

## Semaphores

-   non-negative global integer synchronization variable
-   it is a signalling mechanism. It guarantees both ordering and atomicity.
-   any thread can release a semaphore, not only the one that has acquired it in the first place.

```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <semaphore.h>

long cnt = 0;
sem_t mutex;

void* thread(void* vargp) {
    long i, niters = *((long*) vargp);
    for (i = 0; i < niters; i++) {
        sem_wait(&mutex); // ddecrement 1, locking mutex
        cnt++;
        sem_post(&mutex); // increment 1, unlocking mutex
    }
    return NULL;
}

int main(int argc, char** argv) {
    long niters;
    pthread_t tid1, tid2;
    sem_init(&mutex, 0, 1);

    niters = atoi(argv[1]);
    pthread_create(&tid1, NULL, thread,  &niters);
    pthread_create(&tid2, NULL, thread, &niters);
    pthread_join(tid1, NULL);
    pthread_join(tid2, NULL);

    // check result
    if (cnt != (2 * niters)) {
        printf("BOOM! cnt = %ld\n", cnt);
    } else {
        printf("OK cnt = %ld\n", cnt);
    }
    return 0;
}
```

### Producer-Consumer with Semaphore

```c
sem_t empty; // empty slot in buffer
sem_t occupied; // occupied slot in buffer
sem_t p_lock; // mutex for producer function
sem_t c_lock; // mutex for consumer function

void* producer(void* producer_thread_data) {
    while (!done()) {
        sem_wait(&empty);
        sem_wait(&p_lock);

        insert_into_queue();

        sem_post(&p_lock);
        sem_post(&occupied);
    }
}

void* producer(void* consumer_thread_data) {
    while (!done()) {
        sem_wait(&occupied);
        sem_wait(&c_lock);

        my_task = extract_from_queue();

        sem_post(&c_lock);
        sem_post(&empty);

        process_task(my_task);
    }
}

void main() {
    sem_init(&p_lock, 0, 1);
    sem_init(&c_lock, 0, 1);
    sem_init(&empty, 0, BUFFER_SIZE);
    sem_init(&occupied, 0, 0);
}
```

## Mutex Locks

-   Mutex-locks have two states: locked and unlocked. At any point of time, only one
-   thread can lock a mutex lock. A lock is an atomic operation.
-   A thread entering a critical section first tries to get a lock. It goes ahead when the lock is granted.
-   A thread release the lock when leaving a critical section

```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>

pthread_mutex_t lock;
volatile long cnt = 0;

void* thread(void* vargp) {
    long i, niters = *((long*) vargp);
    pthread_mutex_lock(&lock);
    for (i = 0; i < niters; i++) {
        // pthread_mutex_lock(&lock);
        cnt++;
        // pthread_mutex_unlock(&lock);
    }
    pthread_mutex_unlock(&lock);
    return NULL;
}

int main(int argc, char** argv) {
    long niters;
    pthread_t tid1, tid2;

    if (pthread_mutex_init(&lock, NULL) != 0) {
        printf("\nmutex init has failed\n");
        return 1;
    }

    niters = atoi(argv[1]);
    pthread_create(&tid1, NULL, thread,  &niters);
    pthread_create(&tid2, NULL, thread, &niters);
    pthread_join(tid1, NULL);
    pthread_join(tid2, NULL);

    // check result
    if (cnt != (2 * niters)) {
        printf("BOOM! cnt = %ld\n", cnt);
    } else {
        printf("OK cnt = %ld\n", cnt);
    }

    pthread_mutex_destroy(&lock);
    return 0;
}
```

**Notes**: locking and unlocking is supported by operating system if put locking mechanism within for loop, it will produce a lot of overhead. Because it requires context switch for every iteration.

### Types of Mutex

-   A normal mutex deadlocks if a thread that already has a lock tries a second lock on it. `PTHREAD_MUTEX_NORMAL`

- A recursive mutex allows a single thread to lock a mutex as many times as it wants. It simply increments a count on the number of locks. A lock is relinquished by a thread when the count becomes zero. `PTHREAD_MUTEX_RECURSIVE`
- An error check mutex reports an error when a thread with a lock tries to lock it again (as opposed to deadlocking in the first case, or granting the lock, as in the second case). `PTHREAD_MUTEX_ERRORCHECK`

```c
// initialize a recursive mutex
pthread_mutex_t Mutex;
pthread_mutexattr_t Attr;
pthread_mutexattr_init(&Attr);
pthread_mutexattr_settype(&Attr, PTHREAD_MUTEX_RECURSIVE); pthread_mutex_init(&Mutex, &Attr);
```

### Overheads of Locking

-   Locks represent serialisation points since critical sections must be executed by threads one after the other.
-   Encapsulating large segments of the program within locks can lead to significant performance degradation.
-   It is often possible to reduce the idling overhead associated with locks using `int pthread_mutex_trylock (pthread_mutex_t *mutex_lock);`, which attempts to lock mutex_lock, but if unsuccessful, will return immediately with a `busy` error code.

## Conditional Variables

-   A condition variable always has a mutex associated with it. A thread locks this mutex before issuing a wait, a signal or a broadcast on condition variables.
-   While the thread is waiting (`pthread_cond_wait`) on a condition variable, the mutex is automatically unlocked, and when the thread is signalled (`pthread_cond_signal`), the mutex is automatically locked again.

### Producer-Consumer using Condition Variable

```c
pthread_cond_t queue_not_full, queue_not_empty;
pthread_mutex_t queue_cond_lock;
pthread_t p, c;

void* producer(void* producer_thread_data) {
    while (!done()) {
        pthread_mutex_lock(&queue_cond_lock);

        if (task_available == BUFSIZE)
            pthread_cond_wait(&queue_not_full, &queue_cond_lock);
       	task_available++;
        insert_into_queue();

        pthread_cond_signal(&queue_not_empty);
        pthread_mutex_unlock(&queue_cond_lock);
    }
}

void* consumer(void* consumer_thread_data) {
    while (!done()) {
        pthread_mutex_lock(&queue_cond_lock);

        if (task_available == 0)
            pthread_cond_wait(&queue_not_empty, &queue_cond_lock);
       	task_available--;
        my_task = extract_from_queue();

        pthread_cond_signal(&queue_not_full);
        pthread_mutex_unlock(&queue_cond_lock);
        process_task(my_task);
    }
}

voidd main() {
    task_available = 0;
    pthread_mutex_init(&queue_cond_lock, NULL);
    pthread_create(&p, NULL, producer, NULL);
    pthread_create(&p, NULL, consumer, NULL);
    pthread_cond_init(&queue_not_empty, NULL);
    pthread_cond_init(&queue_not_full, NULL);
    pthread_join(p, NULL);
    pthread_join(c, NULL);
}
```

##  Atomic Operation

-   Concurrent access using atomic operations is guaranteed to not cause data races
-   Allowing for lockless concurrent programming
-   Hardware support mechanism
-   Providing facilities for low-level synchronization operations that will commonly reduce to one or two CPU instructions.
-   `__atomic_add_fetch(type* ret_val, type add_val, int mem_order)`: ++i
-   `__atomic_fetch_add(type* ret_val, type add_val, int mem_order)`: i++
-   Six memory ordering
    -   Sequentially consistent ordering (sequentially consistent)
    -   Acquire-release ordering (consume, acquire, release, acquire-release)
    -   Relaxed ordering (relaxed)

```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <stdatomic.h>

volatile long cnt = 0;

void* thread(void* vargp) {
    long i, niters = *((long*) vargp);
    for (i = 0; i < niters; i++) {
        __atomic_add_fetch(&cnt, 1, __ATOMIC_SEQ_CST);
    }
    return NULL;
}

int main(int argc, char** argv) {
    long niters;
    pthread_t tid1, tid2;

    niters = atoi(argv[1]);
    pthread_create(&tid1, NULL, thread,  &niters);
    pthread_create(&tid2, NULL, thread, &niters);
    pthread_join(tid1, NULL);
    pthread_join(tid2, NULL);

    // check result
    if (cnt != (2 * niters)) {
        printf("BOOM! cnt = %ld\n", cnt);
    } else {
        printf("OK cnt = %ld\n", cnt);
    }

    return 0;
}
```

### Lock vs Atomic

-   Low-level implementation
    -   Atomic operations leverage processor support, no locks at all.

    -   Locks are more OS-dependent

-   Context switch

    - Locks suspend thread execution, free up CPU resource for other threads. Incurring in obvious context switching overhead
    - Atomic operations don't incur in context switching overhead, but suffering from busy-waiting

### Sequentially Consistent Ordering

-   All threads must see the same order of operations
-   Most straightforward and intuitive ordering
    -   But, it's also the most expensive memory ordering because it requires global synchronization between all threads (the same execution order is observed by all threads)
    -   X86/x86-64 architectures offer sequentially consistent with low overhead; however, on other architecture (e.g. ARM), sequentially consistent could be more expensive.

```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <stdatomic.h>
#include <stdbool.h>
#include <assert.h>

bool x,y;
int z;

void* write_x_then_y() {
    __atomic_store_n(&x, true, __ATOMIC_SEQ_CST);
    __atomic_store_n(&y, true, __ATOMIC_SEQ_CST);
    return NULL;
}

void* read_y_then_x() {
    while (!__atomic_load_n(&y, __ATOMIC_SEQ_CST));
    if (__atomic_load_n(&x, __ATOMIC_SEQ_CST)) {
        __atomic_add_fetch(&z, 1, __ATOMIC_SEQ_CST);
    }
    return NULL;
}

int main() {
    x = false;
    y = false;
    z = 0;
    pthread_t tid1, tid2;

    pthread_create(&tid1, NULL, read_y_then_x, NULL);
    pthread_create(&tid2, NULL, write_x_then_y, NULL);
    pthread_join(tid1, NULL);
    pthread_join(tid2, NULL);

    assert(z != 0);
    return 0;
}
```

## Spinlock

-   A spinlock is a simple synchronisation object providing mutual exclusion
-   A thread trying to acquire then lock by simply wait in a loop ("spin")
-   Repeatedly checking if the lock is available.

```c
void spin_lock(spinlock* lock) {
    while(lock.try_get_lock());
}
```

### CAS (Compare-and-swap)

- This compares the contents of  `*ptr` with the contents of `*expected`

- If equal, write desired to `*ptr`. `Return true;`

- If not, read and the current contents of `*ptr` are written into `*expected`. `Return false.`
- Read-write Locks

```c
#define LOCKED 1
#define UNLOCKED 0

void spin_lock(int* lock) {
    int expected = UNLOCKED;
    while(!__atomic_compare_exchange_n(lock, &expected, LOCKED, true, __ATOMIC_SEQ_CST, __ATOMIC_SEQ_CST)) {
        expected = UNLOCKED;
    }
}

void spin_unlock(int* lock) {
    __atomic_store_n(lock, UNLOCKED, __ATOMIC_SEQ_CST);
}
```

-   Examples  - the lock is held when `lock ==  1`

    ```c
    void spin_lock(int* lock) {
        while(!CAS(lock, 0, 1));
    }
    void unlock(int* lock) {
        __atomic_store(lock, 0);
    }
    ```

## Read-Write Locks

-   Somewhat like a mutex except that it provides two lock functions.
-   The first lock function locks the read-write lock for reading, while the second locks it for writing.
-   So multiple threads can simultaneously obtain the lock by calling the r lock function, while only one thread can obtain the lock by calling the write-lock function
-   Thus, if any thread owns the lock for reading, any thread that wants to obtain the lock for writing will block in the call to the write-lock function.

-   If any thread owns the lock for writing, any threads that want to obtain the lock for reading or writing will block in their respective locking functions.

```c
#include <stdio.h>
#include <errno.h>
#include <stdlib.h>
#include <pthread.h>
#include <poll.h>
#define ACCESS_ONCE(x) (*(volatile typeof(x) *)&(x))

int x = 0;
pthread_rwlock_t lock_rw = PTHREAD_RWLOCK_INITIALIZER;

void* reader_thread(void* arg) {
    int i;
    int newx, oldx;
    newx = oldx = -1;
    pthread_rwlock_t* p = (pthread_rwlock_t*)arg;

    pthread_rwlock_rdlock(p);
    for (i = 0; i < 100; i++) {
        newx = ACCESS_ONCE(x);
        if (newx != oldx) {
            printf("reader_lock: x: %d\n",x);
        }
        oldx = newx;
        poll(NULL, 0, 1);
    }
    pthread_rwlock_unlock(p);
    return NULL;
}

void* writer_thread(void* arg) {
    int i;
    pthread_rwlock_t* p = (pthread_rwlock_t*)arg;

    pthread_rwlock_wrlock(p);
    for (i = 0; i < 3; i++) {
        ACCESS_ONCE(x)++;
        poll(NULL, 0, 5);
    }
    pthread_rwlock_unlock(p);
    return NULL;
}

int main(void) {
    pthread_t tid1, tid2;
    void *vp;

    pthread_create(&tid1, NULL, reader_thread, &lock_rw);
    pthread_create(&tid2, NULL, writer_thread, &lock_rw);

    pthread_join(tid1, &vp);
    pthread_join(tid2, &vp);

    pthread_rwlock_destroy(&lock_rw);
    printf("Parent process sees x: %d\n",x);

    return 0;
}
// reader_lock: x: 0
// Parent process sees x: 3
```

## Barrier

-   A barrier holds a thread until all threads participating in the barrier have reached it.
-   Barriers can be implemented using a counter, a mutex and a condition variable.
-   A single integer (counter) is used to keep track of the number of threads that have reached the barrier.
-   If the count is less than the total number of threads, the threads execute a condition wait.
-   The last thread entering (and setting the count to the number of threads) wakes up all the threads using a condition broadcast and resets the count to zero (to prepare for the next barrier).

```c
typedef struct {
    pthread_mutex_t cond_lock;
    pthread_cond_t ok_to_proceed;
    int count;
} mylib_barrier_t;

void mylib_init_barrier(mylib_barrier_t* b) {
    b->count = 0;
    pthread_mutex_init(&(b->count_lock), NULL);
    pthread_cond_init(&(b->ok_to_proceed), NULL);
}

void mulib_barrier(mylib_barrier_t* b, int thread_count) {
    pthreadd_mutex_lock(&(b->count_lock));
    b->count++;
    if (b->count == thread_count) {
        b->count = 0;
        pthread_cond_broadcast(&(b->ok_to_proceed));
    } else {
        pthread_cond_wait(&(b->ok_to_proceed), &(b->count_lock));
    }
    pthread_mutex_unlock(&(b->count_lock));
}
```

```c
mylib_barrier_t my_barrier;

void DoStuff(int threadID) {
    int k;
    B[threadID + 1] = 2 * A[threadID];
    mylib_barrier(my_barrier, 4);
    C[threadID] = 2 * B[threadID];
}

int main() {
    mylib_init_barrrier(my_barrier);
    double A[5], B[5], C[5];

    for (i = 0; i < 5; i++) { A[i] = B[i] = i; }
    for (i = 0; i < 4; i++) { pthread_create(..., DoStuff, int i); }
    for (i = 0; i < 5; i++) { pthread_join(..., DoStuff, ...); }
    print_list(C);
}
```

<img src="https://i.loli.net/2020/12/14/hjmruawWgVUn5kd.png" alt="image-20201214175622668" style="zoom:50%;" />

## Deadlocks

-   Four necessary conditions for a deadlock:
    -   **Mutual exclusion**: a resource can be assigned to at most one thread.
        -   Example: a chopstick is a resource. It can be assigned to at most one philosopher at any time.
    -   **Hold and wait**: threads both hold resources and request other resources.
        -   Example: a philosopher holds the left chopstick and requests the right chopstick
    -   **No preemption**: a resource can only be released by the thread that holds it
        -   Example: it is not possible to forcibly take away a chopstick from a philosopher
    -   **Circular wait**: a cycle exists in which each thread waits for a resource that is assigned to another thread.
        -   Example: case of 2  dining philosophers, ABBA-dedlock
        -   ![image-20201214170949131](https://i.loli.net/2020/12/14/LFgqYDlpuSMh8tr.png)
-   Deadlock Prevention

    - Ensure that at least one of four necessary conditions cannot hold
-   Deadlock Avoidance
    - Do not allow a resource request → Potential to lead to a deadlock

    - Requires advance info of all requests

-   Deadlock Detection
    -   Always allow resource requests

    -   Periodically check for deadlocks

    -   If a deadlock exists → Recover from it

