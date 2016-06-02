---
layout: post
title: ConvNets Explained
excerpt:
categories: blog
tags: ["Deep Learning", "CNNs"]
published: true
comments: true
share: true
---

Summation from: [CS231 by Andrej Karpathy](http://cs231n.github.io/convolutional-networks/)

Convolutional neural network is some specific combination of neural network so, it inherit the main concepts of neural network such having learnable weight and biases. Whole model still expresses a single differentiable score function. And they still have a loss function (e.g. SVM/Softmax) on the last (fully-connected) layer

ConvNet architectures make the explicit assumption that the inputs are images, which allows us to encode certain properties into the architecture.

Regular Neural Nets don't scale well to full images. <p style=color:red>For instance in CIFAR-10, images are only of size 32x32x3 (32 wide, 32 high, 3 color channels), so a single fully-connected neuron in a first hidden layer of a regular Neural Network would have 32*32*3 = 3072 weights.</p> NNs can still manage CIFAR-10 maybe but when sizes get larger, simple NNs are useless.  

Unlike a regular Neural Network, the layers of a ConvNet have neurons arranged in 3 dimensions: width, height, depth. <p style=color:red>(Note that the word depth here refers to the third dimension of an activation volume, not to the depth of a full Neural Network, which can refer to the total number of layers in a network.)</p>

> A ConvNet is made up of Layers. Every Layer has a simple API: It transforms an input 3D volume to an output 3D volume with some differentiable function that may or may not have parameters.

<img src="http://cs231n.github.io/assets/cnn/cnn.jpeg">

### Layers used to build ConvNet
Every layer of a ConvNet transforms one volume of activations to another through a differentiable function. There 3 main types of layers used in CNNs:

- Convolutional Layer
- Pooling Layer
- Fully-Connected Layer

You put these layers together to put up a CNN model.

A simple ConvNet for CIFAR-10 classification could have the architecture __[INPUT - CONV - RELU - POOL - FC]__, how:

- __INPUT__ [32x32x3] will hold the raw pixel values of the image, in this case an image of width 32, height 32, and with three color channels R,G,B.
- __CONV__ layer will compute the output of neurons that are connected to local regions in the input, each computing a dot product between their weights and the region they are connected to in the input volume. This may result in volume such as [32x32x12].
- __RELU__ layer will apply an elementwise activation function, such as the ```max(0,x)``` thresholding at zero. This leaves the size of the volume unchanged ([32x32x12]).
- __POOL__ layer will perform a __downsampling__ operation along the _spatial dimensions (width, height)_, resulting in volume such as [16x16x12].
- __FC__ (i.e. fully-connected) layer will compute the class scores, resulting in volume of size [1x1x10], where each of the 10 numbers correspond to a class score, such as among the 10 categories of CIFAR-10.


Share your thoughts with me by commenting below...

> Until next time, be safe...
