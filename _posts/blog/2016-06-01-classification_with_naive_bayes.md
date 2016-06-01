---
layout: post
title: "Naive Bayes for Classification"
tags:
- R language
- Machine Learning
- naive Bayes
- Classification
---

In this part of our machine learning path, we will look at probabilistic learning. Probabilistic methods use data of past events to extrapolate future events. In weather forecasting, precipitation is typically predicted using terms such as "70 percent chance of rain". 70 percent chance of rain therefore implies that in 7 out of 10 past cases with similar weather patterns, precipitation occured.

We will learn the principles of probabilistic learning with __naive bayes__ algorithm. Like weather forecasters, naive bayes use past data to predict future data.

- Most common application of naive bayes is to predict if email is junk or not.

## Understanding naive Bayes

The basic statistical ideas necessary to understand the naive Bayes algorithm have been around so long, now it known as __Bayesian Methods__ because of the founder _Thomas Bayes_.

Basically the probability of an event is a number between 0 percent and 100 percent that captures the chance that event will occur given the available evidence. The lower probability means that event occurs less likely.

- Bayesian classifiers are best applied to problems in which the information from numerous attributes should be considered simultaneously in order to estimate the probability of an outcome.

### Basic concepts of Bayesian methods

To understand naive Bayes algorithm better we first need to learn some essential concepts of Bayesian methods.

> Bayesian probability theory is rooted in the idea that the estimated likelihood of an event should be based on the evidence at hand.

- __Events__: are possible outcomes (_head, tails_)
- __trial__: is a single opportunity for the event to occur(_a coin flip_)

#### Probability
Probability is roughly the data observed divided by number of trials. Notation ```P(A)``` is used to denote the probability of event A.

- Total probability of all possible outcomes of a trial must always be 100 percent.
- If the trial only has two outcomes that cannot occur simultaneously, like spam and ham(non-spam), the knowing probabilty of either outcome reveals the probability of the other.

> ```P(spam)=0.20```, then we can calculate as ```P(ham)=1-0.20```. Situations like this works because the two variable are __mutually exclusive__ or __exhaustive__.

> mutually exclusive means that the events cannot occur at the same time and are the only two possible outcomes. It is denoted like this: ```P(¬spam) = 0.80.```

#### Joint Probability

Often we are interested in monitoring several non-mutually exclusive events for the same trial. Let's say we have specific word "Winner". This word most of the time placed in spam messages. Using venn diagrams we can show the relations between spam, ham, and a special word "Winner".

Probability of having word "Winner" and being spam is represented ```P(spam ∩ Winner)```

- Calculating ```P(spam ∩ Winner)``` it depends on the __joint probability__ of the two events, or how the probability of one event is related to the probability of the other.
- If the two events are totally unrelated, they are called __independet events__.
- If all events were independent, it would be impossible to predict any event using the data obtained by another.

> From the last statement we understand that the __dependent events__ are the basis of predictive modelling.


#### Conditional probability with Bayes' theorem

We can describe relationships between dependent events using __Bayes' theorem__.

> Notation ```P(A|B)``` can be read as the probability of event A given that B is occured.

```P(A|B)``` is also known as __conditional probability__, since the probability of A is dependent on what happend with event B.

```
P(A|B) = ( P(B|A)* P(A) )/ P(B) = P (A ∩ B) / P(B)
```

In practice understaning bayesian is easier. Suppose that you were tasked with guessing the probability that an incoming email was spam, without any additional evidence, the most reasonable guess would be the probability that any prior message was spam. _This estimate is known as the_ __prior probability__.

Addition to that we get word "Winner" is located in incoming message. The probability that the word "Winner" was used in previous spam messages is called __likelihood__ and the propability that "winner" appeared in any message at all is known as the __marginal likelihood__.

__Posterior probability__ measures how likely the message is to be spam, we can think of it as the left side of the equation.

```
P(spam|Winner) = ( P(Winner|spam)*P(spam) ) / P(Winner)
```

This is pretty much how commercial spam filters work nowadays, although they consider a much larger number of words simultaneously when computing the frequency and likelihood tables.

### The Naive Bayes Algorithm

Naive Bayes algorithm gives you powerful classification method using Bayes' theorem. Naive Bayes algorithm is the most common machine learning algorithm using Bayes' theorem, and most common for text classification.

__Strengths:__

- Simple, fast, and very effective
- Does well with noisy and missing data
- Requiers few examples, also work with large datasets of examples
- Easy to obtain the estimated probability for a prediction

__Weaknesses__:

- Relies on an often-faulty assumption of equally important and independent features
- Not ideal for datasets with large numbers of numeric features
- Estimated probabilities are less reliable that the predicted classes

They call it naive because it's assumptions _(it assumes that all of the features in the dataset are equally important and independent)_ are really optimistic and rarely true in most real-world applications.


## Example - Filtering Mobile Phone Spam with the Naive Bayes Algorithm

We know that naive Bayes is very successfull on filtering spam email, and in theory it should work for SMS spam filtering as well. But, it is not as easy as filtering emails. There are challenges like;

- Characters are limited, means less clue.
- typos and lingos are limiting the prediction of legitimate messages and spam.

Let's try and see how well our spam filtering on SMS will do...

### Step 1 - Collecting Data

The [source](https://raw.githubusercontent.com/brenden17/sklearnlab/master/spam/sms_spam.csv) contains text of SMS messages along with a label indicating whether the message is unwanted. __Junk are labeled as spam, and others labeled as ham.__

```{r}
# Getting the data from github source
download.file(url="https://raw.githubusercontent.com/brenden17/sklearnlab/master/spam/sms_spam.csv", destfile="sms_spam.csv", method="curl")
```


### Step 2 - Exploring and Preparing the Data

```{r}
# adding the downloaded data to R
sms_raw <- read.csv("./sms_spam.csv", stringsAsFactors = FALSE)
str(sms_raw) # We have 2 variables, type and text
```

The ```type``` variable is currently a character vector. Since this is a categorical variable, it would be better to convert it to a factor:

```{r}
# Convert it to factor
sms_raw$type <- factor(sms_raw$type)
str(sms_raw$type)
```

#### Data preperation - processing text data for analysis

Text data is really messy consists of words, numbers, spaces, and punctuation. We have to get rid of numbers, punctuation and uninteresting words like 'and', 'but', 'or'...

The ```tm``` package is really helpful tool for text mining and character manipulation on strings.

```{r}
# install.packages("tm")
library(tm) # calling tm package
```


First thing to do for processing text data is creating collection of texts, which is called __corpus__. It's simply putting together all the SMS messages in one vector

```{r}
sms_corpus <- Corpus(VectorSource(sms_raw$text))
inspect(corpus_clean[1:3])
```
> What is going on above:
>- ```Corpus()``` function creates an R object to store text documents:
- ```VectorSource()``` gets the text documents data source.


Now we have a vector to work on. Before going into splitting the text into words step, we should perform cleaning on the text. (hello!, HELLO, Hello,... must be hello)


```{r}
# tm_map() is transforming with mapping
corpus_clean <- tm_map(sms_corpus, content_transformer(tolower)) # all to lowercase
corpus_clean <- tm_map(corpus_clean, content_transformer(removeNumbers)) # get rid of all numbers
```

In text data analysis, it a good practice to remove words like, "to, and, but, or". These are known as __stop words__ and R has them predefined.

```{r}
corpus_clean <- tm_map(corpus_clean, content_transformer(removeWords), stopwords()) # remove all stopwords
corpus_clean <- tm_map(corpus_clean, content_transformer(removePunctuation)) # removes all punctuation
corpus_clean <- tm_map(corpus_clean, content_transformer(stripWhitespace)) # removes additional white space

# After removing is done we can check our SMS messages
inspect(corpus_clean[1:3])
```

The final thing to do is to split messages into individual components through a process called __tokenization__. (Tokens are single words in our case.)

As you might have guessed, ```tm``` package provides functionality to tokenize the SMS message corpus. ```DocumentTermMatrix()``` function will take a corpus and create a data structure called a __sparse matrix__.


```{r}
sms_dtm <- DocumentTermMatrix(corpus_clean)
```

##### Creating training and test datasets

For all the machine learning tasks we have to split the data into to parts test and train data. We'll divide data into two portions: 75 percent training, 25 percent testing data.

```{r}
#Splitting raw data frame
sms_raw_train <- sms_raw[1:4169, ]
sms_raw_test <- sms_raw[4170:5559, ]

# splitting document-term matrix
sms_dtm_train <- sms_dtm[1:4169, ]
sms_dtm_test <- sms_dtm[4170:5559, ]

# splitting corpus
sms_corpus_train <- corpus_clean[1:4169]
sms_corpus_test <- corpus_clean[4170:5559]

# Proportion of spam in the training and test data frames
prop.table(table(sms_raw_train$type))

prop.table(table(sms_raw_test$type))
```

##### Visualizing text data - Word Cloud
 A word cloud is a way to visually depict the frequency at which words appear in text data. We will use ```wordcloud``` package to create this type of diagram.

```{r}
# install.packages("wordcloud")
library(wordcloud)

# Create the wordcloud diagram, most frequent ones will be close to the center
wordcloud(sms_corpus_train, min.freq = 40, random.order = FALSE)
```

We can also compare the clouds for SMS spam and ham using wordcloud diagram.

```{r}
# subset spam ones
spam <- subset(sms_raw_train, type=="spam")

# subset ham ones
ham <- subset(sms_raw_train, type=="ham")

wordcloud(spam$text, max.word = 40, scale= c(3, 0.5))
wordcloud(ham$text, max.word = 40, scale= c(3, 0.5))
```

##### Creating indicator features for frequent words

The last thing to do in the data preparation process is to transform the sparse matrix into a data structure that can be used to tran a naive Bayes classifier.

Now we have around 7k features, since each word is a feature itself. We will reduce it by eliminating any words appear in less than five SMS message, or less than about 0.1 percent of records in the training data.


```{r}
# finding frequent words in more than 5 SMS using tm function
sms_dict <- c(findFreqTerms(sms_dtm_train, 5) )

# limit train data from dictionary created
sms_train <- DocumentTermMatrix(sms_corpus_train, list(dictionary = sms_dict))

# limit test data from dictionary created
sms_test <- DocumentTermMatrix(sms_corpus_train, list(dictionary=sms_dict))
```

The training and test data now includes around 1200 features corresponding only to words appearing in at least five messages.

Naive Bayes classifier is typically trained on data with categorical features. This poses a problem since the cells in the sparse matrix indicate a count of the times a word appears in a message. We should change this to a factor variable that simply indicates yes or no depending on wheather the words appears at all. Now let's define a function to do this job.

```{r}
convert_counts <- function(x) {
  x <- ifelse(x > 0, 1, 0)
  x <- factor(x, levels=c(0,1), labels=c("'No'", "'Yes'"))
  return(x)
}

sms_train <- apply(sms_train, MARGIN = 2, convert_counts)
sms_test <- apply(sms_test, MARGIN = 2, convert_counts)

```


The result will be two matrixes, each with factor type columns indicating Yes, or No for wheather each column's word appears in the messages comprising the rows.

### Step 3 - Training a Model on Data

After getting usable data format for our model, now we can setup our model to filter SMS messages.

Naive Bayes implementation in R can be found in ```e1071``` package:

```{r}
# install.packages("e1071")
library(e1071)
```

> Unlike kNN algorithm, naive Bayes is using learner to classify.

The structure of the function ```naiveBayes()```:

__Building the classifier:__

```m <- naiveBayes(train, class, laplace=0)```

- _train_ is a data frame or matrix containing training data
- _class_ is a factor vector with the class for each row in the training data
- _laplace_ is a number to control the Laplace estimator

__Making predictions:__

```p <- predict(m, test, type="class")```

- _m_ is a model trained by the ```naiveBayes()``` function
- _test_ is a data frame or matrix containing test data with the same features as the training data used to build the classifier
- _type_ is either ```"class"``` or ```"raw"``` and specifies whether the predictions should be most likely class value or the raw predicted probabilities.


Now let's build our model:

```{r}
sms_classifier <- naiveBayes(sms_train, sms_raw_train$type)
```


### Step 4 - Evaluating Model Performance

The classifier that we trained has been named ```sms_classifier```, we will use this to generate predictions.  

The ```predict()``` function is used to make the predictions:

```{r}
sms_test_pred <- predict(sms_classifier, sms_test)
```

To compare the predicted values to the actual values, we'll use the ```CrossTable()``` function in the ```gmodels``` package.

```{r}
library(gmodels)
CrossTable(sms_test_pred, sms_raw_test$type,
           prop.chisq = FALSE, prop.t=FALSE,
           dnn=c('predicted', 'actual'))
```


We can also improve the accuracy by adjusting parameters, like laplace variable. You might want to try this by yourself and see the difference between first one and yours...

### Summary

In this post we learned about classification using naive Bayes.

- We used Bayes' theorem, to calculate probabilities.
- Naive Bayes is simplified version of Bayes' theorem(which requires intense calculations)
- Naive Bayes classifier is used for text classification.
- We implement this method to filter SMS messages.

You can share your thoughts with me by commenting below…

> Until next time, be safe…
