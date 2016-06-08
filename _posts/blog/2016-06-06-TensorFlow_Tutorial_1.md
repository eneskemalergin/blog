---
layout: post
title: TensorFlow Tutorial 1
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

I will continue to write other 8 tutorials given in github page, and hopefully more...

You can share your thoughts with me by commenting below…

> Until next time, be safe…
