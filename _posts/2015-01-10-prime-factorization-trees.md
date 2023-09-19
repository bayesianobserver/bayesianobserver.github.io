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

This method of displaying numbers has been proposed and implemented by others on the internet, with much prettier results. I was too tempted to quickly try it for myself using a graph visualization library, because the graph drawing library can do all the heavy lifting. I used Graphviz (developed at AT&T Labs) which I use often for visualizing network data. I also wanted to see if the underlying tree structure revealed by the edges in the graph makes the prime factorization more evident.

Here are a few more trees:

243 = 3^5:

Screen shot 2012-10-07 at 11.44.01 AM
Screen shot 2012-10-07 at 11.44.01 AM

43 (a prime):

Screen shot 2012-10-07 at 10.04.39 AM
Screen shot 2012-10-07 at 10.04.39 AM

128 = 2^7:

Screen shot 2012-10-07 at 11.04.56 AM
Screen shot 2012-10-07 at 11.04.56 AM

121 = 11 * 11:

Screen shot 2012-10-07 at 10.55.17 AM
Screen shot 2012-10-07 at 10.55.17 AM

625 = 5^4:

Screen shot 2012-10-07 at 11.42.04 AM
Screen shot 2012-10-07 at 11.42.04 AM

2310 = 11 * 7 * 5 * 3 * 2:

Screen shot 2012-10-07 at 11.09.27 AM
Screen shot 2012-10-07 at 11.09.27 AM

Code gist (Without prime factorization implementation and graph library):

[sourcecode language="python"] def createnode(x): # x == 1: support node # x == 0: real node global nodenames name = random.random() while name in nodenames: name = random.random() nodenames.add(name) if x == 1: retval = '"'+str(name)+'"'+whitenode else: retval = '"'+str(name)+'"'+blacknode print retval return '"'+str(name)+'"'

def createedge(x,y,t): # x and y are nodes, t is type (0=last stage of the tree, 1=all other stages) if t == 1: print x + '--' + y + ' [color="#DDDDDD"]' if t == 0: print x + '--' + y + ' [color=grey]' return x + '--' + y

pf = factorization(n) # keys are factors, values are the multiplicity of the prime factors factors = [] for fac in pf: for multiplicity in range(0, pf[fac]): factors.append(fac) factors = sorted(factors, reverse=True) print 'graph G{' print 'overlap = false' nodenames = set() edgeset = set() whitenode = ' [fixedsize=True, width=0.1, height=0.1, color = white, fontcolor = white, shape = circle]' blacknode = ' [color = black, style = filled, fontcolor = black, shape = circle]' rootnode = createnode(1) currentset = set() currentset.add(rootnode) level = len(factors) + 1 for i in range(0, len(factors)): level -= 1 f = factors[i] nodetype = 1 if i == len(factors) - 1: nodetype = 0 newnodeset = set() for eachnode in currentset: for j in range(0, f): newnode = createnode(nodetype) newnodeset.add(newnode) edgeset.add(createedge(eachnode, newnode, level, nodetype)) currentset = newnodeset print '}' [/sourcecode]

For prime factorization, I used the this implementation.
