---
layout: post
title: Introduction to Pandas 1
excerpt:
categories: blog
tags: ["Python", "Data Science", "Pandas"]
published: true
comments: true
share: true
---

In this post I will summarize the data structures of ```Pandas``` library. ```Pandas``` is a library written for data manipulation and analysis. It is built on top of the ```Numpy``` library and it provides features not available in ```Numpy```, so to be able to follow this tutorial you should have some basics on Python and NumPy library.

I am going to follow the official data structure documentation [here](http://pandas.pydata.org/pandas-docs/dev/dsintro.html.)

If you like to follow this small tutorial in notebook format you can check out [here](https://github.com/eneskemalergin/Blog-Notebooks/blob/master/Introduction_to_Pandas-1.ipynb)

## Data Structures in Pandas

There are 3 main data structures:

### 1. Series

The series are the 1D ```NumPy``` array under the hood. It consists of a ```NumPy``` array coupled with an array of labels.

__Create Series:__

```Python
import pandas as pd
ser = pd.Series(data, index=idx)
```

- ```data``` can be ```ndarray```, a Python dictionary, or a scalar value



```python
# Using Scalar Values
import pandas as pd
ser = pd.Series([20, 21, 12], index=['London', 'New York','Helsinki'])
print(ser)
```

    London      20
    New York    21
    Helsinki    12
    dtype: int64



```python
# Using Numpy ndarray
import numpy as np
np.random.seed(100)
ser=pd.Series(np.random.rand(7))
ser
```




    0    0.543405
    1    0.278369
    2    0.424518
    3    0.844776
    4    0.004719
    5    0.121569
    6    0.670749
    dtype: float64



__Using Python Dictionary:__

If we want to use Python Dictionary, the usage is slighly different. Since dictionary data structure has the


```python
currDict = {'US' : 'dollar', 'UK' : 'pound',
            'Germany': 'euro', 'Mexico':'peso',
            'Nigeria':'naira',
            'China':'yuan', 'Japan':'yen'}
currSeries=pd.Series(currDict)
currSeries
```




    China        yuan
    Germany      euro
    Japan         yen
    Mexico       peso
    Nigeria     naira
    UK          pound
    US         dollar
    dtype: object



The index of a pandas Series structure is of type ```pandas.core.index.Index``` and can be viewed as an ordered multiset.

In the following case, we specify an index, but the index contains one entry that isn't a key in the corresponding ```dict```. The result is that the value for the key is assigned as ```NaN```, indicating that it is missing. We will deal with handling missing values in a later section.


```python
stockPrices = {'GOOG':1180.97,'FB':62.57,
                'TWTR': 64.50, 'AMZN':358.69,
                'AAPL':500.6}
stockPriceSeries=pd.Series(stockPrices,
                            index=['GOOG','FB','YHOO',
                                    'TWTR','AMZN','AAPL'],
                            name='stockPrices')
stockPriceSeries
```




    GOOG    1180.97
    FB        62.57
    YHOO        NaN
    TWTR      64.50
    AMZN     358.69
    AAPL     500.60
    Name: stockPrices, dtype: float64



The behavior of Series is very similar to that of ```numpy``` arrays discussed in a previous section, with one caveat being that an operation such as slicing also slices the index.

- Values can be set and accessed using the index label in a dictionary-like manner:


```python
stockPriceSeries
```




    GOOG    1180.97
    FB        62.57
    YHOO        NaN
    TWTR      64.50
    AMZN     358.69
    AAPL     500.60
    Name: stockPrices, dtype: float64




```python
stockPriceSeries['GOOG']=1200.0
stockPriceSeries
```




    GOOG    1200.00
    FB        62.57
    YHOO        NaN
    TWTR      64.50
    AMZN     358.69
    AAPL     500.60
    Name: stockPrices, dtype: float64



Just as in the case of ```dict```, ```KeyError``` is raised if you try to retrieve a missing label,

We can avoid this error to be avoid by explicitly using get as follows:


```python
stockPriceSeries.get('MSFT',np.NaN)
```




    nan



In this case, the default value of ```np.NaN``` is specified as the value to return when the key does not exist in the Series structure.

The slice operation behaves the same way as a ```NumPy``` array:


```python
stockPriceSeries[:4]
```




    GOOG    1200.00
    FB        62.57
    YHOO        NaN
    TWTR      64.50
    Name: stockPrices, dtype: float64



Logical slicing also works as follows:


```python
stockPriceSeries[stockPriceSeries > 100]
```




    GOOG    1200.00
    AMZN     358.69
    AAPL     500.60
    Name: stockPrices, dtype: float64



Arithmetic and statistical operations can be applied, just as with a NumPy array:


```python
np.mean(stockPriceSeries)
```




    437.27200000000005




```python
np.std(stockPriceSeries)
```




    417.4446361087899




```python
ser
```




    0    0.543405
    1    0.278369
    2    0.424518
    3    0.844776
    4    0.004719
    5    0.121569
    6    0.670749
    dtype: float64




```python
ser*ser
```




    0    0.295289
    1    0.077490
    2    0.180215
    3    0.713647
    4    0.000022
    5    0.014779
    6    0.449904
    dtype: float64




```python
np.sqrt(ser)
```




    0    0.737160
    1    0.527607
    2    0.651550
    3    0.919117
    4    0.068694
    5    0.348668
    6    0.818993
    dtype: float64




```python
ser[1:]
```




    1    0.278369
    2    0.424518
    3    0.844776
    4    0.004719
    5    0.121569
    6    0.670749
    dtype: float64



## 2. Data Frame

DataFrame is an 2-dimensional labeled array. Its column types can be heterogeneous: that is, of varying types. It is similar to structured arrays in NumPy with mutability added. It has the following properties:

- Conceptually analogous to a table or spreadsheet of data.
- Similar to a NumPy ```ndarray``` but not a subclass of ```np.ndarray```.
- Columns can be of heterogeneous types: ```float64, int, bool,``` and so on.
- A DataFrame column is a Series structure.
- It can be thought of as a dictionary of Series structures where both the columns and the rows are indexed, denoted as 'index' in the case of rows and 'columns' in the case of columns.
- It is size mutable: columns can be inserted and deleted.

DataFrame is the most commonly used data structure in pandas. The constructor accepts many different types of arguments:
- Dictionary of ```1D ndarrays```, lists, dictionaries, or Series structures
- ```2D NumPy array```
- Structured or record ndarray
- Series structures
- Another DataFrame structure


__Using Dictionaries of Series:__



```python
# Dictionary created with pandas.Series
stockSummaries={
        'AMZN': pd.Series([346.15,0.59,459,0.52,589.8,158.88],
                            index=['Closing price','EPS','Shares Outstanding(M)',
                            'Beta', 'P/E','Market Cap(B)']),
        'GOOG': pd.Series([1133.43,36.05,335.83,0.87,31.44,380.64],
                            index=['Closing price','EPS','Shares Outstanding(M)',
                            'Beta','P/E','Market Cap(B)']),
        'FB': pd.Series([61.48,0.59,2450,104.93,150.92],
                            index=['Closing price','EPS','Shares Outstanding(M)',
                            'P/E', 'Market Cap(B)']),
        'YHOO': pd.Series([34.90,1.27,1010,27.48,0.66,35.36],
                            index=['Closing price','EPS','Shares Outstanding(M)',
                            'P/E','Beta', 'Market Cap(B)']),
        'TWTR':pd.Series([65.25,-0.3,555.2,36.23],
                            index=['Closing price','EPS','Shares Outstanding(M)',
                            'Market Cap(B)']),
        'AAPL':pd.Series([501.53,40.32,892.45,12.44,447.59,0.84],
                            index=['Closing price','EPS','Shares Outstanding(M)','P/E',
                            'Market Cap(B)','Beta'])}

stockDF=pd.DataFrame(stockSummaries)
stockDF
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>AAPL</th>
      <th>AMZN</th>
      <th>FB</th>
      <th>GOOG</th>
      <th>TWTR</th>
      <th>YHOO</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Beta</th>
      <td>0.84</td>
      <td>0.52</td>
      <td>NaN</td>
      <td>0.87</td>
      <td>NaN</td>
      <td>0.66</td>
    </tr>
    <tr>
      <th>Closing price</th>
      <td>501.53</td>
      <td>346.15</td>
      <td>61.48</td>
      <td>1133.43</td>
      <td>65.25</td>
      <td>34.90</td>
    </tr>
    <tr>
      <th>EPS</th>
      <td>40.32</td>
      <td>0.59</td>
      <td>0.59</td>
      <td>36.05</td>
      <td>-0.30</td>
      <td>1.27</td>
    </tr>
    <tr>
      <th>Market Cap(B)</th>
      <td>447.59</td>
      <td>158.88</td>
      <td>150.92</td>
      <td>380.64</td>
      <td>36.23</td>
      <td>35.36</td>
    </tr>
    <tr>
      <th>P/E</th>
      <td>12.44</td>
      <td>589.80</td>
      <td>104.93</td>
      <td>31.44</td>
      <td>NaN</td>
      <td>27.48</td>
    </tr>
    <tr>
      <th>Shares Outstanding(M)</th>
      <td>892.45</td>
      <td>459.00</td>
      <td>2450.00</td>
      <td>335.83</td>
      <td>555.20</td>
      <td>1010.00</td>
    </tr>
  </tbody>
</table>
</div>




```python
# We can also change the order...
stockDF=pd.DataFrame(stockSummaries,
                    index=['Closing price','EPS',
                    'Shares Outstanding(M)',
                    'P/E', 'Market Cap(B)','Beta'])
stockDF
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>AAPL</th>
      <th>AMZN</th>
      <th>FB</th>
      <th>GOOG</th>
      <th>TWTR</th>
      <th>YHOO</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Closing price</th>
      <td>501.53</td>
      <td>346.15</td>
      <td>61.48</td>
      <td>1133.43</td>
      <td>65.25</td>
      <td>34.90</td>
    </tr>
    <tr>
      <th>EPS</th>
      <td>40.32</td>
      <td>0.59</td>
      <td>0.59</td>
      <td>36.05</td>
      <td>-0.30</td>
      <td>1.27</td>
    </tr>
    <tr>
      <th>Shares Outstanding(M)</th>
      <td>892.45</td>
      <td>459.00</td>
      <td>2450.00</td>
      <td>335.83</td>
      <td>555.20</td>
      <td>1010.00</td>
    </tr>
    <tr>
      <th>P/E</th>
      <td>12.44</td>
      <td>589.80</td>
      <td>104.93</td>
      <td>31.44</td>
      <td>NaN</td>
      <td>27.48</td>
    </tr>
    <tr>
      <th>Market Cap(B)</th>
      <td>447.59</td>
      <td>158.88</td>
      <td>150.92</td>
      <td>380.64</td>
      <td>36.23</td>
      <td>35.36</td>
    </tr>
    <tr>
      <th>Beta</th>
      <td>0.84</td>
      <td>0.52</td>
      <td>NaN</td>
      <td>0.87</td>
      <td>NaN</td>
      <td>0.66</td>
    </tr>
  </tbody>
</table>
</div>



The row index labels and column labels can be accessed via the index and column attributes:


```python
stockDF.index
```




    Index([u'Closing price', u'EPS', u'Shares Outstanding(M)', u'P/E',
           u'Market Cap(B)', u'Beta'],
          dtype='object')




```python
stockDF.columns
```




    Index([u'AAPL', u'AMZN', u'FB', u'GOOG', u'TWTR', u'YHOO'], dtype='object')



__Using ndarrays/lists:__

When we create a dataframe from lists, the keys become the column labels in the DataFrame structure and the data in the list becomes the column values. Note how the row label indexes are generated using ```np.range(n)```.


```python
algos={'search':['DFS','BFS','Binary Search','Linear','ShortestPath (Djikstra)'],
       'sorting': ['Quicksort','Mergesort', 'Heapsort','Bubble Sort', 'Insertion Sort'],
       'machine learning':['RandomForest', 'K Nearest Neighbor', 'Logistic Regression', 'K-Means Clustering', 'Linear Regression']}
algoDF=pd.DataFrame(algos)
algoDF
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>machine learning</th>
      <th>search</th>
      <th>sorting</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>RandomForest</td>
      <td>DFS</td>
      <td>Quicksort</td>
    </tr>
    <tr>
      <th>1</th>
      <td>K Nearest Neighbor</td>
      <td>BFS</td>
      <td>Mergesort</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Logistic Regression</td>
      <td>Binary Search</td>
      <td>Heapsort</td>
    </tr>
    <tr>
      <th>3</th>
      <td>K-Means Clustering</td>
      <td>Linear</td>
      <td>Bubble Sort</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Linear Regression</td>
      <td>ShortestPath (Djikstra)</td>
      <td>Insertion Sort</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Or we can index by specifying the index when creating data frame
pd.DataFrame(algos,index=['algo_1','algo_2','algo_3','algo_4','algo_5'])
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>machine learning</th>
      <th>search</th>
      <th>sorting</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>algo_1</th>
      <td>RandomForest</td>
      <td>DFS</td>
      <td>Quicksort</td>
    </tr>
    <tr>
      <th>algo_2</th>
      <td>K Nearest Neighbor</td>
      <td>BFS</td>
      <td>Mergesort</td>
    </tr>
    <tr>
      <th>algo_3</th>
      <td>Logistic Regression</td>
      <td>Binary Search</td>
      <td>Heapsort</td>
    </tr>
    <tr>
      <th>algo_4</th>
      <td>K-Means Clustering</td>
      <td>Linear</td>
      <td>Bubble Sort</td>
    </tr>
    <tr>
      <th>algo_5</th>
      <td>Linear Regression</td>
      <td>ShortestPath (Djikstra)</td>
      <td>Insertion Sort</td>
    </tr>
  </tbody>
</table>
</div>



__Using Structured Array:__

Structured arrayis an array of records or structs, for more info check [structured arrays documentation](https://docs.scipy.org/doc/numpy/user/basics.rec.html):


```python
memberData = np.zeros((4,), dtype=[('Name','a15'), ('Age','i4'), ('Weight','f4')])
memberData[:] = [('Sanjeev',37,162.4), ('Yingluck',45,137.8), ('Emeka',28,153.2), ('Amy',67,101.3)]
memberDF=pd.DataFrame(memberData)
memberDF
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Age</th>
      <th>Weight</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sanjeev</td>
      <td>37</td>
      <td>162.399994</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Yingluck</td>
      <td>45</td>
      <td>137.800003</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Emeka</td>
      <td>28</td>
      <td>153.199997</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Amy</td>
      <td>67</td>
      <td>101.300003</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.DataFrame(memberData, index=['a','b','c','d'])
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Age</th>
      <th>Weight</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>Sanjeev</td>
      <td>37</td>
      <td>162.399994</td>
    </tr>
    <tr>
      <th>b</th>
      <td>Yingluck</td>
      <td>45</td>
      <td>137.800003</td>
    </tr>
    <tr>
      <th>c</th>
      <td>Emeka</td>
      <td>28</td>
      <td>153.199997</td>
    </tr>
    <tr>
      <th>d</th>
      <td>Amy</td>
      <td>67</td>
      <td>101.300003</td>
    </tr>
  </tbody>
</table>
</div>



__Using a Series Structure:__


```python
currSeries.name='currency'
pd.DataFrame(currSeries)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>currency</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>China</th>
      <td>yuan</td>
    </tr>
    <tr>
      <th>Germany</th>
      <td>euro</td>
    </tr>
    <tr>
      <th>Japan</th>
      <td>yen</td>
    </tr>
    <tr>
      <th>Mexico</th>
      <td>peso</td>
    </tr>
    <tr>
      <th>Nigeria</th>
      <td>naira</td>
    </tr>
    <tr>
      <th>UK</th>
      <td>pound</td>
    </tr>
    <tr>
      <th>US</th>
      <td>dollar</td>
    </tr>
  </tbody>
</table>
</div>



There are also alternative constructors for ```DataFrame```; they can be summarized as follows:

- ```DataFrame.from_dict```: It takes a dictionary of dictionaries or sequences and returns DataFrame.
- ```DataFrame.from_records```: It takes a list of tuples or structured ndarray.
- ```DataFrame.from_items```: It takes a sequence of (key, value) pairs. The keys are the column or index names, and the values are the column or row values. If you wish the keys to be row index names, you must specify orient='index' as a parameter and specify the column names.
- ```pandas.io.parsers.read_csv```: This is a helper function that reads a CSV file into a pandas DataFrame structure.
- ```pandas.io.parsers.read_table```: This is a helper function that reads a delimited file into a pandas DataFrame structure.
- ```pandas.io.parsers.read_fwf```: This is a helper function that reads a table of fixed-width lines into a pandas DataFrame structure.

I will point out some of the operations most commonly used with data frames.


```python
# Specific column can be reached as Series
memberDF['Name']
```




    0     Sanjeev
    1    Yingluck
    2       Emeka
    3         Amy
    Name: Name, dtype: object




```python
# A new column can be added via assignment
memberDF['Height']=[60, 70,80, 90]
memberDF
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Age</th>
      <th>Weight</th>
      <th>Height</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sanjeev</td>
      <td>37</td>
      <td>162.399994</td>
      <td>60</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Yingluck</td>
      <td>45</td>
      <td>137.800003</td>
      <td>70</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Emeka</td>
      <td>28</td>
      <td>153.199997</td>
      <td>80</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Amy</td>
      <td>67</td>
      <td>101.300003</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>




```python
# column can be deleted using del
del memberDF['Height']
memberDF
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Age</th>
      <th>Weight</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sanjeev</td>
      <td>37</td>
      <td>162.399994</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Yingluck</td>
      <td>45</td>
      <td>137.800003</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Emeka</td>
      <td>28</td>
      <td>153.199997</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Amy</td>
      <td>67</td>
      <td>101.300003</td>
    </tr>
  </tbody>
</table>
</div>



Basically, a DataFrame structure can be treated as if it were a dictionary of Series objects. Columns get inserted at the end; to insert a column at a specific location, you can use the insert function:


```python
memberDF.insert(2,'isSenior',memberDF['Age']>60)
memberDF
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Age</th>
      <th>isSenior</th>
      <th>Weight</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sanjeev</td>
      <td>37</td>
      <td>False</td>
      <td>162.399994</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Yingluck</td>
      <td>45</td>
      <td>False</td>
      <td>137.800003</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Emeka</td>
      <td>28</td>
      <td>False</td>
      <td>153.199997</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Amy</td>
      <td>67</td>
      <td>True</td>
      <td>101.300003</td>
    </tr>
  </tbody>
</table>
</div>



DataFrame objects align in a manner similar to Series objects, except that they align on both column and index labels. The resulting object is the union of the column and row labels:


```python
ore1DF=pd.DataFrame(np.array([[20,35,25,20],[11,28,32,29]]),columns=['iron','magnesium','copper','silver'])
ore2DF=pd.DataFrame(np.array([[14,34,26,26],[33,19,25,23]]),columns=['iron','magnesium','gold','silver'])
ore1DF+ore2DF
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>copper</th>
      <th>gold</th>
      <th>iron</th>
      <th>magnesium</th>
      <th>silver</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>34</td>
      <td>69</td>
      <td>46</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>44</td>
      <td>47</td>
      <td>52</td>
    </tr>
  </tbody>
</table>
</div>




```python
ore1DF + pd.Series([25,25,25,25], index=['iron','magnesium', 'copper','silver'])
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>iron</th>
      <th>magnesium</th>
      <th>copper</th>
      <th>silver</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>45</td>
      <td>60</td>
      <td>50</td>
      <td>45</td>
    </tr>
    <tr>
      <th>1</th>
      <td>36</td>
      <td>53</td>
      <td>57</td>
      <td>54</td>
    </tr>
  </tbody>
</table>
</div>



Mathematical operators can be applied element wise on DataFrame structures:


```python
np.sqrt(ore1DF)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>iron</th>
      <th>magnesium</th>
      <th>copper</th>
      <th>silver</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4.472136</td>
      <td>5.916080</td>
      <td>5.000000</td>
      <td>4.472136</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3.316625</td>
      <td>5.291503</td>
      <td>5.656854</td>
      <td>5.385165</td>
    </tr>
  </tbody>
</table>
</div>



## 3. Panel

Panel is a 3D array. It is not as widely used as Series or DataFrame. It is not as easily displayed on screen or visualized as the other two because of its 3D nature.

The three axis names are as follows:

- __items__: This is axis 0. Each each item corresponds to a DataFrame structure.
- __major_axis__: This is axis 1. Each item corresponds to the rows of the DataFrame structure.
- __minor_axis__: This is axis 2. Each item corresponds to the columns of each DataFrame structure.

__Using 3D Numpy array with axis labels:__


```python
stockData=np.array([[[63.03,61.48,75],
                     [62.05,62.75,46],
                     [62.74,62.19,53]],
                    [[411.90, 404.38, 2.9],
                     [405.45, 405.91, 2.6],
                     [403.15, 404.42, 2.4]]])

stockData
```




    array([[[  63.03,   61.48,   75.  ],
            [  62.05,   62.75,   46.  ],
            [  62.74,   62.19,   53.  ]],

           [[ 411.9 ,  404.38,    2.9 ],
            [ 405.45,  405.91,    2.6 ],
            [ 403.15,  404.42,    2.4 ]]])




```python
stockHistoricalPrices = pd.Panel(stockData, items=['FB', 'NFLX'],
                                 major_axis=pd.date_range('2/3/2014', periods=3),
                                 minor_axis=['open price', 'closing price', 'volume'])
stockHistoricalPrices
```




    <class 'pandas.core.panel.Panel'>
    Dimensions: 2 (items) x 3 (major_axis) x 3 (minor_axis)
    Items axis: FB to NFLX
    Major_axis axis: 2014-02-03 00:00:00 to 2014-02-05 00:00:00
    Minor_axis axis: open price to volume



As I mentioned earlier visualizing the 3D data is not really easy so we see a small information instead.

__Using Python Dictionary of Data Frame Objects:__


```python
USData=pd.DataFrame(np.array([[249.62 , 8900], [ 282.16,12680], [309.35,14940]]),
                    columns=['Population(M)','GDP($B)'],
                    index=[1990,2000,2010])
USData
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Population(M)</th>
      <th>GDP($B)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1990</th>
      <td>249.62</td>
      <td>8900.0</td>
    </tr>
    <tr>
      <th>2000</th>
      <td>282.16</td>
      <td>12680.0</td>
    </tr>
    <tr>
      <th>2010</th>
      <td>309.35</td>
      <td>14940.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
ChinaData=pd.DataFrame(np.array([[1133.68, 390.28], [ 1266.83,1198.48], [1339.72, 6988.47]]),
                       columns=['Population(M)','GDP($B)'],
                       index=[1990,2000,2010])
ChinaData
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Population(M)</th>
      <th>GDP($B)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1990</th>
      <td>1133.68</td>
      <td>390.28</td>
    </tr>
    <tr>
      <th>2000</th>
      <td>1266.83</td>
      <td>1198.48</td>
    </tr>
    <tr>
      <th>2010</th>
      <td>1339.72</td>
      <td>6988.47</td>
    </tr>
  </tbody>
</table>
</div>




```python
US_ChinaData={'US' : USData,
              'China': ChinaData}

pd.Panel(US_ChinaData)
```




    <class 'pandas.core.panel.Panel'>
    Dimensions: 2 (items) x 3 (major_axis) x 2 (minor_axis)
    Items axis: China to US
    Major_axis axis: 1990 to 2010
    Minor_axis axis: Population(M) to GDP($B)


> Your input is really valuable, so do not hesitate to leave a comment. I would love to read them and respond to them.

> Until next time, be safe...
