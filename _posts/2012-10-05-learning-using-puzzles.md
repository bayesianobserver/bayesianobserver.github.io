---
layout: post
title: "Learning using Puzzles"
date: 2012-10-05
original_url: "https://thebayesianobserver.wordpress.com/2012/10/05/learning-using-puzzles/"
categories: ["creativity", "learning", "math", "productivity"]
---
Mathematical and logic puzzles are a great way to learn. I think they should be used to a greater extent in school and college education than they are, because they:

1. Create an excitement in the mind of the student/solver.
2. Force the solver to think about what method to use to attack the problem. This is much closer to real world situations, where one is not told about what area a problem is in. Tech companies recognize this when they use puzzles  while interviewing job candidates as a way to observe how the candidate thinks.
3. Over time, allow students to recognize patterns in problems and the best way to attack them, so that wehn they are faced with a new, real world problem, they have a good idea of what to try first.

I am certainly [not the first one](http://cs.adelaide.edu.au/~zbyszek/Papers/PBL.pdf) to note the educational value ofpuzzles. Martin Gardner, whose puzzles I have tremendously enjoyed has himself advocated for puzzle-based learning.

Each puzzle is usually based on one (or, sometimes two, but very rarely more than two) fundamental areas of math: probability, number theory, geometry, critical thinking etc. For example, take the following puzzle (try these puzzles before reading answers at the end of the post):

[1] By moving just one of the digits in the following equation, make the equation true:

![62 - 63 = 1](/images/learning-using-puzzles-img-1.php)

It should be clear that this puzzle is part math and part logic.

Often there is more than one way to arrive at the solutions — e.g. using a geometric visualization for a algebraic problem in 2 or 3 variables. For example take the following puzzle:

[2] A stick is broken up into 3 parts at random. What is the probability that the thee parts form a triangle?

One may choose to solve the above problem using algebra, but it can be visualized geometrically too.

Speaking of geometric methods, there is also something to be said about solving puzzles inside one’s head, rather than using pen and paper. I feel it adds to the thrill because it can be more challenging. It is also fun to visualize objects and their relationships in mathematical terms,  completely inside one’s head. The following is an example of a pretty hard puzzle, which was solved entirely inside one mathematicians head :

[3] Peter is given the product of two integers both of which are between 2 and 99, both included. Sally is given only their sum. The following conversation takes place between them:

P: I cannot figure out the two numbers from the product alone.

S: I already knew that you couldn’t have figured them out.

P: Oh, now that you say that, I know what the two numbers are.

S: I see. Now that you say you know what they are, I also know what they are.

What are the two integers?

\_\_\_

ANSWERS:

[1] ![2^6 - 63 = 1](/images/learning-using-puzzles-img-2.php)

[2] Without loss of generality, assume that the stick is of unit length. Since the three lengths add up to 1, and are each ![\in [0,1]](/images/learning-using-puzzles-img-3.php), they can be treated as three random variables ![(x,y,z)](/images/learning-using-puzzles-img-4.php) in 3D space, lying on the 2-dimensional triangular simplex with vertices at (1,0,0), (0,1,0) and (0,0,1). The problem now boils down to determining what fraction of the surface of this triangle corresponds to tuples that cannot form a triangle. From the triangle inequality, we know that ![x + y > z](/images/learning-using-puzzles-img-5.php) and so on for the other two pairs. A little mental visualization reveals that these boundary conditions are met when each side of these inequalities is ![\frac{1}{2}](/images/learning-using-puzzles-img-6.php). The region corresponding to feasible points is a smaller equilateral triangle inscribed within the simplex and is one-fourth the area of the simplex. The answer therefore must be ![\frac{1}{4}](/images/learning-using-puzzles-img-7.php).

[3] The answer can be found in this [PDF](http://www.cs.utexas.edu/users/EWD/ewd06xx/EWD666.PDF) of a note written by EW Dijkstra, who solved the problem in his head.
