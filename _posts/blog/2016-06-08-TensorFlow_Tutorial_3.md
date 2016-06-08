---
layout: post
title: TensorFlow Tutorial 3
excerpt:
categories: blog
tags: ["Python", "Machine Learning", "TensorFlow"]
published: true
comments: true
share: true
---

# Google's TensorFlow - Part 3

This part of the tutorial covers denoising autoencoder and LSTM implementation.

__Outline of the tutorial:__

0. [Basic multiplication](http://eneskemalergin.github.io//blog/TensorFlow_Tutorial_1/)
1. [Linear Regression](http://eneskemalergin.github.io//blog/TensorFlow_Tutorial_1/)
2. [Logistic Regression](http://eneskemalergin.github.io//blog/TensorFlow_Tutorial_1/)
3. [Feedforward Neural Network (Multilayer Perceptron)](http://eneskemalergin.github.io//blog/TensorFlow_Tutorial_2/)
4. [Deep Feedforward Neural Network (Multilayer Perceptron with 2 Hidden Layers)](http://eneskemalergin.github.io//blog/TensorFlow_Tutorial_2/)
5. [Convolutional Neural Network](http://eneskemalergin.github.io//blog/TensorFlow_Tutorial_2/)
6. [Denoising Autoencoder - Here](http://eneskemalergin.github.io//blog/TensorFlow_Tutorial_3/)
7. [Recurrent Neural Network (LSTM) - Here](http://eneskemalergin.github.io//blog/TensorFlow_Tutorial_3/)

Let's start learning by coding...


```python
# Libraries we will use
import tensorflow as tf
import numpy as np
import tensorflow.examples.tutorials.mnist.input_data as input_data
from tensorflow.models.rnn import rnn, rnn_cell
```

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

With this post I will conclude this series of blog posts, but I will add more posts with TensorFlow, hopefully they will be more original.


You can share your thoughts with me by commenting below…

> Until next time, be safe…
