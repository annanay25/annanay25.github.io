---
layout: post
title: Google Summer of Code with LLVM.
---

Exciting things are happening, as, for the next few months, I will be working on Enabling Polyhedral compilation in TensorFlow as part of the LLVM community in Google Summer of Code - the annual program by Google to promote Open Source contributions by remote developers. 

#### What is Polyhedral Compilation?

Polyhedral compilation is a way of modelling iterations of loop nests into points on a multidimensional space. Each dimension of the space represents one level of the loop nest and every point in the space refers to the state (or the value of the loop iterators) in one execution of the loop statement. Once this is done, we run a dependence analysis on the loop to check which instances of the loop statement execution depend on each other and hence may cause hindrance to parallelize the loop.  

For example: Consider the following loop nest -  


    for (i = 1; i < N; i++)    
      for (j = 1; j < M; j++)    
        A[i][j] = SCALAR_VAL(0.5) * (A[i-1][j] + A[i][j-1]);  
        

In this case, observe that since evaluation of ```A[i][j]``` depends on its neighbors ```A[i-1][j]``` & ```A[i][j-1]```, there is a dependence in the sense that we cannot evaluate the value of ```A[i][j]``` before we evaluate the value of ```A[i-1][j]``` & ```A[i][j-1]``` (they themselves are dependent on ```A[i-2][j]``` & ```A[i-1][j-1]``` and ```A[i-1][j-1]``` & ```A[i][j-2]``` and so on…). Hence, we get a dependence graph on the iteration kernel. This is called the _Dependence Polyhedron_.  

A single step in polyhedral compilation captures what corresponds to a sequence of several textbook loop optimizations. Transforming the dependence polyhedron through skewing, rotating, etc. exposes parallelism that can even be visually identified. Tools like [CLooG](https://www.cloog.org/) - The Chunky Loop Generator, help with these transformations.  

We have seen that Polyhedral compilation is a flexible and expressive framework. However, it can only be used for loops that contain statically predictable control flow.  
Loop nests in which statements use affine accesses (Linear function of induction variable and program parameters) of array elements are called Static Control Parts.


#### How do we use this powerful mathematical representation?  
Although Polyhedral compilation as a concept has been applied to compute intensive fields like Linear algebra kernels, Stencil computations, Differential equation solvers, etc, its use in Deep Learning Frameworks is limited. One such related work is through the [Polymage project at IISc, Bangalore](http://mcl.csa.iisc.ac.in/polymage.html). The project implements a Image processing pipeline and performs automatic parallelization through Polyhedral techniques.

My aim is to incorporate Polyhedral compilation in TensorFlow through Polly-enabled-LLVM. The tensorflow community recently open-sourced a JIT compiler [XLA](www.tensorflow.com/performance/xla), that has low latency implementations for several linear algebra kernels. ( XLA stands for X(acc)ellarated Linear Algebra ) Through this, TensorFlow achieves very high performance throughput that can be built upon with Polyhedral compilation.  

For detailed information on how I plan to do this, feel free to go through my proposal [here](https://docs.google.com/document/d/1mVZTiBrlf6g2bWwO0XUUku1YUsvDBI-pUK3FZgjIFkE/edit).

In my next post, I plan on writing about [Polly](polly.llvm.org), An LLVM framework for high level loop and data locality optimizations.  
