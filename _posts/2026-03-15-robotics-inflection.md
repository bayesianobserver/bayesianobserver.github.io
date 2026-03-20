---
layout: post
title: "Humanoid robots"
date: 2026-03-15
mathjax: true
---

There is perceptible excitement in the humanoid robotics industry these days. Personally, I think this is the most exciting space to be working in today -- because the promise of a fully autonomous, continuously learning, humanoid robot, is within reach. A number of startups are seriously working on developing a humanoid robot: Tesla, 1x, Figure, Boston Dynamics, Agility, Apptronik. This means there is a significant amount of capital betting on either a complete humanoid, or significant unlocking of capability to count as partial progress toward that goal. Not all robotics companies started as 'AI-first' -- several started with a focus on the mechatronics/hydraulics and hand-engineered rules for movement -- but there is a kind of convergence in progress I think, whereing most companies have realized that it is better to use data to learn behavior policies than to explicitly program robots with rules. 


It feels to me like robotics might be at an inflectinon point, turning from a field dominated by impressive demos, academic research and special-purpose factory-robots, to a field that can progressively yield to improvements in engineering, models and scale of data, to show a path to a functioning, relaible humanoid robot within say 5-10 years.

In this note, I want to summarize my recent readings: 
-- Recent developments that are stirring excitement in the robotics world (behavior cloning, VLA models ++), and 
-- The challenges that have yet to be solved. 

#### Classical robotics




#### Recent advances: 

There is perceptible excitement humanoid robotics community these days, and I think it arises from recent applications of AI based approaches to humanoids. 

- VLA (Vision Language Action) models, RT-2 (Robot Transfomer 2): answer the question "what should I do?"

- RT-1 (Robot Transfomer 1), Policy Diffusion: answer the question "how should I do it?"

- Systems are built around a data flywheel (teleop → train → deploy → retrain) that will likely improve all involved AI model as scale of data increases. 

- Training in simulation

- Perception + planning are jointly learned or tightly coupled (similar to what's happeneing in the autonomous vehicle industry). 


The general purpose humanoid design problem can be split into: (1) how a robot should move in a space occupied with other objects, humans and robots, and (2) specific tasks that the humanoid should be capable of doing, like folding clothes, doing dishes, etc. The former problem is a harder version of the problem that autonomous vehicle companies have been chipping away at. The road network had well defined paths and rules that are in general absent from spaces that human inhabit, like a home or a factory floor. Still, if we are to have humanoids that can safely move in the same space as humans (and other humanoids), I believe many of the same priciples should apply: perception, followed by joint [prediction <--> planning]. While the perception stack is realtively mature, the prediction <--> planniner stack is still evolving, and I think the humanoid community can probably leverage a lot of existing work from the the autonomous vehicles community.

RT-1 (2023), and Policy Diffusion (2023) address the problem of how a robot should move in space given what it needs to do, i.e. motion planning

RT-1: 

Policy diffusion: 

VLA Models: RT-2, Open VLA, RTX, GR00T: Vision Language Models are a relatively recent development. They enable the use of large-scale semantic knowledge to inform robot action. RT-2 takes the basic RT-1 idea and strengthens it by grounding the robot policy in a pretrained vision-language model [3]. That means the system is no longer learning only from robot trajectories; it is also inheriting visual and semantic structure learned from internet-scale vision-language data. This allows richer instruction following and some degree of semantic generalization: for example, a model may understand concepts like “pick up something edible” or “place the object that belongs in the drawer,” even if that exact phrasing or object combination was not seen in robot training data [3].

More broadly, VLA models learn mappings from vision + language → action, and are best viewed as answering the question: what should I do next, given this scene and this instruction? They are not usually the right abstraction for direct torque control or high-frequency whole-body stabilization. Rather, they sit at the semantic decision layer and output subgoals, action chunks, end-effector intents, or latent action representations that downstream controllers and visuomotor policies can execute.

OpenVLA is an open large-scale VLA model trained on robot demonstrations [1]. Its significance is partly scientific and partly practical: it makes the VLA paradigm more reproducible and more usable outside a few large labs. RT-X is related in spirit, emphasizing training on a very broad cross-embodiment dataset and leveraging data from many robot platforms. GR00T and similar efforts are especially interesting for humanoids because they explicitly point toward a layered stack in which semantic interpretation, skill generation, and whole-body execution are separate but connected.


#### Challengs: 

-- Covariate shift in live deployment: This is still one of the central technical bottlenecks. In imitation learning, a policy is trained on states visited by an expert demonstrator or teleoperator. But at deployment time, small errors in perception, actuation, latency, calibration, or contact can push the robot into states it never saw during training. Then the policy is effectively forced to extrapolate. In a manipulator benchmark that may mean a failed pick; in a humanoid it may mean a stumble, a collision, or a fall. RT-1-style behavioral cloning and even diffusion-style policies improve data efficiency and expressivity, but they do not remove the basic off-distribution problem [2][4]. Addressing this will likely require some combination of online data aggregation, better recovery behaviors, uncertainty-aware planning, and more robust lower-level control.


-- Hand grasping
-- continuous learning
-- World models

#### Path to humanoids at home

-- pets @ home
-- humanoids @ factories, warehouses


### References

1. Open VLA
2. RT1
3. RT2
4. Diffusion policy
5. The State of Robot Motion Generation

### Gloassary

- Classical robotics: 

- Imitation learning

- Learning from Demonstration

- Model based control

- MuJoCo

- Perception to action

- TeleOperation

- VLA model: 

- VLM model: 

- Visuomotor policy: 

