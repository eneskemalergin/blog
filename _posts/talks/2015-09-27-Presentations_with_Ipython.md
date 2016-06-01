---
layout: presentation
title: Presentations with IPython
theme: moon
categories: talks
published: true
---
{{site.startvertical}}
{{site.startslide}}
# Presentations with IPython

> Presented By Enes Kemal Ergin

{{site.nextslide}}
#### About Me

- [Personal Blog](http://eneskemalergin.github.io/)
- [Github](https://github.com/eneskemalergin)
- [Email](eneskemalergin@gmail.com)
{{site.endslide}}
{{site.endvertical}}

{{site.startslide}}
Outline
---

1. Installing IPython
2. Making the Presentation
3. Converting to Presentation Locally
4. Extra: How am I putting it into my blog

{{site.endslide}}

{{site.startvertical}}
{{site.startslide}}
1. Installing IPython
---

> We are going to install Jupyter instead of IPython, because Jupyter is the version 3.0 of IPython.

{{site.nextslide}}
### __For Linux Users:__

```
sudo apt-get install python-pip
pip install jupyter
```

{{site.nextslide}}
### __For MacOS Users:__

```
sudo easy_install pip
pip install jupyter
```

{{site.nextslide}}
### __For Windows Users:__

Download the latest version of the Python either 2.7.9/newer, or 3.4/newer. They come with pip install already.

```
pip install jupyter

# OR

pip3 install jupyter
```
{{site.endslide}}
{{site.endvertical}}

{{site.startvertical}}
{{site.startslide}}
2. Making the Presentation
---


First thing to do is to open a IPython/jupyter notebook via terminal

```
jupyter notebook
```

> Careful that it will open the jupyter console at the current directory of the terminal.



{{site.nextslide}}
Click the _```new```_ button and choose _```Python 2```_ (or 3 according to your choice of version).
<img style="max-width: 100%;" src="{{site.baseurl}}/images/newNotebook.png"></img>

{{site.nextslide}}
Then you will see an empty notebook like this:

<img style="max-width: 100%;" src="{{site.baseurl}}/images/EmptyNotebook.png"></img>


- Change the ```Cell Toolbar``` to __Slideshow__
- End change the cell type which is next to ```Cell Toolbar``` to __Markdown__.
- If you want to include codes and runned version of the code you may leave the type __code__

{{site.nextslide}}

```python
# Here is how you can put Code inside the Presentation using Jupyter

"""
This example demonstrates the "bmh" style, which is the design used in the
Bayesian Methods for Hackers online book.
"""
%matplotlib inline

from numpy.random import beta
import matplotlib.pyplot as plt

plt.style.use('bmh')


def plot_beta_hist(a, b):
    plt.hist(beta(a, b, size=10000), histtype="stepfilled",
             bins=25, alpha=0.8, normed=True)
    return

plot_beta_hist(10, 10)
plot_beta_hist(4, 12)
plot_beta_hist(50, 12)
plot_beta_hist(6, 55)

print plt.show()
```

<img style="max-width: 100%;" src="{{site.baseurl}}/images/Presentations_with_Ipython_10_0.png"></img>

{{site.endslide}}
{{site.endvertical}}

{{site.startvertical}}
{{site.startslide}}
### How to Use Slide Type

There are 5 types of slide in jupyter available.

This the main type called  ```slide```. They goes horizontally.


{{site.nextslide}}
#### This slide type is called ```Sub-Slide```

They goes vertically to the main cell.

There are other types:

- __Fragment__ comes one another in a slide
- __Skip__ as the names refers, skips whatever inside the cell
- __Notes__ are the slides that only available to the presenter when you click ```s``` during the presentation
{{site.endslide}}
{{site.endvertical}}

{{site.startslide}}

3. Converting to Presentation Locally
---

```
jupyter nbconvert <name.ipynb> --to slides --post serve
```

It will create a presentation in Jupyter defined default.

{{site.endslide}}

{{site.startvertical}}
{{site.startslide}}
4. Extra: How am I putting it into my blog
---

This is very detailed...

As I described above everything is very user friendly with IPython, but it only supports the local hosts for now.

To be able to add presentation to my blog and many others' blog you should use ```Markdown``` files. To be able to convert it:

```
jupyter nbconvert <name.ipynb> --to markdown
```
{{site.nextslide}}


Then we got the notebook in markdown format, alright. Next step is to use some indetifiers to say the website this is a presentation:

```
---
title: Example
layout: presentation
description: This is an example presentation.
---
```

This is called a ```YAML``` format in ```Jekyll``` template. Also to be able to show the markdown is a presentation we should use other identifiers like:

* `site.startslide` - mark the beginning of a slide
* `site.endslide` - mark the end of a slide
* `site.nextslide` - a short cut for `{{ site.endslide }}{{ site.startslide }}`.
* `site.startvertical` - start a vertical slide group
* `site.endvertical` - end a vertical slide group

{{site.endslide}}
{{site.endvertical}}

{{site.startslide}}
Questions? And Answers (Maybe)
---

{{site.endslide}}
