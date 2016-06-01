---
layout: post
title: Solving Kaggle's Titanic with R
excerpt:
categories: blog
tags: ["R", "Machine Learning", "Decision Trees", "Random Forest"]
image:
  feature: so-simple-sample-image-5.jpg
  credit: WeGraphics
  creditlink: http://wegraphics.net/downloads/free-ultimate-blurred-background-pack/
published: true
comments: true
share: true
---


> [Free Course from Data Camp](https://www.datacamp.com/courses/kaggle-r-tutorial-on-machine-learning)

> [Notebook version](https://raw.githubusercontent.com/eneskemalergin/Blog-Notebooks/master/ipython/Kaggle_Introduction_R.ipynb)

In this tutorial we will use R and Kaggle's Titanic competition using Machine Learning Algorithms.

## Getting Familiar with the Kaggle data Sets

In this dataset we are asked to apply machine learning techniques to predict a passanger's chance of surviving using R.

The data that kaggle is giving is stored as ```CSV``` file. We can load the data using ```read.csv()``` function. We will use the training set to build your modle, and the test set to validate it.


```R
# load the train data using read.csv()
train_url <- "http://s3.amazonaws.com/assets.datacamp.com/course/Kaggle/train.csv"
train <- read.csv(train_url)
```


```R
# load the test data using read.csv()
test_url <- "http://s3.amazonaws.com/assets.datacamp.com/course/Kaggle/test.csv"
test <- read.csv(test_url)
```


```R
# just have a glimpse to our train data
head(train)
```




<table>
<thead><tr><th></th><th scope=col>PassengerId</th><th scope=col>Survived</th><th scope=col>Pclass</th><th scope=col>Name</th><th scope=col>Sex</th><th scope=col>Age</th><th scope=col>SibSp</th><th scope=col>Parch</th><th scope=col>Ticket</th><th scope=col>Fare</th><th scope=col>Cabin</th><th scope=col>Embarked</th></tr></thead>
<tbody>
	<tr><th scope=row>1</th><td>1</td><td>0</td><td>3</td><td>Braund, Mr. Owen Harris</td><td>male</td><td>22</td><td>1</td><td>0</td><td>A/5 21171</td><td>7.25</td><td></td><td>S</td></tr>
	<tr><th scope=row>2</th><td>2</td><td>1</td><td>1</td><td>Cumings, Mrs. John Bradley (Florence Briggs Thayer)</td><td>female</td><td>38</td><td>1</td><td>0</td><td>PC 17599</td><td>71.2833</td><td>C85</td><td>C</td></tr>
	<tr><th scope=row>3</th><td>3</td><td>1</td><td>3</td><td>Heikkinen, Miss. Laina</td><td>female</td><td>26</td><td>0</td><td>0</td><td>STON/O2. 3101282</td><td>7.925</td><td></td><td>S</td></tr>
	<tr><th scope=row>4</th><td>4</td><td>1</td><td>1</td><td>Futrelle, Mrs. Jacques Heath (Lily May Peel)</td><td>female</td><td>35</td><td>1</td><td>0</td><td>113803</td><td>53.1</td><td>C123</td><td>S</td></tr>
	<tr><th scope=row>5</th><td>5</td><td>0</td><td>3</td><td>Allen, Mr. William Henry</td><td>male</td><td>35</td><td>0</td><td>0</td><td>373450</td><td>8.05</td><td></td><td>S</td></tr>
	<tr><th scope=row>6</th><td>6</td><td>0</td><td>3</td><td>Moran, Mr. James</td><td>male</td><td>NA</td><td>0</td><td>0</td><td>330877</td><td>8.4583</td><td></td><td>Q</td></tr>
</tbody>
</table>





```R
# just have a glimpse to our test data
tail(test)
```




<table>
<thead><tr><th></th><th scope=col>PassengerId</th><th scope=col>Pclass</th><th scope=col>Name</th><th scope=col>Sex</th><th scope=col>Age</th><th scope=col>SibSp</th><th scope=col>Parch</th><th scope=col>Ticket</th><th scope=col>Fare</th><th scope=col>Cabin</th><th scope=col>Embarked</th></tr></thead>
<tbody>
	<tr><th scope=row>413</th><td>1304</td><td>3</td><td>Henriksson, Miss. Jenny Lovisa</td><td>female</td><td>28</td><td>0</td><td>0</td><td>347086</td><td>7.775</td><td></td><td>S</td></tr>
	<tr><th scope=row>414</th><td>1305</td><td>3</td><td>Spector, Mr. Woolf</td><td>male</td><td>NA</td><td>0</td><td>0</td><td>A.5. 3236</td><td>8.05</td><td></td><td>S</td></tr>
	<tr><th scope=row>415</th><td>1306</td><td>1</td><td>Oliva y Ocana, Dona. Fermina</td><td>female</td><td>39</td><td>0</td><td>0</td><td>PC 17758</td><td>108.9</td><td>C105</td><td>C</td></tr>
	<tr><th scope=row>416</th><td>1307</td><td>3</td><td>Saether, Mr. Simon Sivertsen</td><td>male</td><td>38.5</td><td>0</td><td>0</td><td>SOTON/O.Q. 3101262</td><td>7.25</td><td></td><td>S</td></tr>
	<tr><th scope=row>417</th><td>1308</td><td>3</td><td>Ware, Mr. Frederick</td><td>male</td><td>NA</td><td>0</td><td>0</td><td>359309</td><td>8.05</td><td></td><td>S</td></tr>
	<tr><th scope=row>418</th><td>1309</td><td>3</td><td>Peter, Master. Michael J</td><td>male</td><td>NA</td><td>1</td><td>1</td><td>2668</td><td>22.3583</td><td></td><td>C</td></tr>
</tbody>
</table>




__Understanding our Data:__

Understading the data we have is the most essential thing before analyzing.

- ```test``` and ```train``` are data frames, R's way of representing a dataset
- ```str()``` gives you ability to explore a data frame, which gives you information such as the data types, the number of observations, and the number of variables.


```R
# Observing train data
str(train)
```

    'data.frame':	891 obs. of  12 variables:
     $ PassengerId: int  1 2 3 4 5 6 7 8 9 10 ...
     $ Survived   : int  0 1 1 1 0 0 0 0 1 1 ...
     $ Pclass     : int  3 1 3 1 3 3 1 3 3 2 ...
     $ Name       : Factor w/ 891 levels "Abbing, Mr. Anthony",..: 109 191 358 277 16 559 520 629 416 581 ...
     $ Sex        : Factor w/ 2 levels "female","male": 2 1 1 1 2 2 2 2 1 1 ...
     $ Age        : num  22 38 26 35 35 NA 54 2 27 14 ...
     $ SibSp      : int  1 1 0 1 0 0 0 3 0 1 ...
     $ Parch      : int  0 0 0 0 0 0 0 1 2 0 ...
     $ Ticket     : Factor w/ 681 levels "110152","110413",..: 525 596 662 50 473 276 86 396 345 133 ...
     $ Fare       : num  7.25 71.28 7.92 53.1 8.05 ...
     $ Cabin      : Factor w/ 148 levels "","A10","A14",..: 1 83 1 57 1 1 131 1 1 1 ...
     $ Embarked   : Factor w/ 4 levels "","C","Q","S": 4 2 4 4 4 3 4 4 4 2 ...



```R
# Observing test data
str(test)
```

    'data.frame':	418 obs. of  11 variables:
     $ PassengerId: int  892 893 894 895 896 897 898 899 900 901 ...
     $ Pclass     : int  3 3 2 3 3 3 3 2 3 3 ...
     $ Name       : Factor w/ 418 levels "Abbott, Master. Eugene Joseph",..: 210 409 273 414 182 370 85 58 5 104 ...
     $ Sex        : Factor w/ 2 levels "female","male": 2 1 2 2 1 2 1 2 1 2 ...
     $ Age        : num  34.5 47 62 27 22 14 30 26 18 21 ...
     $ SibSp      : int  0 1 0 0 1 0 0 1 0 2 ...
     $ Parch      : int  0 0 0 0 1 0 0 1 0 0 ...
     $ Ticket     : Factor w/ 363 levels "110469","110489",..: 153 222 74 148 139 262 159 85 101 268 ...
     $ Fare       : num  7.83 7 9.69 8.66 12.29 ...
     $ Cabin      : Factor w/ 77 levels "","A11","A18",..: 1 1 1 1 1 1 1 1 1 1 ...
     $ Embarked   : Factor w/ 3 levels "C","Q","S": 2 3 2 3 3 3 2 3 1 3 ...


How many people in our training set survived the disaster with the Titanic?

- ```table()``` function gives us the absolute numbers
- ```prop.table()``` function combination gives us the proportions

> ```table()``` command can help us to explore which variables have predictive value.


Let's start examining with the data. First thing to thing about this data what is he survival rates, and how gender survival rates are looking?


```R
# absolute numbers
table(train$Survived)
```





      0   1
    549 342




```R
# proportions
prop.table(table(train$Survived)) # get proportions according to specified table
```





            0         1
    0.6161616 0.3838384



0 represents people who died, and 1 who lived.

We can also do two-way comparison including gender as well:


```R
# We get the died,lived + female male
table(train$Sex, train$Survived)
```





               0   1
      female  81 233
      male   468 109




```R
# row-wise comparison with proportions
prop.table(table(train$Sex, train$Survived),1)
```





                     0         1
      female 0.2579618 0.7420382
      male   0.8110919 0.1889081



Second thing to think is, does age play a role on survival rate? Probably the highest survival rate is for children since they are the ones to be saved first by their families.

Let's test this idea by creating new column called ```child```


```R
train$child <- NA # create a new column with NA values
train$child[train$Age < 18 ] <- 1 # If the age is smaller than 18 we add 1 to represent the individual as child
train$child[train$Age >= 18] <- 0 # otherwise 0 to represent as non-child
# Then do a two-way comparison on the number of children vs adults
prop.table(table(train$child, train$Survived),1) # row-wise
```





                0         1
      0 0.6189684 0.3810316
      1 0.4601770 0.5398230



While less obviously than gender, age also seems to have an impact on survival.

With our previous observations, we discovered that in your training set, females had over a 50% chance of surviving and males had less than a 50% chance of surviving.

Using this very basic discovery we could put our first prediction saying that __"all females in the test set survive and all males in the test set die."__

To test our first and very basic prediction with the test data we downloaded. But there is no column called ```Survived``` in the test data, we should add that column with our predicted values. Then when you submit your results Kaggle will use the created ```Survived``` column to score our performance


```R
# First we prepare a copy of test
test_one <- test
```


```R
test_one$Survived <- 0 # created column and intialized to 0
test_one$Survived[test_one$Sex == 'female'] <- 1
```


```R
head(test_one)
# writing to csv file:
# write.csv(test_one, file = "submission1.csv")
```




<table>
<thead><tr><th></th><th scope=col>PassengerId</th><th scope=col>Pclass</th><th scope=col>Name</th><th scope=col>Sex</th><th scope=col>Age</th><th scope=col>SibSp</th><th scope=col>Parch</th><th scope=col>Ticket</th><th scope=col>Fare</th><th scope=col>Cabin</th><th scope=col>Embarked</th><th scope=col>Survived</th></tr></thead>
<tbody>
	<tr><th scope=row>1</th><td>892</td><td>3</td><td>Kelly, Mr. James</td><td>male</td><td>34.5</td><td>0</td><td>0</td><td>330911</td><td>7.8292</td><td></td><td>Q</td><td>0</td></tr>
	<tr><th scope=row>2</th><td>893</td><td>3</td><td>Wilkes, Mrs. James (Ellen Needs)</td><td>female</td><td>47</td><td>1</td><td>0</td><td>363272</td><td>7</td><td></td><td>S</td><td>1</td></tr>
	<tr><th scope=row>3</th><td>894</td><td>2</td><td>Myles, Mr. Thomas Francis</td><td>male</td><td>62</td><td>0</td><td>0</td><td>240276</td><td>9.6875</td><td></td><td>Q</td><td>0</td></tr>
	<tr><th scope=row>4</th><td>895</td><td>3</td><td>Wirz, Mr. Albert</td><td>male</td><td>27</td><td>0</td><td>0</td><td>315154</td><td>8.6625</td><td></td><td>S</td><td>0</td></tr>
	<tr><th scope=row>5</th><td>896</td><td>3</td><td>Hirvonen, Mrs. Alexander (Helga E Lindqvist)</td><td>female</td><td>22</td><td>1</td><td>1</td><td>3101298</td><td>12.2875</td><td></td><td>S</td><td>1</td></tr>
	<tr><th scope=row>6</th><td>897</td><td>3</td><td>Svensson, Mr. Johan Cervin</td><td>male</td><td>14</td><td>0</td><td>0</td><td>7538</td><td>9.225</td><td></td><td>S</td><td>0</td></tr>
</tbody>
</table>




## Part2: Machine Learning with Decision trees

In the previous part we did all the slicing and dicing yourself to find subsets that have a higher chance of surviving. A decision tree automates this process for us, and outputs a flowchart-like structure that is easy to interpret (we'll make one yourself in the next exercise).


Conceptually, the decision tree algorithm starts with all the data at the root node and scans all the variables for the best one to split on. Once a variable is chosen, we do the split and go down one level (or one node) and repeat. The final nodes at the bottom of the decision tree are known as terminal nodes, and the majority vote of the observations in that node determine how to predict for new observations that end up in that terminal node.

To create first decision tree of ours, we will use R's ```rpart``` package.


```R
# Calling the library
library('rpart')
```


The ```rpart()``` function creates our first decision tree. Function takes multiple arguments:

- ```formula``` specifying variable of interest and the variables used for prediction (```formula = Survived ~ Sex + Age```)
- ```data``` the data set to build the decision tree (```train``` in our case)
- ```method``` type of prediction you want. We want to predict a categorical variable, so classification: ```method = "class"```

```r

# Example Syntax of rpart()
my_tree <- rpart(Survived ~ Sex + Age,
                 data = train,
                 method ="class")

```

We can also plot the resulting tree using, ```plot(my_tree)``` and ```text(my_tree)```


```R
# Creating the decision tree
my_tree <- rpart(Survived ~ Pclass + Sex + Age + SibSp + Parch + Fare + Embarked,
                data = train,
                method = "class")
plot(my_tree) # plotting decision tree
text(my_tree) # making text version of decision tree
```

```r
my_tree_two <- rpart(Survived ~ Pclass + Sex + Age + SibSp + Parch + Fare + Embarked,
                data = train,
                method = "class")
plot(my_tree_two) # plotting decision tree
text(my_tree_two) # making text version of decision tree

# Load in the packages to build a fancy plot
library(rattle)
library(rpart.plot)
library(RColorBrewer)

# Time to plot your fancy tree
fancyRpartPlot(my_tree_two)
```

We can use ```predict()``` function to generate our answers:

```r
predict(my_tree, test, type= "class")
```

Before submitting to Kaggle, you'll have to convert your predictions to a CSV file with exactly 418 entries and 2 columns:
- PassengerId
- Survived



```R
# Making a prediction
my_prediction <- predict(my_tree, test, type="class")
```


```R
# Creating a solution data.frame
my_solution <- data.frame(PassengerId = test$PassengerId,
                          Survived = my_prediction)
```


```R
# Checking the solution data.frame, in any case:
head(my_solution)
```




<table>
<thead><tr><th></th><th scope=col>PassengerId</th><th scope=col>Survived</th></tr></thead>
<tbody>
	<tr><th scope=row>1</th><td>892</td><td>0</td></tr>
	<tr><th scope=row>2</th><td>893</td><td>0</td></tr>
	<tr><th scope=row>3</th><td>894</td><td>0</td></tr>
	<tr><th scope=row>4</th><td>895</td><td>0</td></tr>
	<tr><th scope=row>5</th><td>896</td><td>1</td></tr>
	<tr><th scope=row>6</th><td>897</td><td>0</td></tr>
</tbody>
</table>





```R
nrow(my_solution)
```




418




```R
# Making a csv file for solution
write.csv(my_solution, file = "my_solution.csv", row.names = FALSE)
```

When we submit this to Kaggle, you get ~0.78 score. This score put me on 1999.

We can improve our model making more complex ```rpart()```, which uses two more parameter:

- ```cp``` determines when the splitting up of the decision tree stops.
- ```minsplit``` determines the minimum amount of observations in a leaf of the tree.


```R
model2 <- rpart(Survived ~ Pclass + Sex + Age + SibSp + Parch + Fare + Embarked,
                data = train, method = "class",
                control = rpart.control(minsplit = 50, cp = 0))

# fancyRpartPlot(my_tree_three)
```

This ```rpart.control()``` gives more precise result. But thats not all, we can also re-engineer the data to get more precise results.

__Enter feature engineering:__ creatively engineering your own features by combining the different existing variables.

Let's see an example of feature engineering. In this example we will create ```family_size```

A valid assumption is that larger families need more time to get together on a sinking ship, and hence have less chance of surviving.

Family size is determined by the variables ```SibSp``` and ```Parch```, which indicate the number of family members a certain passenger is traveling with. So when doing feature engineering, you add a new variable ```family_size```, which is the sum of ```SibSp``` and ```Parch``` plus one (the observation itself), to the test and train set.


```R
train_two <- train
```


```R
train_two$family_size <- train_two$SibSp + train_two$Parch + 1
```


```R
model3 <- rpart(Survived ~ Pclass + Sex + Age + SibSp + Parch + Fare + Embarked + family_size,
                data = train_two, method = "class")
# fancyRpartPlot(model3)
```

Well done. If you have a close look at your decision tree you see that ```family_size``` is not included. Apparently other variables played a more important role. This is part of the game as well. Sometimes things will not turn out as expected, but it is here that you can make the difference.

Another thing might be about the class difference. Let's have a look...

First we need to create new test and train data with Title column included.


```R
getTitle <- function(data) {
title.dot.start <- regexpr("\\,[A-Z ]{1,20}\\.", data$Name, TRUE)
title.comma.end <- title.dot.start
+ attr(title.dot.start, "match.length")-1
data$Title <- substr(data$Name, title.comma.end+2,title.comma.end+attr(title.dot.start, "match.length")-2)
return (data$Title)
}
```


```R
train_new <-train
test_new <- test
```


```R
train_new$Title <- getTitle(train_new)
test_new$Title <- getTitle(test_new)
```


```R
model4 <- rpart(Survived ~ Pclass + Sex + Age + SibSp + Parch + Fare + Embarked + Title,
                data = train_new, method = "class")
```


```R
# Visualize my_tree_five
fancyRpartPlot(model4)
```


```R
my_prediction2 <- predict(model4, test_new, type = "class")
```


```R
my_solution2 <- data.frame(PassengerId = test_new$PassengerId, Survived = my_prediction)
write.csv(my_solution2, file = "my_solution2.csv", row.names = FALSE)
```

## Part3: More improvements

Random Forest is very popular machine learning technique, often used in such prediction tasks. However we cannot go further into this topic to keep things more close to simple.

In layman's terms, the Random Forest technique handles the overfitting problem you faced with decision trees. It grows multiple (very deep) classification trees using the training set.

At the time of prediction, each tree is used to come up with a prediction and every outcome is counted as a vote. For example, if you have trained 3 trees with 2 saying a passenger in the test set will survive and 1 says he will not, the passenger will be classified as a survivor.

This approach of overtraining trees, but having the majority's vote count as the actual classification decision, avoids overfitting.

> Random forest requires you data to have no missing values.

After this point we will combine the train and test to make ```all_data```

And we will remove NA values and give them values according to most used ones.


```R
load('all_data.RData')
```


```R
tail(all_data)
```




<table>
<thead><tr><th></th><th scope=col>PassengerId</th><th scope=col>Survived</th><th scope=col>Pclass</th><th scope=col>Name</th><th scope=col>Sex</th><th scope=col>Age</th><th scope=col>SibSp</th><th scope=col>Parch</th><th scope=col>Ticket</th><th scope=col>Fare</th><th scope=col>Cabin</th><th scope=col>Embarked</th><th scope=col>family_size</th><th scope=col>Title</th></tr></thead>
<tbody>
	<tr><th scope=row>1304</th><td>1304</td><td>NA</td><td>3</td><td>Henriksson, Miss. Jenny Lovisa</td><td>female</td><td>28</td><td>0</td><td>0</td><td>347086</td><td>7.775</td><td></td><td>S</td><td>1</td><td>Miss</td></tr>
	<tr><th scope=row>1305</th><td>1305</td><td>NA</td><td>3</td><td>Spector, Mr. Woolf</td><td>male</td><td>NA</td><td>0</td><td>0</td><td>A.5. 3236</td><td>8.05</td><td></td><td>S</td><td>1</td><td>Mr</td></tr>
	<tr><th scope=row>1306</th><td>1306</td><td>NA</td><td>1</td><td>Oliva y Ocana, Dona. Fermina</td><td>female</td><td>39</td><td>0</td><td>0</td><td>PC 17758</td><td>108.9</td><td>C105</td><td>C</td><td>1</td><td>Lady</td></tr>
	<tr><th scope=row>1307</th><td>1307</td><td>NA</td><td>3</td><td>Saether, Mr. Simon Sivertsen</td><td>male</td><td>38.5</td><td>0</td><td>0</td><td>SOTON/O.Q. 3101262</td><td>7.25</td><td></td><td>S</td><td>1</td><td>Mr</td></tr>
	<tr><th scope=row>1308</th><td>1308</td><td>NA</td><td>3</td><td>Ware, Mr. Frederick</td><td>male</td><td>NA</td><td>0</td><td>0</td><td>359309</td><td>8.05</td><td></td><td>S</td><td>1</td><td>Mr</td></tr>
	<tr><th scope=row>1309</th><td>1309</td><td>NA</td><td>3</td><td>Peter, Master. Michael J</td><td>male</td><td>NA</td><td>1</td><td>1</td><td>2668</td><td>22.3583</td><td></td><td>C</td><td>3</td><td>Master</td></tr>
</tbody>
</table>





```R
# Passenger on row 62 and 830 do not have a value for embarkment.
# Since many passengers embarked at Southampton, we give them the value S.
all_data$Embarked[c(62, 830)] <- "S"
```


```R
# Factorize embarkment codes.
all_data$Embarked <- factor(all_data$Embarked)
```


```R
# Passenger on row 1044 has an NA Fare value. Let's replace it with the median fare value.
all_data$Fare[1044] <- median(all_data$Fare, na.rm = TRUE)
```


```R
# How to fill in missing Age values?
# We make a prediction of a passengers Age using the other variables and a decision tree model.
# This time you give method = "anova" since you are predicting a continuous variable.
library(rpart)
predicted_age <- rpart(Age ~ Pclass + Sex + SibSp + Parch + Fare + Embarked + Title + family_size,
                       data = all_data[!is.na(all_data$Age),], method = "anova")
```


```R
all_data$Age[is.na(all_data$Age)] <- predict(predicted_age, all_data[is.na(all_data$Age),])
```


```R
# Split the data back into a train set and a test set
train <- all_data[1:891,]
test <- all_data[892:1309,]
```

Okay, now we got rid of the NA values from ```all_data``` and we splitted it into train and test according as it was before.

for Random Forest analysis R has a function called ```randomForest()``` in the ```randomForest``` package.

We call it as we did with ```rpart()```:
- First your provide the ```formula```. There is no argument ```class``` here to inform the function you're dealing with predicting a categorical variable, so you need to turn ```Survived``` into a factor with two levels: ```as.factor(Survived) ~ Pclass + Sex + Age```
- The ```data``` argument takes the train data frame.
- When you put the ```importance``` argument to ```TRUE``` you can inspect variable importance.
- The ```ntree``` argument specifies the number of trees to grow. Limit these when having only limited computational power at your disposal.



```R
library('randomForest')
```


```R
set.seed(111) # set seed for reproducibilty
my_forest <- randomForest(as.factor(Survived) ~ Pclass + Sex + Age + SibSp + Parch + Fare + Embarked + Title,
                         data = train, importance=TRUE, ntree=1000)
```


```R
my_prediction <- predict(my_forest, test)
```


```R
my_solution <- data.frame(PassengerId = test$PassengerId, Survived = my_prediction)
write.csv(my_solution, file = "my_solution3.csv", row.names = FALSE)
```

We set ```importance=TRUE```, so we can now see which variables are important using:

```
varImpPlot(my_forest)
```

When running the function, two graphs appear: the accuracy plot shows how much worse the model would perform without the included variables. So a high decrease (= high value x-axis) links to a high predictive variable. The second plot is the Gini coefficient. The higher the variable scores here, the more important it is for the model.
