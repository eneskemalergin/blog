---
layout: post
title: Classification with Nearest Neighbors
tags:
- R language
- Machine Learning
- kNN
- Classification
---

Nearest neighbor classifiers are defined by their characteristic of classifying unlabeled examples by assigning them the class of the most similar labeled examples. They might look very simple and unimportant but nearest neighbor methods are very powerful tools. Very successful for; 

- Predicting persons choices by looking at the choices, that person already decided on,
- Identifying patterns in genetic data, for use in detecting specific proteins or diseases,
- Computer vision applications.

these classifiers are well-suited for classification tasks where relationships among the features and the target classes are
- numerous, 
- complicated, 
- or items of similar class type tend to be fairly homogeneous.

>  if a concept is difficult to define, but you know it when you see it, then nearest neighbors might be appropriate. 

### The kNN Algorithm

- kNN algorithm is the utilized version of nearest neighbors approach.
- Strengths:
  - Simple and effective
  - Makes no assumptions about the underlying data distribution
  - Fast training phase
- Weaknesses
  - Does't produce a model (limits the ability to find novel insights in relationships among features)
  - Slow classification phase
  - Requires large amount of memory 
  - Nominal features and missing data require additional processing


kNN starts with training dataset with examples that are classified into several categories, as labeled by a nominal(categorical-[such as gender]) variable. Assume that we have a test dataset containing unlabeled examples that otherwise have the same features as the training data. For each record in the test dataset, kNN identifies ```k``` records in the training data that are the "nearest" in similarith, where k is an integer specified in advance. The unlabeled test instance is assigned the class of the majority of the k nearest neighbors. 

To illustrate this process, let's make a small table of foods and their tastes, to make a small tasting prediction. Keeping it very simple we will create a data.frame consists of ingredients name, two features of each ingredient; sweetness and crunchiness, and food type:

```{r}
ingredient <- c("apple", "bacon", "banana", "carrot", "celery", "cheese")
sweetness <- c(10, 1, 10, 7, 3, 1)
crunchiness <- c(9, 4, 1, 10, 10, 1)
food_type <- c("fruit", "protein", "fruit", "vegetable", "vegetable", "protein")
tasting_df <- data.frame(ingredient, sweetness, crunchiness, food_type)
View(tasting_df)
```

The kNN algorithm treats the features as coordinates in a multidimensional feature space. We have two features sweetness anc crunchiness, so our feature space is two-dimensional. Now we can add them into a scatterplot with the labes on them:

```{r}
plot(tasting_df$sweetness, tasting_df$crunchiness, xlab="how sweet the food tastes", ylab = "how cruncy the food is")
text(tasting_df$sweetness, tasting_df$crunchiness, labels=ingredient, cex= 0.7, pos=3)
```

> Using more data would be better for visualization.

We can simply categorized the foods by looking and saying that vegetables, fruits and others have their own groups,

### Calculating distance

With that grouping have done, we can locate a new foods group easily by looking at the distance from the nearest group.  

- the kNN algorithms uses Euclidean distance, which is the distance one would measure if you could use a ruler to connect two points, illustrated in the previous figure by tht dotted, lines connceting the new food to its neighbours. (Another common distance measure is Manhattan distance.)

Let's say our new food is tomato and it's features are sweetness = 6 and crunchiness = 4, let's make a new column to store distance to the tomato value

```{r}
tasting_df$distance_to_tomato <- sqrt((6-tasting_df$sweetness)^2 + (4-tasting_df$crunchiness)^2)
View(tasting_df)
```

When you view the ```tasting_df``` again, you will see the new column at the end. To classify the tomato as a vegetable, protein or fruit, we'll begin by assigning the tomato, the food type of its single nearest neighour. This is called 1NN classification(k=1). 

If we use the kNN algorithm with k=3 instead, it performs a vote among the tree nearest neighbors: orange, grape, and nuts. Because the majority class among these neighbors is fruit (2 of the 3 votes), the tomato again is classified as a fruit.

### Choosing an appropriate k
Choosing an approproate k determines how well model will generalize to future data. 

> The balance between overfitting and underfitting the training data is a problem known as the __bias-variance tradeoff__. 

- Large ```k``` reduces the impact or variance caused by noisy data. It has risk of ignoring small but important patterns

If we take larger k, as we have the number of observations, we will have always the majority of voters. __The model always predict the majority vote.__

- Smallest ```k``` allows noisy data or outliers, to unduly influence the classification of examples. 

For example, suppose that some of the training examples were accidentally mislabeled. Any unlabeled example that happens to be nearest to the incorrectly labeled neighbor will be predicted to have the incorrect class, even if the other nine nearest neighbors would have voted differently.


> In practice, choosing ```k``` depends on the difficulty of the concept to be learned and the number of records in the training data. Typically, ```k``` is set somewhere between 3 and 10. One common practice is to set ```k``` equal to the square root of the number of training examples. 


Such rules may not always work as the best result. Alternative approach is to test multiple ```k``` to get optimum result. __On the other hand, unless the data is very noisy, larger and more representative training datasets can make the choice of ```k``` less important, because even subtle concepts will have a sufficiently large pool of examples to vote as neares neighbors.__

### Preparing data for use with kNN

Using features is not straight forward as we did before with calculating distance. Weight of each feature has a great impact on resulting values as well. We have to rescale the feature determinants to use it with minimilized form. Traditional method of rescaling features for kNN is __min-max normalization.__ 

#### Min-Max Normalization
- Transforms a feature such that all of its values fall in a range between 0 and 1. 
- Formula to calculate min-max normalization as follows:

```
new_X = (X - min(X)) / (max(X) - min(X))
```

- Normalized version can be interpreted as indicating how far, from 0 percent to 100 percent, the original value fell along the range between the original min and max.


#### z-score standardization
- This is another common way of transformation. 
- Formula to calculate as follows:

```
new_X = (X-mean(X)) / sd(X)
```
- This way rescales each of a feature's values in terms of how many standard deviations they fall above or below the mean value. 
- Resulting value is called __z-score__. 
- Unlike, min-max they don't have predefined min and max limit, they have unbounded range to negative and positive.



> The Euclidean distance formule is not defined for nominal data. To calculate the distance between nominal features, we need to convert them into a numeric format. 

Solution to this problem is __dummy coding__, where value of 1 indicated one category, and 0 indicates the other. For instance we can convert genders into numeric format by assigning 1 to male and 0 to female.


Convenient aspect of dummy coding is that the distance between dummy coded features is always one or zero, and thus, the values fall on the same scale as normalized numeric data. __No additional transformation is necessary.__

### Diagnosing breast cancer with the kNN algorithm

Machine learning can be used to identify the cancer cells, which improves the efficiency of the detection process done by the doctors. 

#### Step 1: Collecting Data

Data is coming from UCI's machine learning repository, [link to repo](http://archive.ics.uci.edu/ml)

The breast cancer data includes 569 examples of cancer biopsies, each with 32 features. One feature is an identification number, another is the cancer diagnosis, and 30 are numeric-valued laboratory measurements. The diagnosis is coded as M to indicate malignant or B to indicate benign.

```{r}
# To download the file from internet
download.file(url='https://raw.githubusercontent.com/stedy/Machine-Learning-with-R-datasets/master/wisc_bc_data.csv',destfile='wisc_bc_data.csv',method='curl')
```

#### Step 2: Exploring and Preparing the Data

We will first get the ```csv``` file, and put it to data frame called ```wbcd```

```{r}
wbcd <- read.csv("./wisc_bc_data.csv", stringsAsFactors = FALSE)
```

Now we have the data as ```csv``` format, then we can examine the data

```{r}
str(wbcd)
```

__Implications:__

- ```id``` variable is unique for each patient in the data but not useful for our classification task, so we can exclude it. 

To drop the variable ```id``` which is located in first columne

```{r}
wbcd <- wbcd[-1]
# Now you will see we have 31 variables left.
```

- ```diagnosis``` variable is our first interest by just guessing out of looking at the data. This has two options: benign(B) or malignant(M) mass. To see the distribution of B and M values execute the following command:

```{r}
table(wbcd$diagnosis)
```

In many machine learning tasks requires the target feature is coded as a factor. So we have to _recode_ the ```diagnosis``` variable. 

```{r}
# Converting factors with details
wbcd$diagnosis <- factor(wbcd$diagnosis, levels=c("B", "M"),
                         labels=c("Benign", "Malignant"))

# Showing the percentage of values 
round(prop.table(table(wbcd$diagnosis)) * 100, digits = 1)
```

The remaining 30 features are all numeric, and as expected, consists of three different measurements of ten characteristics. For now we will only take a closer look at three of the features:

```{r}
# showing the summary of 3 features to point out something...
summary(wbcd[c("radius_mean", "area_mean", "smoothness_mean")])
```

In the summary you will see that huge numbers in ```radius_mean``` and ```area_mean```, and really small numbers in ```smoothness_mean```, to be able to use kNN we have to rescale our data. To rescale we will use normalization.

##### Transformation - normalizing numeric data

Since we have to normalize more than 2 variables it is wise to create a function ```normalize``` to get things done more efficient. 


```{r}
# min-max normalization function
normalize <- function(x){
  return ((x - min(x)) / (max(x) - min(x)))
}

```


We can now apply our function to the numeric features in our data frame. Rather than normalizing each of the 30 numeric variables individually, we will use one of R's functions to automate the process.

```lapply()``` function of R takes a list and applies a function to each element of the list. 

```{r}
# applying the same function to all 30 numeric variables
wbcd_n <- as.data.frame(lapply(wbcd[2:31], normalize))

# checking the result
summary(wbcd_n$area_mean)
```



##### Data preparation - creating training and test datasets

Since we are making a learner, it is not very interesting to predict what we already know. A more interesting question will be "how well our learner performs on a dataset of unlabeled(B or M) data?" However we don't have a data that is unlabeled, in this case. But we can test our learners prediction accuracy by splitting up the currenc data into 2: training and test datasets. We will feed the model with training data and keep the test data away from the model, so it cannot cheat.


```{r}
# We will split it 469 to 100
wbcd_train <- wbcd_n[1:469, ]
wbcd_test <- wbcd_n[470:569, ]

```


For training the kNN model, we will need to store these class labels in factor vectors, divided to the training and test datasets:

```{r}
# Takes the diagnosis factor for each datasets.
wbcd_train_labels <- wbcd[1:469, 1]
wbcd_test_labels <- wbcd[470:569, 1]
```

#### Step 3 - Training a Model on the Data
After we are done with data prep phase of the kNN, now we are ready to build our model. __The process of training a kNN simply involvels storing the input data in a structured format.__ 

To classify our test instances we will use a kNN implementation from the ```class``` package. 

```{r}
# If it's not installed
# install.packages("class")
library(class)
```

```knn()``` function in ```class``` package provides a standard, classic implementation of the kNN algorithm. Syntax of the knn classification is:

```
p <- knn(train, test, class, k)
- train: is train data 
- test: is test data
- class: is factor vector with the class for each row in the training data
- k: is an integer indicating the number of nearest neigbors
```

Now let's try ```knn()``` with k=21 which is roughly the square root of 469 and being odd will make sure that you won't get tie.

```{r}
wbcd_test_pred  <- knn(train=wbcd_train, test=wbcd_test,
                       cl=wbcd_train_labels, k=21)
wbcd_test_pred
```

The ```knn()``` function returns a factor vector of predicted labels for each of theexamples in the test dataset, which we have assigned to ```wbcd_test_pred```.


#### Step 4: Evaluating Model Performance
You probably guessed, we will compare the ```wbcd_test_pred``` vector with ```wbcd_test_labels``` vector, to see the accuracy of our learner's predictions.

We can use the ```CrossTable()``` function in the ```gmodels``` package, which makes comparison easier and prettier.

```{r}
# install.packages("gmodels")
library(gmodels)
CrossTable(x=wbcd_test_labels, y=wbcd_test_pred,
           prop.chisq=FALSE) #  FALSE will remove the chi-square values that are not needed
```

The cell percentages in the table indicate the proportion of values that fall into four categories. In the top-left cell, are the true negative results. These 61 of 100 values indicate cases where the mass was benign, and the kNN algorithm correctly identified it as such. The bottom-right cell, indicates the true positive results, where the classifier and the clinically determined label agree that the mass is malignant. A total of 37 of 100 predictions were true positives.

The cells falling on the other diagonal contain counts of examples where the kNN approach disagreed with the true label. The 2 examples in the lower-left cell are false negative results; in this case, the predicted value was benign but the tumor was actually malignant. Errors in this direction could be extremely costly, as they might lead a patient to believe that she is cancer-free, when in reality the disease may continue to spread. The cell labeled FP would contain the false positive results, if there were any. These values occur when the model classifies a mass as malignant when in reality it was benign. Although such errors are less dangerous than a false negative result, they should also be avoided as they could lead to additional financial burden on the health care system, or additional stress for the patient, as additional tests or treatment may have to be provided.

A total of 2 percent, that is, 2 out of 100 masses were incorrectly classified by the kNN approach. 98 percent is very impressive, however we might improve the performance by adjusting ```k``` or/and changing normalization method.


#### Step 5 - Improving Model Performance

##### Transformation - z-score standardization

```{r}
wbcd_z <- as.data.frame(scale(wbcd[-1]))
wbcd_train <- wbcd_z[1:469, ]
wbcd_test <- wbcd_z[470:569, ]
wbcd_train_labels <-wbcd[1:469, 1]
wbcd_test_labels <- wbcd[470:569, 1]
wbcd_test_pred  <- knn(train=wbcd_train, test=wbcd_test,
                       cl=wbcd_train_labels, k=21)
CrossTable(x=wbcd_test_labels, y=wbcd_test_pred,
           prop.chisq=FALSE)
```



### Summary

So far, I tried to explain kNN algorithm with some classification knowledge. kNN is very simple algorithm and -for me- it is the most basic one to learn, however it is powerful. You saw that with a very little line of code we accomplish 98 percent prediction accurcy on identifying cancer.

I will focus more on machine learning and R for the following months and hopefully I will learn the basics of machine learning, as well as share all the things I learned with you...

You can share your thoughts with me by commenting below…

> Until next time, be safe…
