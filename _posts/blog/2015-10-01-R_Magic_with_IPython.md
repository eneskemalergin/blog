---
layout: post
title: R Magic with IPython
excerpt:
categories: blog
tags: ["Bioinformatics", "Python", "R"]
image:
  feature: so-simple-sample-image-5.jpg
  credit: WeGraphics
  creditlink: http://wegraphics.net/downloads/free-ultimate-blurred-background-pack/
published: true
comments: true
share: true
---

IPython, anything flashed? If you are not familiar with IPython, I highly recommend you to learn it, since it's a great tool for reproducible science. Also with extensive features you will increase you productivity with huge rates.

But in this particular post we will examine the ```magic``` commands to deal with R. To be survive on this article you need to use the [previous blog](http://eneskemalergin.github.io/2015/09/18/Interfacing_with_R_via_rpy2/) post examples that we did using ```rpy2```, as well as IPython(or now Jupyter).

There are two options to using Ipython, by interactive environment, or notebook version. I will follow the notebook version because it is more user friendly looking version, which can be customized more.

#### Download Ipython/Jupyter

You can install it by using ```pip```, or ```conda``` package manager

```
$ pip install jupyter
## OR
$ conda install jupyter
```

In you directory of choice start jupyter notebook by writing the following command on terminal-command promt.

```
$ jupyter notebook
```

It will open notebook main interface, click new and open a new notebook. When you get the new notebook go to the cell one and type the following

```Python
import rpy2.robjects.lib.ggplot2 as ggplot2
%load_ext rpy2.ipython
```

- In the code above, we use ```%``` to start IPython specific directives.
- We called the ```rpy2.robjects``` package which allows us to do such things:
  - %R print(c(1,2))

---

Let's Read the ```sequence.index``` file that we download in previous posts. In a new cell which you can add one after one;

```
%%R
seq.data <- read.delim('sequence.index', header = T, stringsAsFactors=F)
seq.data$READ_COUNT <- as.integer(seq.data$READ_COUNT)
seq.data$BASE_COUNT <- as.integer(seq.data$BASE_COUNT)
```

- Writing ```%%R``` allows us to use that specific cell as a R environment.
- When you defined cells with ```%%R``` then Ipython will interpret it as R code no needs for function calls from ```robjects```.

---

Now we can transfer a variable to Python namespace:

```
seq_data = %R seq.data
```

---

If you want to put the data back in R namespace, you may do the following;

```
%R -i seq_data
%R print(colnames(seq_data))
```

- ```-i``` argument informs the magic system that the variable that follows on the Python space is to be copied in the R namespace.

---

R magic system is also allows you to reduce code as it changes the behavior of the interaction of R with IPython.

```
%%R
bar <- ggplot(seq_data) + aes(factor(CENTER_NAME))+ geom_bar() +
      theme(axis_text_x = element_text(angle = 90, hjust = 1))

print(bar)
```

- In previous blog post we should have defined the graphical console and the extension but now IPython notebook deals with it.

---

If you want to use R with Python, R magic makes things much more easier.

I will continue to follow the [Bioinformatics with Python Cookbook](http://www.amazon.com/Bioinformatics-Python-Cookbook-Tiago-Antao/dp/1782175113) to use it as reference to these tutorials, next big topic will be Next Generation Sequencing.

> Until then, be safe...
