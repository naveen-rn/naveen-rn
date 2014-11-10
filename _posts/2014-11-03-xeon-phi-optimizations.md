---
layout: post
title: Optimizations for Xeon Phi - Vectorization.
categories: systems programming
tags: 
  - systems programming
  - memcpy
  - memory bandwidth
comments: false
mathjax: null
featured: true
published: true
---
"A highly optimized and performance tuned software for Intel Xeon Phi must be highly scalable, highly vectorized and make efficient use of memory"

Vector operations can be considered as a single instruction executed on a multiple data. In general we can provide a crude example on how this vector operations look like;
Considered the following loop:

    for (i = 0; i < n; i++)

        a[i] = b[i] + c[i]


A scalar operation will look like this:

    execute this loop 'n' times

        read instructions and decode it

        fetch a[i]

        fetch b[i]

        add them

        put the result in this location

    end loop

The same loop in a vector operation will look like this:

    read instruction and decode it

    fetch n items from a[i]

    fetch n items from b[i]

    add them respectively

    put the result in this location

This will largely influence the cache miss and cache hit, which will in-turn the interfere with the execution time. Hence, vectorizing the code is considered to be an important of optimization and tuning. Compilers are trained to do auto-vectorization. But, relying completely on the compiler to do vectorization is not considered to be a sensible thing.

The current generation of Intel Xeon Phi Many Integrated Core(MIC) architectures are sold in the commercial name Knights Corner. It has 61 cores with 4 threads per physical core and 512 bit registers for SIMD operations. Among the other features one important areas of tuning the application is with this 512 bit registers for SIMD operations.

Programmers should take care to effectively utilize this large SIMD operations and vectorizing the code to produce a completely optimized and tuned software application.

1. Using the proper array notation,
2. Implementing the elemental function, 
3. Making use of Directives and Pragmas are some of the ways through which we can optimize the code. 

**Array Notation**

The below loop can be expressed in Fortran 90 with the following notation:

    for (i = 0; i < n; i++)

        a[i] = b[i] + c[i]

In Fortran 90, it would look like:

    a[0:n:1] = b[0:n:1] + c[0:n:1]

or

    a[0:n] = b[0:n] + c[0:n]

This has been utilized in Intel Cilk plus(parallel programming library) and we can use this in vectorizing the following loop:

**Elemental Function**

An elemental function can considered as a template in C++. We can utilize this in vectorizing the following loop:

    __attribute__(vector (optional clauses))void MyVecMult(double *a, double *b, double *c)

    { c[0] = a[0] * b[0] ; return ;}

as either

    for (i = 0; i < n; i++)

        MyVecMult(a[i], b[i], c[i])

or as 

    MyVecMult(a[:], b[:], c[:])


**Directives and Pragmas**

Making use of #pragma ivdep or #pragma simd can also help us in vectorizing the code easily. But make sure to use them appropriately. 

The above steps in vectorizing and tuning the application are the basic steps to see a visible optimization. This [link](https://software.intel.com/en-us/articles/optimization-and-performance-tuning-for-intel-xeon-phi-coprocessors-part-1-optimization) provides a brief instruction on the same.

To end, Xeon Phi co-processor instruction set is available in this [location](https://software.intel.com/sites/default/files/forum/278102/327364001en.pdf).