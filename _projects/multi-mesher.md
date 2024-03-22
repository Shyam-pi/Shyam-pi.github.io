---
layout: page
title: Multi-Mesher
description: A Diffusion Driven single 2D image to 3D Mesh Reconstruction using Zero123 and PointNet architecture
img: imgs/multi-mesher/multi-mesher.png
importance: 1
category: Computer Vision & Robotics
related_publications: einstein1956investigations, einstein1950meaning
---

<!-- Every project has a beautiful feature showcase page.
It's easy to include images in a flexible 3-column grid format.
Make your photos 1/3, 2/3, or full width.

To give your project a background in the portfolio page, just add the img tag to the front matter like so:

    ---
    layout: page
    title: project
    description: a project with a background image
    img: /assets/img/12.jpg
    --- -->
Note: For a more detailed overview of this project please click on this <a href='https://drive.google.com/file/d/1yn0MjJ9-HBUXjE_IMaKfhP4hUs6p00ui/view'>link</a>.

This project presents a novel approach to single-image 3D reconstruction that leverages novel view synthesis via diffusion with canonical mesh deformation techniques. While prior works (namely Zero-1-to-3 and One-2-3-45) have used diffusion to generate hypothetical novel views, they have focused on NeRFs and SDFs as geometric representations which are later converted to meshes. The method directly predicts meshes and texture, avoiding this multi-stage process. Prior mesh optimization techniques such as Pix2Mesh and Pix2Mesh++ are sensitive to view inconsistencies, so we leverage the PointNet architecture which is better suited for the task. Notably, in contrast to prior mesh optimization techniques that produce only geometry, we aim to propose a network which can predict the texture along with the geometry.

The below figure shows a basic representation of how a mesh optimization pipeline can be used in tandem with the Zero123's outputs

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="imgs/multi-mesher/mm_pipeline.png" title="Multi-Mesher pipeline with Zero123" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Representation of how mesh optimization is done in tandem with Zero123's outputs
</div>

Our approach addresses the challenges posed by the limitations of the optimization pipeline by exploring the strengths of PointNet, a neural network specifically designed for processing 3D point cloud data. Through experimental evaluation, we demonstrate that the fusion of information from multiple views, coupled with the capabilities of PointNet, significantly improves the quality and accuracy of the reconstructed 3D structures compared to traditional methods.

The synergy between multi-view synthesis and PointNet fusion offers a promising avenue for advancing the state-of-the-art in single-image 3D reconstruction. Our findings not only contribute to the refinement of existing methodologies but also underscore the potential for combining neural network architectures with multi-view techniques to enhance the depth and fidelity of 3D reconstructions from single images. The below is a representation of how the PointNet architecture is modified to make use of Zero123's outputs for training a per-shape optimization pipeline



<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="imgs/multi-mesher/multi-mesher-pipeline.png" title="multi-mesher-pipeline" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Representation of using PointNet architecture for Mesh optimization working in tandem with Zero123's outputs
</div>

The given approach uses a per-shape optimization methodology in which a PointNet based architecture takes vertices of a canonical spherical mesh as its inputs, and processes these points through a PointNet pipeline, trains the pipeline using Silhouette and RGB rendering losses, and outputs new vertex positions and RGB color for each vertex. The below image are representations of how the canonical mesh transforms through several iterations. (For each set of images on the right side image, left is the mesh being optimized and right is the reference ground truth image)

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
