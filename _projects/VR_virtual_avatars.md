---
layout: page
title: Creating Immersive VR Avatars with Animation Rigging
description: Implementing inverse kinematics in unity engine to create realistic VR avatars
img: imgs/animation_rigging.png
importance: 3
category: Virtual Reality
---

Click on this <a href="https://youtu.be/wIwl_R5OXfo?si=uQBv-wSz__krkigq">link</a> to get redirected to a demo video of the project.

**Introduction:**
In this project, we delve into the realm of Virtual Reality (VR) development by integrating basic inverse kinematics to create personalized avatars that mimic the movements of users' controllers and head-mounted displays (HMDs). By leveraging Unity's Animation Rigging package, we empower users to interact with their virtual environment through intuitive and natural movements, enhancing immersion and user experience.

**Key Components:**

1. **Importing Humanoid Avatars:**
   - Utilize Unity Asset Store to download and import humanoid avatars, such as the Speedball Player 1 model.

2. **Setting Up Animation Rigging:**
   - Access Animation Rigging window in Unity to organize and set up animation rigs.
   - Configure Rigs and Constraints to modify the animated hierarchy's pose.

3. **Inverse Kinematics for Controllers/Hands:**
   - Create GameObjects for inverse kinematics constraints and add Two Bone IK Constraints component.
   - Use pseudocode to map controller movements to avatar hand movements, adjusting transform and rotation based on user input.

4. **Inverse Kinematics for Head/HMD:**
   - Implement Multi-Parent Constraint component to synchronize avatar head movements with HMD rotations.
   - Map HMD movements to avatar head movements using pseudocode, adjusting transform position and rotation accordingly.

**Extra Immersion:**

1. **Adding Custom Avatars:**
   - Incorporated new avatars downloaded from online repositories or asset stores, rigging them to respond to user movements.

2. **Mirror Implementation:**
   - Improved self-awareness and embodiment in VR by adding mirrors to the virtual environment, allowing users to observe their avatar's movements.

3. **Physically-Based Interactions:**
   - Enhanced interactivity by enabling avatars to interact with virtual objects in a physically plausible manner, such as knocking over objects or reacting to collisions.

**Conclusion:**
By integrating animation rigging and inverse kinematics, we empower users to embody virtual avatars and interact with VR environments in a natural and intuitive manner.