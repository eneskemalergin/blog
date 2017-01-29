---
layout: post
title: Introduction to Pandas 2
excerpt:
categories: blog
tags: ["Python", "Data Science", "Pandas"]
published: true
comments: true
share: true
---

Hello all, I am back with another of my notes on Pandas, Today I will focus on indexing and selection of data from pandas object. It's really important since effective use of pandas requires a good knowledge of the indexing and selection of data.


In the last post while introducing data structures, I talked about basic indexing, I will show here as well for the sake of completeness.

I am going to follow the official documentation [here](http://pandas.pydata.org/pandas-docs/stable/indexing.html)

If you like to follow this small tutorial in notebook format you can check out [here](https://github.com/eneskemalergin/Blog-Notebooks/blob/master/Introduction_to_Pandas-2.ipynb)

## Basic Indexing


```python
import pandas as pd
```


```python
SpotCrudePrices_2013_Data= { 'U.K. Brent' :
                            {'2013-Q1':112.9, '2013-Q2':103.0,
                             '2013-Q3':110.1, '2013-Q4':109.4},
                            'Dubai':
                            {'2013-Q1':108.1, '2013-Q2':100.8,
                             '2013-Q3':106.1,'2013-Q4':106.7},
                             'West Texas Intermediate':
                            {'2013-Q1':94.4, '2013-Q2':94.2,
                             '2013-Q3':105.8,'2013-Q4':97.4}}
SpotCrudePrices_2013=pd.DataFrame.from_dict(SpotCrudePrices_2013_Data)
SpotCrudePrices_2013
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Dubai</th>
      <th>U.K. Brent</th>
      <th>West Texas Intermediate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-Q1</th>
      <td>108.1</td>
      <td>112.9</td>
      <td>94.4</td>
    </tr>
    <tr>
      <th>2013-Q2</th>
      <td>100.8</td>
      <td>103.0</td>
      <td>94.2</td>
    </tr>
    <tr>
      <th>2013-Q3</th>
      <td>106.1</td>
      <td>110.1</td>
      <td>105.8</td>
    </tr>
    <tr>
      <th>2013-Q4</th>
      <td>106.7</td>
      <td>109.4</td>
      <td>97.4</td>
    </tr>
  </tbody>
</table>
</div>



We can select the prices for the available time periods of Dubai crude oil by __using the [] operator__:


```python
dubaiPrices=SpotCrudePrices_2013['Dubai']
dubaiPrices
```




    2013-Q1    108.1
    2013-Q2    100.8
    2013-Q3    106.1
    2013-Q4    106.7
    Name: Dubai, dtype: float64



We can also pass a list of columns to the ```[]``` operator in order to select the columns in a particular order:


```python
SpotCrudePrices_2013[['West Texas Intermediate','U.K. Brent']]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>West Texas Intermediate</th>
      <th>U.K. Brent</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-Q1</th>
      <td>94.4</td>
      <td>112.9</td>
    </tr>
    <tr>
      <th>2013-Q2</th>
      <td>94.2</td>
      <td>103.0</td>
    </tr>
    <tr>
      <th>2013-Q3</th>
      <td>105.8</td>
      <td>110.1</td>
    </tr>
    <tr>
      <th>2013-Q4</th>
      <td>97.4</td>
      <td>109.4</td>
    </tr>
  </tbody>
</table>
</div>



> Rows cannot be selected with the bracket operator ```[]``` in a DataFrame.

One can retrieve values from a Series, DataFrame, or Panel directly as an attribute __using dot operator__


```python
SpotCrudePrices_2013.Dubai
```




    2013-Q1    108.1
    2013-Q2    100.8
    2013-Q3    106.1
    2013-Q4    106.7
    Name: Dubai, dtype: float64



However, this only works if the index element is a valid Python identifier, ```Dubai``` in this case is valid but ```U.K. Brent``` is not.

We can change the names to valid identifiers:



```python
SpotCrudePrices_2013.columns=['Dubai','UK_Brent','West_Texas_Intermediate']
SpotCrudePrices_2013
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Dubai</th>
      <th>UK_Brent</th>
      <th>West_Texas_Intermediate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-Q1</th>
      <td>108.1</td>
      <td>112.9</td>
      <td>94.4</td>
    </tr>
    <tr>
      <th>2013-Q2</th>
      <td>100.8</td>
      <td>103.0</td>
      <td>94.2</td>
    </tr>
    <tr>
      <th>2013-Q3</th>
      <td>106.1</td>
      <td>110.1</td>
      <td>105.8</td>
    </tr>
    <tr>
      <th>2013-Q4</th>
      <td>106.7</td>
      <td>109.4</td>
      <td>97.4</td>
    </tr>
  </tbody>
</table>
</div>




```python
SpotCrudePrices_2013.UK_Brent
```




    2013-Q1    112.9
    2013-Q2    103.0
    2013-Q3    110.1
    2013-Q4    109.4
    Name: UK_Brent, dtype: float64



We can also select prices by __specifying a column index number__ to select column 1 (U.K. Brent)


```python
SpotCrudePrices_2013[[1]]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>UK_Brent</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-Q1</th>
      <td>112.9</td>
    </tr>
    <tr>
      <th>2013-Q2</th>
      <td>103.0</td>
    </tr>
    <tr>
      <th>2013-Q3</th>
      <td>110.1</td>
    </tr>
    <tr>
      <th>2013-Q4</th>
      <td>109.4</td>
    </tr>
  </tbody>
</table>
</div>



We can slice a range by using the [] operator. The syntax of the slicing operator exactly matches that of ```NumPy```'s:

    ar[startIndex: endIndex: stepValue]

For a DataFrame, [] slices across rows, Obrain all rows starting from index 2:


```python
SpotCrudePrices_2013[2:]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Dubai</th>
      <th>UK_Brent</th>
      <th>West_Texas_Intermediate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-Q3</th>
      <td>106.1</td>
      <td>110.1</td>
      <td>105.8</td>
    </tr>
    <tr>
      <th>2013-Q4</th>
      <td>106.7</td>
      <td>109.4</td>
      <td>97.4</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Reverse the order of rows in DataFrame
SpotCrudePrices_2013[::-1]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Dubai</th>
      <th>UK_Brent</th>
      <th>West_Texas_Intermediate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-Q4</th>
      <td>106.7</td>
      <td>109.4</td>
      <td>97.4</td>
    </tr>
    <tr>
      <th>2013-Q3</th>
      <td>106.1</td>
      <td>110.1</td>
      <td>105.8</td>
    </tr>
    <tr>
      <th>2013-Q2</th>
      <td>100.8</td>
      <td>103.0</td>
      <td>94.2</td>
    </tr>
    <tr>
      <th>2013-Q1</th>
      <td>108.1</td>
      <td>112.9</td>
      <td>94.4</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Selecting Dubai's data as Pandas Series
dubaiPrices = SpotCrudePrices_2013['Dubai']
# Obtain the last 3 rows or all rows but the first:
dubaiPrices[1:]
```




    2013-Q2    100.8
    2013-Q3    106.1
    2013-Q4    106.7
    Name: Dubai, dtype: float64




```python
# Obtain all rows but the last
dubaiPrices[:-1]
```




    2013-Q1    108.1
    2013-Q2    100.8
    2013-Q3    106.1
    Name: Dubai, dtype: float64




```python
# Reverse the rows
dubaiPrices[::-1]
```




    2013-Q4    106.7
    2013-Q3    106.1
    2013-Q2    100.8
    2013-Q1    108.1
    Name: Dubai, dtype: float64



## Label, Integer, and Mixed Indexing

In addition to the standard indexing operator [] and attribute operator, there are operators provided in pandas to make the job of indexing easier and more convenient.

By label indexing, we generally mean indexing by a header name, which tends to be a string value in most cases. These operators are as follows:

- The ```.loc``` operator: It allows label-oriented indexing
- The ```.iloc``` operator: It allows integer-based indexing
- The ```.ix``` operator: It allows mixed label and integer-based indexing


### Label-Oriented Indexing

The ```.loc``` operator supports pure label-based indexing.




```python
NYC_SnowAvgsData={'Months' : ['January','February','March','April', 'November', 'December'],
                  'Avg SnowDays' : [4.0,2.7,1.7,0.2,0.2,2.3],
                  'Avg Precip. (cm)' : [17.8,22.4,9.1,1.5,0.8,12.2],
                  'Avg Low Temp. (F)' : [27,29,35,45,42,32] }
NYC_SnowAvgs = pd.DataFrame(NYC_SnowAvgsData,
                            index=NYC_SnowAvgsData['Months'],
                            columns=['Avg SnowDays','Avg Precip. (cm)','Avg Low Temp. (F)'])
NYC_SnowAvgs
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Avg SnowDays</th>
      <th>Avg Precip. (cm)</th>
      <th>Avg Low Temp. (F)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>January</th>
      <td>4.0</td>
      <td>17.8</td>
      <td>27</td>
    </tr>
    <tr>
      <th>February</th>
      <td>2.7</td>
      <td>22.4</td>
      <td>29</td>
    </tr>
    <tr>
      <th>March</th>
      <td>1.7</td>
      <td>9.1</td>
      <td>35</td>
    </tr>
    <tr>
      <th>April</th>
      <td>0.2</td>
      <td>1.5</td>
      <td>45</td>
    </tr>
    <tr>
      <th>November</th>
      <td>0.2</td>
      <td>0.8</td>
      <td>42</td>
    </tr>
    <tr>
      <th>December</th>
      <td>2.3</td>
      <td>12.2</td>
      <td>32</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Using a single label:
NYC_SnowAvgs.loc['January']
```




    Avg SnowDays          4.0
    Avg Precip. (cm)     17.8
    Avg Low Temp. (F)    27.0
    Name: January, dtype: float64




```python
# Using a list of labels
NYC_SnowAvgs.loc[['January', 'April']]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Avg SnowDays</th>
      <th>Avg Precip. (cm)</th>
      <th>Avg Low Temp. (F)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>January</th>
      <td>4.0</td>
      <td>17.8</td>
      <td>27</td>
    </tr>
    <tr>
      <th>April</th>
      <td>0.2</td>
      <td>1.5</td>
      <td>45</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Using a Label range:
NYC_SnowAvgs.loc['January' : 'March']
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Avg SnowDays</th>
      <th>Avg Precip. (cm)</th>
      <th>Avg Low Temp. (F)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>January</th>
      <td>4.0</td>
      <td>17.8</td>
      <td>27</td>
    </tr>
    <tr>
      <th>February</th>
      <td>2.7</td>
      <td>22.4</td>
      <td>29</td>
    </tr>
    <tr>
      <th>March</th>
      <td>1.7</td>
      <td>9.1</td>
      <td>35</td>
    </tr>
  </tbody>
</table>
</div>



> Note that while using the .loc , .iloc , and .ix operators on a DataFrame, the row index must always be specified first. This is the opposite of the [] operator, where only columns can be selected directly.


```python
NYC_SnowAvgs.loc[:,'Avg SnowDays']
```




    January     4.0
    February    2.7
    March       1.7
    April       0.2
    November    0.2
    December    2.3
    Name: Avg SnowDays, dtype: float64




```python
# to select a specific coordinate value
NYC_SnowAvgs.loc['March','Avg SnowDays']
```




    1.7




```python
# Alternative Style
NYC_SnowAvgs.loc['March']['Avg SnowDays']
```




    1.7




```python
# Without using loc function, square bracket as follows
NYC_SnowAvgs['Avg SnowDays']['March']
```




    1.7



We can use the ```.loc``` operator to select the rows instead:


```python
NYC_SnowAvgs.loc['March']
```




    Avg SnowDays          1.7
    Avg Precip. (cm)      9.1
    Avg Low Temp. (F)    35.0
    Name: March, dtype: float64



We can use selection with boolean statements, while we are selecting in Pandas.


```python
# Selecting months have less than one snow day average
NYC_SnowAvgs.loc[NYC_SnowAvgs['Avg SnowDays']<1,:]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Avg SnowDays</th>
      <th>Avg Precip. (cm)</th>
      <th>Avg Low Temp. (F)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>April</th>
      <td>0.2</td>
      <td>1.5</td>
      <td>45</td>
    </tr>
    <tr>
      <th>November</th>
      <td>0.2</td>
      <td>0.8</td>
      <td>42</td>
    </tr>
  </tbody>
</table>
</div>




```python
# brand of crude priced above 110 a barrel for row 2013-Q1
SpotCrudePrices_2013.loc[:,SpotCrudePrices_2013.loc['2013-Q1']>110]
# Using 2 .loc for more precise selection, how cool is that
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>UK_Brent</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-Q1</th>
      <td>112.9</td>
    </tr>
    <tr>
      <th>2013-Q2</th>
      <td>103.0</td>
    </tr>
    <tr>
      <th>2013-Q3</th>
      <td>110.1</td>
    </tr>
    <tr>
      <th>2013-Q4</th>
      <td>109.4</td>
    </tr>
  </tbody>
</table>
</div>



Note that the preceding arguments involve the Boolean operators ```<``` and ```>``` that actually evaluate the Boolean arrays, for example:


```python
SpotCrudePrices_2013.loc['2013-Q1']>110
```




    Dubai                      False
    UK_Brent                    True
    West_Texas_Intermediate    False
    Name: 2013-Q1, dtype: bool



### Integer-Oriented Indexing
The ```.iloc``` operator supports integer-based positional indexing. It accepts the following as inputs:

- A single integer, for example, ```7```
- A list or array of integers, for example, ```[2,3]```
- A slice object with integers, for example, ```1:4```


```python
import scipy.constants as phys
import math
```


```python
sci_values=pd.DataFrame([[math.pi, math.sin(math.pi),math.cos(math.pi)],
                         [math.e,math.log(math.e), phys.golden],
                         [phys.c,phys.g,phys.e],
                         [phys.m_e,phys.m_p,phys.m_n]],
                        index=list(range(0,20,5)))
sci_values
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3.141593e+00</td>
      <td>1.224647e-16</td>
      <td>-1.000000e+00</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2.718282e+00</td>
      <td>1.000000e+00</td>
      <td>1.618034e+00</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2.997925e+08</td>
      <td>9.806650e+00</td>
      <td>1.602177e-19</td>
    </tr>
    <tr>
      <th>15</th>
      <td>9.109384e-31</td>
      <td>1.672622e-27</td>
      <td>1.674927e-27</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Select first two rows by using integer slicing
sci_values.iloc[:2]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3.141593</td>
      <td>1.224647e-16</td>
      <td>-1.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2.718282</td>
      <td>1.000000e+00</td>
      <td>1.618034</td>
    </tr>
  </tbody>
</table>
</div>




```python
sci_values.iloc[2,0:2]
```




    0    2.997925e+08
    1    9.806650e+00
    Name: 10, dtype: float64



Note that the arguments to ```.iloc``` are strictly positional and have nothing to do with the index values.

we should use the label-indexing operator ```.loc``` instead...


```python
sci_values.iloc[10]
```


    ---------------------------------------------------------------------------

    IndexError                                Traceback (most recent call last)

    ...

    IndexError: single positional indexer is out-of-bounds



```python
sci_values.loc[10]
```




    0    2.997925e+08
    1    9.806650e+00
    2    1.602177e-19
    Name: 10, dtype: float64




```python
# To Slice out a specific row
sci_values.iloc[2:3,:]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10</th>
      <td>299792458.0</td>
      <td>9.80665</td>
      <td>1.602177e-19</td>
    </tr>
  </tbody>
</table>
</div>




```python
# TO obtain a cross-section using an integer position
sci_values.iloc[3]
```




    0    9.109384e-31
    1    1.672622e-27
    2    1.674927e-27
    Name: 15, dtype: float64



> The ```.iat``` and ```.at``` operators can be used for a quick selection of scalar values. They are faster than them but not really common


```python
sci_values.iloc[3,0]
```




    9.1093835599999998e-31




```python
sci_values.iat[3,0]
```




    9.1093835599999998e-31




```python
%timeit sci_values.iloc[3,0]
```

    The slowest run took 6.17 times longer than the fastest. This could mean that an intermediate result is being cached.
    10000 loops, best of 3: 84 µs per loop



```python
%timeit sci_values.iat[3,0]
```

    The slowest run took 20.61 times longer than the fastest. This could mean that an intermediate result is being cached.
    100000 loops, best of 3: 6.06 µs per loop


### Mixed Indexing with ```.ix``` operator

The ```.ix``` operator behaves like a mixture of the ```.loc``` and ```.iloc``` operators, with the ```.loc``` behavior taking precedence. It takes the following as possible inputs:

- A single label or integer
- A list of integeres or labels
- An integer slice or label slice
- A Boolean array


- In the following examples I will use this data set imported from csv

        TradingDate,Nasdaq,S&P 500,Russell 2000
        2014/01/30,4123.13,1794.19,1139.36
        2014/01/31,4103.88,1782.59,1130.88
        2014/02/03,3996.96,1741.89,1094.58
        2014/02/04,4031.52,1755.2,1102.84
        2014/02/05,4011.55,1751.64,1093.59
        2014/02/06,4057.12,1773.43,1103.93


```python
stockIndexDataDF=pd.read_csv('stock_index_closing.csv')
stockIndexDataDF
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>TradingDate</th>
      <th>Nasdaq</th>
      <th>S&amp;P 500</th>
      <th>Russell 2000</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2014/01/30</td>
      <td>4123.13</td>
      <td>1794.19</td>
      <td>1139.36</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2014/01/31</td>
      <td>4103.88</td>
      <td>1782.59</td>
      <td>1130.88</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2014/02/03</td>
      <td>3996.96</td>
      <td>1741.89</td>
      <td>1094.58</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2014/02/04</td>
      <td>4031.52</td>
      <td>1755.20</td>
      <td>1102.84</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2014/02/05</td>
      <td>4011.55</td>
      <td>1751.64</td>
      <td>1093.59</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2014/02/06</td>
      <td>4057.12</td>
      <td>1773.43</td>
      <td>1103.93</td>
    </tr>
  </tbody>
</table>
</div>



What we see from the preceding example is that the DataFrame created has an integer-based row index. We promptly set the index to be the trading date to index it based on the trading date so that we can use the .ix operator:


```python
stockIndexDF=stockIndexDataDF.set_index('TradingDate')
stockIndexDF
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Nasdaq</th>
      <th>S&amp;P 500</th>
      <th>Russell 2000</th>
    </tr>
    <tr>
      <th>TradingDate</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2014/01/30</th>
      <td>4123.13</td>
      <td>1794.19</td>
      <td>1139.36</td>
    </tr>
    <tr>
      <th>2014/01/31</th>
      <td>4103.88</td>
      <td>1782.59</td>
      <td>1130.88</td>
    </tr>
    <tr>
      <th>2014/02/03</th>
      <td>3996.96</td>
      <td>1741.89</td>
      <td>1094.58</td>
    </tr>
    <tr>
      <th>2014/02/04</th>
      <td>4031.52</td>
      <td>1755.20</td>
      <td>1102.84</td>
    </tr>
    <tr>
      <th>2014/02/05</th>
      <td>4011.55</td>
      <td>1751.64</td>
      <td>1093.59</td>
    </tr>
    <tr>
      <th>2014/02/06</th>
      <td>4057.12</td>
      <td>1773.43</td>
      <td>1103.93</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Using a single label
stockIndexDF.ix['2014/01/30']
```




    Nasdaq          4123.13
    S&P 500         1794.19
    Russell 2000    1139.36
    Name: 2014/01/30, dtype: float64




```python
# Using a list of labels
stockIndexDF.ix[['2014/01/30', '2014/02/06']]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Nasdaq</th>
      <th>S&amp;P 500</th>
      <th>Russell 2000</th>
    </tr>
    <tr>
      <th>TradingDate</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2014/01/30</th>
      <td>4123.13</td>
      <td>1794.19</td>
      <td>1139.36</td>
    </tr>
    <tr>
      <th>2014/02/06</th>
      <td>4057.12</td>
      <td>1773.43</td>
      <td>1103.93</td>
    </tr>
  </tbody>
</table>
</div>




```python
type(stockIndexDF.ix['2014/01/30'])
```




    pandas.core.series.Series




```python
type(stockIndexDF.ix[['2014/01/30']])
```




    pandas.core.frame.DataFrame



For the former, the indexer is a scalar; for the latter, the indexer is a list. A list indexer is used to select multiple columns. A multi-column slice of a DataFrame can only result in another DataFrame since it is 2D; hence, what is returned in the latter case is a DataFrame.




```python
# Using a label-based slice:
tradingDates=stockIndexDataDF.TradingDate
stockIndexDF.ix[tradingDates[:3]]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Nasdaq</th>
      <th>S&amp;P 500</th>
      <th>Russell 2000</th>
    </tr>
    <tr>
      <th>TradingDate</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2014/01/30</th>
      <td>4123.13</td>
      <td>1794.19</td>
      <td>1139.36</td>
    </tr>
    <tr>
      <th>2014/01/31</th>
      <td>4103.88</td>
      <td>1782.59</td>
      <td>1130.88</td>
    </tr>
    <tr>
      <th>2014/02/03</th>
      <td>3996.96</td>
      <td>1741.89</td>
      <td>1094.58</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Using a single integer:
stockIndexDF.ix[0]
```




    Nasdaq          4123.13
    S&P 500         1794.19
    Russell 2000    1139.36
    Name: 2014/01/30, dtype: float64




```python
# Using a list of integers:
stockIndexDF.ix[[0,2]]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Nasdaq</th>
      <th>S&amp;P 500</th>
      <th>Russell 2000</th>
    </tr>
    <tr>
      <th>TradingDate</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2014/01/30</th>
      <td>4123.13</td>
      <td>1794.19</td>
      <td>1139.36</td>
    </tr>
    <tr>
      <th>2014/02/03</th>
      <td>3996.96</td>
      <td>1741.89</td>
      <td>1094.58</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Using an integer slice:
stockIndexDF.ix[1:3]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Nasdaq</th>
      <th>S&amp;P 500</th>
      <th>Russell 2000</th>
    </tr>
    <tr>
      <th>TradingDate</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2014/01/31</th>
      <td>4103.88</td>
      <td>1782.59</td>
      <td>1130.88</td>
    </tr>
    <tr>
      <th>2014/02/03</th>
      <td>3996.96</td>
      <td>1741.89</td>
      <td>1094.58</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Using an boolean array
stockIndexDF.ix[stockIndexDF['Russell 2000']>1100]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Nasdaq</th>
      <th>S&amp;P 500</th>
      <th>Russell 2000</th>
    </tr>
    <tr>
      <th>TradingDate</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2014/01/30</th>
      <td>4123.13</td>
      <td>1794.19</td>
      <td>1139.36</td>
    </tr>
    <tr>
      <th>2014/01/31</th>
      <td>4103.88</td>
      <td>1782.59</td>
      <td>1130.88</td>
    </tr>
    <tr>
      <th>2014/02/04</th>
      <td>4031.52</td>
      <td>1755.20</td>
      <td>1102.84</td>
    </tr>
    <tr>
      <th>2014/02/06</th>
      <td>4057.12</td>
      <td>1773.43</td>
      <td>1103.93</td>
    </tr>
  </tbody>
</table>
</div>



As in the case of ```.loc``` , the row index must be specified first for the ```.ix``` operator.

We now turn to the topic of MultiIndexing. Multi-level or hierarchical indexing is useful because it enables the pandas user to select and massage data in multiple dimensions by using data structures such as Series and DataFrame.


```python
sharesIndexDataDF=pd.read_csv('stock_index_closing.csv')
sharesIndexDataDF
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>TradingDate</th>
      <th>PriceType</th>
      <th>Nasdaq</th>
      <th>S&amp;P 500</th>
      <th>Russell 2000</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2014/02/21</td>
      <td>open</td>
      <td>4282.17</td>
      <td>1841.07</td>
      <td>1166.25</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2014/02/21</td>
      <td>close</td>
      <td>4263.41</td>
      <td>1836.25</td>
      <td>1164.63</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2014/02/21</td>
      <td>high</td>
      <td>4284.85</td>
      <td>1846.13</td>
      <td>1168.43</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2014/02/24</td>
      <td>open</td>
      <td>4273.32</td>
      <td>1836.78</td>
      <td>1166.74</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2014/02/24</td>
      <td>close</td>
      <td>4292.97</td>
      <td>1847.61</td>
      <td>1174.55</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2014/02/24</td>
      <td>high</td>
      <td>4311.13</td>
      <td>1858.71</td>
      <td>1180.29</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2014/02/25</td>
      <td>open</td>
      <td>4298.48</td>
      <td>1847.66</td>
      <td>1176.00</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2014/02/25</td>
      <td>close</td>
      <td>4287.59</td>
      <td>1845.12</td>
      <td>1173.95</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2014/02/25</td>
      <td>high</td>
      <td>4307.51</td>
      <td>1852.91</td>
      <td>1179.43</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2014/02/26</td>
      <td>open</td>
      <td>4300.45</td>
      <td>1845.79</td>
      <td>1176.11</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2014/02/26</td>
      <td>close</td>
      <td>4292.06</td>
      <td>1845.16</td>
      <td>1181.72</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2014/02/26</td>
      <td>high</td>
      <td>4316.82</td>
      <td>1852.65</td>
      <td>1188.06</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2014/02/27</td>
      <td>open</td>
      <td>4291.47</td>
      <td>1844.90</td>
      <td>1179.28</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2014/02/27</td>
      <td>close</td>
      <td>4318.93</td>
      <td>1854.29</td>
      <td>1187.94</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2014/02/27</td>
      <td>high</td>
      <td>4322.46</td>
      <td>1854.53</td>
      <td>1187.94</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2014/02/28</td>
      <td>open</td>
      <td>4323.52</td>
      <td>1855.12</td>
      <td>1189.19</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2014/02/28</td>
      <td>close</td>
      <td>4308.12</td>
      <td>1859.45</td>
      <td>1183.03</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2014/02/28</td>
      <td>high</td>
      <td>4342.59</td>
      <td>1867.92</td>
      <td>1193.50</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Create a MultiIndex from trading date and priceType columns
sharesIndexDF=sharesIndexDataDF.set_index(['TradingDate','PriceType'])
mIndex = sharesIndexDF.index
mIndex
```




    MultiIndex(levels=[[u'2014/02/21', u'2014/02/24', u'2014/02/25', u'2014/02/26', u'2014/02/27', u'2014/02/28'], [u'close', u'high', u'open']],
               labels=[[0, 0, 0, 1, 1, 1, 2, 2, 2, 3, 3, 3, 4, 4, 4, 5, 5, 5], [2, 0, 1, 2, 0, 1, 2, 0, 1, 2, 0, 1, 2, 0, 1, 2, 0, 1]],
               names=[u'TradingDate', u'PriceType'])




```python
sharesIndexDF
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Nasdaq</th>
      <th>S&amp;P 500</th>
      <th>Russell 2000</th>
    </tr>
    <tr>
      <th>TradingDate</th>
      <th>PriceType</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">2014/02/21</th>
      <th>open</th>
      <td>4282.17</td>
      <td>1841.07</td>
      <td>1166.25</td>
    </tr>
    <tr>
      <th>close</th>
      <td>4263.41</td>
      <td>1836.25</td>
      <td>1164.63</td>
    </tr>
    <tr>
      <th>high</th>
      <td>4284.85</td>
      <td>1846.13</td>
      <td>1168.43</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">2014/02/24</th>
      <th>open</th>
      <td>4273.32</td>
      <td>1836.78</td>
      <td>1166.74</td>
    </tr>
    <tr>
      <th>close</th>
      <td>4292.97</td>
      <td>1847.61</td>
      <td>1174.55</td>
    </tr>
    <tr>
      <th>high</th>
      <td>4311.13</td>
      <td>1858.71</td>
      <td>1180.29</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">2014/02/25</th>
      <th>open</th>
      <td>4298.48</td>
      <td>1847.66</td>
      <td>1176.00</td>
    </tr>
    <tr>
      <th>close</th>
      <td>4287.59</td>
      <td>1845.12</td>
      <td>1173.95</td>
    </tr>
    <tr>
      <th>high</th>
      <td>4307.51</td>
      <td>1852.91</td>
      <td>1179.43</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">2014/02/26</th>
      <th>open</th>
      <td>4300.45</td>
      <td>1845.79</td>
      <td>1176.11</td>
    </tr>
    <tr>
      <th>close</th>
      <td>4292.06</td>
      <td>1845.16</td>
      <td>1181.72</td>
    </tr>
    <tr>
      <th>high</th>
      <td>4316.82</td>
      <td>1852.65</td>
      <td>1188.06</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">2014/02/27</th>
      <th>open</th>
      <td>4291.47</td>
      <td>1844.90</td>
      <td>1179.28</td>
    </tr>
    <tr>
      <th>close</th>
      <td>4318.93</td>
      <td>1854.29</td>
      <td>1187.94</td>
    </tr>
    <tr>
      <th>high</th>
      <td>4322.46</td>
      <td>1854.53</td>
      <td>1187.94</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">2014/02/28</th>
      <th>open</th>
      <td>4323.52</td>
      <td>1855.12</td>
      <td>1189.19</td>
    </tr>
    <tr>
      <th>close</th>
      <td>4308.12</td>
      <td>1859.45</td>
      <td>1183.03</td>
    </tr>
    <tr>
      <th>high</th>
      <td>4342.59</td>
      <td>1867.92</td>
      <td>1193.50</td>
    </tr>
  </tbody>
</table>
</div>



Upon inspection, we see that the MultiIndex consists of a list of tuples. Applying the get_level_values function with the appropriate argument produces a list of the labels for each level of the index:


```python
mIndex.get_level_values(0)
```




    Index([u'2014/02/21', u'2014/02/21', u'2014/02/21', u'2014/02/24',
           u'2014/02/24', u'2014/02/24', u'2014/02/25', u'2014/02/25',
           u'2014/02/25', u'2014/02/26', u'2014/02/26', u'2014/02/26',
           u'2014/02/27', u'2014/02/27', u'2014/02/27', u'2014/02/28',
           u'2014/02/28', u'2014/02/28'],
          dtype='object', name=u'TradingDate')




```python
mIndex.get_level_values(1)
```




    Index([u'open', u'close', u'high', u'open', u'close', u'high', u'open',
           u'close', u'high', u'open', u'close', u'high', u'open', u'close',
           u'high', u'open', u'close', u'high'],
          dtype='object', name=u'PriceType')



You can achieve hierarchical indexing with a MultiIndexed DataFrame:


```python
# Getting All Price Type of date
sharesIndexDF.ix['2014/02/21']
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Nasdaq</th>
      <th>S&amp;P 500</th>
      <th>Russell 2000</th>
    </tr>
    <tr>
      <th>PriceType</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>open</th>
      <td>4282.17</td>
      <td>1841.07</td>
      <td>1166.25</td>
    </tr>
    <tr>
      <th>close</th>
      <td>4263.41</td>
      <td>1836.25</td>
      <td>1164.63</td>
    </tr>
    <tr>
      <th>high</th>
      <td>4284.85</td>
      <td>1846.13</td>
      <td>1168.43</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Getting specific PriceType  of date
sharesIndexDF.ix['2014/02/21','open']
```




    Nasdaq          4282.17
    S&P 500         1841.07
    Russell 2000    1166.25
    Name: (2014/02/21, open), dtype: float64




```python
# We can slice on first level
sharesIndexDF.ix['2014/02/21':'2014/02/24']
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Nasdaq</th>
      <th>S&amp;P 500</th>
      <th>Russell 2000</th>
    </tr>
    <tr>
      <th>TradingDate</th>
      <th>PriceType</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">2014/02/21</th>
      <th>open</th>
      <td>4282.17</td>
      <td>1841.07</td>
      <td>1166.25</td>
    </tr>
    <tr>
      <th>close</th>
      <td>4263.41</td>
      <td>1836.25</td>
      <td>1164.63</td>
    </tr>
    <tr>
      <th>high</th>
      <td>4284.85</td>
      <td>1846.13</td>
      <td>1168.43</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">2014/02/24</th>
      <th>open</th>
      <td>4273.32</td>
      <td>1836.78</td>
      <td>1166.74</td>
    </tr>
    <tr>
      <th>close</th>
      <td>4292.97</td>
      <td>1847.61</td>
      <td>1174.55</td>
    </tr>
    <tr>
      <th>high</th>
      <td>4311.13</td>
      <td>1858.71</td>
      <td>1180.29</td>
    </tr>
  </tbody>
</table>
</div>




```python
# But if we can slice at lower level:
sharesIndexDF.ix[('2014/02/21','open'):('2014/02/24','open')]
```


    ---------------------------------------------------------------------------

    KeyError                                  Traceback (most recent call last)

    ...

    KeyError: 'Key length (2) was greater than MultiIndex lexsort depth (1)'


However, this results in ```KeyError``` with a rather strange error message. The key lesson to be learned here is that the current incarnation of MultiIndex requires the labels to be sorted for the lower-level slicing routines to work correctly.


In order to do this, you can utilize the ```sortlevel()``` method, which sorts the labels of an axis within a MultiIndex. To be on the safe side, sort first before slicing with a MultiIndex. Thus, we can do the following:


```python
sharesIndexDF.sortlevel(0).ix[('2014/02/21','open'):('2014/02/24','open')]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Nasdaq</th>
      <th>S&amp;P 500</th>
      <th>Russell 2000</th>
    </tr>
    <tr>
      <th>TradingDate</th>
      <th>PriceType</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2014/02/21</th>
      <th>open</th>
      <td>4282.17</td>
      <td>1841.07</td>
      <td>1166.25</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">2014/02/24</th>
      <th>close</th>
      <td>4292.97</td>
      <td>1847.61</td>
      <td>1174.55</td>
    </tr>
    <tr>
      <th>high</th>
      <td>4311.13</td>
      <td>1858.71</td>
      <td>1180.29</td>
    </tr>
    <tr>
      <th>open</th>
      <td>4273.32</td>
      <td>1836.78</td>
      <td>1166.74</td>
    </tr>
  </tbody>
</table>
</div>



The ```swaplevel``` function enables levels within the MultiIndex to be swapped:


```python
# Swapping level 0 and 1 in x axis
swappedDF=sharesIndexDF[:7].swaplevel(0, 1, axis=0)
swappedDF
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Nasdaq</th>
      <th>S&amp;P 500</th>
      <th>Russell 2000</th>
    </tr>
    <tr>
      <th>PriceType</th>
      <th>TradingDate</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>open</th>
      <th>2014/02/21</th>
      <td>4282.17</td>
      <td>1841.07</td>
      <td>1166.25</td>
    </tr>
    <tr>
      <th>close</th>
      <th>2014/02/21</th>
      <td>4263.41</td>
      <td>1836.25</td>
      <td>1164.63</td>
    </tr>
    <tr>
      <th>high</th>
      <th>2014/02/21</th>
      <td>4284.85</td>
      <td>1846.13</td>
      <td>1168.43</td>
    </tr>
    <tr>
      <th>open</th>
      <th>2014/02/24</th>
      <td>4273.32</td>
      <td>1836.78</td>
      <td>1166.74</td>
    </tr>
    <tr>
      <th>close</th>
      <th>2014/02/24</th>
      <td>4292.97</td>
      <td>1847.61</td>
      <td>1174.55</td>
    </tr>
    <tr>
      <th>high</th>
      <th>2014/02/24</th>
      <td>4311.13</td>
      <td>1858.71</td>
      <td>1180.29</td>
    </tr>
    <tr>
      <th>open</th>
      <th>2014/02/25</th>
      <td>4298.48</td>
      <td>1847.66</td>
      <td>1176.00</td>
    </tr>
  </tbody>
</table>
</div>



The ```reorder_levels``` function is more general, allowing you to specify the order of the levels:


```python
reorderedDF=sharesIndexDF[:7].reorder_levels(['PriceType','TradingDate'],axis=0)
reorderedDF
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Nasdaq</th>
      <th>S&amp;P 500</th>
      <th>Russell 2000</th>
    </tr>
    <tr>
      <th>PriceType</th>
      <th>TradingDate</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>open</th>
      <th>2014/02/21</th>
      <td>4282.17</td>
      <td>1841.07</td>
      <td>1166.25</td>
    </tr>
    <tr>
      <th>close</th>
      <th>2014/02/21</th>
      <td>4263.41</td>
      <td>1836.25</td>
      <td>1164.63</td>
    </tr>
    <tr>
      <th>high</th>
      <th>2014/02/21</th>
      <td>4284.85</td>
      <td>1846.13</td>
      <td>1168.43</td>
    </tr>
    <tr>
      <th>open</th>
      <th>2014/02/24</th>
      <td>4273.32</td>
      <td>1836.78</td>
      <td>1166.74</td>
    </tr>
    <tr>
      <th>close</th>
      <th>2014/02/24</th>
      <td>4292.97</td>
      <td>1847.61</td>
      <td>1174.55</td>
    </tr>
    <tr>
      <th>high</th>
      <th>2014/02/24</th>
      <td>4311.13</td>
      <td>1858.71</td>
      <td>1180.29</td>
    </tr>
    <tr>
      <th>open</th>
      <th>2014/02/25</th>
      <td>4298.48</td>
      <td>1847.66</td>
      <td>1176.00</td>
    </tr>
  </tbody>
</table>
</div>



## Boolean Indexing

We use Boolean indexing to filter or select parts of the data.

- OR operator is ```|```
- AND operator is ```&```
- NOT operator is ```~```

These operators must be grouped using parentheses when used together.


```python
# Selecting price type close which are bigger than 4300 in Nasdaq
sharesIndexDataDF.ix[(sharesIndexDataDF['PriceType']=='close')&(sharesIndexDataDF['Nasdaq']>4300) ]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>TradingDate</th>
      <th>PriceType</th>
      <th>Nasdaq</th>
      <th>S&amp;P 500</th>
      <th>Russell 2000</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>13</th>
      <td>2014/02/27</td>
      <td>close</td>
      <td>4318.93</td>
      <td>1854.29</td>
      <td>1187.94</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2014/02/28</td>
      <td>close</td>
      <td>4308.12</td>
      <td>1859.45</td>
      <td>1183.03</td>
    </tr>
  </tbody>
</table>
</div>



You can also create Boolean conditions in which you use arrays to filter out parts of the data:



```python
# Ww can also do this extensively
highSelection=sharesIndexDataDF['PriceType']=='high'

NasdaqHigh=sharesIndexDataDF['Nasdaq']<4300

sharesIndexDataDF.ix[highSelection & NasdaqHigh]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>TradingDate</th>
      <th>PriceType</th>
      <th>Nasdaq</th>
      <th>S&amp;P 500</th>
      <th>Russell 2000</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>2014/02/21</td>
      <td>high</td>
      <td>4284.85</td>
      <td>1846.13</td>
      <td>1168.43</td>
    </tr>
  </tbody>
</table>
</div>



The ```isin``` and ```anyall``` methods enable user to achieve more with Boolean indexing that the standart operators used in the preceding sections.

The ```isin``` method takes a list of values and returns a Boolean array with True at the positions within the Series or DataFrame that match the values in the list.



```python
# Check values in Series
stockSeries=pd.Series(['NFLX','AMZN','GOOG','FB','TWTR'])
stockSeries.isin(['AMZN','FB'])
```




    0    False
    1     True
    2    False
    3     True
    4    False
    dtype: bool




```python
# We can use the sub selecting to selecting true values
stockSeries[stockSeries.isin(['AMZN','FB'])]
```




    1    AMZN
    3      FB
    dtype: object




```python
# Dictionary to create a dataframe
australianMammals= {'kangaroo': {'Subclass':'marsupial','Species Origin':'native'},
                    'flying fox' : {'Subclass':'placental','Species Origin':'native'},
                    'black rat': {'Subclass':'placental','Species Origin':'invasive'},
                    'platypus' : {'Subclass':'monotreme','Species Origin':'native'},
                    'wallaby' :{'Subclass':'marsupial','Species Origin':'native'},
                    'palm squirrel' : {'Subclass':'placental','Origin':'invasive'},
                    'anteater': {'Subclass':'monotreme', 'Origin':'native'},
                    'koala': {'Subclass':'marsupial', 'Origin':'native'}}
ozzieMammalsDF = pd.DataFrame(australianMammals)
ozzieMammalsDF
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>anteater</th>
      <th>black rat</th>
      <th>flying fox</th>
      <th>kangaroo</th>
      <th>koala</th>
      <th>palm squirrel</th>
      <th>platypus</th>
      <th>wallaby</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Origin</th>
      <td>native</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>native</td>
      <td>invasive</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Species Origin</th>
      <td>NaN</td>
      <td>invasive</td>
      <td>native</td>
      <td>native</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>native</td>
      <td>native</td>
    </tr>
    <tr>
      <th>Subclass</th>
      <td>monotreme</td>
      <td>placental</td>
      <td>placental</td>
      <td>marsupial</td>
      <td>marsupial</td>
      <td>placental</td>
      <td>monotreme</td>
      <td>marsupial</td>
    </tr>
  </tbody>
</table>
</div>




```python
aussieMammalsDF=ozzieMammalsDF.T # Transposing the data frame
aussieMammalsDF
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Origin</th>
      <th>Species Origin</th>
      <th>Subclass</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>anteater</th>
      <td>native</td>
      <td>NaN</td>
      <td>monotreme</td>
    </tr>
    <tr>
      <th>black rat</th>
      <td>NaN</td>
      <td>invasive</td>
      <td>placental</td>
    </tr>
    <tr>
      <th>flying fox</th>
      <td>NaN</td>
      <td>native</td>
      <td>placental</td>
    </tr>
    <tr>
      <th>kangaroo</th>
      <td>NaN</td>
      <td>native</td>
      <td>marsupial</td>
    </tr>
    <tr>
      <th>koala</th>
      <td>native</td>
      <td>NaN</td>
      <td>marsupial</td>
    </tr>
    <tr>
      <th>palm squirrel</th>
      <td>invasive</td>
      <td>NaN</td>
      <td>placental</td>
    </tr>
    <tr>
      <th>platypus</th>
      <td>NaN</td>
      <td>native</td>
      <td>monotreme</td>
    </tr>
    <tr>
      <th>wallaby</th>
      <td>NaN</td>
      <td>native</td>
      <td>marsupial</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Selecting native animals
aussieMammalsDF.isin({'Subclass':['marsupial'],'Origin':['native']})
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Origin</th>
      <th>Species Origin</th>
      <th>Subclass</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>anteater</th>
      <td>True</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>black rat</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>flying fox</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>kangaroo</th>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>koala</th>
      <td>True</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>palm squirrel</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>platypus</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>wallaby</th>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



### ```where()``` method

The ```where()``` method is used to ensure that the result of Boolean filtering is the same shape as the original data.



```python
import numpy as np
np.random.seed(100)  # Setting random generator to 100 so we can generate same results later
normvals = pd.Series([np.random.normal() for i in np.arange(10)])
normvals
```




    0   -1.749765
    1    0.342680
    2    1.153036
    3   -0.252436
    4    0.981321
    5    0.514219
    6    0.221180
    7   -1.070043
    8   -0.189496
    9    0.255001
    dtype: float64




```python
# Return values bigger than 0
normvals[normvals>0]
```




    1    0.342680
    2    1.153036
    4    0.981321
    5    0.514219
    6    0.221180
    9    0.255001
    dtype: float64




```python
# Return values bigger than 0, prints the same shape
# by putting NaN to other places
normvals.where(normvals>0)
```




    0         NaN
    1    0.342680
    2    1.153036
    3         NaN
    4    0.981321
    5    0.514219
    6    0.221180
    7         NaN
    8         NaN
    9    0.255001
    dtype: float64




```python
# Creating DataFrame with set random values
np.random.seed(100)
normDF = pd.DataFrame([[round(np.random.normal(),3) for i in np.arange(5)] for j in range(3)],
                      columns=['0','30','60','90','120'])
normDF
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>30</th>
      <th>60</th>
      <th>90</th>
      <th>120</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-1.750</td>
      <td>0.343</td>
      <td>1.153</td>
      <td>-0.252</td>
      <td>0.981</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.514</td>
      <td>0.221</td>
      <td>-1.070</td>
      <td>-0.189</td>
      <td>0.255</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.458</td>
      <td>0.435</td>
      <td>-0.584</td>
      <td>0.817</td>
      <td>0.673</td>
    </tr>
  </tbody>
</table>
</div>




```python
# For DataFrames we get same shape no matter we use
normDF[normDF>0]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>30</th>
      <th>60</th>
      <th>90</th>
      <th>120</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>0.343</td>
      <td>1.153</td>
      <td>NaN</td>
      <td>0.981</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.514</td>
      <td>0.221</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.255</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>0.435</td>
      <td>NaN</td>
      <td>0.817</td>
      <td>0.673</td>
    </tr>
  </tbody>
</table>
</div>




```python
# For DataFrames we get same shape no matter we use
normDF.where(normDF>0)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>30</th>
      <th>60</th>
      <th>90</th>
      <th>120</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>0.343</td>
      <td>1.153</td>
      <td>NaN</td>
      <td>0.981</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.514</td>
      <td>0.221</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.255</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>0.435</td>
      <td>NaN</td>
      <td>0.817</td>
      <td>0.673</td>
    </tr>
  </tbody>
</table>
</div>




```python
# The inverse operation of the where is mask
normDF.mask(normDF>0)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>30</th>
      <th>60</th>
      <th>90</th>
      <th>120</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-1.750</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-0.252</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>-1.070</td>
      <td>-0.189</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.458</td>
      <td>NaN</td>
      <td>-0.584</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



### Summary
To summarize, there are various ways of selecting data from pandas:

- We can use basic indexing, which is closest to our understanding of accessing data in an array.
- We can use label- or integer-based indexing with the associated operators.
- We can use a MultiIndex, which is the pandas version of a composite key comprising multiple fields.
- We can use a Boolean/logical index.

For further reading and research check out the offical documentation, [indexing](http://pandas.pydata.org/pandas-docs/stable/indexing.html)


> Your input is really valuable, so do not hesitate to leave a comment. I would love to read them and respond to them.

> Until next time, be safe...
