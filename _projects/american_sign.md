---
layout: page
title: American Sign Language (ASL) Detection
description: A CNN and LSTM based American Sign Language Detector for Letters from video feeds
img: imgs/asl/asl_logo.png
importance: 3
category: Computer Vision
related_publications:
---

Note: For a demo of this project please click on this link

- Communication Gap: There is a fundamental barrier in communication between ASL users and people who are not familiar with ASL. This gap can lead to misunderstandings, exclusion from conversations, and overall difficulties in social and professional interactions for ASL users.

- Variability in Signing Styles: Just like spoken languages, ASL has individualized styles. Different ASL users may have unique ways of signing, including variations in hand shapes and movements. These nuances can make it difficult for even experienced interpreters or other ASL users to understand every individual's signing style.

- Complexity of Sign Languages: ASL is not just about hand gestures; it also encompasses non-manual components such as facial expressions and body movements. These elements are integral to conveying accurate information and emotions, adding layers of complexity to the language.

This mandates for an ASL recognition AI model which can successfully detect different gestures. This project showcases a model which is designed to interpret ASL by analyzing gesture video frames. It processes the visual information of ASL signs and translates them into English words. This approach can potentially standardize the interpretation of various signing styles, making ASL more accessible to non-users. The projct also involved usage of this model with live feed along with a graphical interface, a demo of which can be found below :


<div class="row justify-content-center">
    <div class="col-sm-auto mt-3 mt-md-0 text-center">
        <a href="https://drive.google.com/file/d/1v7pSkC9YUxCdeBODcFnZoVWaNTfSUju-/view?resourcekey">
            {% include figure.html path="imgs/asl/asl_demo.png" title="ASL Demo" class="img-fluid rounded z-depth-1" %}
        </a>
    </div>
</div>

<div class="caption">
    Demo showcasing the ASL model along with the GUI interface. Click on the above image to open the video link.
</div>

The model for ASL recognition uses different GRU and LSTM layers with appropriate hyper-parameters. The model pipeline is as follows:
- The feature vectors are extracted using InceptionResNetV2 and passed to the model.
- The video frames are classified into objects with InceptionResNet-2; then, the task is to create key points stacked for video frames
- The first layer of the neural network is composed of a combination of LSTM and GRU. 
- This composition can be used to capture the semantic dependencies in a more effective way;
- Dropout is used to reduce overfitting and improve the model’s generalization ability;
- The final output is obtained through the ‘softmax’ function
The following figure is a graphical representation of the model :

<div class="row justify-content-center">
    <div class="col-sm-auto mt-3 mt-md-0 text-center">
        {% include figure.html path="imgs/asl/asl_pipeline.png" title="ASL model pipeline" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    CNN model pipeline used for the ASL recognition task
</div>

