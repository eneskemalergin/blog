---
layout: post
title: Creating conda Environment
excerpt:
categories: blog
tags: ["Bioinformatics", "Python", "R", "Terminal"]
published: true
date: 2015-09-11 12:00:00
comments: true
share: true
---

In this small tutorial we will create a virtual conda environment to be able to start your Bioinformatics work with Python.

So you are viewing this because you like to work on Bioinformatics area and you are using Python to do this job. Python has a growing community with a lot of scientists. That means scientific 3rd-party libraries are dramatically increasing. There are some robust libraries/softwares that are using in computational biology, such as;

- [IPython](http://ipython.org/): IPython is an interactive notebook that you can take notes, write codes, prepare presentations with it.
- [SciPy](http://scipy.org/): SciPy provides many user-friendly and efficient numerical routines such as routines for numerical integration and optimization.
- [Biopython](http://biopython.org/wiki/Main_Page): BioPython is a pure Python library that focuses specifically Bioinformatics.
- [matplotlib](http://matplotlib.org/): Matplotlib is a visualization library that you can present your research with fancy graphs and visualizations.

There are more but these are the most common ones in use right now.

Now we can start our little tutorial:

1. First thing that you need to do is to download the [Anaconda distribution](http://continuum.io/downloads) you can choose Python version 2 or 3. Don't worry if you change your mind after you start using the one version, because Anaconda will let you use other versions as well.   

2. Now you have the Anaconda then we create our conda environment with BioPython 1.65 and we will name it bioinformatics.

```
conda create -n bioinformatics biopython biopython=1.65 python=2.7
// OR for Python 3.X
conda create -n bioinformatics biopython biopython=1.65 python=3.4
```

3. We need to activate the environment to use it:

```
source activate bioinformatics
```

4. Then there are some core packages that we need to isntall as well:

```
conda install scipy matplotlib ipython-notebook binstar pip
conda install pandas cyton numba scikit-learn seaborn
```

5. In our future projects we will also need ```pygraphviz``` which is not availabe in anaconda directly so we need to download with pip:

```
pip install pygraphviz
```

6. Now it's time to install the bioinformatics packages, some of them from anaconda and some of them from pypi:

```
conda install -c https://conda.binstar.org/bcbio  pysam
conda install -c https://conda.binstar.org/simupop simuPOP

pip install pyvcf
pip instlal dendropy
```

7. This is optional part but I highly recommend you to do this as well, which is integration R with Python. Since R is also huge in scientific community, using also R with Python will be a plus. You can install R from [here](http://www.r-project.org/)

8. When you get the R, run this command in R to be able to use bioconductor:

```R
source("http://bioconductor.org/biocLite.R")
biocLite()
```

 - Inside the R install the following packages which they will help you:

```R
install.packages("ggplot2")
install.packages("gridExtra")
```

9. Finally you need to install ```rpy2``` package which gives you a bridge between R and Python. Run this on terminal:

```
pip install rpy2
```

This small tutorial was the first bioinformatics tutorial, be tuned for more...
