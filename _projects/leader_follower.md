---
layout: page
title: Leader-Follower using TerpBot*
description: TerpBot following a human leader along with dynamic obstacle avoidance using a synthetic 2D point cloud generated with MiDaS Monocular Depth Estimation
img: imgs/leader_follower/logo.png
importance: 3
category: Robotics
related_publications:
---

**Note:** This project was done in collaboration with <a href='https://github.com/vedran97'>Vedant Ranade</a> and <a href='https://github.com/SakshamV'>Saksham Verma</a>.
**DEMO**

Click on the following image to get redirected to a demo video of the project. It showcases how the TerpBot trying to detect and follow a human leader while avoiding any dynamic obstacles in its path, detected using a combination of YOLO and MiDaS monocular depth estimation models.

<div class="row justify-content-center">
    <div class="col-sm-auto mt-3 mt-md-0 text-center">
        <a href="https://www.youtube.com/watch?v=kOSTu5ZXVmQ&ab_channel=Shyam">
            {% include figure.html path="imgs/rrt_star/demo.png" title="leader-follower Demo" class="img-fluid rounded z-depth-1" %}
        </a>
    </div>
</div>

<div class="caption">
    Demo showcasing Leader-Follower capabilities of TerpBot. Click on the above image to open the video.
</div>

**GOAL**

The idea of a leader-follower system draws inspiration from natural phenomena, such as flocking behavior observed in birds and schooling behavior observed in fish. These natural systems exhibit remarkable coordination and adaptability, where individuals follow a leader while avoiding obstacles and maintaining group cohesion. By emulating these principles in robotics, we can create intelligent machines capable of robust and efficient tracking of dynamic targets.

In this project we enable the TerpBot to become a follower robot that can detect and follow humans who are the leader entities. Taking inspiration from Tesla which predominantly relies on only cameras for perception, the TerpBot uses only a monocular camera (RaspiCamV2) to localize the position of the leader object with respect to the TerpBot and following it. We also enable it to avoid collisions with dynamic obstacles introduced in the environment. This involves setting up the perception stack of TerpBot, which can successfully localize the leader object, as well as create a point cloud of the environment using only a monocular camera. We also formulate a simple control algorithm to make TerpBot follow the leader while avoiding collisions with the dynamic obstacles.

**METHOD - Perception**

The video feed from the Raspicamv2 is read by the software system using ROS cv bridge. Each frame of the feed is then processed through a custom ROS node consisting of two deep learning models, which attempt to detect and localize the leader (humans), with respect to the TerpBot.
The two deep learning models are as follows:
- Object Detection model - Gives a 2D bounding box around the leader object present in the video frame.
- Monocular Depth Estimation model - Gives a pixel-wise depth map using a monocular image as the input.
The bounding box from the first model is retrieved and used in the depth map to get the distance of the leader object from the camera.

The algorithm and architecture of both models can be found in the following sections. A simple representation of this perception pipeline is as follows :
<div class="row justify-content-center">
    <div class="col-sm-auto mt-3 mt-md-0 text-center">
        {% include figure.html path="imgs/leader_follower/perception_pipeline.png" title="Perception Pipeline" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A high level overview of the two model perception stack of TerpBot for Leader-Follower task
</div>

**YOLO Object Detection Model**

The object detection model that the TerpBot uses is based on the 5th iteration of the famous YOLO object detection algorithm, as detailed in the paper "You Only Look Once: Unified, Real-Time Object Detection". The base model is trained on the COCO dataset, which comprises 80 different classes of objects. The model takes a single image as input and provides a set of bounding boxes enclosing different objects present in the image as the output, along with their class names. A pre-trained YOLOv5 model was taken and trained using a dataset which detects humans only using the lower parts of their body (since the camera's FOV can't capture entire humans). A summary of the YOLO model can be found below :

<div class="row justify-content-center">
    <div class="col-sm-auto mt-3 mt-md-0 text-center">
        {% include figure.html path="imgs/leader_follower/yolov5.png" title="YOLO summary" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Summary of the YOLOv5 algorithm and architecture
</div>

The following loss functions are used to train the YOLOv5 model:

<div class="row justify-content-center">
    <div class="col-sm-auto mt-3 mt-md-0 text-center">
        {% include figure.html path="imgs/leader_follower/yolov5_losses.png" title="YOLO losses" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Loss functions used to train the YOLOv5 model
</div>

The below image shows sample results from the YOLOv5 model used on TerpBot:

<div class="row justify-content-center">
    <div class="col-sm-auto mt-3 mt-md-0 text-center">
        {% include figure.html path="imgs/leader_follower/yolov5_results.png" title="YOLO results" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Sample results from TerpBot's YOLOv5 model on detecting the Leader human.
</div>


**MiDaS Monocular Depth Estimation Model**

The Depth Estimation technique used by TerpBot is the 'MiDaS (Monocular Depth Estimation in Real-time with Adaptive Scale)' model, based on the paper 'Towards Robust Monocular Depth Estimation: Mixing Datasets for Zero-shot Cross-dataset Transfer'. This model was chosen for the depth estimation task for our robot due to its exceptional generalizability. It has been trained on a diverse range of data across various task domains, making it state-of-the-art in depth estimation and a pre-trained model was used directly. Moreover, it demonstrates robust performance even on images that do not belong to the training distribution. A summary of the MiDaS model can be found below :

<div class="row justify-content-center">
    <div class="col-sm-auto mt-3 mt-md-0 text-center">
        {% include figure.html path="imgs/leader_follower/midas.png" title="midas summary" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Summary of the MiDaS algorithm and architecture
</div>

The following loss functions are used to train the MiDaS model:

<div class="row justify-content-center">
    <div class="col-sm-auto mt-3 mt-md-0 text-center">
        {% include figure.html path="imgs/leader_follower/midas_losses.png" title="midas losses" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Loss functions used to train the MiDaS model
</div>

The below image shows sample results from the MiDaS model used on TerpBot:

<div class="row justify-content-center">
    <div class="col-sm-auto mt-3 mt-md-0 text-center">
        {% include figure.html path="imgs/leader_follower/midas_results.png" title="midas results" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Sample results from TerpBot's MiDaS model to form a 2D point cloud.
</div>

**OVERALL PIPELINE**

The below image is a schematic representation of the overall pipeline used by the TerpBot to carry out the Leader-Follower task successfully:

<div class="row justify-content-center">
    <div class="col-sm-auto mt-3 mt-md-0 text-center">
        {% include figure.html path="imgs/leader_follower/overall_pipeline.png" title="Overall Pipeline" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Overall pipeline utilized by the TerpBot for Leader-Follower task
</div>