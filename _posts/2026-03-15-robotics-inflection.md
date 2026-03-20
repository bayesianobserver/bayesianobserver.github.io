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

#### **Evolution of robotics in brief**

Robotics has seen roughly 3 eras so far. Oversimplifying a lot, these 3 eras have been: 

- Classical robotics: Compute behavior from explicit world models and planners

- Learning-based robotics: Learn behavior from data instead of hand-coding it

- Foundation-model robotics: Learn general, reusable robot behavior by utilizing pre-trained models combining perception, language, and action at scale. This is the current era. 

Let's dwell on the first two eras briefly before describing the latest improvements that have led to the current era in the following section. The robotics problem, simply stated has always been: 'How do we make a robot act correctly in a known world?'. This includes making the robot move through space correctly and safely and making the robot do the things its needs to do. 

In the classical era (1960s to $$\sim$$2015), the system was built as separate modules: perception → planning → control. First estimate the world, then compute a trajectory, then track it with a controller. Intelligence was mostly engineered by humans. The robot depended on explicit models, geometry, and optimization. This worked best in structured settings, but it was brittle in messy, uncertain, open-ended environments. It was hard to hand-specify complex tasks like folding clothes or cleaning a room. Given that we are labelling a very long period of time as the classical period, there were actually a number of approaches and advances during this period, but for our purpose, viz to build up to the current era, we will not go deeper into each innovation of this era here. 

The 2nd era, namely learning based robotics, aimed to replace hand-engineered rules with machine learning systems that can learn _policies_ directly from observations to actions, using demonstrations or reward-based learning. Instead of explicitly programming all the rules, train the robot on examples. The main modeling paradigms to emerge in this era were (a) Reinforcement Learning (RL) and (b) Imitation learning via behavior cloning (BC). Each moved the field forward in a different way. RL successfully enabled the learning of motion control policies by learning inside simulations. That is, instead of programming how a specific robot with a specific 3D geometry and mass should move via its control actuators, digitally representing the 3D geometry and mass, as well as various spatial courses through which the robot must move, allowed the learning of general policies for robotic control. Simulation offers infinite training data, but generally induces a gap between reality and sim, making learning from sims highly sensitive to how realistic the sims are. A core idea that enabled transfer learning from RL policies learnt in simuation to the real world was _domain randomization_. The core idea was simple: randomize the simulator so much (texture, object shapes \& sizes, camera position, physics parameters) that the real world looks like just another variation. MuJoCo (Multi-Joint dynamics with Contact) is an example of a physics simulator, maintained by DeepMind. RL has proved successful for locomotions tasks: walking, running, jumping, etc. as well as dextrous manipulation, balancing, stablization. These are all cases where it is easy to specify a reward (make progesss, dont fall down). But after having learnt basic locomotion and stability control, what if a general purpose robot needs to perform a new high level task, like "lift a large bag off a conveyor belt"? Instead of teaching this in sim, another approach is to provide expert demonstrations of a human performing the action and then making the robot clone the action, using lots of demonstration data. This is called Behavior Cloning, and can also be placed in the 2nd era of robotics. BC is useful when good behavior is easy to demonstrate but hard to codify as a reward in sim based learning. In practice, RL-learnt policies for basic control \& stability and BC-learnt policies for specific tasks are used together for making a robot perform specific tasks. However, one can see that this combination has several gaps: 

* Lack of generalization: policies are task-specific. There is no notion of abstraction of compositional tasks. 
* No semantic understanding: The RL + BC combo does not really undserstand the world semantically, say in the way that language repreesntations do. 
* Data bottleneck: BC needs a large amount of specialized demo data to be created. RL learning needs a lot of in-sim learning. 
* No shared world model: Each policy learns a task from scratch, in isolation. There is no shared understanding of world objects or physics. 
* Pure BC has a covariate shift problem: in a live setting the robot can enter a state that is rarely or never found in the expert demo dataset.

These gaps are what the curent 3rd geneation of robotics tries to address. 


#### **Recent advances** 

Learned policies from the 2nd generation of robotics work, but they are still too narrow. How do we make robots more general, more reusable, and better at understanding human instructions? The excitement in the robotics community today can be attributed to recent applications of AI based approaches that attempt to answer these questions. These methods generally use large-scale pre-trained foundational models that combine vision, language, and action to bring visual input, language instruction and action sequences that follow into a shared representation space. The robot is trained more like a general-purpose model than a task-specific controller. The shift is from learning individual skills to learning a broad prior over the world, language, and behavior. 

The key advances/papers so far in this era can be summarized by the progression RT-1 --> RT-2 --> 

* RT-1 (Robot Transfomer 1): The core idea is to train a single Transformer-based robot policy that takes as input (a) images from the robot’s cameras and (b) a natural-language instruction, and outputs robot actions. The policy is trained using expert demonstrations, so it is fundamentally a large-scale behavior-cloning system. The key advance is that one shared model is trained across many tasks, rather than training a separate policy for each task. Vision and language together provide the context that tells the model what task is being requested in the current scene, allowing it to learn a shared representation across tasks. RT-1 tokenizes its inputs and predicts discretized action tokens, so the problem becomes: conditioned on visual observations and a language instruction, predict the next robot action token sequence. A typical example would be showing the robot a table with several objects and giving an instruction such as “pick up the pen,” then training on expert demonstrations of the correct action. Architecturally, RT-1 uses an ImageNet-pretrained EfficientNet vision backbone, conditions it on the language instruction, compresses the resulting features into tokens, and then uses a Transformer to predict discretized robot actions. 

* RT-2 (Robot Transformer 2): RT-1 uses the vision model as a pre-trained feature extractor to get vision tokens and combines them with launguage tokens to predict action tokens. However, all the intelligence comes from robot data rather than from pretrained semantic knowledge. RT-2 goes one step further: rather than using vision mainly as a feature extractor, it starts from a Vision-Language Model (VLM), whose representations are already grounded in large-scale image-text data from the web. This means the model brings in prior semantic knowledge about objects, categories, attributes, and simple relationships. The result is that language is no longer just a narrow task-conditioning signal; it can invoke broader concepts. So while RT-1 mainly learns to imitate demonstrated behaviors across many tasks, RT-2 can better generalize to instructions that require semantic interpretation, such as selecting an object by its use or by a higher-level description. In short, RT-2 keeps the same broad goal—mapping visual observations and language instructions to robot actions—but augments it with pretrained world knowledge.

- Diffusion policy: Separate from the use of internet-scale foundation VLM models for robot training, a parallel development has been the use of diffusion models to learn a multi-modal distribution of actions when learning to map image and launguage instruction encodings to expert actions. This is useful because there is often not just a singe correct action pertaining to a given context, i.e. the space of correct actions that a robot could perform, is multi-modal. This paper proposes learning a distribution over action sequences (trajectories) using a DDPM-style diffusion model, rather than point predictions of actions. 


A number of other VLA models have appeared more recently—OpenVLA, GR00T, and others—that move in the direction of a GPT-like foundation model for robotics. The core idea is to train a single, large model on diverse datasets spanning many robots, environments, and tasks, so that it learns a general-purpose mapping from vision and language inputs to actions. Instead of building task-specific policies, these systems aim to learn a broad prior over how to act in the physical world, enabling transfer across tasks and even across different robot embodiments. Much like GPT models in language, the hope is that scale—both in data and model size—combined with a unified architecture over vision, language, and action, will yield emergent capabilities such as compositional task execution, few-shot adaptation to new tasks, and more robust generalization in real-world settings.



#### **Challenges still remaining**

As far as I can tell, we are nowhere close to a general purpose humanoid robot at an acceptable level of fidelity. 

-- Covariate shift in live deployment: This is still one of the central technical bottlenecks. In imitation learning, a policy is trained on states visited by an expert demonstrator or teleoperator. But at deployment time, small errors in perception, actuation, latency, calibration, or contact can push the robot into states it never saw during training. Then the policy is effectively forced to extrapolate. In a manipulator benchmark that may mean a failed pick; in a humanoid it may mean a stumble, a collision, or a fall. RT-1-style behavioral cloning and even diffusion-style policies improve data efficiency and expressivity, but they do not remove the basic off-distribution problem [2][4]. Addressing this will likely require some combination of online data aggregation, better recovery behaviors, uncertainty-aware planning, and more robust lower-level control.


-- Hand grasping
-- continuous learning
-- World models

#### **Path to humanoids at home**

-- pets @ home
-- humanoids @ factories, warehouses


#### **References**

1. Open VLA
2. RT1
3. RT2
4. Diffusion policy
5. The State of Robot Motion Generation
6. Domain Randomization for Transferring Deep Neural Networks from Simulation to the Real World
7. DDPM 

#### **Gloassary**

- Classical robotics: 

- Domain randomization: 

- Imitation learning

- Learning from Demonstration

- Model based control

- MuJoCo

- Perception to action

- Policy

- TeleOperation

- VLA model: 

- VLM model: 

- Visuomotor policy: 

