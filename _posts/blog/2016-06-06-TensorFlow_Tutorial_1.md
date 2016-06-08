---
layout: post
title: Comprehensive TensorFlow Tutorial 
excerpt:
categories: blog
tags: ["Python", "Machine Learning", "TensorFlow"]
published: true
comments: true
share: true
---


# Google's TensorFlow


### About TensorFlow

TensorFlow™ is an open source software library for numerical computation using data flow graphs. Nodes in the graph represent mathematical operations, while the graph edges represent the multidimensional data arrays (tensors) communicated between them. The flexible architecture allows you to deploy computation to one or more CPUs or GPUs in a desktop, server, or mobile device with a single API. TensorFlow was originally developed by researchers and engineers working on the Google Brain Team within Google's Machine Intelligence research organization for the purposes of conducting machine learning and deep neural networks research, but the system is general enough to be applicable in a wide variety of other domains as well.[1](https://www.tensorflow.org/)


In this comprehensive tutorial, I tried to write everything explicitly as I understood from the Nathan Lintz's [tutorial](https://github.com/nlintz/TensorFlow-Tutorials) on github. I used the exact codes and explain statements. I hope this finds you well and you get valuable knowledge out of it.


> I give you here the outline of the list of tutorials will be available in my blog, for this post you will have the first 3.

__Outline of the tutorial:__

0. [Basic multiplication - Here]()
1. [Linear Regression - Here]()
2. [Logistic Regression - Here]()
3. [Feedforward Neural Network (Multilayer Perceptron)]()
4. [Deep Feedforward Neural Network (Multilayer Perceptron with 2 Hidden Layers)]()
5. [Convolutional Neural Network]()
6. [Denoising Autoencoder]()
7. [Recurrent Neural Network (LSTM)]()


## Basic Multiplication

We first call the libraries we will use in our tutorial.
- ```import``` statement is used to call libraries in Python
- ```as``` helps us to use short version of libraries


```python
import tensorflow as tf
import numpy as np
import tensorflow.examples.tutorials.mnist.input_data as input_data
from tensorflow.models.rnn import rnn, rnn_cell
```

TensorFlow is symbolic library meaning that is using symbolic expressions.
- ```tf.placeholder(type)``` creates symbolic variable of given type
- ```tf.mul(x, y)``` multiplies symbolic variables
- ```tf.Session()``` creates a session to evaluate expressions
- ```session.run(z, feed_dict={x:, y:})``` runs expressions with given parameters to already created variables in  ```feed_dict```

Let's see the usage of basic multiplication using TensorFlow:


```python
a = tf.placeholder("float") # Create a symbolic variable 'a'
b = tf.placeholder("float") # Create a symbolic variable 'b'

y = tf.mul(a, b) # multiply the symbolic variables

with tf.Session() as sess: # create a session to evaluate the symbolic expressions
    print("%f should equal 2.0" % sess.run(y, feed_dict={a: 1, b: 2})) # eval expressions with parameters for a and b
    print("%f should equal 9.0" % sess.run(y, feed_dict={a: 3, b: 3}))
```

    2.000000 should equal 2.0
    9.000000 should equal 9.0


## Linear Regression

First let's define our variables

- ```np.linspace(start, stop, number)``` is function of numpy, which returns evenly spaced numbers over a specified interval.
- ```np.random.randn```  creates random numbers with some noise.


```python
trX = np.linspace(-1, 1, 101)
trY = 2 * trX + np.random.randn(*trX.shape) * 0.33 # create a y value which is approximately linear but with some random noise
# create symbolic variables
X = tf.placeholder("float")
Y = tf.placeholder("float")
```

Making the linear regression is pretty easy we just need to multiply ```X``` variable by the ```weight```.


```python
def model(X, w):
    return tf.mul(X, w) # symbolic multiplications
```

In the next step we will create a shared variable for weight matrix
- ```Variable(0.0, name = "")``` initializing shared variable with some name

> <span style="color:red">When you train a model, you use variables to hold and update parameters. Variables are in-memory buffers containing tensors. They must be explicitly initialized and can be saved to disk during and after training. You can later restore saved values to exercise or analyse the model.[2](https://www.tensorflow.org/versions/r0.9/how_tos/variables/index.html)</span>



```python
w = tf.Variable(0.0, name="weights") # create a shared variable (like theano.shared) for the weight matrix
y_model = model(X, w) # Store the model in y_model
```

- ```tf.square(Y - y_model)``` gets the square error for cost function


```python
cost = tf.square(Y - y_model)
```

- ```tf.train.GradientDescentOptimizer(0.01).minimize(cost)``` constructs an optimizer to minimize cost using the cost function we created above, then it fit the line to our data


```python
train_op = tf.train.GradientDescentOptimizer(0.01).minimize(cost)
```

Now we can have the sessions do the rest but before we have to initialize the variables we created.
- ```tf.initialize_all_variables().run()``` is a function under the ```Variable()``` object, then it runs the intialization
- ```sess.run(train_op, feed_dict={X:x, Y:y})```  evaluates ```train_op``` with given parameters for 100 times
- then at the end we get a result of w, and we can run that with sessions.


```python
# Launch the graph in a session
with tf.Session() as sess:
    tf.initialize_all_variables().run()

    for i in range(100):
        for (x, y) in zip(trX, trY):
            sess.run(train_op, feed_dict={X: x, Y: y})

    print(sess.run(w))  # It should be something around 2
```

    2.0185


## Logistic Regression

Statically, logistic regression is type of regression model where the dependent variable (DV) is categorical.

Logistic regression measures the relationship between the categorical dependent variable and one or more independent variables by estimating probabilities using a logistic function, which is the cumulative logistic distribution. Thus, it treats the same set of problems as probit regression using similar techniques, with the latter using a cumulative normal distribution curve instead. Equivalently, in the latent variable interpretations of these two methods, the first assumes a standard logistic distribution of errors and the second a standard normal distribution of errors.[3](https://en.wikipedia.org/wiki/Logistic_regression)


The difference between linear and logistic regression:

In linear regression, the outcome (dependent variable) is continuous. It can have any one of an infinite number of possible values. In logistic regression, the outcome (dependent variable) has only a limited number of possible values.[4](http://stackoverflow.com/questions/12146914/what-is-the-difference-between-linear-regression-and-logistic-regression)

If you have no more questions about what is logistic regression, and if you can differentiate logistic with linear regression, then we can start coding.

In the following function, we initialize our weights with shared variable tactic, like we did in linear regression. Also we randomize it with given shape and standard deviation of 0.01


```python
def init_weights(shape):
    return tf.Variable(tf.random_normal(shape, stddev=0.01))
```


```python
# The same function from linear regression
def model(X, w):
    return tf.matmul(X, w) # same because there is a baked in cost function which performs softmax and cross entropy
```

Then we call our ```input_data``` library from the tensorFlow source. We will use this source to call MNIST data (one of the most popular datasets for deep learning, image processing topics).

- ```input_data.read_data_sets()``` is very straigth forward except ```one_hot=True```, which allows you to encode the data with oneHotencoding (For more information please see this [stackoverflow answer](http://stackoverflow.com/questions/17469835/one-hot-encoding-for-machine-learning))
- Then we assign train, test, and labels into variables


```python
mnist = input_data.read_data_sets("MNIST_data/", one_hot=True)
trX, trY, teX, teY = mnist.train.images, mnist.train.labels, mnist.test.images, mnist.test.labels
```

    Successfully downloaded train-images-idx3-ubyte.gz 9912422 bytes.
    Extracting MNIST_data/train-images-idx3-ubyte.gz
    Successfully downloaded train-labels-idx1-ubyte.gz 28881 bytes.
    Extracting MNIST_data/train-labels-idx1-ubyte.gz
    Successfully downloaded t10k-images-idx3-ubyte.gz 1648877 bytes.
    Extracting MNIST_data/t10k-images-idx3-ubyte.gz
    Successfully downloaded t10k-labels-idx1-ubyte.gz 4542 bytes.
    Extracting MNIST_data/t10k-labels-idx1-ubyte.gz



```python
X = tf.placeholder("float", [None, 784]) # create symbolic variables
Y = tf.placeholder("float", [None, 10])

w = init_weights([784, 10]) # like in linear regression, we need a shared variable weight matrix for logistic regression

py_x = model(X, w)
```

After creating variable and fitting calling the model function, now we have to define our cost function, optimizer.
- ``` tf.reduce_mean()``` gets the mean of given parameter
- ``` tf.nn.softmax_cross_entropy_with_logits(py_x, Y)``` is a intentionally implemented version of softmax


```python
cost = tf.reduce_mean(tf.nn.softmax_cross_entropy_with_logits(py_x, Y))
train_op = tf.train.GradientDescentOptimizer(0.05).minimize(cost) # construct optimizer
```


```python
predict_op = tf.argmax(py_x, 1) # at predict time, evaluate the argmax of the logistic regression
```

The we launch the session to run our objects.


```python
# Launch the graph in a session
with tf.Session() as sess:
    # you need to initialize all variables
    tf.initialize_all_variables().run()

    for i in range(100):
        for start, end in zip(range(0, len(trX), 128), range(128, len(trX), 128)):
            sess.run(train_op, feed_dict={X: trX[start:end], Y: trY[start:end]})
        print(i, np.mean(np.argmax(teY, axis=1) ==
                         sess.run(predict_op, feed_dict={X: teX, Y: teY})))
```

    (0, 0.88370000000000004)
    (1, 0.89690000000000003)
    (2, 0.90339999999999998)
    (3, 0.90739999999999998)
    (4, 0.90939999999999999)
    (5, 0.91059999999999997)
    (6, 0.91149999999999998)
    (7, 0.91310000000000002)
    (8, 0.91459999999999997)
    (9, 0.91500000000000004)
    (10, 0.91610000000000003)
    (11, 0.91669999999999996)
    (12, 0.91659999999999997)
    (13, 0.91659999999999997)
    (14, 0.91690000000000005)
    (15, 0.91749999999999998)
    (16, 0.91830000000000001)
    (17, 0.91849999999999998)
    (18, 0.91879999999999995)
    (19, 0.91920000000000002)
    (20, 0.91990000000000005)
              .
              .
              .
    (90, 0.92359999999999998)
    (91, 0.92359999999999998)
    (92, 0.92349999999999999)
    (93, 0.92349999999999999)
    (94, 0.92349999999999999)
    (95, 0.92369999999999997)
    (96, 0.92369999999999997)
    (97, 0.92369999999999997)
    (98, 0.92369999999999997)
    (99, 0.92359999999999998)


Not very accurate if we compare to it's other competitors but with that less line of code it is pretty awesome as well...

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

## Denoising Autoencoder
Before getting into the algorithm wise application of autoencoder, it will be good to have an understanding of what is autoencoder is. __An autoencoder neural network is an unsupervised learning algorithm that applies backpropagation, setting the target values to be equal to the inputs.__[1](http://ufldl.stanford.edu/tutorial/unsupervised/Autoencoders/)

> I am going to skip more detailed explanation of "What is Autoencoder", but you can learn what it is from [Lazy Programmer's blog post](http://lazyprogrammer.me/a-tutorial-on-autoencoders/).

---

Now we start coding our autoencoder by getting MNIST data, and preparing it as train, test, and labels.


```python
mnist = input_data.read_data_sets("MNIST_data/", one_hot=True)
trX, trY, teX, teY = mnist.train.images, mnist.train.labels, mnist.test.images, mnist.test.labels
```

    Extracting MNIST_data/train-images-idx3-ubyte.gz
    Extracting MNIST_data/train-labels-idx1-ubyte.gz
    Extracting MNIST_data/t10k-images-idx3-ubyte.gz
    Extracting MNIST_data/t10k-labels-idx1-ubyte.gz



```python
# Some variables
mnist_width = 28
n_visible = mnist_width * mnist_width
n_hidden = 500
corruption_level = 0.3
```

We start creating our nodes for input data and corruption mask, which we can name them as a feature of TensorFlow.

When we create nodes for hidden variables, we define the weight's max value and weight's size to stay in range of plus/minus weight's max value.


```python
# create node for input data
X = tf.placeholder("float", [None, n_visible], name='X')

# create node for corruption mask
mask = tf.placeholder("float", [None, n_visible], name='mask')

# create nodes for hidden variables
W_init_max = 4 * np.sqrt(6. / (n_visible + n_hidden))
W_init = tf.random_uniform(shape=[n_visible, n_hidden],
                           minval=-W_init_max,
                           maxval=W_init_max)

W = tf.Variable(W_init, name='W')
b = tf.Variable(tf.zeros([n_hidden]), name='b')

W_prime = tf.transpose(W)  # tied weights between encoder and decoder
b_prime = tf.Variable(tf.zeros([n_visible]), name='b_prime')
```

In the model function we use sigmoid neurons.


```python
def model(X, mask, W, b, W_prime, b_prime):
    tilde_X = mask * X  # corrupted X

    Y = tf.nn.sigmoid(tf.matmul(tilde_X, W) + b)  # hidden state
    Z = tf.nn.sigmoid(tf.matmul(Y, W_prime) + b_prime)  # reconstructed input
    return Z
```

We build the model and create a cost function with minimize squared error. For optimizer we use gradient descent algoritm


```python
# build model graph
Z = model(X, mask, W, b, W_prime, b_prime)

# create cost function
cost = tf.reduce_sum(tf.pow(X - Z, 2))
train_op = tf.train.GradientDescentOptimizer(0.02).minimize(cost)
```


```python
# Launch the graph in a session
with tf.Session() as sess:
    # you need to initialize all variables
    tf.initialize_all_variables().run()

    for i in range(100):
        for start, end in zip(range(0, len(trX), 128), range(128, len(trX), 128)):
            input_ = trX[start:end]
            mask_np = np.random.binomial(1, 1 - corruption_level, input_.shape)
            sess.run(train_op, feed_dict={X: input_, mask: mask_np})

        mask_np = np.random.binomial(1, 1 - corruption_level, teX.shape)
        print(i, sess.run(cost, feed_dict={X: teX, mask: mask_np}))
```

    (0, 111698.59)
    (1, 95930.391)
    (2, 87412.781)
    (3, 80946.078)
    (4, 76827.336)
    (5, 75148.266)
    (6, 73988.781)
    (7, 71955.133)
    (8, 69905.922)
    (9, 68616.172)
    (10, 67826.242)
          .
          .
          .
    (90, 57145.547)
    (91, 56103.793)
    (92, 57205.043)
    (93, 56911.43)
    (94, 56988.91)
    (95, 56763.688)
    (96, 56096.633)
    (97, 56045.938)
    (98, 56550.363)
    (99, 56243.789)


## Recurrent Neural Network(LSTM)

Code is pretty self explanatory...


```python
# variables
input_vec_size = lstm_size = 28
time_step_size = 28

batch_size = 128
test_size = 256

# Initializing Weights function
def init_weights(shape):
    return tf.Variable(tf.random_normal(shape, stddev=0.01))

```


```python
def model(X, W, B, init_state, lstm_size):
    # X, input shape: (batch_size, input_vec_size, time_step_size)
    XT = tf.transpose(X, [1, 0, 2])  # permute time_step_size and batch_size
    # XT shape: (input_vec_size, batch_szie, time_step_size)
    XR = tf.reshape(XT, [-1, lstm_size]) # each row has input for each lstm cell (lstm_size)
    # XR shape: (input vec_size, batch_size)
    X_split = tf.split(0, time_step_size, XR) # split them to time_step_size (28 arrays)
    # Each array shape: (batch_size, input_vec_size)

    # Make lstm with lstm_size (each input vector size)
    lstm = rnn_cell.BasicLSTMCell(lstm_size, forget_bias=1.0)

    # Get lstm cell output, time_step_size (28) arrays with lstm_size output: (batch_size, lstm_size)
    outputs, _states = rnn.rnn(lstm, X_split, initial_state=init_state)

    # Linear activation
    # Get the last output
    return tf.matmul(outputs[-1], W) + B, lstm.state_size # State size to initialize the stat
```


```python
mnist = input_data.read_data_sets("MNIST_data/", one_hot=True)
trX, trY, teX, teY = mnist.train.images, mnist.train.labels, mnist.test.images, mnist.test.labels
trX = trX.reshape(-1, 28, 28)
teX = teX.reshape(-1, 28, 28)

# Tensorflow LSTM cell requires 2x n_hidden length (state & cell)
init_state = tf.placeholder("float", [None, 2*lstm_size])

X = tf.placeholder("float", [None, 28, 28])
Y = tf.placeholder("float", [None, 10])

# get lstm_size and output 10 labels
W = init_weights([lstm_size, 10])
B = init_weights([10])

py_x, state_size = model(X, W, B, init_state, lstm_size)
```

    Extracting MNIST_data/train-images-idx3-ubyte.gz
    Extracting MNIST_data/train-labels-idx1-ubyte.gz
    Extracting MNIST_data/t10k-images-idx3-ubyte.gz
    Extracting MNIST_data/t10k-labels-idx1-ubyte.gz



```python
cost = tf.reduce_mean(tf.nn.softmax_cross_entropy_with_logits(py_x, Y))
train_op = tf.train.RMSPropOptimizer(0.001, 0.9).minimize(cost)
predict_op = tf.argmax(py_x, 1)
```


```python
# Launch the graph in a session
with tf.Session() as sess:
    # you need to initialize all variables
    tf.initialize_all_variables().run()

    for i in range(100):
        for start, end in zip(range(0, len(trX), batch_size), range(batch_size, len(trX), batch_size)):
            sess.run(train_op, feed_dict={X: trX[start:end], Y: trY[start:end],
                                          init_state: np.zeros((batch_size, state_size))})

        test_indices = np.arange(len(teX))  # Get A Test Batch
        np.random.shuffle(test_indices)
        test_indices = test_indices[0:test_size]

        print(i, np.mean(np.argmax(teY[test_indices], axis=1) ==
                         sess.run(predict_op, feed_dict={X: teX[test_indices],
                                                         Y: teY[test_indices],
                                                         init_state: np.zeros((test_size, state_size))})))
```

    (0, 0.6796875)
    (1, 0.8125)
    (2, 0.90234375)
    (3, 0.91015625)
    (4, 0.9375)
    (5, 0.921875)
    (6, 0.953125)
    (7, 0.96484375)
    (8, 0.97265625)
    (9, 0.9609375)
    (10, 0.9609375)
    (11, 0.98046875)
    (12, 0.94921875)
    (13, 0.9765625)
    (14, 0.9609375)
    (15, 0.98046875)
            .
            .
            .
    (85, 0.9921875)
    (86, 0.9609375)
    (87, 0.9765625)
    (88, 0.9765625)
    (89, 0.97265625)
    (90, 0.9765625)
    (91, 0.98046875)
    (92, 0.97265625)
    (93, 0.96875)
    (94, 0.9765625)
    (95, 0.9765625)
    (96, 0.9609375)
    (97, 0.98046875)
    (98, 0.97265625)
    (99, 0.9765625)


As we see from the result we get around ~98/99 accuracy. It's pretty similar to what we get from convolutional neural network, however RNN learns really fast or there is a overfitting.

I enjoyed following the tutorial, I get used to the syntax of TensorFlow and learned the essential concepts with TensorFlow. I will definitely add more blog posts with TensorFlow.

You can share your thoughts with me by commenting below…

> Until next time, be safe…
