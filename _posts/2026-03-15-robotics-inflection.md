---
layout: post
title: "Humanoid robots"
date: 2026-03-15
mathjax: true
---

There is perceptible excitement in the humanoid robotics industry these days. Personally, I think this is the most exciting space to be working in today -- the promise of a fully autonomous, continuously learning, humanoid robot, is within reach. A number of startups are seriously working on developing a humanoid robot: Tesla, 1x, Figure, Boston Dynamics, Agility, Apptronik. This means there is a significant amount of capital betting on either a complete humanoid, or significant unlocking of capability to count as partial progress toward that goal. Not all robotics companies started as 'AI-first' -- several started with a focus on the mechatronics/hydraulics and hand-engineered rules for movement -- but there is a kid of convergence in progress I think, whereing most companies have realized that some form of learnt policies using data are more scalable (whether imitation learning via pure behavior cloning, or inverse RL, or generative modeling). 


It feels to me like robotics might be at an inflectinon point, turning from a field dominated by impressive demos, academic research and special-purpose factory-robots, to a field that can yield to engineering improvements, AI advances and large scale data collection, to show a path to a functioning, relaible humanoid robot within say 5-10 years. 

In this note, I want to summarize my recent readings: 
-- Recent developments that are stirring excitement in the robotics world (behavior cloning, VLA models ++), and 
-- The challenges that have yet to be solved. 


Recent advances: 

There is perceptible excitement humanoid robotics community these days, and I think it arises from recent applications of AI based approaches to humanoids. 

-- VLA (Vision Language Action) models, RT-2 (Robot Transfomer 2): answer the question "what should I do?"
-- RT-1 (Robot Transfomer 1), Policy Diffusion: answer the question "how should I do it?"
-- Systems are built around a data flywheel (teleop → train → deploy → retrain) that will likely improve all involved AI model as scale of data increases. 
-- Perception + planning are jointly learned or tightly coupled (similar to what's happeneing in the autonomous vehicle industry). 


The general purpose humanoid design problem can be split into: (1) how a robot should move in a space occupied with other objects, humans and robots, and (2) specific tasks that the humanoid should be capable of doing, like folding clothes, doing dishes, etc. The former problem is a harder version of the problem that autonomous vehicle companies have been chipping away at. The road network had well defined paths and rules that are in general absent from spaces that human inhabit, like a home or a factory floor. Still, if we are to have humanoids that can safely move in the same space as humans (and other humanoids), I believe many of the same priciples should apply: perception, followed by joint [prediction <--> planning]. While the perception stack is realtively mature, the prediction <--> planniner stack is still evolving, and I think the humanoid community can probably leverage a lot of existing work from the the autonomous vehicles community.

Challengs: 

-- Covariate shift in live deployment
-- Hand grasping
-- continuous learning
-- World models


### References

1. Open VLA
2. RT1
3. RT2
4. Diffusion policy


