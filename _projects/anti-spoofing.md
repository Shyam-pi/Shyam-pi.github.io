---
layout: page
title: Voice Anti-Spoofing
description: A lightweight Support Vector Machine (SVM) based anti-spoofing model which can distinguish between audio from a real human and a playback device
img: imgs/anti-spoof_logo.jpg
importance: 1
category: General AI
related_publications:
---

**Note:** All the data and processing techniques are proprietary to <a href='https://www.renesas.com/us/en'>Renesas America Ltd.</a>, hence only limited non-sensitive information shall be disclosed as a part of the project description here.

Click on the following image to get redirected to a demo video of the project:

<div class="row justify-content-center">
    <div class="col-sm-auto mt-3 mt-md-0 text-center">
        <a href="https://www.youtube.com/watch?v=W2HgrsbJnJA&ab_channel=Shyam">
            {% include figure.html path="imgs/anti-spoof_demo.png" title="Anti-Spoofing Demo" class="img-fluid rounded z-depth-1" %}
        </a>
    </div>
</div>

<div class="caption">
    Demo showcasing the voice authentication model deployed on the Renesas voice board
</div>

**INTRODUCTION**

In this project I developed a voice authentication system for a Renesas voice board, capable of capturing voice samples and distinguishing between genuine and spoofed voices. By leveraging advanced signal processing techniques and machine learning algorithms, we aim to enhance security measures and ensure robust authentication protocols for Renesas voice boards.

**KEY COMPONENTS**

1. **Voice Capture Module:**
   - Utilize a Renesas voice board equipped with a microphone to capture voice samples.
   - Utilized a pre-trained trigger mechanism to initiate voice capture upon detecting the phrase "Hi Renesas."

2. **Data Collection and Processing:**
   - Collect voice samples from multiple individuals, including genuine utterances and spoofed playback.
   - Store voice data for further analysis and feature extraction.

3. **Feature Extraction Pipeline:**
   - Develop a feature extraction pipeline to analyze voice samples and extract relevant features.
   - Explore different feature extraction techniques to capture unique characteristics of each voice.

4. **Machine Learning Model Training:**
   - Train a Support Vector Machine (SVM) model using the extracted features.
   - Implement a classification algorithm capable of distinguishing between genuine and spoofed voices.

5. **System Integration:**
   - Integrate the voice authentication system with the Renesas voice board for live testing.

**PROJECT WORKFLOW**

1. **Voice Capture:**
   - Renesas board detects trigger phrase "Hi Renesas" and initiates voice capture.
   - Voice samples are recorded and stored for analysis.

2. **Data Collection:**
   - Gather voice samples from diverse individuals to create a comprehensive dataset.
   - Include both genuine utterances and spoofed playback for training and testing purposes.

3. **Feature Extraction:**
   - Analyze voice samples using signal processing techniques to extract relevant features.
   - Transform raw voice data into a feature vector representation suitable for machine learning algorithms.

4. **Model Training:**
   - Train an SVM model using the extracted features to classify between genuine and spoofed voices.
   - Validate model performance using cross-validation techniques and optimize hyperparameters for improved accuracy.

5. **System Evaluation:**
   - Integrate the trained model with the Renesas board and playback devices for real-world testing.
   - Evaluate system performance by testing with a diverse range of voice samples and spoofing attempts.

**CONCLUSION**

This project demonstrates the potential of using Renesas boards for implementing advanced voice authentication systems. By leveraging signal processing techniques and machine learning algorithms, we aim to develop a robust and reliable system capable of accurately distinguishing between genuine and spoofed voices. With further refinement and testing, our voice authentication system holds promise for enhancing security measures in various applications, including access control, authentication, and identity verification.
