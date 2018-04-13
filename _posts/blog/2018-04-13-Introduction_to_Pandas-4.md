---
layout: post
title: Introduction to Pandas 4 - Notebook Test
excerpt:
categories: blog
tags: ["Python", "Data Science", "Pandas"]
published: true
comments: true
share: true
---



Let;s get our hands dirty with another important topic in Pandas. We need to able to handle missing data and we will see some methods to handle them. After making our data more suitable for analysis, or prediction we will learn how to plot it with ```matplotlib``` library.  

> I am going to use matplotlib library for this post and other pandas tutorials but I normally prefer using bokeh interactive plotting library.

If you like to follow this small tutorial in notebook format you can check out [here](https://github.com/eneskemalergin/Blog-Notebooks/blob/master/Introduction_to_Pandas-4.ipynb)

## Handling Missing Data

Missing data is usually shows up as ```NULL``` or ```N/A``` or **```NaN```** (Pandas represents this way.)
Other than appearing natively in the source dataset, missing values can be added to a dataset by an operation such as reindexing, or changing frequencies in the case of a time series:


```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
%matplotlib inline
```


```python
date_stngs = ['2014-05-01','2014-05-02','2014-05-05','2014-05-06','2014-05-07']
tradeDates = pd.to_datetime(pd.Series(date_stngs))
closingPrices=[531.35,527.93,527.81,515.14,509.96]
googClosingPrices=pd.DataFrame(data=closingPrices, columns=['closingPrice'], index=tradeDates)
googClosingPrices
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>closingPrice</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2014-05-01</th>
      <td>531.35</td>
    </tr>
    <tr>
      <th>2014-05-02</th>
      <td>527.93</td>
    </tr>
    <tr>
      <th>2014-05-05</th>
      <td>527.81</td>
    </tr>
    <tr>
      <th>2014-05-06</th>
      <td>515.14</td>
    </tr>
    <tr>
      <th>2014-05-07</th>
      <td>509.96</td>
    </tr>
  </tbody>
</table>
</div>



Pandas is also provides a very easy and fast API to read stock data from various finance data providers.


```python
from pandas_datareader import data, wb # pandas data READ API
import datetime
```


```python
googPrices = data.get_data_yahoo("GOOG", start=datetime.datetime(2014, 5, 1),
                                 end=datetime.datetime(2014, 5, 7))
```


```python
googFinalPrices=pd.DataFrame(googPrices['Close'], index=tradeDates)
googFinalPrices
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Close</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2014-05-01</th>
      <td>531.352435</td>
    </tr>
    <tr>
      <th>2014-05-02</th>
      <td>527.932411</td>
    </tr>
    <tr>
      <th>2014-05-05</th>
      <td>527.812392</td>
    </tr>
    <tr>
      <th>2014-05-06</th>
      <td>515.142330</td>
    </tr>
    <tr>
      <th>2014-05-07</th>
      <td>509.962321</td>
    </tr>
  </tbody>
</table>
</div>



We now have a time series that depicts the closing price of Google's stock from May 1, 2014 to May 7, 2014 with gaps in the date range since the trading only occur on business days. If we want to change the date range so that it shows calendar days (that is, along with the weekend), we can change the frequency of the time series index from business days to calendar days as follow:


```python
googClosingPricesCDays = googClosingPrices.asfreq('D')
googClosingPricesCDays
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>closingPrice</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2014-05-01</th>
      <td>531.35</td>
    </tr>
    <tr>
      <th>2014-05-02</th>
      <td>527.93</td>
    </tr>
    <tr>
      <th>2014-05-03</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2014-05-04</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2014-05-05</th>
      <td>527.81</td>
    </tr>
    <tr>
      <th>2014-05-06</th>
      <td>515.14</td>
    </tr>
    <tr>
      <th>2014-05-07</th>
      <td>509.96</td>
    </tr>
  </tbody>
</table>
</div>



Note that we have now introduced NaN values for the closingPrice for the weekend dates of May 3, 2014 and May 4, 2014.

We can check which values are missing by using the ```isnull()``` and ```notnull()``` functions as follows:


```python
googClosingPricesCDays.isnull()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>closingPrice</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2014-05-01</th>
      <td>False</td>
    </tr>
    <tr>
      <th>2014-05-02</th>
      <td>False</td>
    </tr>
    <tr>
      <th>2014-05-03</th>
      <td>True</td>
    </tr>
    <tr>
      <th>2014-05-04</th>
      <td>True</td>
    </tr>
    <tr>
      <th>2014-05-05</th>
      <td>False</td>
    </tr>
    <tr>
      <th>2014-05-06</th>
      <td>False</td>
    </tr>
    <tr>
      <th>2014-05-07</th>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
googClosingPricesCDays.notnull()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>closingPrice</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2014-05-01</th>
      <td>True</td>
    </tr>
    <tr>
      <th>2014-05-02</th>
      <td>True</td>
    </tr>
    <tr>
      <th>2014-05-03</th>
      <td>False</td>
    </tr>
    <tr>
      <th>2014-05-04</th>
      <td>False</td>
    </tr>
    <tr>
      <th>2014-05-05</th>
      <td>True</td>
    </tr>
    <tr>
      <th>2014-05-06</th>
      <td>True</td>
    </tr>
    <tr>
      <th>2014-05-07</th>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



A Boolean DataFrame is returned in each case. In datetime and pandas Timestamps, missing values are represented by the NaT value. This is the equivalent of NaN in pandas for time-based types


```python
tDates=tradeDates.copy()
tDates[1]=np.NaN
tDates[4]=np.NaN
tDates
```


```python
FBVolume=[82.34,54.11,45.99,55.86,78.5]
TWTRVolume=[15.74,12.71,10.39,134.62,68.84]
socialTradingVolume=pd.concat([pd.Series(FBVolume), pd.Series(TWTRVolume),
                               tradeDates], axis=1,keys=['FB','TWTR','TradeDate'])
socialTradingVolume
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>FB</th>
      <th>TWTR</th>
      <th>TradeDate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>82.34</td>
      <td>15.74</td>
      <td>2014-05-01</td>
    </tr>
    <tr>
      <th>1</th>
      <td>54.11</td>
      <td>12.71</td>
      <td>2014-05-02</td>
    </tr>
    <tr>
      <th>2</th>
      <td>45.99</td>
      <td>10.39</td>
      <td>2014-05-05</td>
    </tr>
    <tr>
      <th>3</th>
      <td>55.86</td>
      <td>134.62</td>
      <td>2014-05-06</td>
    </tr>
    <tr>
      <th>4</th>
      <td>78.50</td>
      <td>68.84</td>
      <td>2014-05-07</td>
    </tr>
  </tbody>
</table>
</div>




```python
socialTradingVolTS=socialTradingVolume.set_index('TradeDate')
socialTradingVolTS
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>FB</th>
      <th>TWTR</th>
    </tr>
    <tr>
      <th>TradeDate</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2014-05-01</th>
      <td>82.34</td>
      <td>15.74</td>
    </tr>
    <tr>
      <th>2014-05-02</th>
      <td>54.11</td>
      <td>12.71</td>
    </tr>
    <tr>
      <th>2014-05-05</th>
      <td>45.99</td>
      <td>10.39</td>
    </tr>
    <tr>
      <th>2014-05-06</th>
      <td>55.86</td>
      <td>134.62</td>
    </tr>
    <tr>
      <th>2014-05-07</th>
      <td>78.50</td>
      <td>68.84</td>
    </tr>
  </tbody>
</table>
</div>




```python
socialTradingVolTSCal=socialTradingVolTS.asfreq('D')
socialTradingVolTSCal
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>FB</th>
      <th>TWTR</th>
    </tr>
    <tr>
      <th>TradeDate</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2014-05-01</th>
      <td>82.34</td>
      <td>15.74</td>
    </tr>
    <tr>
      <th>2014-05-02</th>
      <td>54.11</td>
      <td>12.71</td>
    </tr>
    <tr>
      <th>2014-05-03</th>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2014-05-04</th>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2014-05-05</th>
      <td>45.99</td>
      <td>10.39</td>
    </tr>
    <tr>
      <th>2014-05-06</th>
      <td>55.86</td>
      <td>134.62</td>
    </tr>
    <tr>
      <th>2014-05-07</th>
      <td>78.50</td>
      <td>68.84</td>
    </tr>
  </tbody>
</table>
</div>



We can perform arithmetic operations on data containing missing values. For example, we can calculate the total trading volume (in millions of shares) across the two stocks for Facebook and Twitter as follows:


```python
socialTradingVolTSCal['FB']+socialTradingVolTSCal['TWTR']
```




    TradeDate
    2014-05-01     98.08
    2014-05-02     66.82
    2014-05-03       NaN
    2014-05-04       NaN
    2014-05-05     56.38
    2014-05-06    190.48
    2014-05-07    147.34
    Freq: D, dtype: float64



By default, any operation performed on an object that contains missing values will return a missing value at that position as shown in the following command:


```python
pd.Series([1.0,np.NaN,5.9,6])+pd.Series([3,5,2,5.6])
```




    0     4.0
    1     NaN
    2     7.9
    3    11.6
    dtype: float64




```python
pd.Series([1.0,25.0,5.5,6])/pd.Series([3,np.NaN,2,5.6])
```




    0    0.333333
    1         NaN
    2    2.750000
    3    1.071429
    dtype: float64



There is a difference, however, in the way NumPy treats aggregate calculations versus what pandas does.

In pandas, the default is to treat the missing value as 0 and do the aggregate calculation, whereas for NumPy, NaN is returned if any of the values are missing. Here is an illustration:


```python
np.mean([1.0,np.NaN,5.9,6])
```




    nan




```python
np.sum([1.0,np.NaN,5.9,6])
```




    nan



However, if this data is in a pandas Series, we will get the following output:


```python
pd.Series([1.0,np.NaN,5.9,6]).sum()
```




    12.9




```python
pd.Series([1.0,np.NaN,5.9,6]).mean()
```




    4.3



It is important to be aware of this difference in behavior between pandas and NumPy. However, if we wish to get NumPy to behave the same way as pandas, we can use the np.nanmean and np.nansum functions, which are illustrated as follows:


```python
np.nanmean([1.0,np.NaN,5.9,6])
```




    4.2999999999999998




```python
np.nansum([1.0,np.NaN,5.9,6])
```




    12.9



## Handling Missing Values
There are various ways to handle missing values, which are as follows:

__ 1. By using the ```fillna()``` function to fill in the NA values:__


```python
socialTradingVolTSCal
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>FB</th>
      <th>TWTR</th>
    </tr>
    <tr>
      <th>TradeDate</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2014-05-01</th>
      <td>82.34</td>
      <td>15.74</td>
    </tr>
    <tr>
      <th>2014-05-02</th>
      <td>54.11</td>
      <td>12.71</td>
    </tr>
    <tr>
      <th>2014-05-03</th>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2014-05-04</th>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2014-05-05</th>
      <td>45.99</td>
      <td>10.39</td>
    </tr>
    <tr>
      <th>2014-05-06</th>
      <td>55.86</td>
      <td>134.62</td>
    </tr>
    <tr>
      <th>2014-05-07</th>
      <td>78.50</td>
      <td>68.84</td>
    </tr>
  </tbody>
</table>
</div>




```python
socialTradingVolTSCal.fillna(100)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>FB</th>
      <th>TWTR</th>
    </tr>
    <tr>
      <th>TradeDate</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2014-05-01</th>
      <td>82.34</td>
      <td>15.74</td>
    </tr>
    <tr>
      <th>2014-05-02</th>
      <td>54.11</td>
      <td>12.71</td>
    </tr>
    <tr>
      <th>2014-05-03</th>
      <td>100.00</td>
      <td>100.00</td>
    </tr>
    <tr>
      <th>2014-05-04</th>
      <td>100.00</td>
      <td>100.00</td>
    </tr>
    <tr>
      <th>2014-05-05</th>
      <td>45.99</td>
      <td>10.39</td>
    </tr>
    <tr>
      <th>2014-05-06</th>
      <td>55.86</td>
      <td>134.62</td>
    </tr>
    <tr>
      <th>2014-05-07</th>
      <td>78.50</td>
      <td>68.84</td>
    </tr>
  </tbody>
</table>
</div>



We can also fill forward or backward values using the ```ffill()``` or ```bfill()``` arguments:


```python
socialTradingVolTSCal.fillna(method='ffill')
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>FB</th>
      <th>TWTR</th>
    </tr>
    <tr>
      <th>TradeDate</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2014-05-01</th>
      <td>82.34</td>
      <td>15.74</td>
    </tr>
    <tr>
      <th>2014-05-02</th>
      <td>54.11</td>
      <td>12.71</td>
    </tr>
    <tr>
      <th>2014-05-03</th>
      <td>54.11</td>
      <td>12.71</td>
    </tr>
    <tr>
      <th>2014-05-04</th>
      <td>54.11</td>
      <td>12.71</td>
    </tr>
    <tr>
      <th>2014-05-05</th>
      <td>45.99</td>
      <td>10.39</td>
    </tr>
    <tr>
      <th>2014-05-06</th>
      <td>55.86</td>
      <td>134.62</td>
    </tr>
    <tr>
      <th>2014-05-07</th>
      <td>78.50</td>
      <td>68.84</td>
    </tr>
  </tbody>
</table>
</div>




```python
socialTradingVolTSCal.fillna(method='bfill')
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>FB</th>
      <th>TWTR</th>
    </tr>
    <tr>
      <th>TradeDate</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2014-05-01</th>
      <td>82.34</td>
      <td>15.74</td>
    </tr>
    <tr>
      <th>2014-05-02</th>
      <td>54.11</td>
      <td>12.71</td>
    </tr>
    <tr>
      <th>2014-05-03</th>
      <td>45.99</td>
      <td>10.39</td>
    </tr>
    <tr>
      <th>2014-05-04</th>
      <td>45.99</td>
      <td>10.39</td>
    </tr>
    <tr>
      <th>2014-05-05</th>
      <td>45.99</td>
      <td>10.39</td>
    </tr>
    <tr>
      <th>2014-05-06</th>
      <td>55.86</td>
      <td>134.62</td>
    </tr>
    <tr>
      <th>2014-05-07</th>
      <td>78.50</td>
      <td>68.84</td>
    </tr>
  </tbody>
</table>
</div>



__2. By using the ```dropna()``` function to drop/delete rows and columns with missing values.__


```python
socialTradingVolTSCal.dropna()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>FB</th>
      <th>TWTR</th>
    </tr>
    <tr>
      <th>TradeDate</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2014-05-01</th>
      <td>82.34</td>
      <td>15.74</td>
    </tr>
    <tr>
      <th>2014-05-02</th>
      <td>54.11</td>
      <td>12.71</td>
    </tr>
    <tr>
      <th>2014-05-05</th>
      <td>45.99</td>
      <td>10.39</td>
    </tr>
    <tr>
      <th>2014-05-06</th>
      <td>55.86</td>
      <td>134.62</td>
    </tr>
    <tr>
      <th>2014-05-07</th>
      <td>78.50</td>
      <td>68.84</td>
    </tr>
  </tbody>
</table>
</div>



__3. We can also interpolate and fill in the missing values by using the ```interpolate()``` function__


```python
pd.set_option('display.precision',4)
socialTradingVolTSCal.interpolate()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>FB</th>
      <th>TWTR</th>
    </tr>
    <tr>
      <th>TradeDate</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2014-05-01</th>
      <td>82.3400</td>
      <td>15.7400</td>
    </tr>
    <tr>
      <th>2014-05-02</th>
      <td>54.1100</td>
      <td>12.7100</td>
    </tr>
    <tr>
      <th>2014-05-03</th>
      <td>51.4033</td>
      <td>11.9367</td>
    </tr>
    <tr>
      <th>2014-05-04</th>
      <td>48.6967</td>
      <td>11.1633</td>
    </tr>
    <tr>
      <th>2014-05-05</th>
      <td>45.9900</td>
      <td>10.3900</td>
    </tr>
    <tr>
      <th>2014-05-06</th>
      <td>55.8600</td>
      <td>134.6200</td>
    </tr>
    <tr>
      <th>2014-05-07</th>
      <td>78.5000</td>
      <td>68.8400</td>
    </tr>
  </tbody>
</table>
</div>



The ```interpolate()``` function also takes an argument—method that denotes the method. These methods include linear, quadratic, cubic spline, and so on.

## Plotting using matplotlib
The matplotlib api is imported using the standard convention, as shown in the following command: ```import matplotlib.pyplot as plt```

Series and DataFrame have a plot method, which is simply a wrapper around ```plt.plot``` . Here, we will examine how we can do a simple plot of a sine and cosine function. Suppose we wished to plot the following functions over the interval pi to pi:

$$
f(x) = \cos(x) + \sin(x) \\
g(x) = \cos(x) - \sin(x)
$$


```python
X = np.linspace(-np.pi, np.pi, 256, endpoint=True)
f,g = np.cos(X)+np.sin(X), np.sin(X)-np.cos(X)
f_ser=pd.Series(f)
g_ser=pd.Series(g)
```


```python
plotDF=pd.concat([f_ser,g_ser],axis=1)
plotDF.index=X
plotDF.columns=['sin(x)+cos(x)','sin(x)-cos(x)']
plotDF.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>sin(x)+cos(x)</th>
      <th>sin(x)-cos(x)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>-3.1416</th>
      <td>-1.0000</td>
      <td>1.0000</td>
    </tr>
    <tr>
      <th>-3.1170</th>
      <td>-1.0243</td>
      <td>0.9751</td>
    </tr>
    <tr>
      <th>-3.0923</th>
      <td>-1.0480</td>
      <td>0.9495</td>
    </tr>
    <tr>
      <th>-3.0677</th>
      <td>-1.0711</td>
      <td>0.9234</td>
    </tr>
    <tr>
      <th>-3.0430</th>
      <td>-1.0935</td>
      <td>0.8967</td>
    </tr>
  </tbody>
</table>
</div>




```python
plotDF.columns=['f(x)','g(x)']
plotDF.plot(title='Plot of f(x)=sin(x)+cos(x), \n g(x)=sinx(x)-cos(x)')
plt.show()
```


![png](/images/2018-04-13-Introduction_to_Pandas-4_46_0.png)



```python
plotDF.plot(subplots=True, figsize=(6,6))
plt.show()
```


![png](/images/2018-04-13-Introduction_to_Pandas-4_47_0.png)


There is a lot more to using the plotting functionality of matplotlib within pandas. For more information, take a look at the [documentation](http://pandas.pydata.org/pandas-docs/dev/visualization.html)

### Summary
To summarize, we have discussed how to handle missing data values and manipulate dates in pandas. We also took a brief detour to investigate the plotting functionality in pandas using matplotlib .
