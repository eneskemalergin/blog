---
layout: post
title: Interfacing with R via rpy2
excerpt:
categories: blog
tags: ["Bioinformatics", "Python", "Terminal"]
image:
  feature: so-simple-sample-image-5.jpg
  credit: WeGraphics
  creditlink: http://wegraphics.net/downloads/free-ultimate-blurred-background-pack/
published: true
date: 2015-09-18 23:00:00
comments: true
share: true
---

Hey friends, todays post will blow your mind away! You may shocked from the title of the post already, because I did. Since I know R and Python basics <and a little more maybe> I can compare them easily. R has very powerful built-in function for statistics, data analysis, etc. But most importantly R has a library called Bioconductor which is huge in Bioinformatics area. This library ```rpy2``` will allow us to use Bioconductor easily.  

> This tutorial I will introduce you to the library, and I will show you how to use with small exercises.

The rpy2 ~~provides~~ provides a declarative interface from Python to R. As you will see, you will be able to write very elegant Python code to perform the interfacing process.

The [book](http://www.amazon.com/Bioinformatics-Python-Cookbook-Tiago-Antao/dp/1782175113) that I am following in  this tutorial is using a index file from [1000genomes.org](http://www.1000genomes.org/). You should download that file(~61mb) at the beginning because we will rock this tutorial with that source.

- Download the link from the [github repo](https://github.com/tiagoantao/bioinf-python/blob/master/notebooks/Datasets.ipynb) and save it as ```sequence.index``` because we will use it in later tutorials.

> This file has information about all FASTQ files in the human 1000 genomes project.

> FASTQ format is a text-based format for storing both a biological sequence (usually nucleotide sequence) and its corresponding quality scores. Both the sequence letter and quality score are each encoded with a single ASCII character for brevity. It was originally developed at the Wellcome Trust Sanger Institute to bundle a FASTA sequence and its quality data, but has recently become the de facto standard for storing the output of high-throughput sequencing instruments such as the Illumina Genome Analyzer. [Source](https://en.wikipedia.org/wiki/FASTQ_format)


Being all necessary info give we can start the step-by-step tutorial:

## Import ```rpy2``` and Read file

```Python
# Calls the rpy2 with the module called robjects
import rpy2.robjects as robjects

# Reading function set
read_delim = robjects.r('read.delim')

# Now reading sequence.index file with our read_delim function created above
seq_data = read_delim('sequence.index', header=True, stringsAsFactors=False)
```

- We import the library and access the ```read.delim``` in R and call it in ```read_delim```. Now we can read file like we do in R.

- Also if you realized(and also if you have prior knowledge in R) the usage of parameters and names are coming from R as well.

## We call the function proper

Using ```rpy2``` we can pass atomic objects without conversion. We also can convert argument names seamlessly with a dot of course. Finally we can get the object for python namespace

```Python
# Printing the information in beautiful pythonic way.
print ('This dataframe has %d columns and %d rows' % (seq_data.ncol, seq_data.nrow))
print (seq_data.colnames) # see using R methods with dot
# You can even mix the styles (How awesome is this)
# !!! But careful, you may mix everything !!!
# my_cols = robjects.r.ncol(seq_data)
# print (my_cols)
```

- In the code above seq_data object is a data frame. Sounds familiar? Yes it is one of the main data structures in R. Also data frame is in Python's Pandas library as well. Data frame is like a table that we all make in excel. sequence of rowsm where each column has the same types.

- As you seen in the code above we are using R functions directly such as ```ncol``` and ```colnames```. Now look at the output, if you done everything correct until this point you will see vector with 26 elements in it. ([26] means that btw :) )  

> Indexing in R starts from 1 so if I say that 26 elements when we see 26, I am not wrong! Next time maybe...

## Clean Data
Why we need clean data? Because it's more hygienic, NO! To be able to analyze and interpret the given dataset, we have to clean it. By clean I mean making the types same, getting rid of the missing ones, or corrupted info...

```Python
# Calling the integer checking function built-in R
as_integer = robjects.r('as.integer')
# Calling the match function from R
match = robjects.r.match
# Save the results from seq_data colnames with "BASE_COUNT"
my_col = match('BASE_COUNT', seq_data.colnames)[0]
# Print the results
print(seq_data[my_col-1][:3])
# Check and get only the integer versions of the inputs
seq_data[my_col-1]= as_integer(seq_data[my_col-1])
# Prints as it is
print(seq_data[my_col-1][:3])
```

- First print will show strings and the other one will show numbers.

## Finalize the Getting Data Frame part

In here we will create a variable in the R namespace called ```seq.data``` with the content of the data frame from the Python namespace. Note that after whis operation, both objects will be independent.

```Python
robjects.r.assign('seq.data', seq_data)
```
## Using ggplot2 from R
Even if you can use Python plotting libraries and function R has its own built-in plotting functions. But not fancy as ggplot2.

```Python
# We should import another library to call ggplot2
import rpy2.robjects.lib.ggplot2 as ggplot2
```

If you get an error which is saying something like this: ```rpy2.rinterface.RRuntimeError: Error in loadNamespace(name) : there is no package called ‘ggplot2’```, then you should install the ggplot2 in your R system before running this statement.

So, to be able to plot our results we will need an output image base and then we will code through to the result. We need ```png()``` function from R to complete the base.

```Python
# Make the base of an output picture
robjects.r.png('out.png')
# Again calling some libraries
from rpy2.robjects.functions import SignatureTranslatedFunction
# Now we arrange the theme that we will use
ggplot2.theme = SignatureTranslatedFunction(ggplot2.theme, init_prm_translate = {'axis_text_x': 'axis_text_x'})
# We define our plot
bar = ggplot2.ggplot(seq_data) + ggplot2.geom_bar() + ggplot2.aes_string(x = 'CENTER_NAME') + ggplot2.theme(axis_text_x=ggplot2.element_text(angle=90, hjust=1))
# This function plots, meaning shows the results
bar.plot()
dev_off = robjects.r('dev.off')
def_off()
```

Then draw the chart itself. Note the declarative nature of ggplot2 as we add features to the chart. First, we specify the ```seq_data``` data frame, then we will use a histogram bar plot called geom_bar, followed by annotating the X variable (CENTER_NAME).


I would like to finish it here and I will return it with more R magic in Python. This time we will use IPython for interfacing R and Python.

Share your thoughts with me by commenting below...

Until the next time...



> PS: Before I end the tutorial make sure you put the codes together otherwise they will not work :)
