---
layout: post
title: Harvard Log D-3
categories: research
tags: ["Research Log", "Harvard", "Bioinformatics"]
published: true
comments: true
share: true
---

# DAY 3
---

Outline of the Day:
---
- _Arriving the Lab @ 8:45am_
- _Morning Meeting @ 9:15am_
  - Talked about our new project
  - [ENCODE-DREAM in vivo Transcription Factor Binding Site Prediction Challenge](https://www.synapse.org/#!Synapse:syn6131484/wiki/400026)
- _Session 1 @ 10:30am_
  - Log D-2 completed
  - TensorFlow Tutorial Part 3
- _Session 2 @ 2:00pm_
  - Generative Adversarial Networks introduction
  - Converting Torch model to TensorFlow
- _Session 3 @ 5:30pm_
  - HDF5 and Python (h5py)
- _Leaving the Lab @ 6:00pm_

---

### Meeting
We talked about a new project. Our supervisor asked us if we want to go with a new project covering the subject and requiring the usage of same subset of tools. The good thing about this new project is, that it will be for Dream Challenge competition as well. Dream Challenge publishes a paper of winner submission on high impact journals such as Nature Biotechnology, Cell, Science, etc... So we decided to build a new model to be able to solve the challenge. Since they did not start the competition, we cannot see the data they will give to us, but we know what type of data they will give to us, so here our steps until they publish the competition data:

1. Understand the project
  - Read explanation
  - Read about Deep Bind
  - See Encode Data
2. Downloading sample data from [ENCODE]() (ctcf)
3. Motif Finding with FIMO
  - will be used as benchmarking
4. Implementation of model
5. Setting the data I/O style

For modeling we decided to use some kind of generative adversarial networks, which I had no idea what they are about.

### Session 1
In session 1, I complete log day 2 and published it in my blog. Then started working on TensorFlow tutorial from just where I left other day. I was planning on doing every one of them in github page but last 2/3 of them did not look really important to me at this point, so I skipped them. And merge all the 3 tutorials to make one comprehensive tutorial and push them to my website. While I was running the last part of the tutorial, I also fixed the main page ("Latest Posts"). Now you can see everything posted on the website there, before it was only blog posts.


### Session 2
In this session I searched for generative adversarial networks, and tried to understand how they work. I read [this paper](http://arxiv.org/pdf/1406.2661v1.pdf), and [this tutorial](http://evjang.com/articles/genadv1) written out of the paper. Generative adversarial networks are the unsupervised neural networks, which has 2 neural net tries to trick each other. The model learns from the ones error and ones accuracy, to get an optimum center point. It is not really have a end point, you will decide where to stop the iteration, when you think you have enough.

![Adversarial nets](https://pbs.twimg.com/media/CAkxhiNU8AAy9q5.png)

If you find this neural network intriguing, I highly recommend you to read the tutorial, you can also see the ipython notebook version of the codes used in tutorial from [here](https://github.com/eneskemalergin/Blog-Notebooks/blob/master/GenerativeAdversarialNetworks.ipynb)

After learning what is Adversarial network, I continue to convert our old model to TensorFlow.

### Session 3
After working on conversion, I realized that I need to learn hdf5 Python interface, h5py to be able to speed up. Then I started learning h5py library of Python.

This session was really short since I had to leave the lab.

---

> This was my day, see you soon...
