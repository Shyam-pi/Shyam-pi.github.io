---
layout: page
title: American Sign Language Detection
description: A CNN and LSTM based American Sign Language (ASL) Detector for Letters from video feeds
img: imgs/asl/asl_logo_new.jpg
importance: 3
category: Computer Vision
related_publications:
---

**DEMO**

A demo showcasing the ASL model along with the GUI interface is available below:

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

**INTRODUCTION**

- **Communication Gap**: There exists a fundamental barrier in communication between ASL users and individuals unfamiliar with ASL. This gap can lead to misunderstandings, exclusion from conversations, and overall difficulties in social and professional interactions for ASL users.

- **Variability in Signing Styles**: Similar to spoken languages, ASL exhibits individualized styles. Different ASL users may have unique ways of signing, including variations in hand shapes and movements. These nuances can challenge even experienced interpreters or other ASL users to understand every individual's signing style.

- **Complexity of Sign Languages**: ASL encompasses more than just hand gestures; it also includes non-manual components such as facial expressions and body movements. These elements are integral to conveying accurate information and emotions, adding layers of complexity to the language.

This underscores the need for an ASL recognition AI model capable of successfully detecting different gestures. This project presents a model designed to interpret ASL by analyzing gesture video frames. It processes the visual information of ASL signs and translates them into English words. This approach has the potential to standardize the interpretation of various signing styles, thereby making ASL more accessible to non-users.

**OBJECTIVE**

The primary objective of this project is to develop an accurate and efficient ASL detection system using a combination of CNN and LSTM layers. By analyzing gesture video frames, we aim to accurately translate ASL signs into English words, thereby bridging the communication gap between ASL users and non-users.

**METHODOLOGY**

1. **Feature Extraction**: Feature vectors are extracted using InceptionResNetV2, which are then passed to the model for further processing.

2. **Object Classification**: Video frames are classified into objects using InceptionResNetV2. Subsequently, key points are created and stacked for video frames.

3. **Model Architecture**: The model consists of LSTM and GRU layers arranged in a sequential manner to capture semantic dependencies effectively. Dropout is employed to reduce overfitting and improve generalization ability.

4. **Training**: The model is trained using appropriate hyperparameters and the softmax function is utilized to obtain the final output.

<div class="row justify-content-center">
    <div class="col-sm-auto mt-3 mt-md-0 text-center">
        {% include figure.html path="imgs/asl/asl_pipeline.png" title="ASL model pipeline" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Graphical representation of the CNN model pipeline used for the ASL recognition task
</div>

**RESULTS**

The trained ASL recognition model demonstrates promising results in accurately detecting and translating ASL gestures into English words. By leveraging CNN and LSTM layers, the model effectively captures the nuances of ASL, including variations in signing styles and non-manual components such as facial expressions and body movements.

**CONCLUSION**

In conclusion, this project highlights the effectiveness of CNN and LSTM-based models in ASL detection tasks. By accurately interpreting ASL gestures from video feeds, this technology has the potential to significantly improve communication and accessibility for ASL users in various social and professional settings. Further advancements in this field could lead to even greater inclusivity and understanding between ASL users and non-users.