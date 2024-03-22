---
layout: page
title: Leaf Detection
description: A YOLO based Leaf Detection pipeline to aid plant health monitoring for farm robots
img: imgs/leaf_detection/leaf_detect.png
importance: 5
category: Computer Vision & Robotics
related_publications: einstein1956investigations, einstein1950meaning
---

**Title: Deep Learning for Leaf Detection: Utilizing YOLO Model with Transfer Learning**

**Introduction:**
In recent years, deep learning techniques have revolutionized the field of computer vision, enabling robust and efficient object detection in various domains. One such application is leaf detection, which plays a crucial role in fields like agriculture, botany, and environmental science. In this project, we employ the YOLO (You Only Look Once) model, a state-of-the-art deep learning architecture, for leaf detection. By utilizing transfer learning, we tailor the model to our specific leaf dataset, enhancing its performance and adaptability.

**Objective:**
The primary objective of this project is to develop an accurate and efficient leaf detection system using deep learning techniques. By training a YOLO model with transfer learning on a custom leaf dataset, we aim to achieve high precision in detecting and localizing leaves within images. This was developed to be used in tandem with an in-house agricultural robot with vision capabilities.

**Methodology:**
1. **Dataset Collection and Preprocessing:** We used a diverse dataset consisting of images containing various types of leaves in different environmental conditions from the internet. Preprocessing steps involved data augmentation techniques such as rotation, flipping, and resizing to enhance the dataset's diversity and improve model generalization.

2. **Model Architecture:** We chose YOLO (You Only Look Once) as our base architecture due to its real-time processing capabilities and high accuracy. YOLO divides the input image into a grid and predicts bounding boxes and class probabilities for each grid cell simultaneously.

3. **Transfer Learning:** To adapt the YOLO model to our leaf detection task, we employed transfer learning. We initialized the network with weights pre-trained on a large-scale dataset and fine-tuned it on our leaf dataset. This approach leverages the knowledge learned from a general dataset and allows the model to specialize in detecting leaves.

4. **Training:** The training process involved optimizing the model parameters using backpropagation and gradient descent. We utilized tools like CUDA for GPU acceleration to expedite training and minimize computational time.

<div class="row justify-content-center">
    <div class="col-sm-auto mt-3 mt-md-0 text-center">
        {% include figure.html path="imgs/leaf_detection/yolo.jpg" title="YOLO architecture" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Graphical representation of YOLO model used for the leaf detection task
</div>


**Results:**
Our trained YOLO model achieved promising results in leaf detection, demonstrating high precision and recall rates. The model successfully localized leaves within images across various backgrounds and lighting conditions. Additionally, the transfer learning approach enabled efficient training with limited annotated data, showcasing the adaptability of deep learning techniques to domain-specific tasks.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="imgs/leaf_detection/leaf_example_2.jpg" title="easy example" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="imgs/leaf_detection/leaf_example.png" title="difficult example" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
   (Left) Showcases the model's qualitative performance on a simpler example with more isolated leaves (Right) Showcases the model's leaf detection capabilities in a more complicated image with dense leaves
</div>


**Conclusion:**
In conclusion, this project demonstrates the effectiveness of deep learning, specifically the YOLO model with transfer learning, in leaf detection tasks. By leveraging the power of convolutional neural networks and transfer learning, we have developed a robust and adaptable solution for automated leaf detection. This technology holds great potential in various fields, offering opportunities for innovation and advancement in agricultural, botanical, and environmental research domains.