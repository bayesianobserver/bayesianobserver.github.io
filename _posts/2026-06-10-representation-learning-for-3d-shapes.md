---
layout: post
title: "Representation learning for 3D shapes"
date: 2026-06-10
mathjax: true
---

I recently worked on a project on a representation learning model for 3D shapes using their point clouds and meshes -- specifically 3D scans of teeth. The problem was straitforward: given a 3D point cloud from a scan of a single tooth in a manufacturing facility that makes crowns, determine which CAD design mesh, among thousands, it belongs to. The scan and the designs are not in the same orientation/pose. 

There is a geometric solution to this problem - it involves specific steps in 3D-vision for testing each candidate mesh against the 3d scan cloud: (a) global registration, (b) ICP (iterative closest point) to align to point clouds as best as possible, (d) measuring global deviation of the scan points with respect to the design mesh. This is extrmely slow. 

The fact that the scan and the design are not in the same orientation but must still map to the same embedding gives the problem a flavor of SE3-invariance. I built a self-supervised learning model for these 3D objects using two different architectures, both trained using a InfoNCE-style SupCon loss, where for each anchor sample, there are multiple positives and many negatives.

<img width="320"  src="/assets/contrastive.png">

* One, using an inherently SE3-equivariant architecture called [DeepSphere](https://arxiv.org/abs/2012.15000) that builds on the [Spherical CNN](https://arxiv.org/abs/1801.10130) work of Cohen, Welling et al, by replacing the high computational complexity operations of convolutaions with spherical harmonics that yield exact SO3 equivariance, with an approximation: the 3D point cloud or mesh of the object (the tooth inthis case) is first projected onto a sphere to create a spherical depth map. This is then discretized onto a grid that lives on the sphere (some discrete projections are: [Healpix](https://en.wikipedia.org/wiki/HEALPix), [equi-angular](https://en.wikipedia.org/wiki/Equirectangular_projection), and [Fibonacci](https://extremelearning.com.au/how-to-evenly-distribute-points-on-a-sphere-more-effectively-than-the-canonical-fibonacci-lattice/)). I used Healpix using the healpy library. We now have a regular grid, kind of like a 2D image, but instead of a flat plane, it lives on a sphere. DeepSphere then treats these pixels on the sphere as a graph with each pixel being a node with a fixed number of neighbors, and applies a graph neural network whose filters are radial, i.e. the weight of the filters are learnt but are radially symmetric -- this is called [Chebyshev](https://wandb.ai/graph-neural-networks/ChebGCN/reports/Introduction-to-Chebyshev-Graph-Convolutional-Neural-Networks--Vmlldzo2ODY0MTg1) [convolution](https://pytorch-geometric.readthedocs.io/en/2.5.0/generated/torch_geometric.nn.conv.ChebConv.html). If the spherical signal rotates, so does the output of the graph neural network. The extent to which this architecture is equivariant depends upon the number of pixels on the grid -- therefore there is a tradeoff between the amount of compute and the level of equivariance achieved. SO3 invariance is achieved using a pooling layer at the end. I liked the DeepSpere paper and recommend reading it. 

<img width="320"  src="/assets/nefertiti_bust_3d_mesh.png">
As an example, here is a 3D model of the bust of Nefertiti. 
 
<img width="320"  src="/assets/healpix_nefertiti_depthmap.png">
The spherical depthmap, created by casting a ray through the point cloud of the above mesh's vertices. In practice one would cast a ray to every pixel on the healpix grid of a sphere, and intersect with the mesh. 

<img width="320"  src="/assets/healpix_nefertiti_normals.png">
A second channel made using the cosine of the angle between each ray and the normal at the point of intersection. 


* Second, I tried to use a [PointTransformerV3](https://arxiv.org/abs/2312.10035) architecture, which is _not_ SE3-equivariant, but can be driven to learn equivariance by aggressive augmentation. The PTv3 architecture is surprisingly fast for a transformer based architecture -- and it achieves this by using a [space filling curve](https://en.wikipedia.org/wiki/Space-filling_curve) (Hilbert curves or Z-curves) to transform a 3D problem consisting of a point cloud into a 1D problem! On the space filling curves, the 'neighbors' of any point in 3D space are likely to be real 3D nearest neighbors of that point, thereby eliminating the need for 3D nearest neighbors when considering which points to attend to. The 'aggressive augmentation' is achievd by applying a random SO3 rotation to each 3D scan and its corresponding matched design file as the positve sample. 

To my surprise, the PTv3 architecture achieved very strong performance -- better than the spherical CNN when using the same batch size, and surpassed the spherical CNN when the batch size of the PTv3 model was increased (contrastive learning benefits from large batches because they provide a large number of negatives for each positive pair sample in the batch). I also used rotational augmentation on the spherical CNN since this form of spherical CNN is not prfectly SE3-equivariant. 






