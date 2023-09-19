---
layout: post
title: "Prime Factorization Trees""
date: 2015-01-10
mathjax: true
---


A positive integer can be visualized as a tree, structured by its prime factors. I wrote a little program which takes a positive integer as input, and creates a tree layout that shows its prime factors visually. Here's the tree for 70:

<p align="center">
  <img width="320"  src="/assets/screen-shot-2012-10-07-at-9-55-37-am.png">
</p>

The tree is drawn recursively, starting with a root node in the center of a circular layout. The degree of the root node is the largest prime factor. Then, more prime factors are added recursively (including multiplicities of the same prime factor) in decreasing order of factor, by growing the tree. Finally, the leaf nodes are displayed as filled black circles. As seen from the tree above, the prime factorization of 70 is 7*5*2.

Here is the layout for 700 = 7 * 5 * 5 * 2 * 2:

Screen shot 2012-10-07 at 11.17.22 AM
Screen shot 2012-10-07 at 11.17.22 AM

