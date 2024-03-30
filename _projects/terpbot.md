---
layout: page
title: Unicycle Kinematics based mobile robot - TerpBot
description: A RaspberryPi based Unicycle Mobile Robot using wheel odometry and monocular perception, built from scratch
img: imgs/terpbot/hardware.png
importance: 1
category: Robotics
related_publications:
---

**Note:** This project was done in collaboration with <a href='https://github.com/vedran97'>Vedant Ranade</a> and <a href='https://github.com/SakshamV'>Saksham Verma</a> who were majorly responsible for the hardware setup and tuning, while I was involved predominantly with the perception stack.

TerpBot is a unique unicycle mobile robot developed from the ground up, boasting a simple yet effective design. With wheel odometry and a single raspicam for perception, it navigates its surroundings with precision. Running on a Raspberry Pi 4B, TerpBot showcases the power of DIY robotics, offering a cost-effective and versatile solution for autonomous mobility. Its hardware system consists of the following parts :

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="imgs/terpbot/terpbot_hardware_1.png" title="hardware parts 1" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="imgs/terpbot/terpbot_hardware_2.png" title="hardware parts 2" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    TerpBot's hardware parts
</div>


The following diagram is a high level-system representation of how different hardware parts of the TerpBot work in tandem with each other:

<div class="row justify-content-center">
    <div class="col-sm-auto mt-3 mt-md-0 text-center">
        {% include figure.html path="imgs/terpbot/hardware_map.png" title="YOLO architecture" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    TerpBot's System Architecture
</div>

**Kinematics:**
- TerpBot adopts a distinctive unicycle model built upon the principles of a differential drive system. 
- This design choice allows for enhanced maneuverability and agility in navigating diverse terrains. 
- By leveraging differential drive, TerpBot can adjust the speed and direction of its single wheel independently, enabling precise control and efficient movement. 
- This approach not only simplifies the mechanical structure but also maximizes flexibility, making TerpBot well-suited for a variety of tasks and environments.

<div class="row justify-content-center">
    <div class="col-sm-auto mt-3 mt-md-0 text-center">
        {% include figure.html path="imgs/terpbot/kinematics.png" title="YOLO architecture" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    High level overview into the TerpBot's Kinematics design
</div>

**Controls and Controller Design:**
- We have utilized an Anti-Windup PID controller for controlling wheel velocities of the Terpbot.  The Arduino Uno microcontroller has been programmed in a very optimal way, to achieve a near perfect trajectory tracking result. The Arduino Uno had the following tasks: 
- Accurately count time (us resolution)
- Accurately count ticks coming from each encoder. 
- Calculate ticks read in a unit time. (Ticks read in a unit time, is like velocity calculation)
- Communicate this tick rate to the Raspberry PI without loss of synchronization.
- Receive Control Targets of each motor’s tick rate, in a jitter free manner.
- Execute the control loop under the control sampling frequency, leaving enough time for other tasks to run.

<div class="row justify-content-center">
    <div class="col-sm-auto mt-3 mt-md-0 text-center">
        {% include figure.html path="imgs/terpbot/controller.png" title="YOLO architecture" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    High level overview into the TerpBot's controller design and tuning
</div>

The TerpBot was further configured to solve different tasks which can be found in the Projects section.
