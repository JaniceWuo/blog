---
title: 用pandas和sklearn处理数据
date: 2020-04-16 15:31:43
<!-- tags: -->
---
1.`pandas.get_dummies`<br/>
是利用pandas实现one hot编码,如果想对全部列都进行one hot，则为`data=pd.get_dummies(original_data)`,如果是指定列，则`data=pd.get_dummies(列名)`<br/>
2.`sklearn的LabelEncoder()`<br/>
以泰坦尼克号数据集举例，里面的性别原本为male,femal离散数值，要把它变为0,1不需要手动遍历进行转换，直接调用sklearn的函数即可，非常方便。<br/>
```Python
from sklearn import preprocessing
import pandas as pd
le = preprocessing.LabelEncoder()
titanic_data = pd.read_csv(路径)
titanic_data['Sex']=le.fit_transform(titanic_data['Sex'])  #在源数据集上进行改动
```
<!--more-->
3.想要统计数据集某一列的属性值各有多少个，调用`.value_counts()`,比如想查看性别为male和female的各有多少个人：
```Python
titanic_data['Sex'].value_counts()
#输出为： male 577  female 314 Name:Sex,dtype:int64
```
4.统计每个属性里面的NaN值的个数，用`.isna().sum()`
5.填充属性里面的NaN值，可以用属性的平均值填充，计算出平均值后，用fillna。
```Python
data['Age'].fillna(填充的值,inplace=True)
```
