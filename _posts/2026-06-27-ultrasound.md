---
layout: post
title: "Ultrasound is ripe for AI"
date: 2026-06-27
mathjax: true
kramdown:
  math_engine: mathjax
---

<p align="center">
<img width="400" src="/assets/ultrasound.png" alt="Ultrasound imaging">
</p>

Among the various imaging modalities in medicine, ultrasound stands out as an odd man out:


* MRI, CT and X-ray are based on electromagnetic radiation, whereas ultrasound, as the name suggests, is based on sound waves. This is interesting because radiation exposure can be harmful to pregnant women and their foetuses, and too much radiation can be harmful to anyone -- in contrast, ultrasound is relatively harmless.

* MRI, CT and X-rays are standardized, in the sense that they do not require a trained technician to expertly maneuver an imaging probe. Instead, the patient gets into position inside a machine and the machine produces an image with little skill needed from the machine operator. In contrast, ultrasound is manual-labor-intensive. A technician does the following in a closed loop: an ultrasound probe emits a directional sound pulse and catches the reflections from tissue boundaries in the body, and this is meant to 'illuminate' a 2D slice of the patient's body. The 2D image on the screen shows an estimate of the intensity of echoes at each depth and sweep angle for a specific 2D slice that a probe is pointing to. In order to image the target organ and extract a target piece of information (e.g. the size of a foetus' heart), the technician must interpret the 2D image being displayed on a screen, and adjust her probe's position and angle. This manual operation is a bottleneck because in the absence of trained technicians make this technology unavailable, or worse, incorrectly interpreted by untrained individuals, in rural parts of the world. It also makes the quality of clinical information derived from ultrasound dependent on the technician's skill.

The question I'm motivated by is: 

> Can an uncertainty-aware active-acquisition system reconstruct clinically relevant patient-specific quantities from a minimal sequence of adaptively chosen ultrasound measurements?

Below, I will lay out a number of ideas that I think can enable the above when applied in concert. Most of these ideas are already active areas of work in academia or industry. 

Note that like the other imaging modalities, ultrasound is used to image many organs in the body. 

Like many people, I first encountered ultrasound just before the birth of my first child, during a routine doctor visit. I could make no sense of the black and white display on the screen, but the technician seemed to expertly glide through the process, pausing the feed at key moments and marking geometric quantities, like the size of our baby's heart, and even pointing out the beating of the heart. It felt thrilling, yet mysterious. Along with the usual 2D ultrasound black and white image, we were also presented with a '3D ultrasound' of our baby -- a sort of distorted rendering of the 3D view of our baby in sepia color. At the time, I remember wondering how the 3D was constructed, and thinking to myself, surely its possible to do better than this, using a properly trained machine learning model, and lots of data (this was 2015, so after the ImageNet moment of 2012). 

### Deep learning opens new types of inverse problems

<p align="center">
<img width="600" src="/assets/inverse.png" alt="Inverse problem">
</p>

Inverse problems have a long history in both academia and industry. At a high level, inverse problems are problems where you observe an effect $$Y$$ and try to infer the hidden cause or object $$X$$ that produced it. In ultrasound imaging, the cause $$X$$ is the 3D structure inside our body, a precise arrangement of organs and tissues, including any potential defects, abnormalities, tumors, etc. and the measured signal $$Y$$. 

Another example of an inverse problem is RADAR - the observations are reflections of radio waves off moving objects and the cause is generally aircraft or other projectiles. The estimation of $$X$$ from $$Y$$ has traditionally required knowing the physics of how a given $$X$$ produces a certain $$Y$$. In other words the likelihood function $$p(Y \mid X)$$ has traditionally been required to be known and invertible. For example, we know that an object located at a distance $$X$$ from the RADAR transmitter will produce a reflection at a time delay of $$Y = 2X/c$$, so this problem is easily invertible $$X = Yc/2$$. 

Another inverse problem that I've studied in the past, is **blind source separation** wherein one has access to a piece of audio (doesn't need to be audio, but audio motivates this problem well) $$Y$$ that containts a number of people talking at the same time, or a number of different instruments playing at the same time in a single music track. If we call these individual components $$X_1, X_2, ... ,X_n$$ then the inverse problem is to using $$Y$$ to estimate $$X_1, X_2, ... X_n$$. 

Note that in inverse problems the $$X$$ may not always be uniquely determinable, i.e. the problem may not be invertible. A trivial example is $$Y = X^2$$. If we were told that $$Y = 9$$, then we could say that $$p(X = 3) = p(X = -3) = 1/2$$. If we know that the problem is not necesarily identifiable (i.e. there may not be a single X for a given Y), we are better off assuming $$p(X \mid Y)$$ is multi-modal, i.e. a mean-squared loss on $$X, \hat{X}$$ would not work, and instead a generative model like diffusion would be more appropriate for alloing multi-modal $$p(X \mid Y)$$. 

In recent years, deep learning has opened up interesting possibilities in solving some types of inverse problems that were not solvable earlier either because (a) the likelihood function $$p(Y \mid X)$$ was not known from the physics, or (b) it was known but not easily invertible in closed form. Deep learning allows us to estimate $$X$$ from $$Y$$ if we have access to abundant paired data $$X,Y$$. One of these areas is 3D-reconstruction from 2D images -- here $$X$$ is the underlying complete 3D geometry of a scene or object, and $$Y$$ consists of a few different 2D renderings of this 3D scene from a few different camera angles. We can then ask: what is our best estimate of $$X$$ given $$Y$$ - this is termed [3D reconstruction](https://en.wikipedia.org/wiki/3D_reconstruction_from_multiple_images). Another one of these exciting areas is [mind reading](https://medarc-ai.github.io/mindeye/), where X = our thoughts and Y = brain waves. 

Coming back to ultrasound -- the black and white images on the screen (common called B-mode Ultrasound, where the B stands for "brightness") are supposed to represent specific 2D slices of views through a patient's body, showing tissue density and cavities. Therefore, there is already a type of inverse problem being solved but it is rather simplistic, a bit more like RADAR than like 3D reconstruction. B-mode images do not attempt to directly solve the inverse problem of estimating the 3D internal organ structure. Instead the intensity of white pixels on the screen actually represents the reflectivity field estimated using Delay-and-Sum beamforming -- the strength of the echo or echogenicity at each location in the 2D slice is estimated using the received signal and an assumption about the physics of $$p(Y \mid X)$$. It is not directly a map of tissue density or tissue type. That interpretation, if happeneing at all, is in the mind of the technician. In this sense, these images are not very different from X-ray. There too, the images are direct measurements, rather than the solution to an inverse problem. 

### 3D reconstruction*

The first aspect of ultrasound I'm interested in updating is the $$X$$ that is estimated from $$Y$$. B-mode ultrasound does not attempt to estimate the 3D (or even 2D) geometry inside the body, but I believe it is possible to do so by collecting the right kind of paired $$X,Y$$ data and an appropriate deep learning pipeline that does 3D reconstruction. Where can we get paired $$X, Y$$ data? This is probably the most important question, even more important than the model architecture. I think there are two potential answers: 

* Using simultaneous CT + Ultrasound of the same organs. Such datasets have begum appearing. One example is the [TRUSTED Dataset](https://www.nature.com/articles/s41597-025-04467-1) that pairs trans-abdominal ultrasound and CT data. 
* Using synthetic materials similar to human tissue, where we can perfectly control the $$X$$.  

### fastMRI but for Ultrasound

The [fastMRI project](https://nyulangone.org/news/new-research-finds-fastmri-scans-generated-artificial-intelligence-are-accurate-traditional-mri) at NYU + Meta achieved something remarkable that is relevant to Ultrasound. They exploited redundancy in MRI data acquisition by combining a _prior_ over MRI data with restricted data acquisition in a Fourier space, to reduce the total time a patient needs to spend in an MRI machine. This is a form of compressive sensing. This work is relevant to Ultrasound: if we can acquire several random 2D views using ultrasound, and we can quantify uncertainty (see next section below), then we can transcend the bottleneck of relying on operator skill to operate ultrasound. At this point, its worth discussing the recent paper [UltraGauss](https://arxiv.org/pdf/2505.05643). This paper does 2D-to-3D reconstruction with the goal of synthesizing novel 2D views, i.e. estimating the same type of B-mode images for a new 2D slice that has not been probed. This is a worthy goal because it tries to address the problem of dependence on operator skill, but it does not break away from B-mode images. 


### Quantifying uncertainty: removing dependence on technician skill

In any system where we combine a prior with partial measurements, the reconstructed posterior is going to have non-zero uncertainty. This uncertainty may not matter much if the domain is entertainment, but in mission critical applications like medical imaging, it is important to quantify it. We do not want to be fooled into believing that a reconstruction is driven primarily by the prior rather than a specific patient's measurements. As an exmaple [BayesRays](https://arxiv.org/pdf/2309.03185) tries to quantify uncertainty in NeRF based 3D reconstructions created from 2D images. 

Variables of interest: It is even more important to quantify uncertainty in the final clinical variable of interest (e.g. the size of the heart or lung cavity) that a clinician wants to estimate from the reconstruction. That way, we can be sure that the uncertainty estimate pertains to the quantity of interest rather than to an aesthetic measure of reconstruction. This ultimately requires the important extra step of the machine estimating the clinical variable rather than only a human clinician, which would be an important milestone in and of itself in terms of how much clinicians trust AI and its self-reported uncertinaty. 


### The north-star

A home scanner than can be used by laymen. Early detection of tumors. I think low cost early detection is the current best solution to cancer. 

