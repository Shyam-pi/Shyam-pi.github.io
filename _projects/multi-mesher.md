---
layout: page
title: Multi-Mesher
description: A Diffusion Driven single 2D image to 3D Mesh Reconstruction using Zero123 and PointNet architecture
img: imgs/multi-mesher/multi-mesher.png
importance: 1
category: Computer Vision
---

**Note**: For a more detailed overview of this project please click on this <a href='https://drive.google.com/file/d/1yn0MjJ9-HBUXjE_IMaKfhP4hUs6p00ui/view'>link</a>.

**Codes**: Coming soon!

**INTRODUCTION**

Our work presents a novel approach to single-image 3D reconstruction that leverages novel view synthesis via diffusion with canonical mesh deformation techniques. While prior works (namely Zero-1-to-3 [6] and One-2-3-45 [5]) have used diffusion to generate hypothetical novel views, they have focused on NeRFs and SDFs as geometric representations which are later converted to meshes. The method directly predicts meshes and texture, avoiding this multi-stage process. Prior mesh optimization techniques such as Pix2Mesh [9] and Pix2Mesh++ [2] are sensitive to view inconsistencies, so we leverage the PointNet [8] architecture which is better suited for the task. Notably, in contrast to prior mesh optimization techniques that produce only geometry, we aim to propose a network which can predict the texture along with the geometry.

Our approach addresses the challenges posed by the limitations of the optimization pipeline by exploring the strengths of PointNet, a neural network specifically designed for processing 3D point cloud data. Through experimental evaluation, we demonstrate that the fusion of information from multiple views, coupled with the capabilities of PointNet, significantly improves the quality and accuracy of the reconstructed 3D structures compared to traditional methods.

The synergy between multi-view synthesis and PointNet fusion offers a promising avenue for advancing the state-of-the-art in single-image 3D reconstruction. Our findings not only contribute to the refinement of existing methodologies but also underscore the potential for combining mesh conditioning neural network architectures with multi-view generational techniques to enhance the depth estimation and reconstruction process.

**GOAL**

A common method of predicting a 3D model from a single image is using an autoencoder to capture a 2D image in a learned encoding, which is then used to predict the corresponding 3D representation. There are several issues associated with this approach, including problems with handling multiple faces and difficulties in predicting occluded sections accurately. Additionally, the availability of 3D data is much less compared to 2D data, which reduces the effectiveness of this method.

Therefore the aim of this project is to introduce a novel mesh deforming pipeline which can make leverage of the Zero123 diffusion model to generate multi-views of a single view image, to create a 3D mesh directly (in contrast to an intermediate 3D representation like the SOTA single view 3D reconstruction methods). The below figure shows a basic representation of how a mesh optimization pipeline can be used in tandem with the Zero123's outputs

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="imgs/multi-mesher/mm_pipeline.png" title="Multi-Mesher pipeline with Zero123" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Representation of how mesh optimization is done in tandem with Zero123's outputs
</div>


**METHOD**


- The method used in this paper leverages the geometric priors learned by diffusion models to generate alternative views of an object given a single input image. 

- Since these diffusion models are pretrained on 2D data, they are able to overcome the data insufficiencies that autoencoder methods face and therefore capture natural geometries and appearances more accurately. 

- Then we use a novel PointNet based pipeline (Multi-Mesher) that takes a canonical spherical mesh and predicts vertex displacements along with colors for each vertex, hence forming a colored 3D shape. 

- This colored 3D mesh is then rendered using a differential renderer from the same views used in Zero123 to generate ground truth images.

- These rendered images from the predicted mesh and generated images from Zero123 are used to compute Silhouette loss and RGB rendering loss, which is backpropagated through the Multi-Mesher Network

- Multi-mesher is a per shape optimization pipeline, i.e., it is trained over several epochs for each shape, and hence it is analogous to a neural representation of a shape (but is much cheaper owing to the low cost of the PointNet architecture)

Our approach addresses the challenges posed by the limitations of the optimization pipeline by exploring the strengths of PointNet, a neural network specifically designed for processing 3D point cloud data. Through experimental evaluation, we demonstrate that the fusion of information from multiple views, coupled with the capabilities of PointNet, significantly improves the quality and accuracy of the reconstructed 3D structures compared to traditional methods. The below is a representation of how the PointNet architecture is modified to make use of Zero123's outputs for training the Multi-Mesher model:



<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="imgs/multi-mesher/multi-mesher-pipeline.png" title="multi-mesher-pipeline" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Representation of using PointNet architecture for Mesh optimization working in tandem with Zero123's outputs
</div>


**RESULTS**

The below images are some of the results of the pipeline which represent how a canonical spherical mesh transforms through several iterations. (For each set of images, the left side image consists of different views generated by Zero123 pipeline and the right side image shows how a spherical canonical mesh gets optimized with respect to the ground truth over multiple iterations)

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="imgs/multi-mesher/cow_views.png" title="Chair-mesh-optimization" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="imgs/multi-mesher/cow_optim.png" title="Chair-mesh-optimization" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    (Left) Toy cow images generated using zero123 (Right) Per-shape PointNet optimization pipeline run on a Zero123 generated toy cow images over 1250 iterations
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="imgs/multi-mesher/chair_zero123.png" title="Chair-mesh-optimization" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="imgs/multi-mesher/chair_optim.png" title="Chair-mesh-optimization" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    (Left) Chair images generated using zero123 (Right) Per-shape PointNet optimization pipeline run on a Zero123 generated chair images over 1250 iterations
</div>

The below results showcase a complete mesh generated using the above pipeline (Notice how the dustbin has non-uniform colors, which is due to the view inconsistencies from the multi-views generated by Zero123)

<div class="row justify-content-center">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.html path="imgs/multi-mesher/cow_mesh.gif" title="Chair-mesh-optimization" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.html path="imgs/multi-mesher/dustbin_mesh.gif" title="Chair-mesh-optimization" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row justify-content-center">
    <div class="col-sm text-center">
        (Left) Mesh generated from toy cow images
    </div>
    <div class="col-sm text-center">
        (Right) Mesh generated from dustbin images
    </div>
</div>
