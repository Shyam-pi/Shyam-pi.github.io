---
layout: page
title: Multi-Mesher
description: A Diffusion Driven 2D to 3D Mesh Reconstruction
img: assets/img/multi-mesher.png
importance: 1
category: Computer Vision
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

This project presents a novel approach to single-image 3D reconstruction that leverages novel view synthesis via diffusion with canonical mesh deformation techniques. While prior works (namely Zero-1-to-3 and One-2-3-45) have used diffusion to generate hypothetical novel views, they have focused on NeRFs and SDFs as geometric representations which are later converted to meshes. The method directly predicts meshes and texture, avoiding this multi-stage process. Prior mesh optimization techniques such as Pix2Mesh and Pix2Mesh++ are sensitive to view inconsistencies, so we leverage the PointNet architecture which is better suited for the task. Notably, in contrast to prior mesh optimization techniques that produce only geometry, we aim to propose a network which can predict the texture along with the geometry.

Our approach addresses the challenges posed by the limitations of the optimization pipeline by exploring the strengths of PointNet, a neural network specifically designed for processing 3D point cloud data. Through experimental evaluation, we demonstrate that the fusion of information from multiple views, coupled with the capabilities of PointNet, significantly improves the quality and accuracy of the reconstructed 3D structures compared to traditional methods.

The synergy between multi-view synthesis and PointNet fusion offers a promising avenue for advancing the state-of-the-art in single-image 3D reconstruction. Our findings not only contribute to the refinement of existing methodologies but also underscore the potential for combining neural network architectures with multi-view techniques to enhance the depth and fidelity of 3D reconstructions from single images.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/3.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    This image can also have a caption. It's like magic.
</div>

You can also put regular text between your rows of images.
Say you wanted to write a little bit about your project before you posted the rest of the images.
You describe how you toiled, sweated, *bled* for your project, and then... you reveal its glory in the next row of images.


<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>


The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

{% raw %}
```html
<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
```
{% endraw %}
