---
layout: post
title: Harvard Research Experience
excerpt:
categories: blog
tags: ["My Experiences"]
published: true
comments: true
share: true
image:
  feature: HMS_logo.jpg
  credit: Harvard Medical School
  creditlink: http://hms.harvard.edu

---

Hello internet, I am writing this blog post on my flight back to Houston.

You don't know where I did go? I thought that I yelled this to the world... :)

I went to Harvard Medical School, Genetics Department, Churchman Lab for summer research program, and this was not my first. I also work at Churchman Lab previous October as a visiting researcher. First time I was at Churchman Lab we worked on alternative splicing on Human cells, specifically HeLa cells. This time we are attending a competition called [ENCODE-DREAM](https://www.synapse.org/#!Synapse:syn6131484) challenge. I will talk all about the competition but before I wanted to talk about Churchman Lab.

Churchman Lab is at Genetics Department under Harvard Medical School. Main focus of the lab is uncovering the mysteries of transcription. Amazing people... That's really the brief answer of mine, if you ask me. What hit me when I first met with Churchman group, is that they are really close friends, above being only colleagues. That makes a really comforting atmosphere, for newcomers like myself and recently joined graduate students or post-docs. Currently Churchman Lab has 6 post-docs, 4 graduate student, and 1 lab technician, and its growing because of high quality research and publications. They were also really understanding and helpful people. To make it brief, it was a splendid atmosphere for us to do some science!

Let me talk a little bit about the research that we are doing for the churchman lab. (Yes, we are still continuing out research.) As I mentioned above we are attending a DREAM challenge. If you search about DREAM challenges you will see that they are really hard challenges under the biotechnology domain. Since they are hard, the incentives must be really good, right? Yes, they are really awesome incentives, such as publication and invited speaker at the systems biology conference. So, this challenge is worth a shot, as we thought. ENCODE-DREAM's goal is to make to universal toolset that can predict transcription factor binding sites across cell types. This task is done by many methods in the past and most of them are still being used by the community, such as ChIP-seq experiment followed by its analysis. This method actually is locating binding sites, not predicting them. However you can only locate one transcription factors binding site for one cell type for one ChIP-seq. Yeah, it does not sound practical. Thinking that humans have around 200 cell types and around 3000 transcription factors, which makes roughly 600K ChIP-seq experiments to locate all the binding sites of cell specific transcription factors. So, yes they pretty much did find all the binding sites and stored them in databases like [JASPER](http://jaspar.genereg.net). Other downside of ChIP-seq is that it cannot locate positive and negative binding sites, which can be really binding sites for other transcription factor. That's why developing a smart algorithm, that can learn how to locate binding sites, is important. People prefer machine learning algorithms since the prediction is their main purpose of existance. Recently Deep Learning used to predict binding sites; __DeepBind (Alipanahi et al., 2015), and DeepMotif (Lanchatin et al., 2016)__.  However they train their models with limited number of transcription factors and only one cell type. The purpose, again, is to make a model that can predict TFs across all cell types.

So it is what we are actually try to achieve, however our model is slightly more advanced and does more than what ENCODE-DREAM requires us to do. Unfortunately, I will not talk about the model or data processing steps in here, since the competition is going on until September 30th.

It is top secret for now :)

> Hey do you know there is a comment section below that you can share your ideas with me?

> Until next time, be safe...
