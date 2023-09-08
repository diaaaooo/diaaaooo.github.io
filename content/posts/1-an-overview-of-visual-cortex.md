---
title: "An Overview of Visual Cortex"
date: 2023-09-07T00:00:00+00:00
# weight: 1
# aliases: ["/first"]
tags: ["Visual Cortex", "Computer Vision"]
author: "Diao"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
# description: "Desc Text."
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: false
ShowRssButtonInSectionTermList: true
UseHugoToc: true
menu:
  main:
    identifier: "posts"
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
# editPost:
#     URL: "https://github.com/<path_to_repo>/content"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

I like to dig deep into the origin to learn how one thing evolved to its current state when I learn something new. To learn about computer vision, one has to understand Convolutional Neural Network, short for “CNN”. And to fully understand convolutional neural networks, we have to look back to its origin - Visual Cortex. 

I am not an expert of the structure of human eyes or how the visual system works. But I will try my best to explain what I learned about the human visual cortex from reading papers and how it is connected to the structure of convolutional neural networks. 

## Basic Terminology 
These are the unavoidable terms that you will see in a paper involving the visual cortex. 

### Cortex
By definition, cortex means the outer layer of a structure or organ. 

### Cerebral Cortex
In the context of the brain, the cerebral cortex, also known as the neocortex, specifically refers to the outermost layer of the brain’s cerebrum. It’s responsible for higher cognitive functions, including sensory processing (vision, hearing, touch and proprioception, taste and smell), motor control, language processing, perception and attention (object recognition, face recognition, scene analysis), memory and more. 

### Occipital Lobe
Occipital lobe is a region of the cerebral cortex located at the back of the brain, responsible for processing visual information. It handles visual processing (color, shape, motion), visual perception (transform into meaningful visual experiences), object recognition (recognize and identify), spatial awareness (object location, contribute to judging distance to some extent, particularly in the context of depth perception), motion detection (object movement) and more.

### Ventral Stream
Ventral stream is the “what pathway” located in the occipital lobe. It is the pathway for visual inputs processing, object detection and recognition. It is usually considered the inspiration of the design of convolutional neural networks. 

### Dorsal Stream
Dorsal stream is the “where pathway” located in the parietal lobe which is adjacent to the occipital lobe. It is the pathway for spatial perception and motor control. It is so crucial to object detection and recognition, especially in spatial perception, that we cannot ignore it while trying to understand how the visual cortex works. 

[image]

## Relevant Ventral Stream Components

Ventral stream is far more complex than what I can explain. Since we are aiming to understand its connection to CNN, I’ll only cover the components of the ventral stream that I think are relevant to the structure of convolutional neural networks. 

### V1
The primary visual cortex, short for V1,  extracts low-level information from the visual input, such as edges, colors, and orientations. 

### V2 
The secondary visual cortex, short for V2, continues to process basic visual features by extracting more-complex features like shapes and textures, as well as in the detection of motion.

### V3
The third visual cortex, short for V3, analyzes motion, orientation, and basic spatial information. 

### V4
This fourth visual cortex, short for V4, is specialized in color perception, shape processing, the section of object boundaries, and is sensitive to color constancy (the ability to perceive color despite changes in lighting conditions). 

### IT Cortex
The inferotemporal cortex, short for IT cortex, is specialized for object recognition and identification, as well as associates objects with memories to assign meanings and contextual information. 

## Visual Information Flow

All papers pointed me back to [this](https://www.cns.nyu.edu/~tony/vns/readings/ungerleider-mishkin-1982.pdf) original research about how visual information flows. It proposed that visual information splits into two directions after arriving in the retina: ventral stream (the “what” pathway) and dorsal stream (the “where” pathway). Ventral stream focuses on object detection and recognition. Dorsal stream focuses on spatial feature analysis and motor control. 

Since then, the ventral stream information flow was believed to be a feedforward linear architecture specialized for object detection and recognition. 

### Feedforward Linear Architecture

Visual input accepted by retina flows into V1. V1 extracts low-level information like edges, colors, and orientations then passes the processed information onto V2. V2 extracts more complex information like shapes, textures and detects motion then passes the processed information onto V4. V3 is often left out due to the fact that it is specialized in the analysis of spatial information which is more like a dorsal stream’s thing than ventral stream. V4 receives information from V2 and continues to process higher level information like shapes, object boundaries and lighting then pass the processed information to the IT cortex where neurons handle object recognition and identification. The IT cortex is considered the endpoint of the ventral stream. 

[This](https://www.pnas.org/doi/10.1073/pnas.0700622104) biological science paper presented the feedforward linear architecture which looks very similar to a convolutional neural network. The paper also explained why such architecture is supported even though there are local feedback loops and general feedback loops across the entire ventral stream. 

[Image]

The ML field also accepted such a belief. [This](https://arxiv.org/abs/1702.07800) review paper of deep learning models submitted in 2017 proposed one version of explanation. It has become very popular since the citation in [this](https://lilianweng.github.io/posts/2017-06-21-overview/) deep learning overview post published in [Lilian Weng’s blog](https://lilianweng.github.io/). The breakthrough design in Residual Net (ResNet) which allows inputs from one layer to be passed down to two layers after is also associated with the shortcut between V1 and V4. V4 was found to be able to accept information directly from V1. 

It offers a very elegant explanation of how CNN and visual cortex are connected and it could certainly be how convolutional neural networks were inspired. But I felt obligated to also look into different opinions and see if the continuous research in the visual cortex field has moved forward and brought up new ideas. It does. 

### Recurrent Non-Linear Architecture

[This](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3532569/) cognitive science paper published in 2014 brought up a different perspective since it found more and more studies and research that support its opinion. It challenges that the visual information flow is actually a recurrent non-linear architecture instead of a simple feedforward linear architecture. 

V1 actually sends out processed information to V2, V3, V4 and MT (a component related to memory processing) simultaneously. All other components continuously send feedback back to help correct the processing. The entire visual information flow is a continuous loop with multiple complex loops inside it. All of these contribute to correct object detection and recognition. 

It can also explain why YOLO is not good at detecting small objects in local regions to a certain extent. Because YOLO lacks components like V3 that handles basic spatial information processes and keeps correcting the main processing stream. This is just my guess though. To investigate the real causes and solutions, I would need to learn more about how human’s visual system extracts depth information solely from visual inputs and how it can be implemented in ML. 

## References

[1] Ungerleider et al. “[Two Cortical Visual Systems.](https://www.cns.nyu.edu/~tony/vns/readings/ungerleider-mishkin-1982.pdf)" NYU (1982)

[2] Serre et al. “[A feedforward architecture accounts for rapid categorization.](https://www.pnas.org/doi/10.1073/pnas.0700622104)" PNAS PNAS:104(15)6424-6429 (2007)

[3] Wang et al. “[On the Origin of Deep Learning.](https://arxiv.org/abs/1702.07800)" arVix preprint arXiv:1702.07800 (2017)

[4] Weng, Lilian. (Jun 2017). "[An Overview of Deep Learning for Curious People](https://lilianweng.github.io/posts/2023-06-23-agent/)". Lil’Log. https://lilianweng.github.io/posts/2023-06-23-agent/.

[5] Kravitz et al. “[The ventral visual pathway: An expanded neural framework for the processing of object quality.](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3532569/)" NCBI doi: 10.1016/j.tics.2012.10.011 (2014)
