---
layout: post
title: TensorFlow Tutorial 2
excerpt:
categories: blog
tags: ["Python", "Machine Learning", "TensorFlow"]
published: true
comments: true
share: true
---

# Google's TensorFlow - Part 2

This part of the tutorial starts from FeedForward neural network implementation of TensorFlow and goes until Convolutional Neural Network part.

__Outline of the tutorial:__

0. [Basic multiplication](http://eneskemalergin.github.io//blog/TensorFlow_Tutorial_1/)
1. [Linear Regression](http://eneskemalergin.github.io//blog/TensorFlow_Tutorial_1/)
2. [Logistic Regression](http://eneskemalergin.github.io//blog/TensorFlow_Tutorial_1/)
3. [Feedforward Neural Network (Multilayer Perceptron) - Here]()
4. [Deep Feedforward Neural Network (Multilayer Perceptron with 2 Hidden Layers) - Here]()
5. [Convolutional Neural Network - Here]()
6. [Denoising Autoencoder]()
7. [Recurrent Neural Network (LSTM)]()

Let's start learning by coding...


```python
# Libraries we will use
import tensorflow as tf
import numpy as np
import tensorflow.examples.tutorials.mnist.input_data as input_data
```

## Feed-Forward Neural Network (Multilayer Perceptron)

Getting and preparing the data is same as we did before;


```python
mnist = input_data.read_data_sets("MNIST_data/", one_hot=True)
trX, trY, teX, teY = mnist.train.images, mnist.train.labels, mnist.test.images, mnist.test.labels
```

    Extracting MNIST_data/train-images-idx3-ubyte.gz
    Extracting MNIST_data/train-labels-idx1-ubyte.gz
    Extracting MNIST_data/t10k-images-idx3-ubyte.gz
    Extracting MNIST_data/t10k-labels-idx1-ubyte.gz


Let's start creating functions for model and weights:

- ```init_weigths``` function initialize the weights as we did in logistic regression.
- ```model``` functions creates our model structure. For this function since we are seeing it for the first time we will talks about it more:
    - first we initialize our sigmoid function, which will be basic multi layer percetron eventually. It is 2 logistic regression ```tf.matmul(x,y)``` stacked together. For ```h``` we assign ```tf.nn.sigmoid()``` with logistic regression then we also call logistic regression again with our ```h``` and ```w_o```.


```python
def init_weights(shape):
    return tf.Variable(tf.random_normal(shape, stddev=0.01))


def model(X, w_h, w_o):
    h = tf.nn.sigmoid(tf.matmul(X, w_h))
    return tf.matmul(h, w_o)
```

Then we create our symbolic variables, shared weight variables, and make a model out of it.


```python
X = tf.placeholder("float", [None, 784])
Y = tf.placeholder("float", [None, 10])

w_h = init_weights([784, 625])
w_o = init_weights([625, 10])

py_x = model(X, w_h, w_o)
```

Now, like we did in Logistic Regression example, [in the last post](), we compute the cost by using ```tf.reduce_mean()``` and ```tf.nn.softmax_cross_entropy_with_logits(py_x, Y)```(as a parameter).

After that we can construct our optimizers.


```python
cost = tf.reduce_mean(tf.nn.softmax_cross_entropy_with_logits(py_x, Y))
train_op = tf.train.GradientDescentOptimizer(0.05).minimize(cost)
predict_op = tf.argmax(py_x, 1)
```

Now it's time to start session and run all the model.


```python
with tf.Session() as sess:
    # you need to initialize all variables
    tf.initialize_all_variables().run()

    for i in range(100):
        for start, end in zip(range(0, len(trX), 128), range(128, len(trX), 128)):
            sess.run(train_op, feed_dict={X: trX[start:end], Y: trY[start:end]})
        print(i, np.mean(np.argmax(teY, axis=1) ==
                         sess.run(predict_op, feed_dict={X: teX, Y: teY})))
```

    (0, 0.69010000000000005)
    (1, 0.82250000000000001)
    (2, 0.86160000000000003)
    (3, 0.88029999999999997)
    (4, 0.88849999999999996)
    (5, 0.89329999999999998)
    (6, 0.89810000000000001)
    (7, 0.90090000000000003)
    (8, 0.9042)
    (9, 0.90580000000000005)
    (10, 0.90790000000000004)
    (11, 0.91039999999999999)
    (12, 0.91200000000000003)
    (13, 0.91320000000000001)
    (14, 0.91469999999999996)
    (15, 0.91510000000000002)
    (16, 0.91559999999999997)
    (17, 0.9163)
    (18, 0.91720000000000002)
    (19, 0.91790000000000005)
              .
              .
              .
    (90, 0.95120000000000005)
    (91, 0.95169999999999999)
    (92, 0.95199999999999996)
    (93, 0.95250000000000001)
    (94, 0.95309999999999995)
    (95, 0.9536)
    (96, 0.95389999999999997)
    (97, 0.95430000000000004)
    (98, 0.95440000000000003)
    (99, 0.95479999999999998)


As you can see from the accuracy above it works better than the logistic regression, at max ~0.955. Multilayer perceptron, is easily passed logistic regression around 33rd-34th epochs. However it is not the most optimized way possible to predict MNIST.

## Deep Feed-forward Neural Network (with Multiple Hidden Layers)

Our initializing weights functions came without a change:


```python
def init_weights(shape):
    return tf.Variable(tf.random_normal(shape, stddev=0.01))
```

In the model function, however we do add hidden layers and dropout layers, which gives the name deep neural network.

- ```tf.nn.relu()``` is layer for Rectified Linear Units(ReLU), which has logistic regression inside.
- ```tf.nn.dropout()``` is a special function, which drops random units to decrease the chance of overfitting and speeds up the process.
- In the model you can see we have 2 hidden layer 2x(relu + dropout)


```python
def model(X, w_h, w_h2, w_o, p_keep_input, p_keep_hidden):
    h = tf.nn.relu(tf.matmul(X, w_h))

    h = tf.nn.dropout(h, p_keep_hidden)
    h2 = tf.nn.relu(tf.matmul(h, w_h2))

    h2 = tf.nn.dropout(h2, p_keep_hidden)

    return tf.matmul(h2, w_o)
```

Getting the data same as we did above, I will now write here again, you can copy paste from there if you want.

We also create our symbolic variables, shared weight variables, and make a model out of it.


```python
X = tf.placeholder("float", [None, 784])
Y = tf.placeholder("float", [None, 10])

w_h = init_weights([784, 625])
w_h2 = init_weights([625, 625])
w_o = init_weights([625, 10])

p_keep_input = tf.placeholder("float")
p_keep_hidden = tf.placeholder("float")
py_x = model(X, w_h, w_h2, w_o, p_keep_input, p_keep_hidden)
```

Now we create cost function, train and predict optimizers. Cost function is the same as we were doing before, but now we change our optimizer to ```th.train.RMSPropOptimizer()```.

- ```RMSPropOptimizer``` uses RMSProp algorithm, which basically divides the gradient by a running average of its recent magnitude. (0.9 is represents the decay, it's default)

> In [this presentation](http://www.cs.toronto.edu/~tijmen/csc321/slides/lecture_slides_lec6.pdf) you can see different optimizers to use for statistical learning approaches.


```python
cost = tf.reduce_mean(tf.nn.softmax_cross_entropy_with_logits(py_x, Y))
train_op = tf.train.RMSPropOptimizer(0.001, 0.9).minimize(cost)
predict_op = tf.argmax(py_x, 1)
```

Now let's run the model with session:


```python
# Launch the graph in a session
with tf.Session() as sess:
    # you need to initialize all variables
    tf.initialize_all_variables().run()

    for i in range(100):
        for start, end in zip(range(0, len(trX), 128), range(128, len(trX), 128)):
            sess.run(train_op, feed_dict={X: trX[start:end], Y: trY[start:end],
                                          p_keep_input: 0.8, p_keep_hidden: 0.5})
        print(i, np.mean(np.argmax(teY, axis=1) ==
                         sess.run(predict_op, feed_dict={X: teX, Y: teY,
                                                         p_keep_input: 1.0,
                                                         p_keep_hidden: 1.0})))
```

    (0, 0.93969999999999998)
    (1, 0.96499999999999997)
    (2, 0.97109999999999996)
    (3, 0.97450000000000003)
    (4, 0.97509999999999997)
    (5, 0.9768)
    (6, 0.97989999999999999)
    (7, 0.97729999999999995)
    (8, 0.97760000000000002)
    (9, 0.9768)
    (10, 0.97940000000000005)
    (11, 0.9798)
    (12, 0.98119999999999996)
    (13, 0.9819)
    (14, 0.97999999999999998)
    (15, 0.98160000000000003)
    (16, 0.98170000000000002)
    (17, 0.98170000000000002)
    (18, 0.98260000000000003)
    (19, 0.98350000000000004)
    (20, 0.98160000000000003)
                .
                .
                .
    (90, 0.98380000000000001)
    (91, 0.98399999999999999)
    (92, 0.9839)
    (93, 0.98360000000000003)
    (94, 0.9839)
    (95, 0.98370000000000002)
    (96, 0.98419999999999996)
    (97, 0.98460000000000003)
    (98, 0.9839)
    (99, 0.98460000000000003)


So far the best accuracy is achieved with deep neural network model with 2 layer, you can adjust learning rate, batch size and so on, to improve the accuracy. Also you may try to add layers to improve (or maybe not) the model.


Now we more go into deep learning special area of machine learning. Our next stop will be for Convolutional Neural Network implementation for TensorFlow.

## Convolutional Neural Network
We start with the same things for almost all others we did:


```python
# Getting and preparing data for use: train, train.labels, test, test.labels
mnist = input_data.read_data_sets("MNIST_data/", one_hot=True)
trX, trY, teX, teY = mnist.train.images, mnist.train.labels, mnist.test.images, mnist.test.labels

# Defining batch size and test size differently
batch_size = 128
test_size = 256

# Again weight initialization function
def init_weights(shape):
    return tf.Variable(tf.random_normal(shape, stddev=0.01))
```

    Extracting MNIST_data/train-images-idx3-ubyte.gz
    Extracting MNIST_data/train-labels-idx1-ubyte.gz
    Extracting MNIST_data/t10k-images-idx3-ubyte.gz
    Extracting MNIST_data/t10k-labels-idx1-ubyte.gz


This time our model looks more comlicated, however it just has more layers that's only it. Let's have a closer look to it:

- ```tf.nn.relu()``` Rectifier Linear Unit has parameter:
    - ```tf.nn.conv2d()``` Computes a 2-D convolution given 4-D input and filter tensors with parameters:
        - ```X```: input, tensor of shape [batch, in_height, in_width, in_channels]
        - ```strides=[1,1,1,1]```: filter / kernel tensor of shape [filter_height, filter_width, in_channels, out_channels]
        - ```padding='SAME'```: The type of padding algorithm to use.
- ```tf.nn.max_pool()``` Performs the max pooling on the input with parameters:
    - ```l1a```: value: A 4-D Tensor with shape [batch, height, width, channels] comes from relu in our case
    - ```ksize=[1,2,2,1]```: The size of the window for each dimension of the input tensor.

- ```tf.reshape()``` reshapes the given tensor to given shape, ```l3```: given tensor, other gets shape of ```w4```


```python

def model(X, w, w2, w3, w4, w_o, p_keep_conv, p_keep_hidden):
    # Layer 1
    l1a = tf.nn.relu(tf.nn.conv2d(X, w, strides=[1, 1, 1, 1], padding='SAME'))
    l1 = tf.nn.max_pool(l1a, ksize=[1, 2, 2, 1], strides=[1, 2, 2, 1], padding='SAME')
    l1 = tf.nn.dropout(l1, p_keep_conv)

    # Layer 2
    l2a = tf.nn.relu(tf.nn.conv2d(l1, w2, strides=[1, 1, 1, 1], padding='SAME'))
    l2 = tf.nn.max_pool(l2a, ksize=[1, 2, 2, 1], strides=[1, 2, 2, 1], padding='SAME')
    l2 = tf.nn.dropout(l2, p_keep_conv)

    # Layer 3
    l3a = tf.nn.relu(tf.nn.conv2d(l2, w3, strides=[1, 1, 1, 1], padding='SAME'))
    l3 = tf.nn.max_pool(l3a, ksize=[1, 2, 2, 1], strides=[1, 2, 2, 1], padding='SAME')
    l3 = tf.reshape(l3, [-1, w4.get_shape().as_list()[0]])
    l3 = tf.nn.dropout(l3, p_keep_conv)

    # Layer 4
    l4 = tf.nn.relu(tf.matmul(l3, w4))
    l4 = tf.nn.dropout(l4, p_keep_hidden)

    pyx = tf.matmul(l4, w_o)
    return pyx
```

After making our model function for convolutional neural network, we need to reshape the data we have to fit it into our model.


```python
# Reshaping train and test images to 28x28x1 input
trX = trX.reshape(-1, 28, 28, 1)  
teX = teX.reshape(-1, 28, 28, 1)  

# Symbolic variable creationg
X = tf.placeholder("float", [None, 28, 28, 1])
Y = tf.placeholder("float", [None, 10])

# Initalizing weights for different shapes.
w = init_weights([3, 3, 1, 32])       # 3x3x1 conv, 32 outputs
w2 = init_weights([3, 3, 32, 64])     # 3x3x32 conv, 64 outputs
w3 = init_weights([3, 3, 64, 128])    # 3x3x32 conv, 128 outputs
w4 = init_weights([128 * 4 * 4, 625]) # FC 128 * 4 * 4 inputs, 625 outputs
w_o = init_weights([625, 10])         # FC 625 inputs, 10 outputs (labels)

p_keep_conv = tf.placeholder("float")
p_keep_hidden = tf.placeholder("float")

# Making model
py_x = model(X, w, w2, w3, w4, w_o, p_keep_conv, p_keep_hidden)
```

We use the same cost function and optimizers as we did in deep neural network section.


```python
cost = tf.reduce_mean(tf.nn.softmax_cross_entropy_with_logits(py_x, Y))
train_op = tf.train.RMSPropOptimizer(0.001, 0.9).minimize(cost)
predict_op = tf.argmax(py_x, 1)
```

Now let's run the model with sessions:


```python
with tf.Session() as sess:
    # you need to initialize all variables
    tf.initialize_all_variables().run()

    for i in range(100):
        training_batch = zip(range(0, len(trX), batch_size),
                             range(batch_size, len(trX), batch_size))
        for start, end in training_batch:
            sess.run(train_op, feed_dict={X: trX[start:end], Y: trY[start:end],
                                          p_keep_conv: 0.8, p_keep_hidden: 0.5})

        test_indices = np.arange(len(teX)) # Get A Test Batch
        np.random.shuffle(test_indices)
        test_indices = test_indices[0:test_size]

        print(i, np.mean(np.argmax(teY[test_indices], axis=1) ==
                         sess.run(predict_op, feed_dict={X: teX[test_indices],
                                                         Y: teY[test_indices],
                                                         p_keep_conv: 1.0,
                                                         p_keep_hidden: 1.0})))
```

    (0, 0.953125)
    (1, 0.984375)
    (2, 0.98046875)
    (3, 0.97265625)
    (4, 0.98828125)
    (5, 0.984375)
    (6, 0.984375)
    (7, 0.99609375)
    (8, 0.98828125)
    (9, 0.99609375)




I could not wait until convolutional network to complete, it takes really long on the CPU(2,5 hour for this case, I guess).  But in 9th epoch we hit ~0.99 accuracy which is really good.

What I realize while I am writing, running this tutorial up to this point is that the time that took the script to complete is inversely correlated with the model accuracy, which is very logical when you think how models work graphically...

For today, this is enough I have to digest all these information and make some use of it. Hopefully tomorrow, I will publish the 3rd part of this tutorial.

You can share your thoughts with me by commenting below…

> Until next time, be safe…
