---
layout: post
title: Graph Experiment of Research
---



```python
import matplotlib.pylab as pl
import numpy as np
import pandas as pd
from scipy.stats import linregress as ls
%matplotlib inline
```


```python
def plotAccuracy(path,lbl=''):
    train = pd.read_csv(path + 'train.log')
    test = pd.read_csv(path + 'test.log')
    pl.plot(train,'.',linewidth = 1,label=lbl+'_train' )
    pl.plot(test, linewidth = 2, label = lbl+'_test')
    pl.legend(bbox_to_anchor=(1.05, 1),loc=2)
def plotAccuracyZoom(path,lbl=''):
    train = pd.read_csv(path + 'train.log')
    test = pd.read_csv(path + 'test.log')
    pl.plot(train[:50],'.',linewidth = 1,label=lbl+'_train' )
    pl.plot(test[:50], linewidth = 2, label = lbl+'_test')
    pl.legend(bbox_to_anchor=(1.05, 1),loc=2)

def plotAccuracyZoomLast(path, lbl=''):
    train = pd.read_csv(path + 'train.log')
    test = pd.read_csv(path + 'test.log')
    pl.plot(train[500:],'.',linewidth = 1,label=lbl+'_train' )
    pl.plot(test[500:], linewidth = 2, label = lbl+'_test')
    pl.legend(bbox_to_anchor=(1.05, 1),loc=2)    
```

# Experimenting The Parameters


## 11 HeLa chromatins PSI vector  

### Small Size

#### Changing Learning Rate


```python
plotAccuracy('../results/HeLa_6chr_30000_LRtest_01/', '0.1')
plotAccuracy('../results/HeLa_6chr_30000_LRtest_001/', '0.01')
plotAccuracy('../results/HeLa_6chr_30000_LRtest_0001/', '0.001')
plotAccuracy('../results/HeLa_6chr_30000_LRtest_00001/', '0.0001')
pl.show()
plotAccuracyZoom('../results/HeLa_6chr_30000_LRtest_01/', '0.1')
plotAccuracyZoom('../results/HeLa_6chr_30000_LRtest_001/', '0.01')
plotAccuracyZoom('../results/HeLa_6chr_30000_LRtest_0001/', '0.001')
plotAccuracyZoom('../results/HeLa_6chr_30000_LRtest_00001/', '0.0001')
```


![png](http://eneskemalergin.github.io/images/Graph_Experiment_files/Graph_Experiment_6_0.png)



![png](http://eneskemalergin.github.io/images/Graph_Experiment_files/Graph_Experiment_6_1.png)


#### Changing Filter Sizes


```python
# 1
plotAccuracy('../results/HeLa_6chr_S30000NumFilTest_10/','10')
plotAccuracy('../results/HeLa_6chr_30000NumFilTest_20/','20')
plotAccuracy('../results/HeLa_6chr_30000NumFilTest_40/','40')
plotAccuracy('../results/HeLa_6chr_30000NumFilTest_80/','80')
pl.show()
plotAccuracyZoom('../results/HeLa_6chr_S30000NumFilTest_10/','10')
plotAccuracyZoom('../results/HeLa_6chr_30000NumFilTest_20/','20')
plotAccuracyZoom('../results/HeLa_6chr_30000NumFilTest_40/','40')
plotAccuracyZoom('../results/HeLa_6chr_30000NumFilTest_80/','80')
```


![png](http://eneskemalergin.github.io/images/Graph_Experiment_files/Graph_Experiment_8_0.png)



![png](http://eneskemalergin.github.io/images/Graph_Experiment_files/Graph_Experiment_8_1.png)



```python
plotAccuracy('../results/HeLa_6chr_Small30000NumFilTest_10/','10')
plotAccuracy('../results/HeLa_6chr_Small30000NumFilTest_20/','20')
plotAccuracy('../results/HeLa_6chr_Small30000NumFilTest_40/','40')
plotAccuracy('../results/HeLa_6chr_Small30000NumFilTest_80/','80')
pl.show()
plotAccuracyZoomLast('../results/HeLa_6chr_Small30000NumFilTest_10/','10')
plotAccuracyZoom('../results/HeLa_6chr_Small30000NumFilTest_20/','20')
plotAccuracyZoom('../results/HeLa_6chr_Small30000NumFilTest_40/','40')
plotAccuracyZoomLast('../results/HeLa_6chr_Small30000NumFilTest_80/','80')
```


![png](http://eneskemalergin.github.io/images/Graph_Experiment_files/Graph_Experiment_9_0.png)



![png](http://eneskemalergin.github.io/images/Graph_Experiment_files/Graph_Experiment_9_1.png)


### extra Size

#### Changing Filter Numbers


```python
# 10
plotAccuracy('../results/HeLa_6chr_Full30000NumFilTest_10/','10')

pl.show()

plotAccuracyZoom('../results/HeLa_6chr_Full30000NumFilTest_10/','10')
```


![png](http://eneskemalergin.github.io/images/Graph_Experiment_files/Graph_Experiment_12_0.png)



![png](http://eneskemalergin.github.io/images/Graph_Experiment_files/Graph_Experiment_12_1.png)



```python
# 20
plotAccuracy('../results/HeLa_6chr_Full30000NumFilTest_20/','20')
pl.show()
plotAccuracyZoom('../results/HeLa_6chr_Full30000NumFilTest_20/','20')
```


![png](http://eneskemalergin.github.io/images/Graph_Experiment_files/Graph_Experiment_13_0.png)



![png](http://eneskemalergin.github.io/images/Graph_Experiment_files/Graph_Experiment_13_1.png)



```python
plotAccuracy('../results/HeLa_6chr_Full30000NumFilTest_40/','40')
pl.show()
plotAccuracyZoom('../results/HeLa_6chr_Full30000NumFilTest_40/','40')
```


![png](http://eneskemalergin.github.io/images/Graph_Experiment_files/Graph_Experiment_14_0.png)



![png](http://eneskemalergin.github.io/images/Graph_Experiment_files/Graph_Experiment_14_1.png)



```python
plotAccuracy('../results/HeLa_6chr_Full30000NumFilTest_80/','80')
pl.show()
plotAccuracyZoom('../results/HeLa_6chr_Full30000NumFilTest_80/','80')
```


![png](http://eneskemalergin.github.io/images/Graph_Experiment_files/Graph_Experiment_15_0.png)



![png](http://eneskemalergin.github.io/images/Graph_Experiment_files/Graph_Experiment_15_1.png)



```python
plotAccuracy('../results/HeLa_6chr_Full30000NumFilTest_10/','10')
plotAccuracy('../results/HeLa_6chr_Full30000NumFilTest_20/','20')
plotAccuracy('../results/HeLa_6chr_Full30000NumFilTest_40/','40')
plotAccuracy('../results/HeLa_6chr_Full30000NumFilTest_80/','80')
pl.show()
plotAccuracyZoom('../results/HeLa_6chr_Full30000NumFilTest_10/','10')
plotAccuracyZoom('../results/HeLa_6chr_Full30000NumFilTest_20/','20')
plotAccuracyZoom('../results/HeLa_6chr_Full30000NumFilTest_40/','40')
plotAccuracyZoom('../results/HeLa_6chr_Full30000NumFilTest_80/','80')
```


![png](http://eneskemalergin.github.io/images/Graph_Experiment_files/Graph_Experiment_16_0.png)



![png](http://eneskemalergin.github.io/images/Graph_Experiment_files/Graph_Experiment_16_1.png)


#### Changing Learning Rate


```python
plotAccuracy('../results/HeLa_6chr_Full30000_LRtest_01//', '0.1')
plotAccuracy('../results/HeLa_6chr_Full30000_LRtest_001/', '0.01')
plotAccuracy('../results/HeLa_6chr_Full30000_LRtest_0001/', '0.001')
plotAccuracy('../results/HeLa_6chr_Full30000_LRtest_00001/', '0.0001')
pl.show()
plotAccuracyZoom('../results/HeLa_6chr_Full30000_LRtest_01/', '0.1')
plotAccuracyZoom('../results/HeLa_6chr_Full30000_LRtest_001/', '0.01')
plotAccuracyZoom('../results/HeLa_6chr_Full30000_LRtest_0001/', '0.001')
plotAccuracyZoom('../results/HeLa_6chr_Full30000_LRtest_00001/', '0.0001')
```


![png](http://eneskemalergin.github.io/images/Graph_Experiment_files/Graph_Experiment_18_0.png)



![png](http://eneskemalergin.github.io/images/Graph_Experiment_files/Graph_Experiment_18_1.png)



```python
plotAccuracy('../results/HeLa_6chr_Full30000_LRtest_01//', '0.1')
plotAccuracy('../results/HeLa_6chr_Full30000_LRtest_001/', '0.01')
pl.show()
plotAccuracyZoom('../results/HeLa_6chr_Full30000_LRtest_01/', '0.1')
plotAccuracyZoom('../results/HeLa_6chr_Full30000_LRtest_001/', '0.01')
```


![png](http://eneskemalergin.github.io/images/Graph_Experiment_files/Graph_Experiment_19_0.png)



![png](http://eneskemalergin.github.io/images/Graph_Experiment_files/Graph_Experiment_19_1.png)



```python
plotAccuracy('../results/HeLa_6chr_30000NumFilTest_10/', '10')
pl.show()
plotAccuracyZoom('../results/HeLa_6chr_30000NumFilTest_10/', '10')
```


![png](http://eneskemalergin.github.io/images/Graph_Experiment_files/Graph_Experiment_20_0.png)



![png](http://eneskemalergin.github.io/images/Graph_Experiment_files/Graph_Experiment_20_1.png)


## Binary Plotting


```python
plotAccuracy('../results/exonRetantionBinary_LR0.001_FS10/', '0.01-10')
plotAccuracy('../results/exonRetantionBinary_LR0.01_FS10/', '0.01-10')
plotAccuracy('../results/exonRetantionBinary_LR0.1_FS10/', '0.1-10')
pl.show()
plotAccuracyZoom('../results/exonRetantionBinary_LR0.001_FS10/', '0.01-10')
plotAccuracyZoom('../results/exonRetantionBinary_LR0.01_FS10/', '0.1-10')
plotAccuracyZoom('../results/exonRetantionBinary_LR0.1_FS10/', '0.1-10')
```


![png](http://eneskemalergin.github.io/images/Graph_Experiment_files/Graph_Experiment_22_0.png)



![png](http://eneskemalergin.github.io/images/Graph_Experiment_files/Graph_Experiment_22_1.png)



```python
plotAccuracy('../results/exonRetantionBinary_LR0.001_FS50/', '0.01-50')
plotAccuracy('../results/exonRetantionBinary_LR0.01_FS50/', '0.01-50')
plotAccuracy('../results/exonRetantionBinary_LR0.1_FS50/', '0.1-50')
pl.show()
plotAccuracyZoom('../results/exonRetantionBinary_LR0.001_FS50/', '0.01-50')
plotAccuracyZoom('../results/exonRetantionBinary_LR0.01_FS50/', '0.1-50')
plotAccuracyZoom('../results/exonRetantionBinary_LR0.1_FS50/', '0.1-50')
```


![png](http://eneskemalergin.github.io/images/Graph_Experiment_files/Graph_Experiment_23_0.png)



![png](http://eneskemalergin.github.io/images/Graph_Experiment_files/Graph_Experiment_23_1.png)
