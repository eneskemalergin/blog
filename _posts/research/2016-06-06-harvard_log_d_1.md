---
layout: post
title: Harvard Log D-1
date: 06/06/16
categories: research
tags: ["Research Log", "Harvard", "Bioinformatics"]
published: true
comments: true
share: true
---


# DAY 1
---

Outline of the Day:
---
- _Arriving the Lab @ 8:45 am_
- _Morning Meeting @ 9:45 am_
  - Talked about language, __TensorFlow__
  - Talked about databasing tool, __genome database__
  - Talked about model type, __LSTM__
- _Session 1 @ 11:00 am_
  - TensorFlow installed
  - TensorFlow LSTM on MNIST data run
  - Making a virtualenv in Orchestra Cluster
  - TensorFlow installed for Orchestra Cluster
- _Session 2 @ 2:30 pm_
  -  __Reading:__ The human splicing code reveals new insights into the genetic determinants of disease by Brendan J. Frey
- _Seminar @ 3:00 pm_
- _Session 3 @ 4:00 pm_   
  - TensorFlow Tutorial Part 1
- _Leaving the Lab @ 7:30pm_

---

### Meeting

First thing in the morning, as soon as my supervisor arrives to the lab, we get together and had a meeting on what will be our next step on the computational model we were working in October 2015.

Previously we were using Torch7 for the CNN(convolutional neural network) model. This time to make it more accessible, and flexible to me (Since I am more fluent in Python) we changed our modeling language to Google's TensorFlow. TensorFlow is symbolic language for numerical computation using data flow graphs, and its with Python. I did't know about TensorFlow, however the syntax is Python's syntax, so it will not be hard for me to learn it.

Also during the meeting we decided to change our databasing tool (genomedata) to [genome database](https://github.com/gmcvicker/genome). We wanted to change our databasing tool because genomedata has very little support on the internet and their documentation is not very helpful. On the other hand genome database is more recent github project which has more support and the documentation is more clear and helpful.

In the meeting we also talked about the latest model's problems and how we could fix those problems. We decided to change the model type from CNN to LSTM(long-short time memory) type.

### Session 1
In the first session, I start installing the new tools we are going to use for following 2 months. First thing was to install TensorFlow in my macbook retina. To do that I went to github page of [TensorFlow](https://github.com/tensorflow/tensorflow), and used the setup method given [here](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/g3doc/get_started/os_setup.md) for Anaconda install, and Mac OS X.
In the installation guide, it was recommended to use virtual environment but I skipped that part directly installed TensorFlow into my system.

```bash
$ pip install --ignore-installed --upgrade https://storage.googleapis.com/tensorflow/mac/tensorflow-0.8.0-py2-none-any.whl
```

After Mac OS X installation is completed, I installed TensorFlow for my other laptop with Ubuntu 16.04 inside, using pretty much everything same. There are two options for Linux system installation, with GPU or without GPU. My laptop does not have GPU so I went with, without GPU option.

```bash
$ pip install --ignore-installed --upgrade https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-0.8.0-cp27-none-linux_x86_64.whl
```

I also need TensorFlow for my account on Orchestra Cluster. So I start installation process by creating a virtualenv, since my account in server is not admin I cannot do ```sudo```. To do this job I had to call Python module and CUDA module available in the cluster.


```bash
$ module load dev/python/2.7.6
$ module load dev/cuda/7.5.1
$ virtualenv name --system-site-packages # allows you to get ready  packages
$ source name/bin/activate
$ pip install --upgrade https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow-0.8.0-cp27-none-linux_x86_64.whl
```

After TensorFlow installation is done, I tried to install genome database tool but it was somewhat complicated and my computer complained about it a lot so I skipped installing that tool.

For session 2, I only read one paper: __The human splicing code reveals new insights into the genetic determinants of disease by Brendan J. Frey__, then my supervisor invited me to a seminar.

### Seminar
 In the seminar there was a student from University of Toronto, who came here for collaboration with our lab. He gave a small presentation, on his research about detecting protein density activity during cell cycle. Their research vastly depend on computational methods, like deep learning. Here are some points I understood.
 - They used convolutional neural network to classify the phases of cell cycle, from given image.
 - They also used another CNN model to detect all the cells in given image


They first locate cells and get small images of it using deep learning CNN model, then they analyze these small images of cells and classify them into phases in cell cycle. Then using some kind of coloring techniques they could color proteins by their types. With accomplishing these they can measure which proteins' density in cytoplasm is changed during different phases of cell cycle.

In results part of his presentation, he said "there are around 200 proteins that change in density according to different cell cycles."

Knowing which proteins work a part in this cell division might open a lot of different opportunities in medical area.

### Session 3
This was my last session in my first day, since I have to learn TensorFlow I started to search for good hands-on tutorial on TensorFlow and found really good one really quick.

I started [this](https://github.com/nlintz/TensorFlow-Tutorials) tutorial and also write more comments with jupyter notebook's amazing environment, so it became a blog post type of tutorial. ([You can find see my blog post](http://eneskemalergin.github.io//blog/TensorFlow_Tutorial_1/))

In this session, I managed to finish first 3 of 10 tutorials:
- Basic Multiplication
- Linear Regression
- Logistic Regression

---

> This was my day, see you soon...
