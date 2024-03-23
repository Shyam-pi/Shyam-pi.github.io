---
layout: page
title: RRT* Smart Offline Planning along with Live Planning for TerpBot*
description: Global path planning using A* and local dynamic path planning using potential fields algorithm for TerpBot
img: imgs/rrt_star/logo.png
importance: 2
category: Robotics
related_publications:
---

**Note:** This project was done in collaboration with <a href='https://github.com/vedran97'>Vedant Ranade</a> and <a href='https://github.com/SakshamV'>Saksham Verma</a>.

Click on the following image to get redirected to a demo video of the project. It showcases how the TerpBot navigates a complex maze with RRT* Smart algorithm and avoids live obstacles (orange cones), detected using a combination of YOLO and MiDaS monocular depth estimation models, using a Potential Fields live planner.

<div class="row justify-content-center">
    <div class="col-sm-auto mt-3 mt-md-0 text-center">
        <a href="https://www.youtube.com/watch?v=x7VzOseteOU&ab_channel=SakshamVerma">
            {% include figure.html path="imgs/rrt_star/demo.png" title="Navigation Demo" class="img-fluid rounded z-depth-1" %}
        </a>
    </div>
</div>

<div class="caption">
    Demo showcasing navigation capabilities of TerpBot. Click on the above image to open the video.
</div>

**GOAL**

Path planning is a critical part of ground robot navigation, and many different algorithms have been developed to tackle it. The choice of algorithm depends on the specific requirements of the application, such as the environment, the robot's capabilities, and the performance constraints.

In this project, we enable our TerpBot to navigate through a maze with unknown obstacles. The TerpBot will use a path planning algorithm to find the optimal path to the target location, detect the pose and location of any obstacles during the way, replan if needed, and execute the path to reach the goal. The project will involve designing and implementing the hardware and software components of TerpBot, as well as testing its performance in an actual maze environment.

The project goals can be broken down into 2 main parts:

- Develop a planning strategy that can plan a global path for a differential drive ground robot from a start position to a goal position, and a local planner which runs during operation and integrates with the global path to avoid any detected obstacles.

- Evaluate and demonstrate the algorithm’s effectiveness through a simulation and a physical robot traversing a known map, with unknown obstacles.

**METHOD - Planning**

Two path planning algorithms were utilized in this project. The offline global planner generates a trajectory to be followed from start to goal node before the execution begins. So, this algorithm can work offline, create a trajectory and then store it. There are no strict bounds on time complexity. On the other hand, the live planner, whose task is to avoid the obstacles, must be running live and should be quick to execute for small deviations necessary in the global path to avoid any detected obstacles. Our choices for the planning algorithms are explained as follows:

**Offline Global planning – RRT* Smart** 
<a href='https://journals.sagepub.com/doi/10.5772/56718'>[RRT*-SMART: A Rapid Convergence Implementation of RRT]</a>

- Rapidly exploring random trees (RRT) is a popular path planning algorithm used in robotics to find feasible paths in high-dimensional and complex environments. RRT* is an extension of the RRT algorithm that improves the quality of the generated path.

- The RRT* algorithm works by first creating a random tree rooted at the robot's initial position. It then explores the space by randomly sampling points and growing the tree towards the sampled point while maintaining collision-free paths. Unlike RRT, RRT* continuously re-wires the tree by re-evaluating the cost of each node and its connections to its neighbors. This re-wiring process reduces the overall path cost and generates a more optimal path.

- The RRT* Smart algorithm further improves the RRT* algorithm by introducing a heuristic that biases the sampling towards the goal region. By prioritizing the search towards the goal region, the algorithm can generate high-quality paths quickly and efficiently. 

<div class="row justify-content-center">
    <div class="col-sm-auto mt-3 mt-md-0 text-center">
        {% include figure.html path="imgs/rrt_star/global_result.png" title="RRT* Smart" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A sample result of RRT* Smart global planner applied on a Map (Black boxes represent obstacles, Red lines represent the planned path, Blue dots represent the explored nodes)
</div>

**Live planning – Potential Field planning**
<a href='https://ieeexplore.ieee.org/document/127236'>[A potential field approach to path planning]</a>

- The Potential Field Planning algorithm is a popular method used in robotics and autonomous navigation to plan the trajectory of a robot. The algorithm works by modeling the environment as a potential field, where each point in the field has a scalar value representing the attraction or repulsion force exerted on the robot. The potential field is generated by combining two types of fields: the attractive field that pulls the robot towards the goal, and the repulsive field that pushes the robot away from obstacles.

- The robot's trajectory is planned by calculating the resulting force vector on the robot at every point in the environment. The robot moves in the direction of the resulting force vector, and the magnitude of the force vector determines the speed of the robot. The algorithm continuously updates the potential field and recalculates the force vector at each step, allowing the robot to navigate dynamically through the environment and avoid obstacles.

<div class="row justify-content-center">
    <div class="col-sm-auto mt-3 mt-md-0 text-center">
        {% include figure.html path="imgs/rrt_star/local_result.png" title="Potential Fields planner" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A sample result of the Potential Fields local planner
</div>

**METHOD - Perception**

In order to showcase the live planning capabilities of the TerpBot, we had to implement a perception stack which was capable of detecting live obstacles that do not belong to the static map. We trained and integrated a YOLO object detection piplene with MiDaS depth estimation for the monocular camera, which enables TerpBot the ability to detect obstacles, particularly cones in this case, in its environment while accurately estimating their distance. The figure below showcases the pipeline used for live object detection :

<div class="row justify-content-center">
    <div class="col-sm-auto mt-3 mt-md-0 text-center">
        {% include figure.html path="imgs/rrt_star/perception_pipeline.png" title="Perception Pipeline" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Higher level representation of the Live Object Detection pipeline
</div>

The figure below showcases example results of the object detection and monocular depth estimation pipelines : 

<div class="row justify-content-center">
    <div class="col-sm-auto mt-3 mt-md-0 text-center">
        {% include figure.html path="imgs/rrt_star/perception_example.png" title="Perception Example" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    (Left) Object Detection result from the YOLO model (Right) Depth Estimation from MiDaS monocular depth estimation model
</div>