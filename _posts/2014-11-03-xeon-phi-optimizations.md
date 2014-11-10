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

The current generation of Intel Xeon Phi Many Integrated Core(MIC) architectures are sold in the commercial name Knights Corner. It has 61 cores with 4 threads per physical core and 512 bit registers for SIMD operations. Among the other features one important areas of tuning the application is with this 512 bit registers for SIMD operations.

To begin with the main Xeon Phi co-processor instruction set is available in this location(https://software.intel.com/sites/default/files/forum/278102/327364001en.pdf).