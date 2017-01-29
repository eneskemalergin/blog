---
layout: post
title: Introduction to Pandas 3
excerpt:
categories: blog
tags: ["Python", "Data Science", "Pandas"]
published: true
comments: true
share: true
---

Hello all, I am back with another of my notes on Pandas. Today our focus will be grouping, merging and reshaping our data with Pandas. Modifiying data is very fundamental when it comes to data analysis and other core subjects requiring data cleaning.

I am going to follow the official documentation [here](http://pandas.pydata.org/pandas-docs/stable/groupby.html) 

If you like to follow this small tutorial in notebook format you can check out [here](https://github.com/eneskemalergin/Blog-Notebooks/blob/master/Introduction_to_Pandas-3.ipynb)

## Grouping of Data

The ```groupby``` operation can be thought of as part of a process that involves the following 3 steps:

- Splitting the dataset
- Analyzing the data
- Aggregating or combining the data


The ```groupby``` won't really work with Series since they are 1D object. However can be performed to obtain distinct rows of the Series.

Dataset we will use taken from [Chris Albon's Web Notes](http://chrisalbon.com/)


```python
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
%matplotlib inline
```


```python
raw_data = {'regiment': ['Nighthawks', 'Nighthawks', 'Nighthawks', 'Nighthawks', 'Dragoons', 'Dragoons', 'Dragoons', 'Dragoons', 'Scouts', 'Scouts', 'Scouts', 'Scouts'],
        'company': ['1st', '1st', '2nd', '2nd', '1st', '1st', '2nd', '2nd','1st', '1st', '2nd', '2nd'],
        'name': ['Miller', 'Jacobson', 'Ali', 'Milner', 'Cooze', 'Jacon', 'Ryaner', 'Sone', 'Sloan', 'Piger', 'Riani', 'Ali'],
        'preTestScore': [4, 24, 31, 2, 3, 4, 24, 31, 2, 3, 2, 3],
        'postTestScore': [25, 94, 57, 62, 70, 25, 94, 57, 62, 70, 62, 70]}
df = pd.DataFrame(raw_data, columns = ['regiment', 'company', 'name', 'preTestScore', 'postTestScore'])
df.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>regiment</th>
      <th>company</th>
      <th>name</th>
      <th>preTestScore</th>
      <th>postTestScore</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Nighthawks</td>
      <td>1st</td>
      <td>Miller</td>
      <td>4</td>
      <td>25</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Nighthawks</td>
      <td>1st</td>
      <td>Jacobson</td>
      <td>24</td>
      <td>94</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Nighthawks</td>
      <td>2nd</td>
      <td>Ali</td>
      <td>31</td>
      <td>57</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Nighthawks</td>
      <td>2nd</td>
      <td>Milner</td>
      <td>2</td>
      <td>62</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Dragoons</td>
      <td>1st</td>
      <td>Cooze</td>
      <td>3</td>
      <td>70</td>
    </tr>
  </tbody>
</table>
</div>



Let's apply  ```groupby``` to the DataFrame and see what is the type of the result:


```python
companyGrp = df.groupby('company')
type(companyGrp)
```




    pandas.core.groupby.DataFrameGroupBy




```python
# We can see the groups and the indexes accordingly
companyGrp.groups
```




    {'1st': [0, 1, 4, 5, 8, 9], '2nd': [2, 3, 6, 7, 10, 11]}




```python
# Returns the length of the number of groups
len(companyGrp.groups)
```




    2




```python
# Prints the full sizes of the elements of groups
companyGrp.size()
```




    company
    1st    6
    2nd    6
    dtype: int64



A multicolumn groupby specifies more than one column to be used as the key by
specifying the key columns as a list.


```python
seasonData = pd.read_csv("./data/full_soccer.csv", header=None)
seasonData.columns = ["league", 'date', 'home', 'away', 'hgoal', 'agoal', 'result', 'season']
seasonData.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>league</th>
      <th>date</th>
      <th>home</th>
      <th>away</th>
      <th>hgoal</th>
      <th>agoal</th>
      <th>result</th>
      <th>season</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>D1</td>
      <td>22/08/14</td>
      <td>Bayern Munich</td>
      <td>Wolfsburg</td>
      <td>2</td>
      <td>1</td>
      <td>H</td>
      <td>14-15</td>
    </tr>
    <tr>
      <th>1</th>
      <td>D1</td>
      <td>23/08/14</td>
      <td>Dortmund</td>
      <td>Leverkusen</td>
      <td>0</td>
      <td>2</td>
      <td>A</td>
      <td>14-15</td>
    </tr>
    <tr>
      <th>2</th>
      <td>D1</td>
      <td>23/08/14</td>
      <td>Ein Frankfurt</td>
      <td>Freiburg</td>
      <td>1</td>
      <td>0</td>
      <td>H</td>
      <td>14-15</td>
    </tr>
    <tr>
      <th>3</th>
      <td>D1</td>
      <td>23/08/14</td>
      <td>FC Koln</td>
      <td>Hamburg</td>
      <td>0</td>
      <td>0</td>
      <td>D</td>
      <td>14-15</td>
    </tr>
    <tr>
      <th>4</th>
      <td>D1</td>
      <td>23/08/14</td>
      <td>Hannover</td>
      <td>Schalke 04</td>
      <td>2</td>
      <td>1</td>
      <td>H</td>
      <td>14-15</td>
    </tr>
  </tbody>
</table>
</div>




```python
seasonData = seasonData.set_index('date')
seasonData.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>league</th>
      <th>home</th>
      <th>away</th>
      <th>hgoal</th>
      <th>agoal</th>
      <th>result</th>
      <th>season</th>
    </tr>
    <tr>
      <th>date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>22/08/14</th>
      <td>D1</td>
      <td>Bayern Munich</td>
      <td>Wolfsburg</td>
      <td>2</td>
      <td>1</td>
      <td>H</td>
      <td>14-15</td>
    </tr>
    <tr>
      <th>23/08/14</th>
      <td>D1</td>
      <td>Dortmund</td>
      <td>Leverkusen</td>
      <td>0</td>
      <td>2</td>
      <td>A</td>
      <td>14-15</td>
    </tr>
    <tr>
      <th>23/08/14</th>
      <td>D1</td>
      <td>Ein Frankfurt</td>
      <td>Freiburg</td>
      <td>1</td>
      <td>0</td>
      <td>H</td>
      <td>14-15</td>
    </tr>
    <tr>
      <th>23/08/14</th>
      <td>D1</td>
      <td>FC Koln</td>
      <td>Hamburg</td>
      <td>0</td>
      <td>0</td>
      <td>D</td>
      <td>14-15</td>
    </tr>
    <tr>
      <th>23/08/14</th>
      <td>D1</td>
      <td>Hannover</td>
      <td>Schalke 04</td>
      <td>2</td>
      <td>1</td>
      <td>H</td>
      <td>14-15</td>
    </tr>
  </tbody>
</table>
</div>




```python
seasonDataGroupbyYear = seasonData.groupby(lambda date: date.split('/')[2])
```

We can then iterate over the resulting groupby object and display the groups. In the following command, we see the two sets of statistics grouped by year. Note the use of the lambda function to obtain the year group from the first day of the month.


```python
for name, group in seasonDataGroupbyYear:
    print name
    print group
```

    11
             league                home                away  hgoal  agoal result  \
    date                                                                           
    27/08/11    SP1             Granada               Betis      0      1      A   
    27/08/11    SP1            Sp Gijon            Sociedad      1      2      A   
    27/08/11    SP1            Valencia           Santander      4      3      H   
    28/08/11    SP1          Ath Bilbao           Vallecano      1      1      D   
    28/08/11    SP1          Ath Madrid             Osasuna      0      0      D   
    28/08/11    SP1              Getafe             Levante      1      1      D   
    28/08/11    SP1            Mallorca             Espanol      1      0      H   
    28/08/11    SP1             Sevilla              Malaga      2      1      H   
    28/08/11    SP1            Zaragoza         Real Madrid      0      6      A   
    29/08/11    SP1           Barcelona          Villarreal      5      0      H   
    10/09/11    SP1         Real Madrid              Getafe      4      2      H   
    10/09/11    SP1            Sociedad           Barcelona      2      2      D   
    10/09/11    SP1            Valencia          Ath Madrid      1      0      H   
    10/09/11    SP1          Villarreal             Sevilla      2      2      D   
    11/09/11    SP1               Betis            Mallorca      1      0      H   
    11/09/11    SP1             Espanol          Ath Bilbao      2      1      H   
    11/09/11    SP1             Osasuna            Sp Gijon      2      1      H   
    11/09/11    SP1           Santander             Levante      0      0      D   
    11/09/11    SP1           Vallecano            Zaragoza      0      0      D   
    12/09/11    SP1              Malaga             Granada      4      0      H   
    17/09/11    SP1           Barcelona             Osasuna      8      0      H   
    17/09/11    SP1             Granada          Villarreal      1      0      H   
    17/09/11    SP1            Mallorca              Malaga      0      1      A   
    17/09/11    SP1             Sevilla            Sociedad      1      0      H   
    17/09/11    SP1            Sp Gijon            Valencia      0      1      A   
    18/09/11    SP1          Ath Bilbao               Betis      2      3      A   
    18/09/11    SP1          Ath Madrid           Santander      4      0      H   
    18/09/11    SP1              Getafe           Vallecano      0      1      A   
    18/09/11    SP1             Levante         Real Madrid      1      0      H   
    18/09/11    SP1            Zaragoza             Espanol      2      1      H   
    ...         ...                 ...                 ...    ...    ...    ...   
    17/12/11     E2              Exeter          Scunthorpe      0      0      D   
    17/12/11     E2          Hartlepool          Colchester      0      1      A   
    17/12/11     E2  Milton Keynes Dons             Preston      0      1      A   
    17/12/11     E2        Notts County       Leyton Orient      1      2      A   
    17/12/11     E2            Rochdale              Yeovil      0      0      D   
    17/12/11     E2      Sheffield Weds        Huddersfield      4      4      D   
    17/12/11     E2           Stevenage            Tranmere      2      1      H   
    26/12/11     E2           Brentford         Bournemouth      1      1      D   
    26/12/11     E2          Colchester           Stevenage      1      6      A   
    26/12/11     E2        Huddersfield        Chesterfield      1      0      H   
    26/12/11     E2       Leyton Orient  Milton Keynes Dons      0      3      A   
    26/12/11     E2              Oldham          Hartlepool      0      1      A   
    26/12/11     E2             Preston            Carlisle      3      3      D   
    26/12/11     E2          Scunthorpe                Bury      1      3      A   
    26/12/11     E2             Walsall      Sheffield Weds      2      1      H   
    26/12/11     E2             Wycombe              Exeter      3      1      H   
    26/12/11     E2              Yeovil            Charlton      2      3      A   
    27/12/11     E2    Sheffield United        Notts County      2      1      H   
    30/12/11     E2        Huddersfield            Carlisle      1      1      D   
    30/12/11     E2            Tranmere                Bury      2      0      H   
    31/12/11     E2           Brentford  Milton Keynes Dons      3      3      D   
    31/12/11     E2          Colchester              Exeter      2      0      H   
    31/12/11     E2       Leyton Orient            Charlton      1      0      H   
    31/12/11     E2              Oldham        Notts County      3      2      H   
    31/12/11     E2             Preston      Sheffield Weds      0      2      A   
    31/12/11     E2          Scunthorpe        Chesterfield      2      2      D   
    31/12/11     E2    Sheffield United          Hartlepool      3      1      H   
    31/12/11     E2             Walsall            Rochdale      0      0      D   
    31/12/11     E2             Wycombe           Stevenage      0      1      A   
    31/12/11     E2              Yeovil         Bournemouth      1      3      A   



If we wished to group by individual month instead, we would need to apply groupby with a level argument, as follows:


```python
# Same day games
for name, group in (seasonData.groupby(level=0)):
    print name
    print group
    print "\n"
```

    01/01/13
             league          home                away  hgoal  agoal result season
    date                                                                         
    01/01/13     E2     Brentford         Bournemouth      0      0      D  12-13
    01/01/13     E2          Bury            Tranmere      0      1      A  12-13
    01/01/13     E2      Coventry          Shrewsbury      0      1      A  12-13
    01/01/13     E2  Crawley Town          Colchester      3      0      H  12-13
    01/01/13     E2         Crewe            Carlisle      1      0      H  12-13
    01/01/13     E2     Doncaster    Sheffield United      2      2      D  12-13
    01/01/13     E2    Hartlepool             Preston      0      1      A  12-13
    01/01/13     E2  Notts County  Milton Keynes Dons      1      2      A  12-13
    01/01/13     E2    Scunthorpe              Oldham      2      2      D  12-13
    01/01/13     E2       Swindon          Portsmouth      5      0      H  12-13
    01/01/13     E2       Walsall           Stevenage      1      0      H  12-13
    01/01/13     E2        Yeovil       Leyton Orient      3      0      H  12-13


    01/01/14
             league                home              away  hgoal  agoal result  \
    date                                                                         
    01/01/14     E2               Crewe          Carlisle      2      1      H   
    01/01/14     E2  Milton Keynes Dons        Colchester      0      0      D   
    01/01/14     E2        Notts County          Bradford      3      0      H   
    01/01/14     E2              Oldham        Shrewsbury      1      2      A   
    01/01/14     E2           Peterboro         Brentford      1      3      A   
    01/01/14     E2             Preston         Port Vale      3      2      H   
    01/01/14     E2           Rotherham          Coventry      1      3      A   
    01/01/14     E2            Tranmere            Wolves      1      1      D   
    01/01/14     E2             Walsall  Sheffield United      2      1      H   

    ...

    11/02/13
             league           home        away  hgoal  agoal result season
    date                                                                  
    11/02/13    SP1          Betis  Valladolid      0      0      D  12-13
    11/02/13     T1  Gaziantepspor   Kasimpasa      2      1      H  12-13


    11/02/14
             league           home          away  hgoal  agoal result season
    date                                                                    
    11/02/14     T1      Kasimpasa      Besiktas      0      3      A  13-14
    11/02/14     E2       Carlisle      Bradford      1      0      H  13-14
    11/02/14     E2  Leyton Orient  Bristol City      1      3      A  13-14
    11/02/14     E2      Port Vale    Colchester      2      0      H  13-14


    11/02/15
             league   home    away  hgoal  agoal result season
    date                                                      
    11/02/15     I1  Parma  Chievo      0      1      A  14-15


    11/02/16
             league   home    away  hgoal  agoal result season
    date                                                      
    11/02/16     I1  Lazio  Verona      5      2      H  15-16



Note that since in the preceding commands we're grouping on an index, we need to specify the level argument as opposed to just using a column name. When we group by multiple keys, the resulting group name is a tuple, as shown in the upcoming commands. First, we reset the index to obtain the original DataFrame and define a MultiIndex in order to be able to group by multiple keys. If this is not done, it will result in a ```ValueError``` :


```python
seasonData = seasonData.reset_index()
```


```python
seasonData = seasonData.set_index(['date', 'league'])
```


```python
dateAndLeague = seasonData.groupby(level=['date', 'league'])
```


```python
for name, group in dateAndLeague:
    print(name)
    print(group)
```

    ('01/01/13', 'E2')
                             home                away  hgoal  agoal result season
    date     league                                                              
    01/01/13 E2         Brentford         Bournemouth      0      0      D  12-13
             E2              Bury            Tranmere      0      1      A  12-13
             E2          Coventry          Shrewsbury      0      1      A  12-13
             E2      Crawley Town          Colchester      3      0      H  12-13
             E2             Crewe            Carlisle      1      0      H  12-13
             E2         Doncaster    Sheffield United      2      2      D  12-13
             E2        Hartlepool             Preston      0      1      A  12-13
             E2      Notts County  Milton Keynes Dons      1      2      A  12-13
             E2        Scunthorpe              Oldham      2      2      D  12-13
             E2           Swindon          Portsmouth      5      0      H  12-13
             E2           Walsall           Stevenage      1      0      H  12-13
             E2            Yeovil       Leyton Orient      3      0      H  12-13
    ('01/01/14', 'E2')
                                   home              away  hgoal  agoal result  \
    date     league                                                              
    01/01/14 E2                   Crewe          Carlisle      2      1      H   
             E2      Milton Keynes Dons        Colchester      0      0      D   
             E2            Notts County          Bradford      3      0      H   
             E2                  Oldham        Shrewsbury      1      2      A   
             E2               Peterboro         Brentford      1      3      A   
             E2                 Preston         Port Vale      3      2      H   
             E2               Rotherham          Coventry      1      3      A   
             E2                Tranmere            Wolves      1      1      D   
             E2                 Walsall  Sheffield United      2      1      H   

                    season  
    date     league         
    01/01/14 E2      13-14  
             E2      13-14  
             E2      13-14  
             E2      13-14  
             E2      13-14  
             E2      13-14  
             E2      13-14  
             E2      13-14  
             E2      13-14  
    ('01/02/12', 'I1')
                         home     away  hgoal  agoal result season
    date     league                                               
    01/02/12 I1      Cagliari     Roma      4      2      H  11-12
             I1         Inter  Palermo      4      4      D  11-12
             I1         Lazio    Milan      2      0      H  11-12
             I1        Napoli   Cesena      0      0      D  11-12
             I1       Udinese    Lecce      2      1      H  11-12
    ('18/04/14', 'SP1')
                           home   away  hgoal  agoal result season
    date     league                                               
    18/04/14 SP1     Ath Madrid  Elche      2      0      H  13-14

    ...

    ('31/12/11', 'E2')
                                 home                away  hgoal  agoal result  \
    date     league                                                              
    31/12/11 E2             Brentford  Milton Keynes Dons      3      3      D   
             E2            Colchester              Exeter      2      0      H   
             E2         Leyton Orient            Charlton      1      0      H   
             E2                Oldham        Notts County      3      2      H   
             E2               Preston      Sheffield Weds      0      2      A   
             E2            Scunthorpe        Chesterfield      2      2      D   
             E2      Sheffield United          Hartlepool      3      1      H   
             E2               Walsall            Rochdale      0      0      D   
             E2               Wycombe           Stevenage      0      1      A   
             E2                Yeovil         Bournemouth      1      3      A   

                    season  
    date     league         
    31/12/11 E2      11-12  
             E2      11-12  
             E2      11-12  
             E2      11-12  
             E2      11-12  
             E2      11-12  
             E2      11-12  
             E2      11-12  
             E2      11-12  
             E2      11-12  
    ('31/12/15', 'SP1')
                           home      away  hgoal  agoal result season
    date     league                                                  
    31/12/15 SP1     Villarreal  Valencia      1      0      H  15-16



```python
seasonData.head(3)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>home</th>
      <th>away</th>
      <th>hgoal</th>
      <th>agoal</th>
      <th>result</th>
      <th>season</th>
    </tr>
    <tr>
      <th>date</th>
      <th>league</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>22/08/14</th>
      <th>D1</th>
      <td>Bayern Munich</td>
      <td>Wolfsburg</td>
      <td>2</td>
      <td>1</td>
      <td>H</td>
      <td>14-15</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">23/08/14</th>
      <th>D1</th>
      <td>Dortmund</td>
      <td>Leverkusen</td>
      <td>0</td>
      <td>2</td>
      <td>A</td>
      <td>14-15</td>
    </tr>
    <tr>
      <th>D1</th>
      <td>Ein Frankfurt</td>
      <td>Freiburg</td>
      <td>1</td>
      <td>0</td>
      <td>H</td>
      <td>14-15</td>
    </tr>
  </tbody>
</table>
</div>



Suppose we wish to compute the total number of goals scored by home team and away team in each date. We can achieve that by grouping the data by date column and calling sum() function on the that data.


```python
grouped2Data = seasonData.groupby(level='date')
(grouped2Data.sum()).head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>hgoal</th>
      <th>agoal</th>
    </tr>
    <tr>
      <th>date</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>01/01/13</th>
      <td>18</td>
      <td>9</td>
    </tr>
    <tr>
      <th>01/01/14</th>
      <td>14</td>
      <td>13</td>
    </tr>
    <tr>
      <th>01/02/12</th>
      <td>18</td>
      <td>9</td>
    </tr>
    <tr>
      <th>01/02/13</th>
      <td>10</td>
      <td>12</td>
    </tr>
    <tr>
      <th>01/02/14</th>
      <td>39</td>
      <td>21</td>
    </tr>
  </tbody>
</table>
</div>



We can achieve the same results without creating a new data frame and by calling the level as sum function's parameter:


```python
(seasonData.sum(level='date')).head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>hgoal</th>
      <th>agoal</th>
    </tr>
    <tr>
      <th>date</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>01/01/13</th>
      <td>18</td>
      <td>9</td>
    </tr>
    <tr>
      <th>01/01/14</th>
      <td>14</td>
      <td>13</td>
    </tr>
    <tr>
      <th>01/02/12</th>
      <td>18</td>
      <td>9</td>
    </tr>
    <tr>
      <th>01/02/13</th>
      <td>10</td>
      <td>12</td>
    </tr>
    <tr>
      <th>01/02/14</th>
      <td>39</td>
      <td>21</td>
    </tr>
  </tbody>
</table>
</div>




```python
totalgoal = grouped2Data.sum()
```


```python
# I just wanted to see the percentages of home-away goal number in given dates
totalgoal['hgoal']/totalgoal['agoal']
```




    date
    01/01/13    2.000000
    01/01/14    1.076923
    01/02/12    2.000000
    01/02/13    0.833333
    01/02/14    1.857143
    01/02/15    1.809524
    01/02/16    1.000000
    01/03/13    1.500000
    01/03/14    2.769231
    01/03/15    0.727273
    01/03/16    1.769231
    01/04/12    1.631579
    01/04/13    3.833333
    01/04/14    2.000000
    01/04/15    0.000000
    01/04/16         inf

                  ...   

    31/03/12    0.850000
    31/03/13    1.133333
    31/03/14    3.000000
    31/03/15    0.000000
    31/05/15    1.600000
    31/08/12    0.400000
    31/08/13    1.171429
    31/08/14    1.235294
    31/08/15    1.000000
    31/10/11    1.333333
    31/10/12    1.800000
    31/10/13    0.666667
    31/10/14    1.333333
    31/10/15    1.322581
    31/12/11    1.071429
    31/12/15         inf
    dtype: float64




```python
# This has inf values inside so I need to change inf to 0
num_array = (totalgoal['hgoal'] / totalgoal['agoal']).values
```


```python
# If inf and nan change to 0
num_array[num_array == np.inf] = 0
num_array = np.nan_to_num(num_array)
```


```python
# the histogram of the data
plt.hist(num_array, bins=100, facecolor='y')

plt.xlabel('Home/Away')
plt.ylabel('Occurences')
plt.title('Home-Away Goal Distribution')
plt.axis([0.0, 8.0, 0, 100])
plt.grid(True)

plt.show()
```


![graph](https://raw.githubusercontent.com/eneskemalergin/eneskemalergin.github.io/master/images/Pandas-3-graph.png)


## Merging and Joining

There are various functions that can be used to merge and join pandas' data structures, which include the following functions:

- ```concat```
- ```append```

### The ```concat``` function

The concat function is used to join multiple pandas' data structures along a specified axis and possibly perform union or intersection operations along other axes.

    concat(objs, axis=0, , join='outer', join_axes=None, ignore_index=False,
    keys=None, levels=None, names=None, verify_integrity=False)

_The synopsis of the elements of concat function are as follows:_

- The ```objs``` parameter: A list or dictionary of Series, DataFrame, or Panel objects to be concatenated.
- The ```axis``` parameter: The axis along which the concatenation should be performed. 0 is the default value.
- The ```join``` parameter: The type of join to perform when handling indexes on other axes. The 'outer' function is the default.
- The ```join_axes``` parameter: This is used to specify exact indexes for the remaining indexes instead of doing outer/inner join.
- The ```keys``` parameter: This specifies a list of keys to be used to construct a MultiIndex.

Check more parameter features in the [official documentation](http://pandas.pydata.org/pandas-docs/stable/merging.html)

We will use the Yahoo Finance's stock data of Apple, Amazon, Facebook, Google, Twitter, and Yahoo. Pandas library has a great API interface for Yahoo and Google Finance. It is really efficient and conveniet. Let's see how we can do it.


```python
import pandas_datareader.data as web # The Library to call
import datetime   # Just for getting time
```


```python
stocks = ["AAPL", "AMZN", "FB", "GOOG", "TWTR", "YHOO"] # Specify the stocks to get
start = datetime.datetime(2015, 1, 1) # Start time
end = datetime.datetime(2016, 1, 27) # End time

# We will have daily data.
# Get the stock data from yahoo and using stocks list
df = web.DataReader(stocks, 'yahoo', start, end) # Returns a Panel
df = df.to_frame() # Convert to dataframe and reset the indexes
```


```python
df.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Volume</th>
      <th>Adj Close</th>
    </tr>
    <tr>
      <th>Date</th>
      <th>minor</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">2015-01-02</th>
      <th>AAPL</th>
      <td>111.389999</td>
      <td>111.440002</td>
      <td>107.349998</td>
      <td>109.330002</td>
      <td>53204600.0</td>
      <td>105.158716</td>
    </tr>
    <tr>
      <th>AMZN</th>
      <td>312.579987</td>
      <td>314.750000</td>
      <td>306.959991</td>
      <td>308.519989</td>
      <td>2783200.0</td>
      <td>308.519989</td>
    </tr>
    <tr>
      <th>FB</th>
      <td>78.580002</td>
      <td>78.930000</td>
      <td>77.699997</td>
      <td>78.449997</td>
      <td>18177500.0</td>
      <td>78.449997</td>
    </tr>
    <tr>
      <th>GOOG</th>
      <td>529.012399</td>
      <td>531.272382</td>
      <td>524.102388</td>
      <td>524.812404</td>
      <td>1447500.0</td>
      <td>524.812404</td>
    </tr>
    <tr>
      <th>TWTR</th>
      <td>36.230000</td>
      <td>36.740002</td>
      <td>35.540001</td>
      <td>36.560001</td>
      <td>12062500.0</td>
      <td>36.560001</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Slicing the data, taking the first 4 row and Adj Close and Open
A = df.ix[:4, ['Adj Close', 'Open']]
A
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Adj Close</th>
      <th>Open</th>
    </tr>
    <tr>
      <th>Date</th>
      <th>minor</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="4" valign="top">2015-01-02</th>
      <th>AAPL</th>
      <td>105.158716</td>
      <td>111.389999</td>
    </tr>
    <tr>
      <th>AMZN</th>
      <td>308.519989</td>
      <td>312.579987</td>
    </tr>
    <tr>
      <th>FB</th>
      <td>78.449997</td>
      <td>78.580002</td>
    </tr>
    <tr>
      <th>GOOG</th>
      <td>524.812404</td>
      <td>529.012399</td>
    </tr>
  </tbody>
</table>
</div>




```python
B = df.ix[2:10, ['Volume']]
B
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th>minor</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="4" valign="top">2015-01-02</th>
      <th>FB</th>
      <td>18177500.0</td>
    </tr>
    <tr>
      <th>GOOG</th>
      <td>1447500.0</td>
    </tr>
    <tr>
      <th>TWTR</th>
      <td>12062500.0</td>
    </tr>
    <tr>
      <th>YHOO</th>
      <td>11924500.0</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">2015-01-05</th>
      <th>AAPL</th>
      <td>64285500.0</td>
    </tr>
    <tr>
      <th>AMZN</th>
      <td>2774200.0</td>
    </tr>
    <tr>
      <th>FB</th>
      <td>26452200.0</td>
    </tr>
    <tr>
      <th>GOOG</th>
      <td>2059800.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
C = df.ix[1:5, ['Low']]
C
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Low</th>
    </tr>
    <tr>
      <th>Date</th>
      <th>minor</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="4" valign="top">2015-01-02</th>
      <th>AMZN</th>
      <td>306.959991</td>
    </tr>
    <tr>
      <th>FB</th>
      <td>77.699997</td>
    </tr>
    <tr>
      <th>GOOG</th>
      <td>524.102388</td>
    </tr>
    <tr>
      <th>TWTR</th>
      <td>35.540001</td>
    </tr>
  </tbody>
</table>
</div>



Here, we perform a concatenation by specifying an outer join, which concatenates and performs a union on all the three data frames, and includes entries that do not have values for all the columns by inserting ```NaN``` for such columns


```python
pd.concat([A,B,C], axis=1) # Outer Join -> axis=1
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Adj Close</th>
      <th>Open</th>
      <th>Volume</th>
      <th>Low</th>
    </tr>
    <tr>
      <th>Date</th>
      <th>minor</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="6" valign="top">2015-01-02</th>
      <th>AAPL</th>
      <td>105.158716</td>
      <td>111.389999</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>AMZN</th>
      <td>308.519989</td>
      <td>312.579987</td>
      <td>NaN</td>
      <td>306.959991</td>
    </tr>
    <tr>
      <th>FB</th>
      <td>78.449997</td>
      <td>78.580002</td>
      <td>18177500.0</td>
      <td>77.699997</td>
    </tr>
    <tr>
      <th>GOOG</th>
      <td>524.812404</td>
      <td>529.012399</td>
      <td>1447500.0</td>
      <td>524.102388</td>
    </tr>
    <tr>
      <th>TWTR</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>12062500.0</td>
      <td>35.540001</td>
    </tr>
    <tr>
      <th>YHOO</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>11924500.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">2015-01-05</th>
      <th>AAPL</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>64285500.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>AMZN</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>2774200.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>FB</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>26452200.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>GOOG</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>2059800.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



Here is another illustration of concat , but this time, it is on random statistical distributions. Note that in the absence of an axis argument, the default axis of concatenation is 0 :


```python
np.random.seed(100)
normDF =pd.DataFrame(np.random.randn(3,4))
normDF
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-1.749765</td>
      <td>0.342680</td>
      <td>1.153036</td>
      <td>-0.252436</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.981321</td>
      <td>0.514219</td>
      <td>0.221180</td>
      <td>-1.070043</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.189496</td>
      <td>0.255001</td>
      <td>-0.458027</td>
      <td>0.435163</td>
    </tr>
  </tbody>
</table>
</div>




```python
binomDF=pd.DataFrame(np.random.binomial(100,0.5,(3,4)))
binomDF
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>57</td>
      <td>50</td>
      <td>57</td>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>48</td>
      <td>56</td>
      <td>49</td>
      <td>43</td>
    </tr>
    <tr>
      <th>2</th>
      <td>40</td>
      <td>47</td>
      <td>49</td>
      <td>55</td>
    </tr>
  </tbody>
</table>
</div>




```python
poissonDF=pd.DataFrame(np.random.poisson(100,(3,4)))
poissonDF
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>93</td>
      <td>96</td>
      <td>96</td>
      <td>89</td>
    </tr>
    <tr>
      <th>1</th>
      <td>76</td>
      <td>96</td>
      <td>104</td>
      <td>103</td>
    </tr>
    <tr>
      <th>2</th>
      <td>96</td>
      <td>93</td>
      <td>107</td>
      <td>84</td>
    </tr>
  </tbody>
</table>
</div>




```python
rand_distribs=[normDF,binomDF,poissonDF]
rand_distribsDF=pd.concat(rand_distribs,keys=['Normal', 'Binomial', 'Poisson'])
rand_distribsDF
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">Normal</th>
      <th>0</th>
      <td>-1.749765</td>
      <td>0.342680</td>
      <td>1.153036</td>
      <td>-0.252436</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.981321</td>
      <td>0.514219</td>
      <td>0.221180</td>
      <td>-1.070043</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.189496</td>
      <td>0.255001</td>
      <td>-0.458027</td>
      <td>0.435163</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">Binomial</th>
      <th>0</th>
      <td>57.000000</td>
      <td>50.000000</td>
      <td>57.000000</td>
      <td>50.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>48.000000</td>
      <td>56.000000</td>
      <td>49.000000</td>
      <td>43.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>40.000000</td>
      <td>47.000000</td>
      <td>49.000000</td>
      <td>55.000000</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">Poisson</th>
      <th>0</th>
      <td>93.000000</td>
      <td>96.000000</td>
      <td>96.000000</td>
      <td>89.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>76.000000</td>
      <td>96.000000</td>
      <td>104.000000</td>
      <td>103.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>96.000000</td>
      <td>93.000000</td>
      <td>107.000000</td>
      <td>84.000000</td>
    </tr>
  </tbody>
</table>
</div>



### Using ```append``` function
The append function is a simpler version of concat that concatenates along axis=0. Here is an illustration of its use where we slice out the first two rows and first three columns of the stockData DataFrame:


```python
stockDataDFA = stockDataDF.ix[:2,:3]
stockDataDFB = stockDataDF[2:]
```


```python
stockDataDFA.append(stockDataDFB).head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Adj Close</th>
      <th>Close</th>
      <th>Date</th>
      <th>High</th>
      <th>Low</th>
      <th>Open</th>
      <th>Volume</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>2015-01-02</td>
      <td>111.440002</td>
      <td>NaN</td>
      <td>111.389999</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>2015-01-05</td>
      <td>108.650002</td>
      <td>NaN</td>
      <td>108.290001</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>2015-01-06</td>
      <td>107.430000</td>
      <td>NaN</td>
      <td>106.540001</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>102.205846</td>
      <td>106.260002</td>
      <td>2015-01-06</td>
      <td>107.430000</td>
      <td>104.629997</td>
      <td>106.540001</td>
      <td>65797100.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>103.638996</td>
      <td>107.750000</td>
      <td>2015-01-07</td>
      <td>108.199997</td>
      <td>106.699997</td>
      <td>107.199997</td>
      <td>40105900.0</td>
    </tr>
  </tbody>
</table>
</div>



### Appending a single row to a DataFrame
We can append a single row to a DataFrame by passing a series or dictionary to the append method:


```python
algos={'search':['DFS','BFS','Binary Search','Linear'],
       'sorting': ['Quicksort','Mergesort','Heapsort','Bubble Sort'],
       'machine learning':['RandomForest','K Nearest Neighbor','LogisticRegression','K-Means Clustering']}
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
      <td>LogisticRegression</td>
      <td>Binary Search</td>
      <td>Heapsort</td>
    </tr>
    <tr>
      <th>3</th>
      <td>K-Means Clustering</td>
      <td>Linear</td>
      <td>Bubble Sort</td>
    </tr>
  </tbody>
</table>
</div>




```python
moreAlgos={'search': 'ShortestPath',
           'sorting': 'Insertion Sort',
           'machine learning': 'Linear Regression'}
algoDF.append(moreAlgos, ignore_index=True)
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
      <td>LogisticRegression</td>
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
      <td>ShortestPath</td>
      <td>Insertion Sort</td>
    </tr>
  </tbody>
</table>
</div>



In order for this to work, you must pass the ```ignore_index=True``` argument so that the index [0,1,2,3] in ```algoDF``` is ignored.

## Summary
In this tutorial, we saw that there are various ways to rearrange data in pandas. We can group data using the pandas.groupby operator and the associated methods on groupby objects. We can merge and join Series and DataFrame objects using the ```concat```, ```append```, and ```merge``` functions.


> Your input is really valuable, so do not hesitate to leave a comment. I would love to read them and respond to them.

> Until next time, be safe...
