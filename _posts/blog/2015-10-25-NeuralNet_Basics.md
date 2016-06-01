---
layout: post
title: Neural Network Basics
excerpt:
categories: blog
tags: ["Deep Learning", "Python", Neural Networks]
image:
  feature: so-simple-sample-image-5.jpg
  credit: WeGraphics
  creditlink: http://wegraphics.net/downloads/free-ultimate-blurred-background-pack/
published: true
comments: true
share: true

---


Hello all today I will start deep learning series by starting with the Neural Networks Basics. Understanding of neural networks is the key to deep learning. So if you cannot get some thing or you find fallacies, please let me know. Here it comes...

> Also if you want to see the ipython version you can view it from this  [link](https://github.com/eneskemalergin/Blog-Notebooks/blob/master/Basic_NeuralNets.ipynb), and download it from this [link](https://raw.githubusercontent.com/eneskemalergin/Blog-Notebooks/master/Basic_NeuralNets.ipynb)

## Introduction
We humans are really good at recognizing and making sense of objects around us by simply looking at them, and we do this instantly without realizing it. But the same task is not as easy as for computers. They cannot understand what they have given by defining some conditions easily.

To be able to make computers to recognize objects we may use neural networks. Neural network was a tool for machine learning at the first then they improved the functions and algorithms, and they make it the basics of "Deep Learning".

Neural networks as we defined in machine learning, they need __test data__ to learn from. If we give accurate training data then we can use them to teach computer. After iterations then we will use test data to calculate accuracy. If we increase the number of examples in training data, the accuracy of algorithm might increase.(I used "might" because using proper data is essential on data)




## Perceptrons

- Their history goes back to 1950's, they are not common today.
- They are called artificial neural networks, and they are very basic design of neural network
- Gets multiple binary inputs and produces single output.

![Single Perceptron](http://eneskemalergin.github.io/images/perceptron.png)

- Then inputs are multiplyed by weights which effects the output
- Output result only 0 or 1, determined by the following;

\\[
\begin{eqnarray}
  \mbox{output} & = & \left\{ \begin{array}{ll}
      0 & \mbox{if } \sum_j w_j x_j \leq \mbox{ threshold} \\
      1 & \mbox{if } \sum_j w_j x_j > \mbox{ threshold}
      \end{array} \right
\tag{1}\end{eqnarray}
\\]

- By varying weight and treshold, we can get different models of decision making
- Each neuron/node in a neural network have a different decisions to make
- Increasing nodes or layers you get more sophisticated decisions
- Perceptron has only 1 output.

Let's simplfy the way we describe it.  

\\[ w \cdot x \equiv \sum_j w_j x_j \\]


- Let's moce the treshold to the otherside of the inequality and replace it by what's known as the perceptron's bias,

\\[
b \equiv
-\mbox{threshold}
\\]

Now we have:

\\[
\begin{eqnarray}
  \mbox{output} = \left\{
    \begin{array}{ll}
      0 & \mbox{if } w\cdot x + b \leq 0 \\
      1 & \mbox{if } w\cdot x + b > 0
    \end{array}
  \right
\tag{2}\end{eqnarray}
\\]

> __Bias__: is measure of how easy it is to get the perceptron output a 1.

- Described perceptrons as a method for weighing evidence to make decisions.
- Perceptrons can be used to computer logical functions (AND, OR, and NAND) too

## Sigmoid Neurons

After finding out that perceptrons are not very useful for small changes or real numerical changes, they upgrade concept by changing the function.

Small changes in sigmoid neurons' weight and bias won't cause huge changes. It has also the same structure but the function in neuron is different.

![Perceptron](http://eneskemalergin.github.io/images/perceptron.png)

Inputs can have values between 0 and 1, real numbers like, 0.65245... Also the output may get float numbers as well.

Since sigmoid neurons are derived from perceptrons the function will be ```sigmoid(w.x+b)``` and functional,

\\[
\begin{eqnarray}
  \sigma(z) \equiv \frac{1}{1+e^{-z}}.
\tag{3}\end{eqnarray}
\\]

Explicitly:

\\[
\begin{eqnarray}
  \frac{1}{1+\exp(-\sum_j w_j x_j-b)}.
\tag{4}\end{eqnarray}
\\]

Sigmoid Function
![Sigmoid Function](http://eneskemalergin.github.io/images/sigmoidfunction.png)


Step Function
![Step Function](http://eneskemalergin.github.io/images/step.png)

If sigma function had infact been a step functions then the sigmoid neuron would be a perceptron since the output would be 0 or 1.

- By using sigma function we smoothed out perceptron.

\\[
\begin{eqnarray}
  \Delta \mbox{output} \approx \sum_j \frac{\partial \, \mbox{output}}{\partial w_j}
  \Delta w_j + \frac{\partial \, \mbox{output}}{\partial b} \Delta b,
\tag{5}\end{eqnarray}
\\]

The \\( \Delta \mbox{output} \\) is a linear function of the changes \\(\Delta w_j \\) and \\( \Delta b \\) in the weight and bias.

Biggest difference between perceptron and sigmoid neurons is that sigmoid won't jump 0 to 1 real numbers are possible.

## The Architecture of Neural Networks

- Hidden layer only means not input or output
- In deep learning more than one hidden layer situation is possible

![](http://eneskemalergin.github.io/images/neuralNets1.png)

- Designing input and output nodes are more straightforward.

Let's try to determine wheather a handwritten image despites a "9" or not.

1. Encoding the intensities of image pixels into the input neurons
2. 64x64 pix image 4096 input neurons, with th intensities scaled appropriately between 0 and 1
3. Output layer will contain just a single neuron, with output values of less than 0.5 indicating "input image is not a 9", and values greate than 0.5 indicating "input image is a 9"


Neural networks where the output from one layer is used as input to the next layer which is called feedforward networks. There is no looping in this kind of network.

> Recurrent Neural Networks are the ones which allows you to use looping in network. Concept of RNN is interesting because it works more similar to our Brain work flow. They are less powerful, and not popular because of that.

Share your thoughts with me by commenting below...

> Until next time, be safe...
