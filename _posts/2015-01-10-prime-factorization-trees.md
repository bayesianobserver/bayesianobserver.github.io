---
layout: post
title: "Prime Factorization Trees"
date: 2015-01-10
mathjax: true
---


A positive integer can be visualized as a tree, structured by its prime factors. I wrote a little program which takes a positive integer as input, and creates a tree layout that shows its prime factors visually. Here's the tree for 70:

<p align="center">
  <img width="320"  src="/assets/screen-shot-2012-10-07-at-9-55-37-am.png">
</p>

```
def createnode(x):
    # x == 1: support node
    # x == 0: real node
    global nodenames
    name = random.random()
    while name in nodenames:
        name = random.random()
    nodenames.add(name)
    if x == 1:
        retval = '"'+str(name)+'"'+whitenode
    else:
        retval = '"'+str(name)+'"'+blacknode
    print retval
    return '"'+str(name)+'"'
 
def createedge(x,y,t):
    # x and y are nodes, t is type (0=last stage of the tree, 1=all other stages)
    if t == 1:
        print x + '--' + y + ' [color="#DDDDDD"]'
    if t == 0:
        print x + '--' + y + ' [color=grey]'
    return x + '--' + y
 
pf = factorization(n) # keys are factors, values are the multiplicity of the prime factors
factors = []
for fac in pf:
    for multiplicity in range(0, pf[fac]):
        factors.append(fac)
factors = sorted(factors, reverse=True)
print 'graph G{'
print 'overlap = false'
nodenames = set()
edgeset = set()
whitenode = ' [fixedsize=True, width=0.1, height=0.1, color = white, fontcolor = white, shape = circle]'
blacknode = ' [color = black, style = filled, fontcolor = black, shape = circle]'
rootnode = createnode(1)
currentset = set()
currentset.add(rootnode)
level = len(factors) + 1
for i in range(0, len(factors)):
    level -= 1
    f = factors[i]
    nodetype = 1
    if i == len(factors) - 1:
        nodetype = 0
    newnodeset = set()
    for eachnode in currentset:
        for j in range(0, f):
            newnode = createnode(nodetype)
            newnodeset.add(newnode)
            edgeset.add(createedge(eachnode, newnode, level, nodetype))
    currentset = newnodeset
print '}'
```
