---
layout: post
title: "Machine learning and Programming Languages"
date: 2012-02-24
original_url: "https://thebayesianobserver.wordpress.com/2012/02/24/machine-learning-and-programming-languages/"
categories: ["machine-learning"]
---
I have been thinking quite a bit about the best language to write machine learning algorithms in. While this depends on the exact algorithm in questions, there are certain constructs and tasks that show up in many algorithms. As I work through this, I’ll publish my notes here on this blog as I go along.

There seems to be a fairly clear tradeoff between the speed of computation and the speed of development. For example, the speed of computation is best with low level languages like C/C++, but writing code can be cumbersome and time consuming. On the other hand, high level languages like R and Python offer very quick development times and have a good number of libraries/packages developed by the community, but have very poor computational performance. For this reason most professional environments seem to adopt the approach of first hacking in a high level language like R and then writing production quality code in C or C++. I have been hearing this quite a bit recently both within AT&T, as well as from other friends doing machine learning work in other industries, and most recently at the [NY linux user group’s meeting about R](http://www.meetup.com/nylug-meetings/events/45922022/). The tradeoff between performance and development time is important for me at AT&T because I often need to deal with very large volumes of data, often both in terms of sample size as well as dimensionality.

Programming languages are known to be good at specific things and not necessarily generalizable to all types of tasks. I will use this post as a working document to summarize the best practices in the use of picking the right languages/features for writing and running machine learning algorithms and why. Often, the type of computation needed by a class of machine learning algorithms (e.g. MCMC require repeated sampling in a sequential manner making parallelizeability difficult) suggests the type of language features that would be useful. Other times, the mapping is not so obvious.

**Matlab/Octave:** Expensive for individual users. Quite powerful, the many toolboxes that are available (for a price) make it worthwhile. Fast development time. Octave is the free open source version of Matlab, but does not include all its functionality. I don’t know if special toolboxes for Octave exist.

**Java:** I have no real experience with writing machine learning algorithms or using other people’s ML code in Java.

**R:** Open source, big community, large number of packages, slower than Python and Java, similar in speed to Octave. the large number of packages available makes it very attractive as the language for initial hacking on a learning problem. R also has very good built-in visualization. All these factors make R very very useful for *interactively* work with data.

**Python:** Python is my personal favorite language to write code in, so I may be biased, but there are good technical reasons for that bias. Python is open source, it has a huge user community, and a number of good packages for machine learning. Matplotlib/pylab are packages that offer good solid visualization, IMO comparable to R’s visualization.  The design of Python stresses good code readability. It is a full fledged language offering simple objected oriented design. The only downside to Python is its execution speed. In many cases, this can be overcome by careful optimization of the data structures. Various efforts have been made to improve the speed of Python. [PyPy](http://pypy.org/) is a just-in-time compiler for Python that can sometimes speed up your Python code, depending on what it does. [Cython](http://www.cython.org/) allows for low level optimization using C by first translating Python code to equivalent C code.

**C/C++:** Best in performance. Use only if (i) other approaches prove too slow for the problem at hand, or (ii) if a well-tested library is already available (there are lots of unbaked, buggy libraries out there), or (iii) the code needs to go into production or a real-time system in which  performance is important (e.g. finance). Some good libraries: SVMlight, liblinear. The boost set of libraries usually proves to be pretty useful, especially when dealing with a learning algorithm that afford parallelism. C and C++ are often clubbed together in discussions on programming languages, but there is a lot of difference between the two. Personally, I have spent more time with C than C++.  C is cleaner than C++. In terms of ease of coding and  readability, C++ is an ugly language. [Here](http://harmful.cat-v.org/software/c++/linus) is what Linus Torvalds had to say about C++.

**[Torch 7](https://github.com/andresy/torch)** is a recently (NIPS, Dec 2011) released library in C++/GPL for writing ML algorithms and interfaces with a scripting language called Lua. In their words. it provides “*a Matlab-like environment for state-of-the-art machine learning algorithms. It is easy to use and provides a very efficient implementation, thanks to an easy and fast scripting language (Lua) and a underlying C implementation.”*I am told that Torch7 + Lua is a good combination for writing neural networks, but I haven’t verified this myself yet. I wish they had interfaced Torch 7 with Python instead of Lua, but in their [words](http://publications.idiap.ch/downloads/papers/2011/Collobert_NIPSWORKSHOP_2011.pdf):

[![](/images/machine-learning-and-programming-languages-img-1.png "Screen shot 2012-02-27 at 5.33.40 PM")](https://thebayesianobserver.wordpress.com/wp-content/uploads/2012/02/screen-shot-2012-02-27-at-5-33-40-pm.png)

For neural networks, I have used R’s nnet package (very mature, included in the base distribution), and toyed briefly with the lisp-like language Lush (also mature, but has a sttep learning curve if you havent played with functional languages like lisp/scheme before), developed by Yann lecun.

[Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit/wiki) is another C++ library (with Boost as a dependency) with a focus on online learning, that I haven’t yet tried but have heard about quite a bit. Claims by the authors of vw include high speed and scalability. Will post an update here after I try it.

The dream language for machine learning: Fast development, very good performance. Close to english (like Python) but compiled and optimized (like C) instead of interpreted. It sounds like these qualities have little to do with machine learning, but are desirable for most tasks.

Writeups by other people on the topic of best programming languages for machine learning (I will continue to add to this list as I find them):

> 1. [Hoyt Koepke](http://www.stat.washington.edu/~hoytak/blog/whypython.html) on why Python rocks for use in machine learning (and scientific computing in general).
> 2. [Two](http://darrenjw.wordpress.com/2011/07/31/faster-gibbs-sampling-mcmc-from-within-r/) [writeups](http://darrenjw.wordpress.com/2011/07/16/gibbs-sampler-in-various-languages-revisited/) by Darren Wilkinson on empirical evaluations of R, Java, Python, Scala and C for MCMC based learning, in particular for Gibbs Sampling (a type of MCMC algorithm).
> 3. John Langford has a [nice wiretup](http://hunch.net/?p=230) discussing various aspects important to the choice of language for machine learning.
