
# Pandas教程下


```python
目录：
-分组与聚合
-表格的匹配和拼接
-bikes项目
```

## 分组与聚合

### 分组/groupby


```python
%config ZMQInteractiveShell.ast_node_interactivity='all'
%pprint
```

    Pretty printing has been turned OFF
    

公司的收入流水


```python
import pandas as pd
import numpy as np
%matplotlib inline
salaries = pd.DataFrame({'Name': ['BOSS', 'Jason', 'Jason', 'Han', 'BOSS', 'BOSS', 'Jason', 'BOSS'],'Year': [2016,2016,2016,2016,2017,2017,2017,2017],'Salary': [10000,2000,4000,5000,18000,25000,3000,4000],'Bonus': [3000,1000,1000,1200,4000,2300,500,1000]})
salaries
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Year</th>
      <th>Salary</th>
      <th>Bonus</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>BOSS</td>
      <td>2016</td>
      <td>10000</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Jason</td>
      <td>2016</td>
      <td>2000</td>
      <td>1000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Jason</td>
      <td>2016</td>
      <td>4000</td>
      <td>1000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Han</td>
      <td>2016</td>
      <td>5000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>4</th>
      <td>BOSS</td>
      <td>2017</td>
      <td>18000</td>
      <td>4000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>BOSS</td>
      <td>2017</td>
      <td>25000</td>
      <td>2300</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Jason</td>
      <td>2017</td>
      <td>3000</td>
      <td>500</td>
    </tr>
    <tr>
      <th>7</th>
      <td>BOSS</td>
      <td>2017</td>
      <td>4000</td>
      <td>1000</td>
    </tr>
  </tbody>
</table>
</div>




```python
import pandas as pd
import numpy as np
data=[{"Name":"BOSS","Year":2016,"Salary":10000,"Bonus":3000},{"Name":"Jason","Year":2016,"Salary":2000,"Bonus":1000},{"Name":"Jason","Year":2016,"Salary":4000,"Bonus":1000},{"Name":"Han","Year":2016,"Salary":5000,"Bonus":1200},{"Name":"BOSS","Year":2017,"Salary":18000,"Bonus":4000},{"Name":"BOSS","Year":2017,"Salary":25000,"Bonus":2300},{"Name":"Jason","Year":2017,"Salary":3000,"Bonus":500},{"Name":"BOSS","Year":2017,"Salary":4000,"Bonus":1000}]
salaries = pd.DataFrame(data,columns=["Name","Year","Salary","Bonus"])
salaries
                        
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Year</th>
      <th>Salary</th>
      <th>Bonus</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>BOSS</td>
      <td>2016</td>
      <td>10000</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Jason</td>
      <td>2016</td>
      <td>2000</td>
      <td>1000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Jason</td>
      <td>2016</td>
      <td>4000</td>
      <td>1000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Han</td>
      <td>2016</td>
      <td>5000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>4</th>
      <td>BOSS</td>
      <td>2017</td>
      <td>18000</td>
      <td>4000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>BOSS</td>
      <td>2017</td>
      <td>25000</td>
      <td>2300</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Jason</td>
      <td>2017</td>
      <td>3000</td>
      <td>500</td>
    </tr>
    <tr>
      <th>7</th>
      <td>BOSS</td>
      <td>2017</td>
      <td>4000</td>
      <td>1000</td>
    </tr>
  </tbody>
</table>
</div>



接下来我给大家演示一下什么叫做Group By


```python
group_by_name = salaries.groupby('Name')
group_by_name
```




    <pandas.core.groupby.groupby.DataFrameGroupBy object at 0x0000000008227F98>




```python
salaries.groupby(salaries.Name).mean()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Year</th>
      <th>Salary</th>
      <th>Bonus</th>
    </tr>
    <tr>
      <th>Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BOSS</th>
      <td>2016.750000</td>
      <td>14250.0</td>
      <td>2575.000000</td>
    </tr>
    <tr>
      <th>Han</th>
      <td>2016.000000</td>
      <td>5000.0</td>
      <td>1200.000000</td>
    </tr>
    <tr>
      <th>Jason</th>
      <td>2016.333333</td>
      <td>3000.0</td>
      <td>833.333333</td>
    </tr>
  </tbody>
</table>
</div>



上面的运行结果表示：groupby是dataframe分组的对象

### 聚合


```python
group_by_name.sum()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Year</th>
      <th>Salary</th>
      <th>Bonus</th>
    </tr>
    <tr>
      <th>Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BOSS</th>
      <td>8067</td>
      <td>57000</td>
      <td>10300</td>
    </tr>
    <tr>
      <th>Han</th>
      <td>2016</td>
      <td>5000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>Jason</th>
      <td>6049</td>
      <td>9000</td>
      <td>2500</td>
    </tr>
  </tbody>
</table>
</div>




```python
salaries.groupby("Name",sort=False).sum() #从大到小：逆序
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Year</th>
      <th>Salary</th>
      <th>Bonus</th>
    </tr>
    <tr>
      <th>Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BOSS</th>
      <td>8067</td>
      <td>57000</td>
      <td>10300</td>
    </tr>
    <tr>
      <th>Jason</th>
      <td>6049</td>
      <td>9000</td>
      <td>2500</td>
    </tr>
    <tr>
      <th>Han</th>
      <td>2016</td>
      <td>5000</td>
      <td>1200</td>
    </tr>
  </tbody>
</table>
</div>




```python
group_by_name.aggregate(sum)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Year</th>
      <th>Salary</th>
      <th>Bonus</th>
    </tr>
    <tr>
      <th>Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BOSS</th>
      <td>8067</td>
      <td>57000</td>
      <td>10300</td>
    </tr>
    <tr>
      <th>Han</th>
      <td>2016</td>
      <td>5000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>Jason</th>
      <td>6049</td>
      <td>9000</td>
      <td>2500</td>
    </tr>
  </tbody>
</table>
</div>



group by的attributes


```python
print(group_by_name.groups)
print(len(group_by_name))
```

    {'BOSS': Int64Index([0, 4, 5, 7], dtype='int64'), 'Han': Int64Index([3], dtype='int64'), 'Jason': Int64Index([1, 2, 6], dtype='int64')}
    3
    


```python
group_by_name_year=salaries.groupby(["Name","Year"])
group_by_name_year.aggregate(sum)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Salary</th>
      <th>Bonus</th>
    </tr>
    <tr>
      <th>Name</th>
      <th>Year</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">BOSS</th>
      <th>2016</th>
      <td>10000</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>2017</th>
      <td>47000</td>
      <td>7300</td>
    </tr>
    <tr>
      <th>Han</th>
      <th>2016</th>
      <td>5000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Jason</th>
      <th>2016</th>
      <td>6000</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>2017</th>
      <td>3000</td>
      <td>500</td>
    </tr>
  </tbody>
</table>
</div>




```python
group_by_name_year=salaries.groupby(["Name","Year"])
group_by_name_year.sum()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Salary</th>
      <th>Bonus</th>
    </tr>
    <tr>
      <th>Name</th>
      <th>Year</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">BOSS</th>
      <th>2016</th>
      <td>10000</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>2017</th>
      <td>47000</td>
      <td>7300</td>
    </tr>
    <tr>
      <th>Han</th>
      <th>2016</th>
      <td>5000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Jason</th>
      <th>2016</th>
      <td>6000</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>2017</th>
      <td>3000</td>
      <td>500</td>
    </tr>
  </tbody>
</table>
</div>




```python
group_by_name.mean()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Year</th>
      <th>Salary</th>
      <th>Bonus</th>
    </tr>
    <tr>
      <th>Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BOSS</th>
      <td>2016.750000</td>
      <td>14250.0</td>
      <td>2575.000000</td>
    </tr>
    <tr>
      <th>Han</th>
      <td>2016.000000</td>
      <td>5000.0</td>
      <td>1200.000000</td>
    </tr>
    <tr>
      <th>Jason</th>
      <td>2016.333333</td>
      <td>3000.0</td>
      <td>833.333333</td>
    </tr>
  </tbody>
</table>
</div>




```python
group_by_name.size()
```




    Name
    BOSS     4
    Han      1
    Jason    3
    dtype: int64




```python
group_by_name.median()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Year</th>
      <th>Salary</th>
      <th>Bonus</th>
    </tr>
    <tr>
      <th>Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BOSS</th>
      <td>2017</td>
      <td>14000</td>
      <td>2650</td>
    </tr>
    <tr>
      <th>Han</th>
      <td>2016</td>
      <td>5000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th>Jason</th>
      <td>2016</td>
      <td>3000</td>
      <td>1000</td>
    </tr>
  </tbody>
</table>
</div>




```python
group_by_name.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="8" halign="left">Bonus</th>
      <th colspan="5" halign="left">Salary</th>
      <th colspan="8" halign="left">Year</th>
    </tr>
    <tr>
      <th></th>
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>max</th>
      <th>count</th>
      <th>mean</th>
      <th>...</th>
      <th>75%</th>
      <th>max</th>
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>max</th>
    </tr>
    <tr>
      <th>Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
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
      <th>BOSS</th>
      <td>4.0</td>
      <td>2575.000000</td>
      <td>1260.621540</td>
      <td>1000.0</td>
      <td>1975.0</td>
      <td>2650.0</td>
      <td>3250.0</td>
      <td>4000.0</td>
      <td>4.0</td>
      <td>14250.0</td>
      <td>...</td>
      <td>19750.0</td>
      <td>25000.0</td>
      <td>4.0</td>
      <td>2016.750000</td>
      <td>0.50000</td>
      <td>2016.0</td>
      <td>2016.75</td>
      <td>2017.0</td>
      <td>2017.0</td>
      <td>2017.0</td>
    </tr>
    <tr>
      <th>Han</th>
      <td>1.0</td>
      <td>1200.000000</td>
      <td>NaN</td>
      <td>1200.0</td>
      <td>1200.0</td>
      <td>1200.0</td>
      <td>1200.0</td>
      <td>1200.0</td>
      <td>1.0</td>
      <td>5000.0</td>
      <td>...</td>
      <td>5000.0</td>
      <td>5000.0</td>
      <td>1.0</td>
      <td>2016.000000</td>
      <td>NaN</td>
      <td>2016.0</td>
      <td>2016.00</td>
      <td>2016.0</td>
      <td>2016.0</td>
      <td>2016.0</td>
    </tr>
    <tr>
      <th>Jason</th>
      <td>3.0</td>
      <td>833.333333</td>
      <td>288.675135</td>
      <td>500.0</td>
      <td>750.0</td>
      <td>1000.0</td>
      <td>1000.0</td>
      <td>1000.0</td>
      <td>3.0</td>
      <td>3000.0</td>
      <td>...</td>
      <td>3500.0</td>
      <td>4000.0</td>
      <td>3.0</td>
      <td>2016.333333</td>
      <td>0.57735</td>
      <td>2016.0</td>
      <td>2016.00</td>
      <td>2016.0</td>
      <td>2016.5</td>
      <td>2017.0</td>
    </tr>
  </tbody>
</table>
<p>3 rows × 24 columns</p>
</div>



## 遍历分组


```python
for name,group in group_by_name:
    print(name)
    print("-------------")
    print(group)
    print("\n")
```

    BOSS
    -------------
       Name  Year  Salary  Bonus
    0  BOSS  2016   10000   3000
    4  BOSS  2017   18000   4000
    5  BOSS  2017   25000   2300
    7  BOSS  2017    4000   1000
    
    
    Han
    -------------
      Name  Year  Salary  Bonus
    3  Han  2016    5000   1200
    
    
    Jason
    -------------
        Name  Year  Salary  Bonus
    1  Jason  2016    2000   1000
    2  Jason  2016    4000   1000
    6  Jason  2017    3000    500
    
    
    


```python
group_by_name.get_group("Jason")
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Year</th>
      <th>Salary</th>
      <th>Bonus</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Jason</td>
      <td>2016</td>
      <td>2000</td>
      <td>1000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Jason</td>
      <td>2016</td>
      <td>4000</td>
      <td>1000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Jason</td>
      <td>2017</td>
      <td>3000</td>
      <td>500</td>
    </tr>
  </tbody>
</table>
</div>




```python
group_by_name.agg([np.sum,np.mean,np.std])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="3" halign="left">Year</th>
      <th colspan="3" halign="left">Salary</th>
      <th colspan="3" halign="left">Bonus</th>
    </tr>
    <tr>
      <th></th>
      <th>sum</th>
      <th>mean</th>
      <th>std</th>
      <th>sum</th>
      <th>mean</th>
      <th>std</th>
      <th>sum</th>
      <th>mean</th>
      <th>std</th>
    </tr>
    <tr>
      <th>Name</th>
      <th></th>
      <th></th>
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
      <th>BOSS</th>
      <td>8067</td>
      <td>2016.750000</td>
      <td>0.50000</td>
      <td>57000</td>
      <td>14250</td>
      <td>9178.779875</td>
      <td>10300</td>
      <td>2575.000000</td>
      <td>1260.621540</td>
    </tr>
    <tr>
      <th>Han</th>
      <td>2016</td>
      <td>2016.000000</td>
      <td>NaN</td>
      <td>5000</td>
      <td>5000</td>
      <td>NaN</td>
      <td>1200</td>
      <td>1200.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Jason</th>
      <td>6049</td>
      <td>2016.333333</td>
      <td>0.57735</td>
      <td>9000</td>
      <td>3000</td>
      <td>1000.000000</td>
      <td>2500</td>
      <td>833.333333</td>
      <td>288.675135</td>
    </tr>
  </tbody>
</table>
</div>




```python
salaries.groupby(["Name","Year"]).sum()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Salary</th>
      <th>Bonus</th>
    </tr>
    <tr>
      <th>Name</th>
      <th>Year</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">BOSS</th>
      <th>2016</th>
      <td>10000</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>2017</th>
      <td>47000</td>
      <td>7300</td>
    </tr>
    <tr>
      <th>Han</th>
      <th>2016</th>
      <td>5000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Jason</th>
      <th>2016</th>
      <td>6000</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>2017</th>
      <td>3000</td>
      <td>500</td>
    </tr>
  </tbody>
</table>
</div>




```python
salaries.groupby(["Name","Year"]).agg(["sum"])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th></th>
      <th>Salary</th>
      <th>Bonus</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>sum</th>
      <th>sum</th>
    </tr>
    <tr>
      <th>Name</th>
      <th>Year</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">BOSS</th>
      <th>2016</th>
      <td>10000</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>2017</th>
      <td>47000</td>
      <td>7300</td>
    </tr>
    <tr>
      <th>Han</th>
      <th>2016</th>
      <td>5000</td>
      <td>1200</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Jason</th>
      <th>2016</th>
      <td>6000</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>2017</th>
      <td>3000</td>
      <td>500</td>
    </tr>
  </tbody>
</table>
</div>




```python
salaries.groupby(["Name","Year"]).agg({"Bonus":np.sum,"Salary":np.sum})
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Bonus</th>
      <th>Salary</th>
    </tr>
    <tr>
      <th>Name</th>
      <th>Year</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">BOSS</th>
      <th>2016</th>
      <td>3000</td>
      <td>10000</td>
    </tr>
    <tr>
      <th>2017</th>
      <td>7300</td>
      <td>47000</td>
    </tr>
    <tr>
      <th>Han</th>
      <th>2016</th>
      <td>1200</td>
      <td>5000</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Jason</th>
      <th>2016</th>
      <td>2000</td>
      <td>6000</td>
    </tr>
    <tr>
      <th>2017</th>
      <td>500</td>
      <td>3000</td>
    </tr>
  </tbody>
</table>
</div>



对每一列采取不同的aggregate操作


```python
salaries.groupby(["Name","Year"]).agg({"Bonus":np.sum,"Salary":np.mean})
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Bonus</th>
      <th>Salary</th>
    </tr>
    <tr>
      <th>Name</th>
      <th>Year</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">BOSS</th>
      <th>2016</th>
      <td>3000</td>
      <td>10000.000000</td>
    </tr>
    <tr>
      <th>2017</th>
      <td>7300</td>
      <td>15666.666667</td>
    </tr>
    <tr>
      <th>Han</th>
      <th>2016</th>
      <td>1200</td>
      <td>5000.000000</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Jason</th>
      <th>2016</th>
      <td>2000</td>
      <td>3000.000000</td>
    </tr>
    <tr>
      <th>2017</th>
      <td>500</td>
      <td>3000.000000</td>
    </tr>
  </tbody>
</table>
</div>



## transform & apply 数据变换


```python
import pandas as pd
nvda = pd.read_csv("../Anaconda3/NVDA.csv")
nvda
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1999-01-22</td>
      <td>1.750000</td>
      <td>1.953125</td>
      <td>1.552083</td>
      <td>1.640625</td>
      <td>1.523430</td>
      <td>67867200</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1999-01-25</td>
      <td>1.770833</td>
      <td>1.833333</td>
      <td>1.640625</td>
      <td>1.812500</td>
      <td>1.683028</td>
      <td>12762000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1999-01-26</td>
      <td>1.833333</td>
      <td>1.869792</td>
      <td>1.645833</td>
      <td>1.671875</td>
      <td>1.552448</td>
      <td>8580000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1999-01-27</td>
      <td>1.677083</td>
      <td>1.718750</td>
      <td>1.583333</td>
      <td>1.666667</td>
      <td>1.547611</td>
      <td>6109200</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1999-01-28</td>
      <td>1.666667</td>
      <td>1.677083</td>
      <td>1.651042</td>
      <td>1.661458</td>
      <td>1.542776</td>
      <td>5688000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1999-01-29</td>
      <td>1.661458</td>
      <td>1.666667</td>
      <td>1.583333</td>
      <td>1.583333</td>
      <td>1.470231</td>
      <td>6100800</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1999-02-01</td>
      <td>1.583333</td>
      <td>1.625000</td>
      <td>1.583333</td>
      <td>1.614583</td>
      <td>1.499249</td>
      <td>3867600</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1999-02-02</td>
      <td>1.583333</td>
      <td>1.625000</td>
      <td>1.442708</td>
      <td>1.489583</td>
      <td>1.383178</td>
      <td>6602400</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1999-02-03</td>
      <td>1.468750</td>
      <td>1.541667</td>
      <td>1.458333</td>
      <td>1.520833</td>
      <td>1.412196</td>
      <td>1878000</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1999-02-04</td>
      <td>1.541667</td>
      <td>1.645833</td>
      <td>1.520833</td>
      <td>1.604167</td>
      <td>1.489577</td>
      <td>4548000</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1999-02-05</td>
      <td>1.630208</td>
      <td>1.666667</td>
      <td>1.588542</td>
      <td>1.651042</td>
      <td>1.533103</td>
      <td>3421200</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1999-02-08</td>
      <td>1.661458</td>
      <td>1.666667</td>
      <td>1.593750</td>
      <td>1.593750</td>
      <td>1.479904</td>
      <td>3852000</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1999-02-09</td>
      <td>1.625000</td>
      <td>1.635417</td>
      <td>1.510417</td>
      <td>1.531250</td>
      <td>1.421868</td>
      <td>2174400</td>
    </tr>
    <tr>
      <th>13</th>
      <td>1999-02-10</td>
      <td>1.531250</td>
      <td>1.572917</td>
      <td>1.489583</td>
      <td>1.515625</td>
      <td>1.407360</td>
      <td>3705600</td>
    </tr>
    <tr>
      <th>14</th>
      <td>1999-02-11</td>
      <td>1.520833</td>
      <td>1.708333</td>
      <td>1.520833</td>
      <td>1.645833</td>
      <td>1.528267</td>
      <td>3306000</td>
    </tr>
    <tr>
      <th>15</th>
      <td>1999-02-12</td>
      <td>1.666667</td>
      <td>1.750000</td>
      <td>1.666667</td>
      <td>1.739583</td>
      <td>1.615320</td>
      <td>2743200</td>
    </tr>
    <tr>
      <th>16</th>
      <td>1999-02-16</td>
      <td>1.770833</td>
      <td>1.843750</td>
      <td>1.572917</td>
      <td>1.750000</td>
      <td>1.624992</td>
      <td>5275200</td>
    </tr>
    <tr>
      <th>17</th>
      <td>1999-02-17</td>
      <td>1.708333</td>
      <td>1.729167</td>
      <td>1.625000</td>
      <td>1.656250</td>
      <td>1.537939</td>
      <td>1693200</td>
    </tr>
    <tr>
      <th>18</th>
      <td>1999-02-18</td>
      <td>1.708333</td>
      <td>1.729167</td>
      <td>1.635417</td>
      <td>1.682292</td>
      <td>1.562121</td>
      <td>1767600</td>
    </tr>
    <tr>
      <th>19</th>
      <td>1999-02-19</td>
      <td>1.666667</td>
      <td>1.770833</td>
      <td>1.645833</td>
      <td>1.739583</td>
      <td>1.615320</td>
      <td>1884000</td>
    </tr>
    <tr>
      <th>20</th>
      <td>1999-02-22</td>
      <td>1.770833</td>
      <td>1.791667</td>
      <td>1.656250</td>
      <td>1.750000</td>
      <td>1.624992</td>
      <td>5131200</td>
    </tr>
    <tr>
      <th>21</th>
      <td>1999-02-23</td>
      <td>1.791667</td>
      <td>1.869792</td>
      <td>1.687500</td>
      <td>1.833333</td>
      <td>1.702373</td>
      <td>3452400</td>
    </tr>
    <tr>
      <th>22</th>
      <td>1999-02-24</td>
      <td>2.104167</td>
      <td>2.187500</td>
      <td>1.932292</td>
      <td>1.979167</td>
      <td>1.837789</td>
      <td>15319200</td>
    </tr>
    <tr>
      <th>23</th>
      <td>1999-02-25</td>
      <td>2.062500</td>
      <td>2.125000</td>
      <td>1.885417</td>
      <td>1.916667</td>
      <td>1.779754</td>
      <td>3728400</td>
    </tr>
    <tr>
      <th>24</th>
      <td>1999-02-26</td>
      <td>1.937500</td>
      <td>2.000000</td>
      <td>1.812500</td>
      <td>1.828125</td>
      <td>1.697537</td>
      <td>4315200</td>
    </tr>
    <tr>
      <th>25</th>
      <td>1999-03-01</td>
      <td>1.875000</td>
      <td>1.916667</td>
      <td>1.750000</td>
      <td>1.838542</td>
      <td>1.707209</td>
      <td>2304000</td>
    </tr>
    <tr>
      <th>26</th>
      <td>1999-03-02</td>
      <td>1.833333</td>
      <td>1.843750</td>
      <td>1.791667</td>
      <td>1.822917</td>
      <td>1.692701</td>
      <td>1381200</td>
    </tr>
    <tr>
      <th>27</th>
      <td>1999-03-03</td>
      <td>1.833333</td>
      <td>1.833333</td>
      <td>1.687500</td>
      <td>1.697917</td>
      <td>1.576630</td>
      <td>1534800</td>
    </tr>
    <tr>
      <th>28</th>
      <td>1999-03-04</td>
      <td>1.781250</td>
      <td>1.791667</td>
      <td>1.645833</td>
      <td>1.661458</td>
      <td>1.542776</td>
      <td>1434000</td>
    </tr>
    <tr>
      <th>29</th>
      <td>1999-03-05</td>
      <td>1.677083</td>
      <td>1.760417</td>
      <td>1.677083</td>
      <td>1.755208</td>
      <td>1.629829</td>
      <td>1969200</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>4624</th>
      <td>2017-06-08</td>
      <td>153.460007</td>
      <td>160.000000</td>
      <td>151.789993</td>
      <td>159.940002</td>
      <td>159.940002</td>
      <td>29043600</td>
    </tr>
    <tr>
      <th>4625</th>
      <td>2017-06-09</td>
      <td>164.740005</td>
      <td>168.500000</td>
      <td>142.750000</td>
      <td>149.600006</td>
      <td>149.600006</td>
      <td>92323200</td>
    </tr>
    <tr>
      <th>4626</th>
      <td>2017-06-12</td>
      <td>145.880005</td>
      <td>151.699997</td>
      <td>142.110001</td>
      <td>149.970001</td>
      <td>149.970001</td>
      <td>42438300</td>
    </tr>
    <tr>
      <th>4627</th>
      <td>2017-06-13</td>
      <td>154.399994</td>
      <td>154.770004</td>
      <td>145.649994</td>
      <td>151.399994</td>
      <td>151.399994</td>
      <td>41812600</td>
    </tr>
    <tr>
      <th>4628</th>
      <td>2017-06-14</td>
      <td>151.520004</td>
      <td>154.059998</td>
      <td>148.500000</td>
      <td>151.720001</td>
      <td>151.720001</td>
      <td>29616000</td>
    </tr>
    <tr>
      <th>4629</th>
      <td>2017-06-15</td>
      <td>146.960007</td>
      <td>153.600006</td>
      <td>146.500000</td>
      <td>152.369995</td>
      <td>152.369995</td>
      <td>24095600</td>
    </tr>
    <tr>
      <th>4630</th>
      <td>2017-06-16</td>
      <td>152.759995</td>
      <td>154.699997</td>
      <td>150.240005</td>
      <td>151.619995</td>
      <td>151.619995</td>
      <td>23124000</td>
    </tr>
    <tr>
      <th>4631</th>
      <td>2017-06-19</td>
      <td>153.410004</td>
      <td>157.529999</td>
      <td>153.259995</td>
      <td>157.320007</td>
      <td>157.320007</td>
      <td>19454400</td>
    </tr>
    <tr>
      <th>4632</th>
      <td>2017-06-20</td>
      <td>159.029999</td>
      <td>161.740005</td>
      <td>156.919998</td>
      <td>157.089996</td>
      <td>157.089996</td>
      <td>27386100</td>
    </tr>
    <tr>
      <th>4633</th>
      <td>2017-06-21</td>
      <td>158.210007</td>
      <td>159.619995</td>
      <td>155.699997</td>
      <td>159.470001</td>
      <td>159.470001</td>
      <td>17066300</td>
    </tr>
    <tr>
      <th>4634</th>
      <td>2017-06-22</td>
      <td>159.800003</td>
      <td>160.339996</td>
      <td>157.399994</td>
      <td>158.369995</td>
      <td>158.369995</td>
      <td>11728300</td>
    </tr>
    <tr>
      <th>4635</th>
      <td>2017-06-23</td>
      <td>158.679993</td>
      <td>159.320007</td>
      <td>153.220001</td>
      <td>153.830002</td>
      <td>153.830002</td>
      <td>27214700</td>
    </tr>
    <tr>
      <th>4636</th>
      <td>2017-06-26</td>
      <td>155.160004</td>
      <td>156.600006</td>
      <td>148.330002</td>
      <td>152.149994</td>
      <td>152.149994</td>
      <td>26599000</td>
    </tr>
    <tr>
      <th>4637</th>
      <td>2017-06-27</td>
      <td>151.440002</td>
      <td>151.789993</td>
      <td>146.350006</td>
      <td>146.580002</td>
      <td>146.580002</td>
      <td>24987300</td>
    </tr>
    <tr>
      <th>4638</th>
      <td>2017-06-28</td>
      <td>149.320007</td>
      <td>151.940002</td>
      <td>145.750000</td>
      <td>151.750000</td>
      <td>151.750000</td>
      <td>24873700</td>
    </tr>
    <tr>
      <th>4639</th>
      <td>2017-06-29</td>
      <td>150.600006</td>
      <td>150.720001</td>
      <td>144.080002</td>
      <td>146.679993</td>
      <td>146.679993</td>
      <td>26610600</td>
    </tr>
    <tr>
      <th>4640</th>
      <td>2017-06-30</td>
      <td>147.380005</td>
      <td>147.929993</td>
      <td>143.500000</td>
      <td>144.559998</td>
      <td>144.559998</td>
      <td>18203400</td>
    </tr>
    <tr>
      <th>4641</th>
      <td>2017-07-03</td>
      <td>145.050003</td>
      <td>145.649994</td>
      <td>138.580002</td>
      <td>139.330002</td>
      <td>139.330002</td>
      <td>17726800</td>
    </tr>
    <tr>
      <th>4642</th>
      <td>2017-07-05</td>
      <td>141.899994</td>
      <td>144.220001</td>
      <td>141.130005</td>
      <td>143.050003</td>
      <td>143.050003</td>
      <td>20504700</td>
    </tr>
    <tr>
      <th>4643</th>
      <td>2017-07-06</td>
      <td>141.869995</td>
      <td>145.380005</td>
      <td>139.759995</td>
      <td>143.479996</td>
      <td>143.479996</td>
      <td>18657100</td>
    </tr>
    <tr>
      <th>4644</th>
      <td>2017-07-07</td>
      <td>145.779999</td>
      <td>147.500000</td>
      <td>144.850006</td>
      <td>146.759995</td>
      <td>146.759995</td>
      <td>16374300</td>
    </tr>
    <tr>
      <th>4645</th>
      <td>2017-07-10</td>
      <td>149.740005</td>
      <td>154.000000</td>
      <td>148.679993</td>
      <td>153.699997</td>
      <td>153.699997</td>
      <td>23962300</td>
    </tr>
    <tr>
      <th>4646</th>
      <td>2017-07-11</td>
      <td>153.850006</td>
      <td>156.190002</td>
      <td>152.149994</td>
      <td>155.880005</td>
      <td>155.880005</td>
      <td>18948900</td>
    </tr>
    <tr>
      <th>4647</th>
      <td>2017-07-12</td>
      <td>158.300003</td>
      <td>163.000000</td>
      <td>156.559998</td>
      <td>162.509995</td>
      <td>162.509995</td>
      <td>28630200</td>
    </tr>
    <tr>
      <th>4648</th>
      <td>2017-07-13</td>
      <td>163.000000</td>
      <td>166.300003</td>
      <td>158.750000</td>
      <td>160.630005</td>
      <td>160.630005</td>
      <td>34228300</td>
    </tr>
    <tr>
      <th>4649</th>
      <td>2017-07-14</td>
      <td>161.289993</td>
      <td>165.009995</td>
      <td>161.009995</td>
      <td>164.949997</td>
      <td>164.949997</td>
      <td>23548700</td>
    </tr>
    <tr>
      <th>4650</th>
      <td>2017-07-17</td>
      <td>166.330002</td>
      <td>167.500000</td>
      <td>161.750000</td>
      <td>164.250000</td>
      <td>164.250000</td>
      <td>23269800</td>
    </tr>
    <tr>
      <th>4651</th>
      <td>2017-07-18</td>
      <td>161.779999</td>
      <td>166.550003</td>
      <td>161.300003</td>
      <td>165.960007</td>
      <td>165.960007</td>
      <td>19416000</td>
    </tr>
    <tr>
      <th>4652</th>
      <td>2017-07-19</td>
      <td>166.330002</td>
      <td>167.399994</td>
      <td>164.610001</td>
      <td>165.100006</td>
      <td>165.100006</td>
      <td>17176100</td>
    </tr>
    <tr>
      <th>4653</th>
      <td>2017-07-20</td>
      <td>165.929993</td>
      <td>167.509995</td>
      <td>163.910004</td>
      <td>167.500000</td>
      <td>167.500000</td>
      <td>17363300</td>
    </tr>
  </tbody>
</table>
<p>4654 rows × 7 columns</p>
</div>




```python
import pandas as pd
nvda=pd.read_csv("../Anaconda3/nvda.csv",index_col=0,parse_dates=[0])
nvda
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
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
      <th>1999-01-22</th>
      <td>1.750000</td>
      <td>1.953125</td>
      <td>1.552083</td>
      <td>1.640625</td>
      <td>1.523430</td>
      <td>67867200</td>
    </tr>
    <tr>
      <th>1999-01-25</th>
      <td>1.770833</td>
      <td>1.833333</td>
      <td>1.640625</td>
      <td>1.812500</td>
      <td>1.683028</td>
      <td>12762000</td>
    </tr>
    <tr>
      <th>1999-01-26</th>
      <td>1.833333</td>
      <td>1.869792</td>
      <td>1.645833</td>
      <td>1.671875</td>
      <td>1.552448</td>
      <td>8580000</td>
    </tr>
    <tr>
      <th>1999-01-27</th>
      <td>1.677083</td>
      <td>1.718750</td>
      <td>1.583333</td>
      <td>1.666667</td>
      <td>1.547611</td>
      <td>6109200</td>
    </tr>
    <tr>
      <th>1999-01-28</th>
      <td>1.666667</td>
      <td>1.677083</td>
      <td>1.651042</td>
      <td>1.661458</td>
      <td>1.542776</td>
      <td>5688000</td>
    </tr>
    <tr>
      <th>1999-01-29</th>
      <td>1.661458</td>
      <td>1.666667</td>
      <td>1.583333</td>
      <td>1.583333</td>
      <td>1.470231</td>
      <td>6100800</td>
    </tr>
    <tr>
      <th>1999-02-01</th>
      <td>1.583333</td>
      <td>1.625000</td>
      <td>1.583333</td>
      <td>1.614583</td>
      <td>1.499249</td>
      <td>3867600</td>
    </tr>
    <tr>
      <th>1999-02-02</th>
      <td>1.583333</td>
      <td>1.625000</td>
      <td>1.442708</td>
      <td>1.489583</td>
      <td>1.383178</td>
      <td>6602400</td>
    </tr>
    <tr>
      <th>1999-02-03</th>
      <td>1.468750</td>
      <td>1.541667</td>
      <td>1.458333</td>
      <td>1.520833</td>
      <td>1.412196</td>
      <td>1878000</td>
    </tr>
    <tr>
      <th>1999-02-04</th>
      <td>1.541667</td>
      <td>1.645833</td>
      <td>1.520833</td>
      <td>1.604167</td>
      <td>1.489577</td>
      <td>4548000</td>
    </tr>
    <tr>
      <th>1999-02-05</th>
      <td>1.630208</td>
      <td>1.666667</td>
      <td>1.588542</td>
      <td>1.651042</td>
      <td>1.533103</td>
      <td>3421200</td>
    </tr>
    <tr>
      <th>1999-02-08</th>
      <td>1.661458</td>
      <td>1.666667</td>
      <td>1.593750</td>
      <td>1.593750</td>
      <td>1.479904</td>
      <td>3852000</td>
    </tr>
    <tr>
      <th>1999-02-09</th>
      <td>1.625000</td>
      <td>1.635417</td>
      <td>1.510417</td>
      <td>1.531250</td>
      <td>1.421868</td>
      <td>2174400</td>
    </tr>
    <tr>
      <th>1999-02-10</th>
      <td>1.531250</td>
      <td>1.572917</td>
      <td>1.489583</td>
      <td>1.515625</td>
      <td>1.407360</td>
      <td>3705600</td>
    </tr>
    <tr>
      <th>1999-02-11</th>
      <td>1.520833</td>
      <td>1.708333</td>
      <td>1.520833</td>
      <td>1.645833</td>
      <td>1.528267</td>
      <td>3306000</td>
    </tr>
    <tr>
      <th>1999-02-12</th>
      <td>1.666667</td>
      <td>1.750000</td>
      <td>1.666667</td>
      <td>1.739583</td>
      <td>1.615320</td>
      <td>2743200</td>
    </tr>
    <tr>
      <th>1999-02-16</th>
      <td>1.770833</td>
      <td>1.843750</td>
      <td>1.572917</td>
      <td>1.750000</td>
      <td>1.624992</td>
      <td>5275200</td>
    </tr>
    <tr>
      <th>1999-02-17</th>
      <td>1.708333</td>
      <td>1.729167</td>
      <td>1.625000</td>
      <td>1.656250</td>
      <td>1.537939</td>
      <td>1693200</td>
    </tr>
    <tr>
      <th>1999-02-18</th>
      <td>1.708333</td>
      <td>1.729167</td>
      <td>1.635417</td>
      <td>1.682292</td>
      <td>1.562121</td>
      <td>1767600</td>
    </tr>
    <tr>
      <th>1999-02-19</th>
      <td>1.666667</td>
      <td>1.770833</td>
      <td>1.645833</td>
      <td>1.739583</td>
      <td>1.615320</td>
      <td>1884000</td>
    </tr>
    <tr>
      <th>1999-02-22</th>
      <td>1.770833</td>
      <td>1.791667</td>
      <td>1.656250</td>
      <td>1.750000</td>
      <td>1.624992</td>
      <td>5131200</td>
    </tr>
    <tr>
      <th>1999-02-23</th>
      <td>1.791667</td>
      <td>1.869792</td>
      <td>1.687500</td>
      <td>1.833333</td>
      <td>1.702373</td>
      <td>3452400</td>
    </tr>
    <tr>
      <th>1999-02-24</th>
      <td>2.104167</td>
      <td>2.187500</td>
      <td>1.932292</td>
      <td>1.979167</td>
      <td>1.837789</td>
      <td>15319200</td>
    </tr>
    <tr>
      <th>1999-02-25</th>
      <td>2.062500</td>
      <td>2.125000</td>
      <td>1.885417</td>
      <td>1.916667</td>
      <td>1.779754</td>
      <td>3728400</td>
    </tr>
    <tr>
      <th>1999-02-26</th>
      <td>1.937500</td>
      <td>2.000000</td>
      <td>1.812500</td>
      <td>1.828125</td>
      <td>1.697537</td>
      <td>4315200</td>
    </tr>
    <tr>
      <th>1999-03-01</th>
      <td>1.875000</td>
      <td>1.916667</td>
      <td>1.750000</td>
      <td>1.838542</td>
      <td>1.707209</td>
      <td>2304000</td>
    </tr>
    <tr>
      <th>1999-03-02</th>
      <td>1.833333</td>
      <td>1.843750</td>
      <td>1.791667</td>
      <td>1.822917</td>
      <td>1.692701</td>
      <td>1381200</td>
    </tr>
    <tr>
      <th>1999-03-03</th>
      <td>1.833333</td>
      <td>1.833333</td>
      <td>1.687500</td>
      <td>1.697917</td>
      <td>1.576630</td>
      <td>1534800</td>
    </tr>
    <tr>
      <th>1999-03-04</th>
      <td>1.781250</td>
      <td>1.791667</td>
      <td>1.645833</td>
      <td>1.661458</td>
      <td>1.542776</td>
      <td>1434000</td>
    </tr>
    <tr>
      <th>1999-03-05</th>
      <td>1.677083</td>
      <td>1.760417</td>
      <td>1.677083</td>
      <td>1.755208</td>
      <td>1.629829</td>
      <td>1969200</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2017-06-08</th>
      <td>153.460007</td>
      <td>160.000000</td>
      <td>151.789993</td>
      <td>159.940002</td>
      <td>159.940002</td>
      <td>29043600</td>
    </tr>
    <tr>
      <th>2017-06-09</th>
      <td>164.740005</td>
      <td>168.500000</td>
      <td>142.750000</td>
      <td>149.600006</td>
      <td>149.600006</td>
      <td>92323200</td>
    </tr>
    <tr>
      <th>2017-06-12</th>
      <td>145.880005</td>
      <td>151.699997</td>
      <td>142.110001</td>
      <td>149.970001</td>
      <td>149.970001</td>
      <td>42438300</td>
    </tr>
    <tr>
      <th>2017-06-13</th>
      <td>154.399994</td>
      <td>154.770004</td>
      <td>145.649994</td>
      <td>151.399994</td>
      <td>151.399994</td>
      <td>41812600</td>
    </tr>
    <tr>
      <th>2017-06-14</th>
      <td>151.520004</td>
      <td>154.059998</td>
      <td>148.500000</td>
      <td>151.720001</td>
      <td>151.720001</td>
      <td>29616000</td>
    </tr>
    <tr>
      <th>2017-06-15</th>
      <td>146.960007</td>
      <td>153.600006</td>
      <td>146.500000</td>
      <td>152.369995</td>
      <td>152.369995</td>
      <td>24095600</td>
    </tr>
    <tr>
      <th>2017-06-16</th>
      <td>152.759995</td>
      <td>154.699997</td>
      <td>150.240005</td>
      <td>151.619995</td>
      <td>151.619995</td>
      <td>23124000</td>
    </tr>
    <tr>
      <th>2017-06-19</th>
      <td>153.410004</td>
      <td>157.529999</td>
      <td>153.259995</td>
      <td>157.320007</td>
      <td>157.320007</td>
      <td>19454400</td>
    </tr>
    <tr>
      <th>2017-06-20</th>
      <td>159.029999</td>
      <td>161.740005</td>
      <td>156.919998</td>
      <td>157.089996</td>
      <td>157.089996</td>
      <td>27386100</td>
    </tr>
    <tr>
      <th>2017-06-21</th>
      <td>158.210007</td>
      <td>159.619995</td>
      <td>155.699997</td>
      <td>159.470001</td>
      <td>159.470001</td>
      <td>17066300</td>
    </tr>
    <tr>
      <th>2017-06-22</th>
      <td>159.800003</td>
      <td>160.339996</td>
      <td>157.399994</td>
      <td>158.369995</td>
      <td>158.369995</td>
      <td>11728300</td>
    </tr>
    <tr>
      <th>2017-06-23</th>
      <td>158.679993</td>
      <td>159.320007</td>
      <td>153.220001</td>
      <td>153.830002</td>
      <td>153.830002</td>
      <td>27214700</td>
    </tr>
    <tr>
      <th>2017-06-26</th>
      <td>155.160004</td>
      <td>156.600006</td>
      <td>148.330002</td>
      <td>152.149994</td>
      <td>152.149994</td>
      <td>26599000</td>
    </tr>
    <tr>
      <th>2017-06-27</th>
      <td>151.440002</td>
      <td>151.789993</td>
      <td>146.350006</td>
      <td>146.580002</td>
      <td>146.580002</td>
      <td>24987300</td>
    </tr>
    <tr>
      <th>2017-06-28</th>
      <td>149.320007</td>
      <td>151.940002</td>
      <td>145.750000</td>
      <td>151.750000</td>
      <td>151.750000</td>
      <td>24873700</td>
    </tr>
    <tr>
      <th>2017-06-29</th>
      <td>150.600006</td>
      <td>150.720001</td>
      <td>144.080002</td>
      <td>146.679993</td>
      <td>146.679993</td>
      <td>26610600</td>
    </tr>
    <tr>
      <th>2017-06-30</th>
      <td>147.380005</td>
      <td>147.929993</td>
      <td>143.500000</td>
      <td>144.559998</td>
      <td>144.559998</td>
      <td>18203400</td>
    </tr>
    <tr>
      <th>2017-07-03</th>
      <td>145.050003</td>
      <td>145.649994</td>
      <td>138.580002</td>
      <td>139.330002</td>
      <td>139.330002</td>
      <td>17726800</td>
    </tr>
    <tr>
      <th>2017-07-05</th>
      <td>141.899994</td>
      <td>144.220001</td>
      <td>141.130005</td>
      <td>143.050003</td>
      <td>143.050003</td>
      <td>20504700</td>
    </tr>
    <tr>
      <th>2017-07-06</th>
      <td>141.869995</td>
      <td>145.380005</td>
      <td>139.759995</td>
      <td>143.479996</td>
      <td>143.479996</td>
      <td>18657100</td>
    </tr>
    <tr>
      <th>2017-07-07</th>
      <td>145.779999</td>
      <td>147.500000</td>
      <td>144.850006</td>
      <td>146.759995</td>
      <td>146.759995</td>
      <td>16374300</td>
    </tr>
    <tr>
      <th>2017-07-10</th>
      <td>149.740005</td>
      <td>154.000000</td>
      <td>148.679993</td>
      <td>153.699997</td>
      <td>153.699997</td>
      <td>23962300</td>
    </tr>
    <tr>
      <th>2017-07-11</th>
      <td>153.850006</td>
      <td>156.190002</td>
      <td>152.149994</td>
      <td>155.880005</td>
      <td>155.880005</td>
      <td>18948900</td>
    </tr>
    <tr>
      <th>2017-07-12</th>
      <td>158.300003</td>
      <td>163.000000</td>
      <td>156.559998</td>
      <td>162.509995</td>
      <td>162.509995</td>
      <td>28630200</td>
    </tr>
    <tr>
      <th>2017-07-13</th>
      <td>163.000000</td>
      <td>166.300003</td>
      <td>158.750000</td>
      <td>160.630005</td>
      <td>160.630005</td>
      <td>34228300</td>
    </tr>
    <tr>
      <th>2017-07-14</th>
      <td>161.289993</td>
      <td>165.009995</td>
      <td>161.009995</td>
      <td>164.949997</td>
      <td>164.949997</td>
      <td>23548700</td>
    </tr>
    <tr>
      <th>2017-07-17</th>
      <td>166.330002</td>
      <td>167.500000</td>
      <td>161.750000</td>
      <td>164.250000</td>
      <td>164.250000</td>
      <td>23269800</td>
    </tr>
    <tr>
      <th>2017-07-18</th>
      <td>161.779999</td>
      <td>166.550003</td>
      <td>161.300003</td>
      <td>165.960007</td>
      <td>165.960007</td>
      <td>19416000</td>
    </tr>
    <tr>
      <th>2017-07-19</th>
      <td>166.330002</td>
      <td>167.399994</td>
      <td>164.610001</td>
      <td>165.100006</td>
      <td>165.100006</td>
      <td>17176100</td>
    </tr>
    <tr>
      <th>2017-07-20</th>
      <td>165.929993</td>
      <td>167.509995</td>
      <td>163.910004</td>
      <td>167.500000</td>
      <td>167.500000</td>
      <td>17363300</td>
    </tr>
  </tbody>
</table>
<p>4654 rows × 6 columns</p>
</div>




```python
import pandas as pd
tmp = pd.read_csv("../Anaconda3/NVDA.csv",parse_dates=["Date"])
tmp.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1999-01-22</td>
      <td>1.750000</td>
      <td>1.953125</td>
      <td>1.552083</td>
      <td>1.640625</td>
      <td>1.523430</td>
      <td>67867200</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1999-01-25</td>
      <td>1.770833</td>
      <td>1.833333</td>
      <td>1.640625</td>
      <td>1.812500</td>
      <td>1.683028</td>
      <td>12762000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1999-01-26</td>
      <td>1.833333</td>
      <td>1.869792</td>
      <td>1.645833</td>
      <td>1.671875</td>
      <td>1.552448</td>
      <td>8580000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1999-01-27</td>
      <td>1.677083</td>
      <td>1.718750</td>
      <td>1.583333</td>
      <td>1.666667</td>
      <td>1.547611</td>
      <td>6109200</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1999-01-28</td>
      <td>1.666667</td>
      <td>1.677083</td>
      <td>1.651042</td>
      <td>1.661458</td>
      <td>1.542776</td>
      <td>5688000</td>
    </tr>
  </tbody>
</table>
</div>




```python
tmp.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 4654 entries, 0 to 4653
    Data columns (total 7 columns):
    Date         4654 non-null datetime64[ns]
    Open         4654 non-null float64
    High         4654 non-null float64
    Low          4654 non-null float64
    Close        4654 non-null float64
    Adj Close    4654 non-null float64
    Volume       4654 non-null int64
    dtypes: datetime64[ns](1), float64(5), int64(1)
    memory usage: 254.6 KB
    

把tmp解析成data和不解析成data有什么区别呢
+ tmp解析成日期之后可以获得很多属性


```python
data_col = tmp["Date"]
```


```python
data_col.dt.dayofweek
```




    0       4
    1       0
    2       1
    3       2
    4       3
    5       4
    6       0
    7       1
    8       2
    9       3
    10      4
    11      0
    12      1
    13      2
    14      3
    15      4
    16      1
    17      2
    18      3
    19      4
    20      0
    21      1
    22      2
    23      3
    24      4
    25      0
    26      1
    27      2
    28      3
    29      4
           ..
    4624    3
    4625    4
    4626    0
    4627    1
    4628    2
    4629    3
    4630    4
    4631    0
    4632    1
    4633    2
    4634    3
    4635    4
    4636    0
    4637    1
    4638    2
    4639    3
    4640    4
    4641    0
    4642    2
    4643    3
    4644    4
    4645    0
    4646    1
    4647    2
    4648    3
    4649    4
    4650    0
    4651    1
    4652    2
    4653    3
    Name: Date, Length: 4654, dtype: int64




```python
#给dataframe赋值，用loc
tmp.loc[:,"dof"] = data_col.dt.dayofweek
tmp.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
      <th>dof</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1999-01-22</td>
      <td>1.750000</td>
      <td>1.953125</td>
      <td>1.552083</td>
      <td>1.640625</td>
      <td>1.523430</td>
      <td>67867200</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1999-01-25</td>
      <td>1.770833</td>
      <td>1.833333</td>
      <td>1.640625</td>
      <td>1.812500</td>
      <td>1.683028</td>
      <td>12762000</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1999-01-26</td>
      <td>1.833333</td>
      <td>1.869792</td>
      <td>1.645833</td>
      <td>1.671875</td>
      <td>1.552448</td>
      <td>8580000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1999-01-27</td>
      <td>1.677083</td>
      <td>1.718750</td>
      <td>1.583333</td>
      <td>1.666667</td>
      <td>1.547611</td>
      <td>6109200</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1999-01-28</td>
      <td>1.666667</td>
      <td>1.677083</td>
      <td>1.651042</td>
      <td>1.661458</td>
      <td>1.542776</td>
      <td>5688000</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
nvda.index
```




    DatetimeIndex(['1999-01-22', '1999-01-25', '1999-01-26', '1999-01-27',
                   '1999-01-28', '1999-01-29', '1999-02-01', '1999-02-02',
                   '1999-02-03', '1999-02-04',
                   ...
                   '2017-07-07', '2017-07-10', '2017-07-11', '2017-07-12',
                   '2017-07-13', '2017-07-14', '2017-07-17', '2017-07-18',
                   '2017-07-19', '2017-07-20'],
                  dtype='datetime64[ns]', name='Date', length=4654, freq=None)




```python
nvda.groupby(nvda.index.year).mean()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
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
      <th>1999</th>
      <td>1.950782</td>
      <td>2.007317</td>
      <td>1.883559</td>
      <td>1.947230</td>
      <td>1.808134</td>
      <td>6.433220e+06</td>
    </tr>
    <tr>
      <th>2000</th>
      <td>8.781084</td>
      <td>9.222697</td>
      <td>8.360522</td>
      <td>8.778826</td>
      <td>8.151729</td>
      <td>1.104182e+07</td>
    </tr>
    <tr>
      <th>2001</th>
      <td>13.091254</td>
      <td>13.600750</td>
      <td>12.680548</td>
      <td>13.181552</td>
      <td>12.239956</td>
      <td>2.782387e+07</td>
    </tr>
    <tr>
      <th>2002</th>
      <td>9.690344</td>
      <td>9.955093</td>
      <td>9.344391</td>
      <td>9.614749</td>
      <td>8.927940</td>
      <td>3.168655e+07</td>
    </tr>
    <tr>
      <th>2003</th>
      <td>5.902434</td>
      <td>6.042659</td>
      <td>5.764960</td>
      <td>5.900344</td>
      <td>5.478865</td>
      <td>2.430220e+07</td>
    </tr>
    <tr>
      <th>2004</th>
      <td>6.484735</td>
      <td>6.608810</td>
      <td>6.353558</td>
      <td>6.465913</td>
      <td>6.004034</td>
      <td>1.706331e+07</td>
    </tr>
    <tr>
      <th>2005</th>
      <td>9.512381</td>
      <td>9.659656</td>
      <td>9.353175</td>
      <td>9.513823</td>
      <td>8.834223</td>
      <td>1.542825e+07</td>
    </tr>
    <tr>
      <th>2006</th>
      <td>18.057902</td>
      <td>18.425126</td>
      <td>17.720279</td>
      <td>18.095963</td>
      <td>16.803316</td>
      <td>1.534446e+07</td>
    </tr>
    <tr>
      <th>2007</th>
      <td>27.762045</td>
      <td>28.251673</td>
      <td>27.206056</td>
      <td>27.724542</td>
      <td>25.744098</td>
      <td>1.514562e+07</td>
    </tr>
    <tr>
      <th>2008</th>
      <td>16.004308</td>
      <td>16.426245</td>
      <td>15.521462</td>
      <td>15.945613</td>
      <td>14.806572</td>
      <td>2.022721e+07</td>
    </tr>
    <tr>
      <th>2009</th>
      <td>11.825119</td>
      <td>12.114762</td>
      <td>11.565952</td>
      <td>11.850873</td>
      <td>11.004331</td>
      <td>1.919821e+07</td>
    </tr>
    <tr>
      <th>2010</th>
      <td>13.576349</td>
      <td>13.802659</td>
      <td>13.318532</td>
      <td>13.563175</td>
      <td>12.594318</td>
      <td>1.853295e+07</td>
    </tr>
    <tr>
      <th>2011</th>
      <td>16.912540</td>
      <td>17.267540</td>
      <td>16.512143</td>
      <td>16.887540</td>
      <td>15.681214</td>
      <td>2.289352e+07</td>
    </tr>
    <tr>
      <th>2012</th>
      <td>13.526200</td>
      <td>13.717400</td>
      <td>13.319800</td>
      <td>13.507880</td>
      <td>12.551166</td>
      <td>1.207757e+07</td>
    </tr>
    <tr>
      <th>2013</th>
      <td>14.173571</td>
      <td>14.329802</td>
      <td>14.035278</td>
      <td>14.189127</td>
      <td>13.412278</td>
      <td>8.843986e+06</td>
    </tr>
    <tr>
      <th>2014</th>
      <td>18.543056</td>
      <td>18.745476</td>
      <td>18.348214</td>
      <td>18.547064</td>
      <td>17.875053</td>
      <td>7.098902e+06</td>
    </tr>
    <tr>
      <th>2015</th>
      <td>23.680595</td>
      <td>23.979524</td>
      <td>23.411071</td>
      <td>23.718254</td>
      <td>23.262283</td>
      <td>7.756520e+06</td>
    </tr>
    <tr>
      <th>2016</th>
      <td>53.630833</td>
      <td>54.415397</td>
      <td>52.895119</td>
      <td>53.761190</td>
      <td>53.475737</td>
      <td>1.107062e+07</td>
    </tr>
    <tr>
      <th>2017</th>
      <td>120.481305</td>
      <td>122.300725</td>
      <td>118.402754</td>
      <td>120.547971</td>
      <td>120.436863</td>
      <td>1.907742e+07</td>
    </tr>
  </tbody>
</table>
</div>




```python
zscore = lambda x:(x-x.mean())/x.std()
zscore
```




    <function __main__.<lambda>(x)>




```python
transformed_to_zscore=nvda.groupby(nvda.index.year).transform(zscore)
transformed_to_zscore.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
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
      <th>1999-01-22</th>
      <td>-0.340955</td>
      <td>-0.088217</td>
      <td>-0.579850</td>
      <td>-0.510124</td>
      <td>-0.510124</td>
      <td>7.544438</td>
    </tr>
    <tr>
      <th>1999-01-25</th>
      <td>-0.305578</td>
      <td>-0.283222</td>
      <td>-0.424964</td>
      <td>-0.224161</td>
      <td>-0.224161</td>
      <td>0.777210</td>
    </tr>
    <tr>
      <th>1999-01-26</th>
      <td>-0.199444</td>
      <td>-0.223871</td>
      <td>-0.415854</td>
      <td>-0.458130</td>
      <td>-0.458131</td>
      <td>0.263637</td>
    </tr>
    <tr>
      <th>1999-01-27</th>
      <td>-0.464778</td>
      <td>-0.469747</td>
      <td>-0.525185</td>
      <td>-0.466795</td>
      <td>-0.466798</td>
      <td>-0.039791</td>
    </tr>
    <tr>
      <th>1999-01-28</th>
      <td>-0.482465</td>
      <td>-0.537575</td>
      <td>-0.406741</td>
      <td>-0.475462</td>
      <td>-0.475461</td>
      <td>-0.091517</td>
    </tr>
  </tbody>
</table>
</div>



apply可以对某一列做处理


```python
transformed_to_zscore=nvda.groupby(nvda.index.year).apply(zscore)
transformed_to_zscore
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
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
      <th>1999-01-22</th>
      <td>-0.340955</td>
      <td>-0.088217</td>
      <td>-0.579850</td>
      <td>-0.510124</td>
      <td>-0.510124</td>
      <td>7.544438</td>
    </tr>
    <tr>
      <th>1999-01-25</th>
      <td>-0.305578</td>
      <td>-0.283222</td>
      <td>-0.424964</td>
      <td>-0.224161</td>
      <td>-0.224161</td>
      <td>0.777210</td>
    </tr>
    <tr>
      <th>1999-01-26</th>
      <td>-0.199444</td>
      <td>-0.223871</td>
      <td>-0.415854</td>
      <td>-0.458130</td>
      <td>-0.458131</td>
      <td>0.263637</td>
    </tr>
    <tr>
      <th>1999-01-27</th>
      <td>-0.464778</td>
      <td>-0.469747</td>
      <td>-0.525185</td>
      <td>-0.466795</td>
      <td>-0.466798</td>
      <td>-0.039791</td>
    </tr>
    <tr>
      <th>1999-01-28</th>
      <td>-0.482465</td>
      <td>-0.537575</td>
      <td>-0.406741</td>
      <td>-0.475462</td>
      <td>-0.475461</td>
      <td>-0.091517</td>
    </tr>
    <tr>
      <th>1999-01-29</th>
      <td>-0.491311</td>
      <td>-0.554531</td>
      <td>-0.525185</td>
      <td>-0.605445</td>
      <td>-0.605445</td>
      <td>-0.040823</td>
    </tr>
    <tr>
      <th>1999-02-01</th>
      <td>-0.623978</td>
      <td>-0.622359</td>
      <td>-0.525185</td>
      <td>-0.553452</td>
      <td>-0.553451</td>
      <td>-0.315073</td>
    </tr>
    <tr>
      <th>1999-02-02</th>
      <td>-0.623978</td>
      <td>-0.622359</td>
      <td>-0.771180</td>
      <td>-0.761424</td>
      <td>-0.761424</td>
      <td>0.020776</td>
    </tr>
    <tr>
      <th>1999-02-03</th>
      <td>-0.818555</td>
      <td>-0.758014</td>
      <td>-0.743847</td>
      <td>-0.709431</td>
      <td>-0.709430</td>
      <td>-0.559407</td>
    </tr>
    <tr>
      <th>1999-02-04</th>
      <td>-0.694732</td>
      <td>-0.588446</td>
      <td>-0.634516</td>
      <td>-0.570782</td>
      <td>-0.570781</td>
      <td>-0.231516</td>
    </tr>
    <tr>
      <th>1999-02-05</th>
      <td>-0.544378</td>
      <td>-0.554531</td>
      <td>-0.516073</td>
      <td>-0.492792</td>
      <td>-0.492793</td>
      <td>-0.369893</td>
    </tr>
    <tr>
      <th>1999-02-08</th>
      <td>-0.491311</td>
      <td>-0.554531</td>
      <td>-0.506962</td>
      <td>-0.588113</td>
      <td>-0.588113</td>
      <td>-0.316988</td>
    </tr>
    <tr>
      <th>1999-02-09</th>
      <td>-0.553221</td>
      <td>-0.605402</td>
      <td>-0.652737</td>
      <td>-0.692099</td>
      <td>-0.692100</td>
      <td>-0.523007</td>
    </tr>
    <tr>
      <th>1999-02-10</th>
      <td>-0.712421</td>
      <td>-0.707143</td>
      <td>-0.689181</td>
      <td>-0.718096</td>
      <td>-0.718095</td>
      <td>-0.334967</td>
    </tr>
    <tr>
      <th>1999-02-11</th>
      <td>-0.730111</td>
      <td>-0.486705</td>
      <td>-0.634516</td>
      <td>-0.501459</td>
      <td>-0.501458</td>
      <td>-0.384040</td>
    </tr>
    <tr>
      <th>1999-02-12</th>
      <td>-0.482465</td>
      <td>-0.418876</td>
      <td>-0.379409</td>
      <td>-0.345479</td>
      <td>-0.345479</td>
      <td>-0.453155</td>
    </tr>
    <tr>
      <th>1999-02-16</th>
      <td>-0.305578</td>
      <td>-0.266264</td>
      <td>-0.543405</td>
      <td>-0.328148</td>
      <td>-0.328149</td>
      <td>-0.142211</td>
    </tr>
    <tr>
      <th>1999-02-17</th>
      <td>-0.411711</td>
      <td>-0.452790</td>
      <td>-0.452297</td>
      <td>-0.484127</td>
      <td>-0.484128</td>
      <td>-0.582101</td>
    </tr>
    <tr>
      <th>1999-02-18</th>
      <td>-0.411711</td>
      <td>-0.452790</td>
      <td>-0.434074</td>
      <td>-0.440799</td>
      <td>-0.440799</td>
      <td>-0.572964</td>
    </tr>
    <tr>
      <th>1999-02-19</th>
      <td>-0.482465</td>
      <td>-0.384963</td>
      <td>-0.415854</td>
      <td>-0.345479</td>
      <td>-0.345479</td>
      <td>-0.558670</td>
    </tr>
    <tr>
      <th>1999-02-22</th>
      <td>-0.305578</td>
      <td>-0.351048</td>
      <td>-0.397631</td>
      <td>-0.328148</td>
      <td>-0.328149</td>
      <td>-0.159895</td>
    </tr>
    <tr>
      <th>1999-02-23</th>
      <td>-0.270199</td>
      <td>-0.223871</td>
      <td>-0.342966</td>
      <td>-0.189500</td>
      <td>-0.189499</td>
      <td>-0.366061</td>
    </tr>
    <tr>
      <th>1999-02-24</th>
      <td>0.260468</td>
      <td>0.293314</td>
      <td>0.085249</td>
      <td>0.053136</td>
      <td>0.053135</td>
      <td>1.091248</td>
    </tr>
    <tr>
      <th>1999-02-25</th>
      <td>0.189712</td>
      <td>0.191572</td>
      <td>0.003250</td>
      <td>-0.050850</td>
      <td>-0.050850</td>
      <td>-0.332167</td>
    </tr>
    <tr>
      <th>1999-02-26</th>
      <td>-0.022555</td>
      <td>-0.011911</td>
      <td>-0.124303</td>
      <td>-0.198165</td>
      <td>-0.198164</td>
      <td>-0.260105</td>
    </tr>
    <tr>
      <th>1999-03-01</th>
      <td>-0.128688</td>
      <td>-0.147565</td>
      <td>-0.233634</td>
      <td>-0.180833</td>
      <td>-0.180834</td>
      <td>-0.507091</td>
    </tr>
    <tr>
      <th>1999-03-02</th>
      <td>-0.199444</td>
      <td>-0.266264</td>
      <td>-0.160746</td>
      <td>-0.206830</td>
      <td>-0.206829</td>
      <td>-0.620416</td>
    </tr>
    <tr>
      <th>1999-03-03</th>
      <td>-0.199444</td>
      <td>-0.283222</td>
      <td>-0.342966</td>
      <td>-0.414802</td>
      <td>-0.414802</td>
      <td>-0.601554</td>
    </tr>
    <tr>
      <th>1999-03-04</th>
      <td>-0.287888</td>
      <td>-0.351048</td>
      <td>-0.415854</td>
      <td>-0.475462</td>
      <td>-0.475461</td>
      <td>-0.613932</td>
    </tr>
    <tr>
      <th>1999-03-05</th>
      <td>-0.464778</td>
      <td>-0.401919</td>
      <td>-0.361188</td>
      <td>-0.319483</td>
      <td>-0.319482</td>
      <td>-0.548207</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2017-06-08</th>
      <td>1.497139</td>
      <td>1.674761</td>
      <td>1.568812</td>
      <td>1.791207</td>
      <td>1.791015</td>
      <td>0.928518</td>
    </tr>
    <tr>
      <th>2017-06-09</th>
      <td>2.009218</td>
      <td>2.052367</td>
      <td>1.144037</td>
      <td>1.321034</td>
      <td>1.322214</td>
      <td>6.824084</td>
    </tr>
    <tr>
      <th>2017-06-12</th>
      <td>1.153028</td>
      <td>1.306040</td>
      <td>1.113965</td>
      <td>1.337858</td>
      <td>1.338989</td>
      <td>2.176461</td>
    </tr>
    <tr>
      <th>2017-06-13</th>
      <td>1.539811</td>
      <td>1.442422</td>
      <td>1.280303</td>
      <td>1.402881</td>
      <td>1.403823</td>
      <td>2.118167</td>
    </tr>
    <tr>
      <th>2017-06-14</th>
      <td>1.409068</td>
      <td>1.410881</td>
      <td>1.414220</td>
      <td>1.417432</td>
      <td>1.418332</td>
      <td>0.981847</td>
    </tr>
    <tr>
      <th>2017-06-15</th>
      <td>1.202057</td>
      <td>1.390446</td>
      <td>1.320244</td>
      <td>1.446989</td>
      <td>1.447802</td>
      <td>0.467528</td>
    </tr>
    <tr>
      <th>2017-06-16</th>
      <td>1.465360</td>
      <td>1.439312</td>
      <td>1.495980</td>
      <td>1.412885</td>
      <td>1.413798</td>
      <td>0.377007</td>
    </tr>
    <tr>
      <th>2017-06-19</th>
      <td>1.494869</td>
      <td>1.565033</td>
      <td>1.637885</td>
      <td>1.672072</td>
      <td>1.672228</td>
      <td>0.035122</td>
    </tr>
    <tr>
      <th>2017-06-20</th>
      <td>1.750000</td>
      <td>1.752059</td>
      <td>1.809862</td>
      <td>1.661613</td>
      <td>1.661800</td>
      <td>0.774094</td>
    </tr>
    <tr>
      <th>2017-06-21</th>
      <td>1.712775</td>
      <td>1.657879</td>
      <td>1.752537</td>
      <td>1.769835</td>
      <td>1.769706</td>
      <td>-0.187370</td>
    </tr>
    <tr>
      <th>2017-06-22</th>
      <td>1.784956</td>
      <td>1.689865</td>
      <td>1.832417</td>
      <td>1.719816</td>
      <td>1.719833</td>
      <td>-0.684695</td>
    </tr>
    <tr>
      <th>2017-06-23</th>
      <td>1.734111</td>
      <td>1.644553</td>
      <td>1.636006</td>
      <td>1.513377</td>
      <td>1.513996</td>
      <td>0.758125</td>
    </tr>
    <tr>
      <th>2017-06-26</th>
      <td>1.574314</td>
      <td>1.523719</td>
      <td>1.406233</td>
      <td>1.436985</td>
      <td>1.437827</td>
      <td>0.700763</td>
    </tr>
    <tr>
      <th>2017-06-27</th>
      <td>1.405436</td>
      <td>1.310038</td>
      <td>1.313196</td>
      <td>1.183710</td>
      <td>1.185292</td>
      <td>0.550605</td>
    </tr>
    <tr>
      <th>2017-06-28</th>
      <td>1.309195</td>
      <td>1.316702</td>
      <td>1.285002</td>
      <td>1.418797</td>
      <td>1.419692</td>
      <td>0.540022</td>
    </tr>
    <tr>
      <th>2017-06-29</th>
      <td>1.367303</td>
      <td>1.262504</td>
      <td>1.206532</td>
      <td>1.188257</td>
      <td>1.189825</td>
      <td>0.701843</td>
    </tr>
    <tr>
      <th>2017-06-30</th>
      <td>1.221124</td>
      <td>1.138560</td>
      <td>1.179279</td>
      <td>1.091858</td>
      <td>1.093708</td>
      <td>-0.081430</td>
    </tr>
    <tr>
      <th>2017-07-03</th>
      <td>1.115349</td>
      <td>1.037273</td>
      <td>0.948096</td>
      <td>0.854043</td>
      <td>0.856587</td>
      <td>-0.125833</td>
    </tr>
    <tr>
      <th>2017-07-05</th>
      <td>0.972347</td>
      <td>0.973747</td>
      <td>1.067916</td>
      <td>1.023196</td>
      <td>1.025247</td>
      <td>0.132975</td>
    </tr>
    <tr>
      <th>2017-07-06</th>
      <td>0.970985</td>
      <td>1.025279</td>
      <td>1.003542</td>
      <td>1.042749</td>
      <td>1.044742</td>
      <td>-0.039160</td>
    </tr>
    <tr>
      <th>2017-07-07</th>
      <td>1.148488</td>
      <td>1.119458</td>
      <td>1.242713</td>
      <td>1.191895</td>
      <td>1.193452</td>
      <td>-0.251841</td>
    </tr>
    <tr>
      <th>2017-07-10</th>
      <td>1.328261</td>
      <td>1.408216</td>
      <td>1.422678</td>
      <td>1.507465</td>
      <td>1.508102</td>
      <td>0.455109</td>
    </tr>
    <tr>
      <th>2017-07-11</th>
      <td>1.514843</td>
      <td>1.505505</td>
      <td>1.585728</td>
      <td>1.606593</td>
      <td>1.606940</td>
      <td>-0.011974</td>
    </tr>
    <tr>
      <th>2017-07-12</th>
      <td>1.716861</td>
      <td>1.808033</td>
      <td>1.792947</td>
      <td>1.908067</td>
      <td>1.907534</td>
      <td>0.890003</td>
    </tr>
    <tr>
      <th>2017-07-13</th>
      <td>1.930227</td>
      <td>1.954634</td>
      <td>1.895851</td>
      <td>1.822582</td>
      <td>1.822298</td>
      <td>1.411561</td>
    </tr>
    <tr>
      <th>2017-07-14</th>
      <td>1.852598</td>
      <td>1.897326</td>
      <td>2.002045</td>
      <td>2.019017</td>
      <td>2.018161</td>
      <td>0.416575</td>
    </tr>
    <tr>
      <th>2017-07-17</th>
      <td>2.081400</td>
      <td>2.007942</td>
      <td>2.036816</td>
      <td>1.987188</td>
      <td>1.986424</td>
      <td>0.390591</td>
    </tr>
    <tr>
      <th>2017-07-18</th>
      <td>1.874842</td>
      <td>1.965740</td>
      <td>2.015672</td>
      <td>2.064944</td>
      <td>2.063953</td>
      <td>0.031544</td>
    </tr>
    <tr>
      <th>2017-07-19</th>
      <td>2.081400</td>
      <td>2.003500</td>
      <td>2.171203</td>
      <td>2.025839</td>
      <td>2.024962</td>
      <td>-0.177140</td>
    </tr>
    <tr>
      <th>2017-07-20</th>
      <td>2.063240</td>
      <td>2.008386</td>
      <td>2.138311</td>
      <td>2.134969</td>
      <td>2.133774</td>
      <td>-0.159699</td>
    </tr>
  </tbody>
</table>
<p>4654 rows × 6 columns</p>
</div>




```python
def trans(x):
    return x**2 if x<1.6 else x

nvda.loc[:,"new"]=nvda["Close"].apply(trans)
nvda.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
      <th>new</th>
    </tr>
    <tr>
      <th>Date</th>
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
      <th>1999-01-22</th>
      <td>1.750000</td>
      <td>1.953125</td>
      <td>1.552083</td>
      <td>1.640625</td>
      <td>1.523430</td>
      <td>67867200</td>
      <td>1.640625</td>
    </tr>
    <tr>
      <th>1999-01-25</th>
      <td>1.770833</td>
      <td>1.833333</td>
      <td>1.640625</td>
      <td>1.812500</td>
      <td>1.683028</td>
      <td>12762000</td>
      <td>1.812500</td>
    </tr>
    <tr>
      <th>1999-01-26</th>
      <td>1.833333</td>
      <td>1.869792</td>
      <td>1.645833</td>
      <td>1.671875</td>
      <td>1.552448</td>
      <td>8580000</td>
      <td>1.671875</td>
    </tr>
    <tr>
      <th>1999-01-27</th>
      <td>1.677083</td>
      <td>1.718750</td>
      <td>1.583333</td>
      <td>1.666667</td>
      <td>1.547611</td>
      <td>6109200</td>
      <td>1.666667</td>
    </tr>
    <tr>
      <th>1999-01-28</th>
      <td>1.666667</td>
      <td>1.677083</td>
      <td>1.651042</td>
      <td>1.661458</td>
      <td>1.542776</td>
      <td>5688000</td>
      <td>1.661458</td>
    </tr>
  </tbody>
</table>
</div>




```python
def trans(x):
    return x**2 if x<1.6 else x 
#新增一列
nvda.loc[:,"new1"]=nvda["Close"].transform(trans)
nvda.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
      <th>new</th>
      <th>new1</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
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
      <th>1999-01-22</th>
      <td>1.750000</td>
      <td>1.953125</td>
      <td>1.552083</td>
      <td>1.640625</td>
      <td>1.523430</td>
      <td>67867200</td>
      <td>1.640625</td>
      <td>1.640625</td>
    </tr>
    <tr>
      <th>1999-01-25</th>
      <td>1.770833</td>
      <td>1.833333</td>
      <td>1.640625</td>
      <td>1.812500</td>
      <td>1.683028</td>
      <td>12762000</td>
      <td>1.812500</td>
      <td>1.812500</td>
    </tr>
    <tr>
      <th>1999-01-26</th>
      <td>1.833333</td>
      <td>1.869792</td>
      <td>1.645833</td>
      <td>1.671875</td>
      <td>1.552448</td>
      <td>8580000</td>
      <td>1.671875</td>
      <td>1.671875</td>
    </tr>
    <tr>
      <th>1999-01-27</th>
      <td>1.677083</td>
      <td>1.718750</td>
      <td>1.583333</td>
      <td>1.666667</td>
      <td>1.547611</td>
      <td>6109200</td>
      <td>1.666667</td>
      <td>1.666667</td>
    </tr>
    <tr>
      <th>1999-01-28</th>
      <td>1.666667</td>
      <td>1.677083</td>
      <td>1.651042</td>
      <td>1.661458</td>
      <td>1.542776</td>
      <td>5688000</td>
      <td>1.661458</td>
      <td>1.661458</td>
    </tr>
  </tbody>
</table>
</div>




```python
compared = pd.DataFrame({"Original Adj Close":nvda["Adj Close"],"transformed_to_zscore":transformed_to_zscore["Adj Close"]})
compared.plot()
```




    <matplotlib.axes._subplots.AxesSubplot at 0x9766ef0>




![png](output_50_1.png)



```python
nvda.groupby(nvda.index.year).transform("min")
nvda.head(3)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
      <th>new</th>
      <th>new1</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
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
      <th>1999-01-22</th>
      <td>1.750000</td>
      <td>1.953125</td>
      <td>1.552083</td>
      <td>1.640625</td>
      <td>1.523430</td>
      <td>67867200</td>
      <td>1.640625</td>
      <td>1.640625</td>
    </tr>
    <tr>
      <th>1999-01-25</th>
      <td>1.770833</td>
      <td>1.833333</td>
      <td>1.640625</td>
      <td>1.812500</td>
      <td>1.683028</td>
      <td>12762000</td>
      <td>1.812500</td>
      <td>1.812500</td>
    </tr>
    <tr>
      <th>1999-01-26</th>
      <td>1.833333</td>
      <td>1.869792</td>
      <td>1.645833</td>
      <td>1.671875</td>
      <td>1.552448</td>
      <td>8580000</td>
      <td>1.671875</td>
      <td>1.671875</td>
    </tr>
  </tbody>
</table>
</div>




```python
nvda.loc[:,"High"]=nvda.groupby(nvda.index.year).transform("min")
nvda.head(9)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
      <th>new</th>
      <th>new1</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
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
      <th>1999-01-22</th>
      <td>1.750000</td>
      <td>1.421875</td>
      <td>1.552083</td>
      <td>1.640625</td>
      <td>1.523430</td>
      <td>67867200</td>
      <td>1.640625</td>
      <td>1.640625</td>
    </tr>
    <tr>
      <th>1999-01-25</th>
      <td>1.770833</td>
      <td>1.421875</td>
      <td>1.640625</td>
      <td>1.812500</td>
      <td>1.683028</td>
      <td>12762000</td>
      <td>1.812500</td>
      <td>1.812500</td>
    </tr>
    <tr>
      <th>1999-01-26</th>
      <td>1.833333</td>
      <td>1.421875</td>
      <td>1.645833</td>
      <td>1.671875</td>
      <td>1.552448</td>
      <td>8580000</td>
      <td>1.671875</td>
      <td>1.671875</td>
    </tr>
    <tr>
      <th>1999-01-27</th>
      <td>1.677083</td>
      <td>1.421875</td>
      <td>1.583333</td>
      <td>1.666667</td>
      <td>1.547611</td>
      <td>6109200</td>
      <td>1.666667</td>
      <td>1.666667</td>
    </tr>
    <tr>
      <th>1999-01-28</th>
      <td>1.666667</td>
      <td>1.421875</td>
      <td>1.651042</td>
      <td>1.661458</td>
      <td>1.542776</td>
      <td>5688000</td>
      <td>1.661458</td>
      <td>1.661458</td>
    </tr>
    <tr>
      <th>1999-01-29</th>
      <td>1.661458</td>
      <td>1.421875</td>
      <td>1.583333</td>
      <td>1.583333</td>
      <td>1.470231</td>
      <td>6100800</td>
      <td>2.506943</td>
      <td>2.506943</td>
    </tr>
    <tr>
      <th>1999-02-01</th>
      <td>1.583333</td>
      <td>1.421875</td>
      <td>1.583333</td>
      <td>1.614583</td>
      <td>1.499249</td>
      <td>3867600</td>
      <td>1.614583</td>
      <td>1.614583</td>
    </tr>
    <tr>
      <th>1999-02-02</th>
      <td>1.583333</td>
      <td>1.421875</td>
      <td>1.442708</td>
      <td>1.489583</td>
      <td>1.383178</td>
      <td>6602400</td>
      <td>2.218858</td>
      <td>2.218858</td>
    </tr>
    <tr>
      <th>1999-02-03</th>
      <td>1.468750</td>
      <td>1.421875</td>
      <td>1.458333</td>
      <td>1.520833</td>
      <td>1.412196</td>
      <td>1878000</td>
      <td>2.312933</td>
      <td>2.312933</td>
    </tr>
  </tbody>
</table>
</div>



## filter


```python
import pandas as pd
df = pd.DataFrame({"A": np.arange(8), "B":list("aaabbbcc")},columns=["A","B"])
df
df.groupby("B").filter(lambda x: len(x) > 2)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>a</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>a</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>a</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>b</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>b</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>b</td>
    </tr>
  </tbody>
</table>
</div>




```python
import numpy as np
data={"A":np.arange(8),"B":[1,2,3,3,3,3,4,4]}
df =pd.DataFrame(data,columns=["A","B"])
df.groupby("B").filter(lambda x :len(x)>2)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>3</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
nvda.groupby([nvda.index.year,nvda.index.month]).filter(lambda x: x["Adj Close"].mean() > 50).head()
nvda.groupby([nvda.index.year,nvda.index.month,nvda.index.day]).filter(lambda x:  x["Adj Close"]>100).head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
      <th>new</th>
      <th>new1</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
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
      <th>2016-12-16</th>
      <td>99.830002</td>
      <td>25.559999</td>
      <td>97.730003</td>
      <td>100.410004</td>
      <td>100.177933</td>
      <td>27238200</td>
      <td>100.410004</td>
      <td>100.410004</td>
    </tr>
    <tr>
      <th>2016-12-19</th>
      <td>99.699997</td>
      <td>25.559999</td>
      <td>99.000000</td>
      <td>101.629997</td>
      <td>101.395111</td>
      <td>18616400</td>
      <td>101.629997</td>
      <td>101.629997</td>
    </tr>
    <tr>
      <th>2016-12-20</th>
      <td>104.580002</td>
      <td>25.559999</td>
      <td>104.120003</td>
      <td>105.169998</td>
      <td>104.926933</td>
      <td>21201400</td>
      <td>105.169998</td>
      <td>105.169998</td>
    </tr>
    <tr>
      <th>2016-12-21</th>
      <td>105.639999</td>
      <td>25.559999</td>
      <td>103.709999</td>
      <td>105.830002</td>
      <td>105.585411</td>
      <td>14403400</td>
      <td>105.830002</td>
      <td>105.830002</td>
    </tr>
    <tr>
      <th>2016-12-22</th>
      <td>106.820000</td>
      <td>25.559999</td>
      <td>106.529999</td>
      <td>107.110001</td>
      <td>106.862442</td>
      <td>17965300</td>
      <td>107.110001</td>
      <td>107.110001</td>
    </tr>
  </tbody>
</table>
</div>



Group by: split-apply-combine

首先第一步是分离数据split，按照一定的规则把数据分成几类。
第二步是对每一部分数据都做一定的操作，这个操作可以是汇总操作aggregate，可以是一个变换transform，也可以是过滤数据filter。
最后一步就是把处理过的数据再合成一张DataFrame。

# 多表合并与拼接


```python
import pandas as pd
import numpy as np
```


```python
data={"apts":[55000,200000],"cars":[60000,300000]}
df1=pd.DataFrame(data,index=["Shanghai","Beijing"],columns=["apts","cars"])
df1
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>apts</th>
      <th>cars</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Shanghai</th>
      <td>55000</td>
      <td>60000</td>
    </tr>
    <tr>
      <th>Beijing</th>
      <td>200000</td>
      <td>300000</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2 = pd.DataFrame({'cars': [150000, 120000], 'apts': [25000, 20000],},index = ['Hangzhou', 'Nanjing'])
df2
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>cars</th>
      <th>apts</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Hangzhou</th>
      <td>150000</td>
      <td>25000</td>
    </tr>
    <tr>
      <th>Nanjing</th>
      <td>120000</td>
      <td>20000</td>
    </tr>
  </tbody>
</table>
</div>




```python
df3 = pd.DataFrame({'apts': [30000, 10000],'cars': [180000, 100000],'mar': [180000, 100000]},index = ['Guangzhou', 'Chongqing'])
df3
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>apts</th>
      <th>cars</th>
      <th>mar</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Guangzhou</th>
      <td>30000</td>
      <td>180000</td>
      <td>180000</td>
    </tr>
    <tr>
      <th>Chongqing</th>
      <td>10000</td>
      <td>100000</td>
      <td>100000</td>
    </tr>
  </tbody>
</table>
</div>




```python
import warnings
warnings.filterwarning("ignore")
```


```python
frames=[df1,df2,df3]
#以列对齐的方式做拼接
result=pd.concat([df1,df2,df3])
type(frames)
result
```

    D:\anaconda2\lib\site-packages\ipykernel_launcher.py:2: FutureWarning: Sorting because non-concatenation axis is not aligned. A future version
    of pandas will change to not sort by default.
    
    To accept the future behavior, pass 'sort=False'.
    
    To retain the current behavior and silence the warning, pass 'sort=True'.
    
      
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>apts</th>
      <th>cars</th>
      <th>mar</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Shanghai</th>
      <td>55000</td>
      <td>60000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Beijing</th>
      <td>200000</td>
      <td>300000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Hangzhou</th>
      <td>25000</td>
      <td>150000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Nanjing</th>
      <td>20000</td>
      <td>120000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Guangzhou</th>
      <td>30000</td>
      <td>180000</td>
      <td>180000.0</td>
    </tr>
    <tr>
      <th>Chongqing</th>
      <td>10000</td>
      <td>100000</td>
      <td>100000.0</td>
    </tr>
  </tbody>
</table>
</div>



在concat的时候可以指定keys，这样可以给每一个部分加上一个Key。

以下的例子就构造了一个hierarchical index。


```python
result2=pd.concat(frames,keys=["x","y","z"],sort=False)
print(result2)
```

                   apts    cars       mar
    x Shanghai    55000   60000       NaN
      Beijing    200000  300000       NaN
    y Hangzhou    25000  150000       NaN
      Nanjing     20000  120000       NaN
    z Guangzhou   30000  180000  180000.0
      Chongqing   10000  100000  100000.0
    


```python
result2.loc["y","apts"]
```




    Hangzhou    25000
    Nanjing     20000
    Name: apts, dtype: int64




```python
df4 = pd.DataFrame({'salaries': [10000, 30000, 30000, 20000, 15000]},
                  index = ['Suzhou', 'Beijing', 'Shanghai', 'Guangzhou', 'Tianjin'])
print(df4)
```

               salaries
    Suzhou        10000
    Beijing       30000
    Shanghai      30000
    Guangzhou     20000
    Tianjin       15000
    


```python
#做列拼接，对齐index行索引
result3 = pd.concat([result, df4], axis=1, sort=False)
result3
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>apts</th>
      <th>cars</th>
      <th>mar</th>
      <th>salaries</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Shanghai</th>
      <td>55000.0</td>
      <td>60000.0</td>
      <td>NaN</td>
      <td>30000.0</td>
    </tr>
    <tr>
      <th>Beijing</th>
      <td>200000.0</td>
      <td>300000.0</td>
      <td>NaN</td>
      <td>30000.0</td>
    </tr>
    <tr>
      <th>Hangzhou</th>
      <td>25000.0</td>
      <td>150000.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Nanjing</th>
      <td>20000.0</td>
      <td>120000.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Guangzhou</th>
      <td>30000.0</td>
      <td>180000.0</td>
      <td>180000.0</td>
      <td>20000.0</td>
    </tr>
    <tr>
      <th>Chongqing</th>
      <td>10000.0</td>
      <td>100000.0</td>
      <td>100000.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Suzhou</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>10000.0</td>
    </tr>
    <tr>
      <th>Tianjin</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>15000.0</td>
    </tr>
  </tbody>
</table>
</div>



用inner可以去掉NaN,也就是说如果出现了不匹配的行就会被忽略


```python
result3 = pd.concat([result, df4], axis=1, join='inner')
print(result3)
```

          apts      cars       city  salaries  salaries       city
    0  55000.0  200000.0   Shanghai   30000.0     10000     Suzhou
    1  60000.0  300000.0    Beijing   30000.0     30000    Beijing
    2  58000.0  250000.0   Shenzhen       NaN     30000   Shanghai
    3      NaN       NaN     Suzhou   10000.0     20000  Guangzhou
    4      NaN       NaN  Guangzhou   20000.0     15000    Tianjin
    

**用[append](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.append.html)来做concat**


```python
print(df1.append(df2, sort=False))
```

               apts    cars
    Shanghai  55000  200000
    Beijing   60000  300000
    Hangzhou  25000  150000
    Nanjing   20000  120000
    


```python
df1.join
```




    <bound method DataFrame.join of            apts    cars
    Shanghai  55000  200000
    Beijing   60000  300000>




```python
print(df1)
```

               apts    cars
    Shanghai  55000  200000
    Beijing   60000  300000
    


```python
print(df1.append(df4,sort=False))
```

                  apts      cars  salaries
    Shanghai   55000.0  200000.0       NaN
    Beijing    60000.0  300000.0       NaN
    Suzhou         NaN       NaN   10000.0
    Beijing        NaN       NaN   30000.0
    Shanghai       NaN       NaN   30000.0
    Guangzhou      NaN       NaN   20000.0
    Tianjin        NaN       NaN   15000.0
    


```python
df1.join
```




    <bound method DataFrame.join of            apts    cars
    Shanghai  55000  200000
    Beijing   60000  300000>




```python
#按行对齐
print(pd.concat([df1,s1],axis=1))
```

               apts    cars  meal
    Shanghai  55000  200000    60
    Beijing   60000  300000    50
    

Series和DataFrame还可以被一起concatenate，这时候Series会先被转成DataFrame然后做Join，因为Series本来就是一个只有一维的DataFrame对吧


```python
s1 = pd.Series([60, 50], index=['Shanghai', 'Beijing'], name='meal')
print(s1)
```

    Shanghai    60
    Beijing     50
    Name: meal, dtype: int64
    

### append一个row加入dataframe


```python
s2 = pd.Series([18000, 12000,4000],index=['apts', 'cars',"meal"], name='Xiamen') #注意这里的name是必须要有的，因为要用作Index。
print(s2)
```

    apts    18000
    cars    12000
    meal     4000
    Name: Xiamen, dtype: int64
    


```python
print(df1.append(s2))
```

               apts    cars    meal
    Shanghai  55000  200000     NaN
    Beijing   60000  300000     NaN
    Xiamen    18000   12000  4000.0
    


```python
s1 = pd.Series([60, 50], index=["apts","cars"], name='Tianjing')
print(s1)
```

    apts    60
    cars    50
    Name: Tianjing, dtype: int64
    


```python
print(df1.append(s1))
```

               apts    cars
    Shanghai  55000  200000
    Beijing   60000  300000
    Tianjing     60      50
    

### 两张表基于某个字段做连接
### Merge/Join


```python
df1 = pd.DataFrame({'apts': [55000, 60000, 58000], 'cars': [200000, 300000,250000], 'city': ['Shanghai', 'Beijing','Shenzhen']})
df1
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>apts</th>
      <th>cars</th>
      <th>city</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>55000</td>
      <td>200000</td>
      <td>Shanghai</td>
    </tr>
    <tr>
      <th>1</th>
      <td>60000</td>
      <td>300000</td>
      <td>Beijing</td>
    </tr>
    <tr>
      <th>2</th>
      <td>58000</td>
      <td>250000</td>
      <td>Shenzhen</td>
    </tr>
  </tbody>
</table>
</div>




```python
df4 = pd.DataFrame({'salaries': [10000, 30000, 30000, 20000, 15000], 'city': ['Suzhou', 'Beijing', 'Shanghai', 'Guangzhou', 'Tianjin']})
df4
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>salaries</th>
      <th>city</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10000</td>
      <td>Suzhou</td>
    </tr>
    <tr>
      <th>1</th>
      <td>30000</td>
      <td>Beijing</td>
    </tr>
    <tr>
      <th>2</th>
      <td>30000</td>
      <td>Shanghai</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20000</td>
      <td>Guangzhou</td>
    </tr>
    <tr>
      <th>4</th>
      <td>15000</td>
      <td>Tianjin</td>
    </tr>
  </tbody>
</table>
</div>




```python
result=pd.merge(df1,df4,on="city")
result
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>apts</th>
      <th>cars</th>
      <th>city</th>
      <th>salaries</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>55000</td>
      <td>200000</td>
      <td>Shanghai</td>
      <td>30000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>60000</td>
      <td>300000</td>
      <td>Beijing</td>
      <td>30000</td>
    </tr>
  </tbody>
</table>
</div>




```python
#外部连接指的是：两张表里有任意一张表里有，就会把它留下来
result=pd.merge(df1,df4,on="city",how="outer")
result
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>apts</th>
      <th>cars</th>
      <th>city</th>
      <th>salaries</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>55000.0</td>
      <td>200000.0</td>
      <td>Shanghai</td>
      <td>30000.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>60000.0</td>
      <td>300000.0</td>
      <td>Beijing</td>
      <td>30000.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>58000.0</td>
      <td>250000.0</td>
      <td>Shenzhen</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>Suzhou</td>
      <td>10000.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>Guangzhou</td>
      <td>20000.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>Tianjin</td>
      <td>15000.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
result=pd.merge(df1,df4,how="right")
result
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>apts</th>
      <th>cars</th>
      <th>city</th>
      <th>salaries</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>55000.0</td>
      <td>200000.0</td>
      <td>Shanghai</td>
      <td>30000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>60000.0</td>
      <td>300000.0</td>
      <td>Beijing</td>
      <td>30000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>Suzhou</td>
      <td>10000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>Guangzhou</td>
      <td>20000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>Tianjin</td>
      <td>15000</td>
    </tr>
  </tbody>
</table>
</div>




```python
result=pd.merge(df1,df4,on="city",how="left")
result
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>apts</th>
      <th>cars</th>
      <th>city</th>
      <th>salaries</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>55000.0</td>
      <td>200000.0</td>
      <td>Shanghai</td>
      <td>30000.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>60000.0</td>
      <td>300000.0</td>
      <td>Beijing</td>
      <td>30000.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>58000.0</td>
      <td>250000.0</td>
      <td>Shenzhen</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>Suzhou</td>
      <td>10000.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>Guangzhou</td>
      <td>20000.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>Tianjin</td>
      <td>15000.0</td>
    </tr>
  </tbody>
</table>
</div>



## 高级用法

### 用concat做同样的事情


```python
pd.concat([df1.set_index("city"), df4.set_index('city')], sort=False, axis=1, join="inner")
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>apts</th>
      <th>cars</th>
      <th>salaries</th>
    </tr>
    <tr>
      <th>city</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Shanghai</th>
      <td>55000</td>
      <td>200000</td>
      <td>30000</td>
    </tr>
    <tr>
      <th>Beijing</th>
      <td>60000</td>
      <td>300000</td>
      <td>30000</td>
    </tr>
  </tbody>
</table>
</div>



总结：
1.concat主要做的是表格中行和列的拼接
#在行索引中添加值
pd.concat([df1,s1],keys=["x","y","z"],sorted=False)
#行对齐
pd.concat([df1,s1])
#列对齐
pd.concat([df1,s1]，axis=1)
2.merge主要做的是某一列，或者某一列做一个表的关联，比如常会用到on（重点关注哪一项）和how（以何种方式关联）

# 项目1


```python
import pandas as pd
import numpy as np
ratings = pd.read_csv("../Anaconda3/ratings_small.csv")
ratings.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>userId</th>
      <th>movieId</th>
      <th>rating</th>
      <th>timestamp</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>31</td>
      <td>2.5</td>
      <td>1260759144</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1029</td>
      <td>3.0</td>
      <td>1260759179</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>1061</td>
      <td>3.0</td>
      <td>1260759182</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>1129</td>
      <td>2.0</td>
      <td>1260759185</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>1172</td>
      <td>4.0</td>
      <td>1260759205</td>
    </tr>
  </tbody>
</table>
</div>




```python
#分组可以用size也可以用aggregate里的count
ratings.groupby("movieId").size()
```




    movieId
    1         247
    2         107
    3          59
    4          13
    5          56
    6         104
    7          53
    8           5
    9          20
    10        122
    11         82
    12         18
    13          8
    14         31
    15         11
    16         88
    17         86
    18         26
    19         92
    20         13
    21         95
    22         38
    23         22
    24         34
    25        101
    26          5
    27          7
    28         18
    29         40
    30         10
             ... 
    158238      2
    158314      1
    158528      1
    158956      1
    159093      2
    159462      1
    159690      1
    159755      1
    159858      2
    159972      1
    160080      1
    160271      1
    160438      2
    160440      1
    160563      2
    160565      1
    160567      1
    160590      1
    160656      1
    160718      1
    161084      1
    161155      1
    161594      1
    161830      1
    161918      1
    161944      1
    162376      1
    162542      1
    162672      1
    163949      1
    Length: 9066, dtype: int64




```python
import pandas as pd
import numpy as np
ratings.shape
count=ratings.groupby("movieId").aggregate({"rating":"count"}).rename(columns={"rating":"count"})
count
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>movieId</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>247</td>
    </tr>
    <tr>
      <th>2</th>
      <td>107</td>
    </tr>
    <tr>
      <th>3</th>
      <td>59</td>
    </tr>
    <tr>
      <th>4</th>
      <td>13</td>
    </tr>
    <tr>
      <th>5</th>
      <td>56</td>
    </tr>
    <tr>
      <th>6</th>
      <td>104</td>
    </tr>
    <tr>
      <th>7</th>
      <td>53</td>
    </tr>
    <tr>
      <th>8</th>
      <td>5</td>
    </tr>
    <tr>
      <th>9</th>
      <td>20</td>
    </tr>
    <tr>
      <th>10</th>
      <td>122</td>
    </tr>
    <tr>
      <th>11</th>
      <td>82</td>
    </tr>
    <tr>
      <th>12</th>
      <td>18</td>
    </tr>
    <tr>
      <th>13</th>
      <td>8</td>
    </tr>
    <tr>
      <th>14</th>
      <td>31</td>
    </tr>
    <tr>
      <th>15</th>
      <td>11</td>
    </tr>
    <tr>
      <th>16</th>
      <td>88</td>
    </tr>
    <tr>
      <th>17</th>
      <td>86</td>
    </tr>
    <tr>
      <th>18</th>
      <td>26</td>
    </tr>
    <tr>
      <th>19</th>
      <td>92</td>
    </tr>
    <tr>
      <th>20</th>
      <td>13</td>
    </tr>
    <tr>
      <th>21</th>
      <td>95</td>
    </tr>
    <tr>
      <th>22</th>
      <td>38</td>
    </tr>
    <tr>
      <th>23</th>
      <td>22</td>
    </tr>
    <tr>
      <th>24</th>
      <td>34</td>
    </tr>
    <tr>
      <th>25</th>
      <td>101</td>
    </tr>
    <tr>
      <th>26</th>
      <td>5</td>
    </tr>
    <tr>
      <th>27</th>
      <td>7</td>
    </tr>
    <tr>
      <th>28</th>
      <td>18</td>
    </tr>
    <tr>
      <th>29</th>
      <td>40</td>
    </tr>
    <tr>
      <th>30</th>
      <td>10</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>158238</th>
      <td>2</td>
    </tr>
    <tr>
      <th>158314</th>
      <td>1</td>
    </tr>
    <tr>
      <th>158528</th>
      <td>1</td>
    </tr>
    <tr>
      <th>158956</th>
      <td>1</td>
    </tr>
    <tr>
      <th>159093</th>
      <td>2</td>
    </tr>
    <tr>
      <th>159462</th>
      <td>1</td>
    </tr>
    <tr>
      <th>159690</th>
      <td>1</td>
    </tr>
    <tr>
      <th>159755</th>
      <td>1</td>
    </tr>
    <tr>
      <th>159858</th>
      <td>2</td>
    </tr>
    <tr>
      <th>159972</th>
      <td>1</td>
    </tr>
    <tr>
      <th>160080</th>
      <td>1</td>
    </tr>
    <tr>
      <th>160271</th>
      <td>1</td>
    </tr>
    <tr>
      <th>160438</th>
      <td>2</td>
    </tr>
    <tr>
      <th>160440</th>
      <td>1</td>
    </tr>
    <tr>
      <th>160563</th>
      <td>2</td>
    </tr>
    <tr>
      <th>160565</th>
      <td>1</td>
    </tr>
    <tr>
      <th>160567</th>
      <td>1</td>
    </tr>
    <tr>
      <th>160590</th>
      <td>1</td>
    </tr>
    <tr>
      <th>160656</th>
      <td>1</td>
    </tr>
    <tr>
      <th>160718</th>
      <td>1</td>
    </tr>
    <tr>
      <th>161084</th>
      <td>1</td>
    </tr>
    <tr>
      <th>161155</th>
      <td>1</td>
    </tr>
    <tr>
      <th>161594</th>
      <td>1</td>
    </tr>
    <tr>
      <th>161830</th>
      <td>1</td>
    </tr>
    <tr>
      <th>161918</th>
      <td>1</td>
    </tr>
    <tr>
      <th>161944</th>
      <td>1</td>
    </tr>
    <tr>
      <th>162376</th>
      <td>1</td>
    </tr>
    <tr>
      <th>162542</th>
      <td>1</td>
    </tr>
    <tr>
      <th>162672</th>
      <td>1</td>
    </tr>
    <tr>
      <th>163949</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>9066 rows × 1 columns</p>
</div>



#### 计算每部电影的平均分，以及有多少人打分


```python
ratings_mean = ratings.groupby("movieId").agg({"rating":np.mean,"timestamp":"count"}).rename(columns={"timestamp":"count"})
ratings_mean.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>rating</th>
      <th>count</th>
    </tr>
    <tr>
      <th>movieId</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>3.872470</td>
      <td>247</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.401869</td>
      <td>107</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3.161017</td>
      <td>59</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2.384615</td>
      <td>13</td>
    </tr>
    <tr>
      <th>5</th>
      <td>3.267857</td>
      <td>56</td>
    </tr>
  </tbody>
</table>
</div>




```python
ratings_mean.shape
```




    (9066, 2)




```python
meta = pd.read_csv("../Anaconda3/movies_metadata.csv")
meta.head()
```

    D:\anaconda2\lib\site-packages\IPython\core\interactiveshell.py:2785: DtypeWarning: Columns (10) have mixed types. Specify dtype option on import or set low_memory=False.
      interactivity=interactivity, compiler=compiler, result=result)
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>adult</th>
      <th>belongs_to_collection</th>
      <th>budget</th>
      <th>genres</th>
      <th>homepage</th>
      <th>id</th>
      <th>imdb_id</th>
      <th>original_language</th>
      <th>original_title</th>
      <th>overview</th>
      <th>...</th>
      <th>release_date</th>
      <th>revenue</th>
      <th>runtime</th>
      <th>spoken_languages</th>
      <th>status</th>
      <th>tagline</th>
      <th>title</th>
      <th>video</th>
      <th>vote_average</th>
      <th>vote_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>False</td>
      <td>{'id': 10194, 'name': 'Toy Story Collection', ...</td>
      <td>30000000</td>
      <td>[{'id': 16, 'name': 'Animation'}, {'id': 35, '...</td>
      <td>http://toystory.disney.com/toy-story</td>
      <td>862</td>
      <td>tt0114709</td>
      <td>en</td>
      <td>Toy Story</td>
      <td>Led by Woody, Andy's toys live happily in his ...</td>
      <td>...</td>
      <td>1995-10-30</td>
      <td>373554033.0</td>
      <td>81.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>NaN</td>
      <td>Toy Story</td>
      <td>False</td>
      <td>7.7</td>
      <td>5415.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>False</td>
      <td>NaN</td>
      <td>65000000</td>
      <td>[{'id': 12, 'name': 'Adventure'}, {'id': 14, '...</td>
      <td>NaN</td>
      <td>8844</td>
      <td>tt0113497</td>
      <td>en</td>
      <td>Jumanji</td>
      <td>When siblings Judy and Peter discover an encha...</td>
      <td>...</td>
      <td>1995-12-15</td>
      <td>262797249.0</td>
      <td>104.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}, {'iso...</td>
      <td>Released</td>
      <td>Roll the dice and unleash the excitement!</td>
      <td>Jumanji</td>
      <td>False</td>
      <td>6.9</td>
      <td>2413.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>False</td>
      <td>{'id': 119050, 'name': 'Grumpy Old Men Collect...</td>
      <td>0</td>
      <td>[{'id': 10749, 'name': 'Romance'}, {'id': 35, ...</td>
      <td>NaN</td>
      <td>15602</td>
      <td>tt0113228</td>
      <td>en</td>
      <td>Grumpier Old Men</td>
      <td>A family wedding reignites the ancient feud be...</td>
      <td>...</td>
      <td>1995-12-22</td>
      <td>0.0</td>
      <td>101.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>Still Yelling. Still Fighting. Still Ready for...</td>
      <td>Grumpier Old Men</td>
      <td>False</td>
      <td>6.5</td>
      <td>92.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>False</td>
      <td>NaN</td>
      <td>16000000</td>
      <td>[{'id': 35, 'name': 'Comedy'}, {'id': 18, 'nam...</td>
      <td>NaN</td>
      <td>31357</td>
      <td>tt0114885</td>
      <td>en</td>
      <td>Waiting to Exhale</td>
      <td>Cheated on, mistreated and stepped on, the wom...</td>
      <td>...</td>
      <td>1995-12-22</td>
      <td>81452156.0</td>
      <td>127.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>Friends are the people who let you be yourself...</td>
      <td>Waiting to Exhale</td>
      <td>False</td>
      <td>6.1</td>
      <td>34.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>False</td>
      <td>{'id': 96871, 'name': 'Father of the Bride Col...</td>
      <td>0</td>
      <td>[{'id': 35, 'name': 'Comedy'}]</td>
      <td>NaN</td>
      <td>11862</td>
      <td>tt0113041</td>
      <td>en</td>
      <td>Father of the Bride Part II</td>
      <td>Just when George Banks has recovered from his ...</td>
      <td>...</td>
      <td>1995-02-10</td>
      <td>76578911.0</td>
      <td>106.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>Just When His World Is Back To Normal... He's ...</td>
      <td>Father of the Bride Part II</td>
      <td>False</td>
      <td>5.7</td>
      <td>173.0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 24 columns</p>
</div>




```python
meta
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>adult</th>
      <th>belongs_to_collection</th>
      <th>budget</th>
      <th>genres</th>
      <th>homepage</th>
      <th>id</th>
      <th>imdb_id</th>
      <th>original_language</th>
      <th>original_title</th>
      <th>overview</th>
      <th>...</th>
      <th>release_date</th>
      <th>revenue</th>
      <th>runtime</th>
      <th>spoken_languages</th>
      <th>status</th>
      <th>tagline</th>
      <th>title</th>
      <th>video</th>
      <th>vote_average</th>
      <th>vote_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>False</td>
      <td>{'id': 10194, 'name': 'Toy Story Collection', ...</td>
      <td>30000000</td>
      <td>[{'id': 16, 'name': 'Animation'}, {'id': 35, '...</td>
      <td>http://toystory.disney.com/toy-story</td>
      <td>862</td>
      <td>tt0114709</td>
      <td>en</td>
      <td>Toy Story</td>
      <td>Led by Woody, Andy's toys live happily in his ...</td>
      <td>...</td>
      <td>1995-10-30</td>
      <td>373554033.0</td>
      <td>81.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>NaN</td>
      <td>Toy Story</td>
      <td>False</td>
      <td>7.7</td>
      <td>5415.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>False</td>
      <td>NaN</td>
      <td>65000000</td>
      <td>[{'id': 12, 'name': 'Adventure'}, {'id': 14, '...</td>
      <td>NaN</td>
      <td>8844</td>
      <td>tt0113497</td>
      <td>en</td>
      <td>Jumanji</td>
      <td>When siblings Judy and Peter discover an encha...</td>
      <td>...</td>
      <td>1995-12-15</td>
      <td>262797249.0</td>
      <td>104.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}, {'iso...</td>
      <td>Released</td>
      <td>Roll the dice and unleash the excitement!</td>
      <td>Jumanji</td>
      <td>False</td>
      <td>6.9</td>
      <td>2413.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>False</td>
      <td>{'id': 119050, 'name': 'Grumpy Old Men Collect...</td>
      <td>0</td>
      <td>[{'id': 10749, 'name': 'Romance'}, {'id': 35, ...</td>
      <td>NaN</td>
      <td>15602</td>
      <td>tt0113228</td>
      <td>en</td>
      <td>Grumpier Old Men</td>
      <td>A family wedding reignites the ancient feud be...</td>
      <td>...</td>
      <td>1995-12-22</td>
      <td>0.0</td>
      <td>101.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>Still Yelling. Still Fighting. Still Ready for...</td>
      <td>Grumpier Old Men</td>
      <td>False</td>
      <td>6.5</td>
      <td>92.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>False</td>
      <td>NaN</td>
      <td>16000000</td>
      <td>[{'id': 35, 'name': 'Comedy'}, {'id': 18, 'nam...</td>
      <td>NaN</td>
      <td>31357</td>
      <td>tt0114885</td>
      <td>en</td>
      <td>Waiting to Exhale</td>
      <td>Cheated on, mistreated and stepped on, the wom...</td>
      <td>...</td>
      <td>1995-12-22</td>
      <td>81452156.0</td>
      <td>127.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>Friends are the people who let you be yourself...</td>
      <td>Waiting to Exhale</td>
      <td>False</td>
      <td>6.1</td>
      <td>34.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>False</td>
      <td>{'id': 96871, 'name': 'Father of the Bride Col...</td>
      <td>0</td>
      <td>[{'id': 35, 'name': 'Comedy'}]</td>
      <td>NaN</td>
      <td>11862</td>
      <td>tt0113041</td>
      <td>en</td>
      <td>Father of the Bride Part II</td>
      <td>Just when George Banks has recovered from his ...</td>
      <td>...</td>
      <td>1995-02-10</td>
      <td>76578911.0</td>
      <td>106.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>Just When His World Is Back To Normal... He's ...</td>
      <td>Father of the Bride Part II</td>
      <td>False</td>
      <td>5.7</td>
      <td>173.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>False</td>
      <td>NaN</td>
      <td>60000000</td>
      <td>[{'id': 28, 'name': 'Action'}, {'id': 80, 'nam...</td>
      <td>NaN</td>
      <td>949</td>
      <td>tt0113277</td>
      <td>en</td>
      <td>Heat</td>
      <td>Obsessive master thief, Neil McCauley leads a ...</td>
      <td>...</td>
      <td>1995-12-15</td>
      <td>187436818.0</td>
      <td>170.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}, {'iso...</td>
      <td>Released</td>
      <td>A Los Angeles Crime Saga</td>
      <td>Heat</td>
      <td>False</td>
      <td>7.7</td>
      <td>1886.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>False</td>
      <td>NaN</td>
      <td>58000000</td>
      <td>[{'id': 35, 'name': 'Comedy'}, {'id': 10749, '...</td>
      <td>NaN</td>
      <td>11860</td>
      <td>tt0114319</td>
      <td>en</td>
      <td>Sabrina</td>
      <td>An ugly duckling having undergone a remarkable...</td>
      <td>...</td>
      <td>1995-12-15</td>
      <td>0.0</td>
      <td>127.0</td>
      <td>[{'iso_639_1': 'fr', 'name': 'Français'}, {'is...</td>
      <td>Released</td>
      <td>You are cordially invited to the most surprisi...</td>
      <td>Sabrina</td>
      <td>False</td>
      <td>6.2</td>
      <td>141.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 28, 'name': 'Action'}, {'id': 12, 'nam...</td>
      <td>NaN</td>
      <td>45325</td>
      <td>tt0112302</td>
      <td>en</td>
      <td>Tom and Huck</td>
      <td>A mischievous young boy, Tom Sawyer, witnesses...</td>
      <td>...</td>
      <td>1995-12-22</td>
      <td>0.0</td>
      <td>97.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}, {'iso...</td>
      <td>Released</td>
      <td>The Original Bad Boys.</td>
      <td>Tom and Huck</td>
      <td>False</td>
      <td>5.4</td>
      <td>45.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>False</td>
      <td>NaN</td>
      <td>35000000</td>
      <td>[{'id': 28, 'name': 'Action'}, {'id': 12, 'nam...</td>
      <td>NaN</td>
      <td>9091</td>
      <td>tt0114576</td>
      <td>en</td>
      <td>Sudden Death</td>
      <td>International action superstar Jean Claude Van...</td>
      <td>...</td>
      <td>1995-12-22</td>
      <td>64350171.0</td>
      <td>106.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>Terror goes into overtime.</td>
      <td>Sudden Death</td>
      <td>False</td>
      <td>5.5</td>
      <td>174.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>False</td>
      <td>{'id': 645, 'name': 'James Bond Collection', '...</td>
      <td>58000000</td>
      <td>[{'id': 12, 'name': 'Adventure'}, {'id': 28, '...</td>
      <td>http://www.mgm.com/view/movie/757/Goldeneye/</td>
      <td>710</td>
      <td>tt0113189</td>
      <td>en</td>
      <td>GoldenEye</td>
      <td>James Bond must unmask the mysterious head of ...</td>
      <td>...</td>
      <td>1995-11-16</td>
      <td>352194034.0</td>
      <td>130.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}, {'iso...</td>
      <td>Released</td>
      <td>No limits. No fears. No substitutes.</td>
      <td>GoldenEye</td>
      <td>False</td>
      <td>6.6</td>
      <td>1194.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>False</td>
      <td>NaN</td>
      <td>62000000</td>
      <td>[{'id': 35, 'name': 'Comedy'}, {'id': 18, 'nam...</td>
      <td>NaN</td>
      <td>9087</td>
      <td>tt0112346</td>
      <td>en</td>
      <td>The American President</td>
      <td>Widowed U.S. president Andrew Shepherd, one of...</td>
      <td>...</td>
      <td>1995-11-17</td>
      <td>107879496.0</td>
      <td>106.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>Why can't the most powerful man in the world h...</td>
      <td>The American President</td>
      <td>False</td>
      <td>6.5</td>
      <td>199.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 35, 'name': 'Comedy'}, {'id': 27, 'nam...</td>
      <td>NaN</td>
      <td>12110</td>
      <td>tt0112896</td>
      <td>en</td>
      <td>Dracula: Dead and Loving It</td>
      <td>When a lawyer shows up at the vampire's doorst...</td>
      <td>...</td>
      <td>1995-12-22</td>
      <td>0.0</td>
      <td>88.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}, {'iso...</td>
      <td>Released</td>
      <td>NaN</td>
      <td>Dracula: Dead and Loving It</td>
      <td>False</td>
      <td>5.7</td>
      <td>210.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>False</td>
      <td>{'id': 117693, 'name': 'Balto Collection', 'po...</td>
      <td>0</td>
      <td>[{'id': 10751, 'name': 'Family'}, {'id': 16, '...</td>
      <td>NaN</td>
      <td>21032</td>
      <td>tt0112453</td>
      <td>en</td>
      <td>Balto</td>
      <td>An outcast half-wolf risks his life to prevent...</td>
      <td>...</td>
      <td>1995-12-22</td>
      <td>11348324.0</td>
      <td>78.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>Part Dog. Part Wolf. All Hero.</td>
      <td>Balto</td>
      <td>False</td>
      <td>7.1</td>
      <td>423.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>False</td>
      <td>NaN</td>
      <td>44000000</td>
      <td>[{'id': 36, 'name': 'History'}, {'id': 18, 'na...</td>
      <td>NaN</td>
      <td>10858</td>
      <td>tt0113987</td>
      <td>en</td>
      <td>Nixon</td>
      <td>An all-star cast powers this epic look at Amer...</td>
      <td>...</td>
      <td>1995-12-22</td>
      <td>13681765.0</td>
      <td>192.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>Triumphant in Victory, Bitter in Defeat. He Ch...</td>
      <td>Nixon</td>
      <td>False</td>
      <td>7.1</td>
      <td>72.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>False</td>
      <td>NaN</td>
      <td>98000000</td>
      <td>[{'id': 28, 'name': 'Action'}, {'id': 12, 'nam...</td>
      <td>NaN</td>
      <td>1408</td>
      <td>tt0112760</td>
      <td>en</td>
      <td>Cutthroat Island</td>
      <td>Morgan Adams and her slave, William Shaw, are ...</td>
      <td>...</td>
      <td>1995-12-22</td>
      <td>10017322.0</td>
      <td>119.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}, {'iso...</td>
      <td>Released</td>
      <td>The Course Has Been Set. There Is No Turning B...</td>
      <td>Cutthroat Island</td>
      <td>False</td>
      <td>5.7</td>
      <td>137.0</td>
    </tr>
    <tr>
      <th>15</th>
      <td>False</td>
      <td>NaN</td>
      <td>52000000</td>
      <td>[{'id': 18, 'name': 'Drama'}, {'id': 80, 'name...</td>
      <td>NaN</td>
      <td>524</td>
      <td>tt0112641</td>
      <td>en</td>
      <td>Casino</td>
      <td>The life of the gambling paradise – Las Vegas ...</td>
      <td>...</td>
      <td>1995-11-22</td>
      <td>116112375.0</td>
      <td>178.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>No one stays at the top forever.</td>
      <td>Casino</td>
      <td>False</td>
      <td>7.8</td>
      <td>1343.0</td>
    </tr>
    <tr>
      <th>16</th>
      <td>False</td>
      <td>NaN</td>
      <td>16500000</td>
      <td>[{'id': 18, 'name': 'Drama'}, {'id': 10749, 'n...</td>
      <td>NaN</td>
      <td>4584</td>
      <td>tt0114388</td>
      <td>en</td>
      <td>Sense and Sensibility</td>
      <td>Rich Mr. Dashwood dies, leaving his second wif...</td>
      <td>...</td>
      <td>1995-12-13</td>
      <td>135000000.0</td>
      <td>136.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>Lose your heart and come to your senses.</td>
      <td>Sense and Sensibility</td>
      <td>False</td>
      <td>7.2</td>
      <td>364.0</td>
    </tr>
    <tr>
      <th>17</th>
      <td>False</td>
      <td>NaN</td>
      <td>4000000</td>
      <td>[{'id': 80, 'name': 'Crime'}, {'id': 35, 'name...</td>
      <td>NaN</td>
      <td>5</td>
      <td>tt0113101</td>
      <td>en</td>
      <td>Four Rooms</td>
      <td>It's Ted the Bellhop's first night on the job....</td>
      <td>...</td>
      <td>1995-12-09</td>
      <td>4300000.0</td>
      <td>98.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>Twelve outrageous guests. Four scandalous requ...</td>
      <td>Four Rooms</td>
      <td>False</td>
      <td>6.5</td>
      <td>539.0</td>
    </tr>
    <tr>
      <th>18</th>
      <td>False</td>
      <td>{'id': 3167, 'name': 'Ace Ventura Collection',...</td>
      <td>30000000</td>
      <td>[{'id': 80, 'name': 'Crime'}, {'id': 35, 'name...</td>
      <td>NaN</td>
      <td>9273</td>
      <td>tt0112281</td>
      <td>en</td>
      <td>Ace Ventura: When Nature Calls</td>
      <td>Summoned from an ashram in Tibet, Ace finds hi...</td>
      <td>...</td>
      <td>1995-11-10</td>
      <td>212385533.0</td>
      <td>90.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>New animals. New adventures. Same hair.</td>
      <td>Ace Ventura: When Nature Calls</td>
      <td>False</td>
      <td>6.1</td>
      <td>1128.0</td>
    </tr>
    <tr>
      <th>19</th>
      <td>False</td>
      <td>NaN</td>
      <td>60000000</td>
      <td>[{'id': 28, 'name': 'Action'}, {'id': 35, 'nam...</td>
      <td>NaN</td>
      <td>11517</td>
      <td>tt0113845</td>
      <td>en</td>
      <td>Money Train</td>
      <td>A vengeful New York transit cop decides to ste...</td>
      <td>...</td>
      <td>1995-11-21</td>
      <td>35431113.0</td>
      <td>103.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>Get on, or GET OUT THE WAY!</td>
      <td>Money Train</td>
      <td>False</td>
      <td>5.4</td>
      <td>224.0</td>
    </tr>
    <tr>
      <th>20</th>
      <td>False</td>
      <td>{'id': 91698, 'name': 'Chili Palmer Collection...</td>
      <td>30250000</td>
      <td>[{'id': 35, 'name': 'Comedy'}, {'id': 53, 'nam...</td>
      <td>NaN</td>
      <td>8012</td>
      <td>tt0113161</td>
      <td>en</td>
      <td>Get Shorty</td>
      <td>Chili Palmer is a Miami mobster who gets sent ...</td>
      <td>...</td>
      <td>1995-10-20</td>
      <td>115101622.0</td>
      <td>105.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>The mob is tough, but it’s nothing like show b...</td>
      <td>Get Shorty</td>
      <td>False</td>
      <td>6.4</td>
      <td>305.0</td>
    </tr>
    <tr>
      <th>21</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 18, 'name': 'Drama'}, {'id': 53, 'name...</td>
      <td>NaN</td>
      <td>1710</td>
      <td>tt0112722</td>
      <td>en</td>
      <td>Copycat</td>
      <td>An agoraphobic psychologist and a female detec...</td>
      <td>...</td>
      <td>1995-10-27</td>
      <td>0.0</td>
      <td>124.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}, {'iso...</td>
      <td>Released</td>
      <td>One man is copying the most notorious killers ...</td>
      <td>Copycat</td>
      <td>False</td>
      <td>6.5</td>
      <td>199.0</td>
    </tr>
    <tr>
      <th>22</th>
      <td>False</td>
      <td>NaN</td>
      <td>50000000</td>
      <td>[{'id': 28, 'name': 'Action'}, {'id': 12, 'nam...</td>
      <td>NaN</td>
      <td>9691</td>
      <td>tt0112401</td>
      <td>en</td>
      <td>Assassins</td>
      <td>Assassin Robert Rath arrives at a funeral to k...</td>
      <td>...</td>
      <td>1995-10-06</td>
      <td>30303072.0</td>
      <td>132.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}, {'iso...</td>
      <td>Released</td>
      <td>In the shadows of life, In the business of dea...</td>
      <td>Assassins</td>
      <td>False</td>
      <td>6.0</td>
      <td>394.0</td>
    </tr>
    <tr>
      <th>23</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 18, 'name': 'Drama'}, {'id': 14, 'name...</td>
      <td>NaN</td>
      <td>12665</td>
      <td>tt0114168</td>
      <td>en</td>
      <td>Powder</td>
      <td>Harassed by classmates who won't accept his sh...</td>
      <td>...</td>
      <td>1995-10-27</td>
      <td>0.0</td>
      <td>111.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>An extraordinary encounter with another human ...</td>
      <td>Powder</td>
      <td>False</td>
      <td>6.3</td>
      <td>143.0</td>
    </tr>
    <tr>
      <th>24</th>
      <td>False</td>
      <td>NaN</td>
      <td>3600000</td>
      <td>[{'id': 18, 'name': 'Drama'}, {'id': 10749, 'n...</td>
      <td>http://www.mgm.com/title_title.do?title_star=L...</td>
      <td>451</td>
      <td>tt0113627</td>
      <td>en</td>
      <td>Leaving Las Vegas</td>
      <td>Ben Sanderson, an alcoholic Hollywood screenwr...</td>
      <td>...</td>
      <td>1995-10-27</td>
      <td>49800000.0</td>
      <td>112.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>I Love You... The Way You Are.</td>
      <td>Leaving Las Vegas</td>
      <td>False</td>
      <td>7.1</td>
      <td>365.0</td>
    </tr>
    <tr>
      <th>25</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 18, 'name': 'Drama'}]</td>
      <td>NaN</td>
      <td>16420</td>
      <td>tt0114057</td>
      <td>en</td>
      <td>Othello</td>
      <td>The evil Iago pretends to be friend of Othello...</td>
      <td>...</td>
      <td>1995-12-15</td>
      <td>0.0</td>
      <td>123.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>Envy, greed, jealousy and love.</td>
      <td>Othello</td>
      <td>False</td>
      <td>7.0</td>
      <td>33.0</td>
    </tr>
    <tr>
      <th>26</th>
      <td>False</td>
      <td>NaN</td>
      <td>12000000</td>
      <td>[{'id': 35, 'name': 'Comedy'}, {'id': 18, 'nam...</td>
      <td>NaN</td>
      <td>9263</td>
      <td>tt0114011</td>
      <td>en</td>
      <td>Now and Then</td>
      <td>Waxing nostalgic about the bittersweet passage...</td>
      <td>...</td>
      <td>1995-10-20</td>
      <td>27400000.0</td>
      <td>100.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>In every woman there is the girl she left behind.</td>
      <td>Now and Then</td>
      <td>False</td>
      <td>6.6</td>
      <td>91.0</td>
    </tr>
    <tr>
      <th>27</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 18, 'name': 'Drama'}, {'id': 10749, 'n...</td>
      <td>NaN</td>
      <td>17015</td>
      <td>tt0114117</td>
      <td>en</td>
      <td>Persuasion</td>
      <td>This film adaptation of Jane Austen's last nov...</td>
      <td>...</td>
      <td>1995-09-27</td>
      <td>0.0</td>
      <td>104.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>NaN</td>
      <td>Persuasion</td>
      <td>False</td>
      <td>7.4</td>
      <td>36.0</td>
    </tr>
    <tr>
      <th>28</th>
      <td>False</td>
      <td>NaN</td>
      <td>18000000</td>
      <td>[{'id': 14, 'name': 'Fantasy'}, {'id': 878, 'n...</td>
      <td>NaN</td>
      <td>902</td>
      <td>tt0112682</td>
      <td>fr</td>
      <td>La Cité des Enfants Perdus</td>
      <td>A scientist in a surrealist society kidnaps ch...</td>
      <td>...</td>
      <td>1995-05-16</td>
      <td>1738611.0</td>
      <td>108.0</td>
      <td>[{'iso_639_1': 'cn', 'name': '广州话 / 廣州話'}, {'i...</td>
      <td>Released</td>
      <td>Where happily ever after is just a dream.</td>
      <td>The City of Lost Children</td>
      <td>False</td>
      <td>7.6</td>
      <td>308.0</td>
    </tr>
    <tr>
      <th>29</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 18, 'name': 'Drama'}, {'id': 80, 'name...</td>
      <td>NaN</td>
      <td>37557</td>
      <td>tt0115012</td>
      <td>zh</td>
      <td>摇啊摇，摇到外婆桥</td>
      <td>A provincial boy related to a Shanghai crime f...</td>
      <td>...</td>
      <td>1995-04-30</td>
      <td>0.0</td>
      <td>108.0</td>
      <td>[{'iso_639_1': 'zh', 'name': '普通话'}]</td>
      <td>Released</td>
      <td>In 1930's Shanghai violence was not the proble...</td>
      <td>Shanghai Triad</td>
      <td>False</td>
      <td>6.5</td>
      <td>17.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>45436</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 28, 'name': 'Action'}, {'id': 9648, 'n...</td>
      <td>NaN</td>
      <td>45527</td>
      <td>tt1331329</td>
      <td>en</td>
      <td>The Final Storm</td>
      <td>A stranger named Silas flees from a devastatin...</td>
      <td>...</td>
      <td>2010-01-01</td>
      <td>0.0</td>
      <td>92.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>Action, Horror</td>
      <td>The Final Storm</td>
      <td>False</td>
      <td>3.7</td>
      <td>11.0</td>
    </tr>
    <tr>
      <th>45437</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 10751, 'name': 'Family'}, {'id': 16, '...</td>
      <td>NaN</td>
      <td>455661</td>
      <td>tt6969946</td>
      <td>en</td>
      <td>In a Heartbeat</td>
      <td>A closeted boy runs the risk of being outed by...</td>
      <td>...</td>
      <td>2017-06-01</td>
      <td>0.0</td>
      <td>4.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>The Heart Wants What The Heart Wants</td>
      <td>In a Heartbeat</td>
      <td>False</td>
      <td>8.3</td>
      <td>146.0</td>
    </tr>
    <tr>
      <th>45438</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 18, 'name': 'Drama'}]</td>
      <td>NaN</td>
      <td>327237</td>
      <td>tt3814486</td>
      <td>nl</td>
      <td>Bloed, Zweet en Tranen</td>
      <td>Bloed, Zweet en Tranen (Blood, Sweat and Tears...</td>
      <td>...</td>
      <td>2015-04-02</td>
      <td>0.0</td>
      <td>111.0</td>
      <td>[{'iso_639_1': 'nl', 'name': 'Nederlands'}]</td>
      <td>Released</td>
      <td>The movie about Andre Hazes</td>
      <td>Blood, Sweat and Tears</td>
      <td>False</td>
      <td>6.8</td>
      <td>11.0</td>
    </tr>
    <tr>
      <th>45439</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 18, 'name': 'Drama'}, {'id': 14, 'name...</td>
      <td>NaN</td>
      <td>84710</td>
      <td>tt0036975</td>
      <td>en</td>
      <td>Jungle Woman</td>
      <td>Paula the ape woman (Acquanetta) is alive and ...</td>
      <td>...</td>
      <td>1944-06-01</td>
      <td>0.0</td>
      <td>61.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>RAPTUROUS BEAUTY!...FURY OF A BEAST!</td>
      <td>Jungle Woman</td>
      <td>False</td>
      <td>5.8</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>45440</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 18, 'name': 'Drama'}, {'id': 10751, 'n...</td>
      <td>NaN</td>
      <td>39562</td>
      <td>tt0889600</td>
      <td>en</td>
      <td>To Be Fat Like Me</td>
      <td>Pretty, popular, and slim high-schooler Aly Sc...</td>
      <td>...</td>
      <td>2007-01-08</td>
      <td>0.0</td>
      <td>89.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>NaN</td>
      <td>To Be Fat Like Me</td>
      <td>False</td>
      <td>5.0</td>
      <td>12.0</td>
    </tr>
    <tr>
      <th>45441</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 35, 'name': 'Comedy'}]</td>
      <td>NaN</td>
      <td>14008</td>
      <td>tt0294425</td>
      <td>en</td>
      <td>Cadet Kelly</td>
      <td>Hyperactive teenager Kelly is enrolled into a ...</td>
      <td>...</td>
      <td>2002-03-07</td>
      <td>0.0</td>
      <td>101.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>Too Cool For The Rules!</td>
      <td>Cadet Kelly</td>
      <td>False</td>
      <td>5.2</td>
      <td>145.0</td>
    </tr>
    <tr>
      <th>45442</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[]</td>
      <td>NaN</td>
      <td>44330</td>
      <td>tt0135690</td>
      <td>en</td>
      <td>Le tripot clandestin</td>
      <td>A combination gambling den and bawdy house is ...</td>
      <td>...</td>
      <td>1905-01-01</td>
      <td>0.0</td>
      <td>3.0</td>
      <td>[]</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>The Scheming Gambler's Paradise</td>
      <td>False</td>
      <td>5.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>45443</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 35, 'name': 'Comedy'}, {'id': 14, 'nam...</td>
      <td>NaN</td>
      <td>49279</td>
      <td>tt0000359</td>
      <td>fr</td>
      <td>L'Homme à la tête de caoutchouc</td>
      <td>A chemist in his laboratory places upon a tabl...</td>
      <td>...</td>
      <td>1901-01-01</td>
      <td>0.0</td>
      <td>3.0</td>
      <td>[]</td>
      <td>Released</td>
      <td>NaN</td>
      <td>The Man with the Rubber Head</td>
      <td>False</td>
      <td>7.6</td>
      <td>29.0</td>
    </tr>
    <tr>
      <th>45444</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 14, 'name': 'Fantasy'}]</td>
      <td>NaN</td>
      <td>44333</td>
      <td>tt0135179</td>
      <td>fr</td>
      <td>Les cartes vivantes</td>
      <td>A bearded magician holds up a large playing ca...</td>
      <td>...</td>
      <td>1905-01-01</td>
      <td>0.0</td>
      <td>3.0</td>
      <td>[{'iso_639_1': 'xx', 'name': 'No Language'}]</td>
      <td>Released</td>
      <td>NaN</td>
      <td>The Living Playing Cards</td>
      <td>False</td>
      <td>6.1</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>45445</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 14, 'name': 'Fantasy'}, {'id': 35, 'na...</td>
      <td>NaN</td>
      <td>49277</td>
      <td>tt0135122</td>
      <td>en</td>
      <td>Les affiches en goguette</td>
      <td>A wall full of advertising posters comes to life.</td>
      <td>...</td>
      <td>1906-01-01</td>
      <td>0.0</td>
      <td>3.0</td>
      <td>[{'iso_639_1': 'fr', 'name': 'Français'}, {'is...</td>
      <td>Released</td>
      <td>NaN</td>
      <td>The Hilarious Posters</td>
      <td>False</td>
      <td>4.5</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>45446</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 14, 'name': 'Fantasy'}, {'id': 35, 'na...</td>
      <td>NaN</td>
      <td>49271</td>
      <td>tt0127948</td>
      <td>en</td>
      <td>Le locataire diabolique</td>
      <td>A man rents an apartment and furnishes it in r...</td>
      <td>...</td>
      <td>1909-01-01</td>
      <td>0.0</td>
      <td>6.0</td>
      <td>[]</td>
      <td>Released</td>
      <td>NaN</td>
      <td>The Devilish Tenant</td>
      <td>False</td>
      <td>6.7</td>
      <td>12.0</td>
    </tr>
    <tr>
      <th>45447</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[]</td>
      <td>NaN</td>
      <td>44324</td>
      <td>tt0135631</td>
      <td>fr</td>
      <td>Le Roi du maquillage</td>
      <td>The background of this picture represents a sc...</td>
      <td>...</td>
      <td>1904-03-05</td>
      <td>0.0</td>
      <td>3.0</td>
      <td>[]</td>
      <td>Released</td>
      <td>NaN</td>
      <td>The Untameable Whiskers</td>
      <td>False</td>
      <td>6.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>45448</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[]</td>
      <td>NaN</td>
      <td>122036</td>
      <td>tt0224286</td>
      <td>fr</td>
      <td>Les Transmutations imperceptibles</td>
      <td>This shows a prince entering upon the stage of...</td>
      <td>...</td>
      <td>1904-01-01</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>[]</td>
      <td>Released</td>
      <td>NaN</td>
      <td>The Imperceptable Transmutations</td>
      <td>False</td>
      <td>5.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>45449</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 16, 'name': 'Animation'}, {'id': 10751...</td>
      <td>NaN</td>
      <td>14885</td>
      <td>tt0457437</td>
      <td>en</td>
      <td>Pooh's Heffalump Halloween Movie</td>
      <td>It's Halloween in the 100 Acre Wood, and Roo's...</td>
      <td>...</td>
      <td>2005-09-13</td>
      <td>0.0</td>
      <td>67.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>Celebrate Lumpy's First Halloween.</td>
      <td>Pooh's Heffalump Halloween Movie</td>
      <td>False</td>
      <td>5.4</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>45450</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 14, 'name': 'Fantasy'}, {'id': 28, 'na...</td>
      <td>NaN</td>
      <td>49280</td>
      <td>tt0135453</td>
      <td>fr</td>
      <td>L'Homme orchestre</td>
      <td>A band-leader has arranged seven chairs for th...</td>
      <td>...</td>
      <td>1900-01-01</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>[{'iso_639_1': 'xx', 'name': 'No Language'}]</td>
      <td>Released</td>
      <td>NaN</td>
      <td>The One-Man Band</td>
      <td>False</td>
      <td>6.5</td>
      <td>22.0</td>
    </tr>
    <tr>
      <th>45451</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 35, 'name': 'Comedy'}, {'id': 14, 'nam...</td>
      <td>NaN</td>
      <td>106807</td>
      <td>tt0135571</td>
      <td>fr</td>
      <td>Nouvelles luttes extravagantes</td>
      <td>A series of fantastical wrestling matches.</td>
      <td>...</td>
      <td>1900-01-01</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>[{'iso_639_1': 'xx', 'name': 'No Language'}]</td>
      <td>Released</td>
      <td>NaN</td>
      <td>The Fat and Lean Wrestling Match</td>
      <td>False</td>
      <td>6.5</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>45452</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 99, 'name': 'Documentary'}]</td>
      <td>NaN</td>
      <td>276895</td>
      <td>tt3054038</td>
      <td>en</td>
      <td>Deep Hearts</td>
      <td>Deep Hearts is a film about the Bororo Fulani,...</td>
      <td>...</td>
      <td>1981-01-01</td>
      <td>0.0</td>
      <td>58.0</td>
      <td>[{'iso_639_1': 'ff', 'name': 'Fulfulde'}, {'is...</td>
      <td>Released</td>
      <td>NaN</td>
      <td>Deep Hearts</td>
      <td>False</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>45453</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 80, 'name': 'Crime'}, {'id': 18, 'name...</td>
      <td>NaN</td>
      <td>404604</td>
      <td>tt5690142</td>
      <td>hi</td>
      <td>Maa</td>
      <td>The bliss of a biology teacher’s family life i...</td>
      <td>...</td>
      <td>2017-07-07</td>
      <td>0.0</td>
      <td>146.0</td>
      <td>[{'iso_639_1': 'hi', 'name': 'हिन्दी'}]</td>
      <td>Released</td>
      <td>NaN</td>
      <td>Mom</td>
      <td>False</td>
      <td>6.6</td>
      <td>14.0</td>
    </tr>
    <tr>
      <th>45454</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 35, 'name': 'Comedy'}, {'id': 18, 'nam...</td>
      <td>NaN</td>
      <td>420346</td>
      <td>tt4130180</td>
      <td>en</td>
      <td>The Morning After</td>
      <td>The Morning After is a feature film that consi...</td>
      <td>...</td>
      <td>2015-01-11</td>
      <td>0.0</td>
      <td>79.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>What happened last night?</td>
      <td>The Morning After</td>
      <td>False</td>
      <td>4.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>45455</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[]</td>
      <td>NaN</td>
      <td>67179</td>
      <td>tt0069215</td>
      <td>it</td>
      <td>San Michele aveva un gallo</td>
      <td>Sentenced to life imprisonment for illegal act...</td>
      <td>...</td>
      <td>1972-01-01</td>
      <td>0.0</td>
      <td>90.0</td>
      <td>[{'iso_639_1': 'it', 'name': 'Italiano'}]</td>
      <td>Released</td>
      <td>NaN</td>
      <td>St. Michael Had a Rooster</td>
      <td>False</td>
      <td>6.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>45456</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 27, 'name': 'Horror'}, {'id': 9648, 'n...</td>
      <td>NaN</td>
      <td>84419</td>
      <td>tt0038621</td>
      <td>en</td>
      <td>House of Horrors</td>
      <td>An unsuccessful sculptor saves a madman named ...</td>
      <td>...</td>
      <td>1946-03-29</td>
      <td>0.0</td>
      <td>65.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>Meet...The CREEPER!</td>
      <td>House of Horrors</td>
      <td>False</td>
      <td>6.3</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>45457</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 9648, 'name': 'Mystery'}, {'id': 27, '...</td>
      <td>NaN</td>
      <td>390959</td>
      <td>tt0265736</td>
      <td>en</td>
      <td>Shadow of the Blair Witch</td>
      <td>In this true-crime documentary, we delve into ...</td>
      <td>...</td>
      <td>2000-10-22</td>
      <td>0.0</td>
      <td>45.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>NaN</td>
      <td>Shadow of the Blair Witch</td>
      <td>False</td>
      <td>7.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>45458</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 27, 'name': 'Horror'}]</td>
      <td>NaN</td>
      <td>289923</td>
      <td>tt0252966</td>
      <td>en</td>
      <td>The Burkittsville 7</td>
      <td>A film archivist revisits the story of Rustin ...</td>
      <td>...</td>
      <td>2000-10-03</td>
      <td>0.0</td>
      <td>30.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>Do you know what happened 50 years before "The...</td>
      <td>The Burkittsville 7</td>
      <td>False</td>
      <td>7.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>45459</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 878, 'name': 'Science Fiction'}]</td>
      <td>NaN</td>
      <td>222848</td>
      <td>tt0112613</td>
      <td>en</td>
      <td>Caged Heat 3000</td>
      <td>It's the year 3000 AD. The world's most danger...</td>
      <td>...</td>
      <td>1995-01-01</td>
      <td>0.0</td>
      <td>85.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>NaN</td>
      <td>Caged Heat 3000</td>
      <td>False</td>
      <td>3.5</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>45460</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 18, 'name': 'Drama'}, {'id': 28, 'name...</td>
      <td>NaN</td>
      <td>30840</td>
      <td>tt0102797</td>
      <td>en</td>
      <td>Robin Hood</td>
      <td>Yet another version of the classic epic, with ...</td>
      <td>...</td>
      <td>1991-05-13</td>
      <td>0.0</td>
      <td>104.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>NaN</td>
      <td>Robin Hood</td>
      <td>False</td>
      <td>5.7</td>
      <td>26.0</td>
    </tr>
    <tr>
      <th>45461</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 18, 'name': 'Drama'}, {'id': 10751, 'n...</td>
      <td>http://www.imdb.com/title/tt6209470/</td>
      <td>439050</td>
      <td>tt6209470</td>
      <td>fa</td>
      <td>رگ خواب</td>
      <td>Rising and falling between a man and woman.</td>
      <td>...</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>90.0</td>
      <td>[{'iso_639_1': 'fa', 'name': 'فارسی'}]</td>
      <td>Released</td>
      <td>Rising and falling between a man and woman</td>
      <td>Subdue</td>
      <td>False</td>
      <td>4.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>45462</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 18, 'name': 'Drama'}]</td>
      <td>NaN</td>
      <td>111109</td>
      <td>tt2028550</td>
      <td>tl</td>
      <td>Siglo ng Pagluluwal</td>
      <td>An artist struggles to finish his work while a...</td>
      <td>...</td>
      <td>2011-11-17</td>
      <td>0.0</td>
      <td>360.0</td>
      <td>[{'iso_639_1': 'tl', 'name': ''}]</td>
      <td>Released</td>
      <td>NaN</td>
      <td>Century of Birthing</td>
      <td>False</td>
      <td>9.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>45463</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[{'id': 28, 'name': 'Action'}, {'id': 18, 'nam...</td>
      <td>NaN</td>
      <td>67758</td>
      <td>tt0303758</td>
      <td>en</td>
      <td>Betrayal</td>
      <td>When one of her hits goes wrong, a professiona...</td>
      <td>...</td>
      <td>2003-08-01</td>
      <td>0.0</td>
      <td>90.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>A deadly game of wits.</td>
      <td>Betrayal</td>
      <td>False</td>
      <td>3.8</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>45464</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[]</td>
      <td>NaN</td>
      <td>227506</td>
      <td>tt0008536</td>
      <td>en</td>
      <td>Satana likuyushchiy</td>
      <td>In a small town live two brothers, one a minis...</td>
      <td>...</td>
      <td>1917-10-21</td>
      <td>0.0</td>
      <td>87.0</td>
      <td>[]</td>
      <td>Released</td>
      <td>NaN</td>
      <td>Satan Triumphant</td>
      <td>False</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>45465</th>
      <td>False</td>
      <td>NaN</td>
      <td>0</td>
      <td>[]</td>
      <td>NaN</td>
      <td>461257</td>
      <td>tt6980792</td>
      <td>en</td>
      <td>Queerama</td>
      <td>50 years after decriminalisation of homosexual...</td>
      <td>...</td>
      <td>2017-06-09</td>
      <td>0.0</td>
      <td>75.0</td>
      <td>[{'iso_639_1': 'en', 'name': 'English'}]</td>
      <td>Released</td>
      <td>NaN</td>
      <td>Queerama</td>
      <td>False</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>45466 rows × 24 columns</p>
</div>



#### 我们只需要电影的id和名字


```python
meta.loc[:,["id","origial_language","original_title"]].head()
```

    D:\anaconda2\lib\site-packages\pandas\core\indexing.py:1472: FutureWarning: 
    Passing list-likes to .loc or [] with any missing label will raise
    KeyError in the future, you can use .reindex() as an alternative.
    
    See the documentation here:
    https://pandas.pydata.org/pandas-docs/stable/indexing.html#deprecate-loc-reindex-listlike
      return self._getitem_tuple(key)
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>origial_language</th>
      <th>original_title</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>862</td>
      <td>NaN</td>
      <td>Toy Story</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8844</td>
      <td>NaN</td>
      <td>Jumanji</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15602</td>
      <td>NaN</td>
      <td>Grumpier Old Men</td>
    </tr>
    <tr>
      <th>3</th>
      <td>31357</td>
      <td>NaN</td>
      <td>Waiting to Exhale</td>
    </tr>
    <tr>
      <th>4</th>
      <td>11862</td>
      <td>NaN</td>
      <td>Father of the Bride Part II</td>
    </tr>
  </tbody>
</table>
</div>




```python
movie_title=meta[["id","original_language","original_title"]]
movie_title.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>original_language</th>
      <th>original_title</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>862</td>
      <td>en</td>
      <td>Toy Story</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8844</td>
      <td>en</td>
      <td>Jumanji</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15602</td>
      <td>en</td>
      <td>Grumpier Old Men</td>
    </tr>
    <tr>
      <th>3</th>
      <td>31357</td>
      <td>en</td>
      <td>Waiting to Exhale</td>
    </tr>
    <tr>
      <th>4</th>
      <td>11862</td>
      <td>en</td>
      <td>Father of the Bride Part II</td>
    </tr>
  </tbody>
</table>
</div>




```python
print(movie_title.shape)
print(ratings_mean.shape)
```

    (45466, 3)
    (9066, 2)
    

#### 在处理实际数据的时候，经常容易碰到脏数据，而怎么样处理脏数据其实就需要根据实际情况来决定了。


```python
for i in range(movie_title.shape[0]):
    try:
        id = int(movie_title.loc[i, "id"])
    except ValueError:
        movie_title.loc[i, "id"] = 99999999999999
```

    D:\anaconda2\lib\site-packages\pandas\core\indexing.py:189: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      self._setitem_with_indexer(indexer, value)
    D:\anaconda2\lib\site-packages\ipykernel_launcher.py:5: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      """
    


```python
movie_title.loc[:, "id"] = pd.to_numeric(movie_title.loc[:, "id"])
```

    D:\anaconda2\lib\site-packages\pandas\core\indexing.py:630: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      self.obj[item_labels[indexer[info_axis]]] = value
    


```python
ratings_mean.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>rating</th>
      <th>count</th>
    </tr>
    <tr>
      <th>movieId</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>3.872470</td>
      <td>247</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.401869</td>
      <td>107</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3.161017</td>
      <td>59</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2.384615</td>
      <td>13</td>
    </tr>
    <tr>
      <th>5</th>
      <td>3.267857</td>
      <td>56</td>
    </tr>
  </tbody>
</table>
</div>




```python
movie_title.head()
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-3-0d7606f969db> in <module>()
    ----> 1 movie_title.head()
    

    NameError: name 'movie_title' is not defined



```python
movie_name_ratings = pd.merge(ratings_mean, movie_title, how="inner", left_index=True, right_on="id")
movie_name_ratings.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>rating</th>
      <th>count</th>
      <th>id</th>
      <th>original_language</th>
      <th>original_title</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4342</th>
      <td>3.401869</td>
      <td>107</td>
      <td>2</td>
      <td>fi</td>
      <td>Ariel</td>
    </tr>
    <tr>
      <th>12947</th>
      <td>3.161017</td>
      <td>59</td>
      <td>3</td>
      <td>fi</td>
      <td>Varjoja paratiisissa</td>
    </tr>
    <tr>
      <th>17</th>
      <td>3.267857</td>
      <td>56</td>
      <td>5</td>
      <td>en</td>
      <td>Four Rooms</td>
    </tr>
    <tr>
      <th>474</th>
      <td>3.884615</td>
      <td>104</td>
      <td>6</td>
      <td>en</td>
      <td>Judgment Night</td>
    </tr>
    <tr>
      <th>256</th>
      <td>3.689024</td>
      <td>82</td>
      <td>11</td>
      <td>en</td>
      <td>Star Wars</td>
    </tr>
  </tbody>
</table>
</div>




```python
movie_name_ratings.sort_values(by=["count","rating"],ascending=False).head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>rating</th>
      <th>count</th>
      <th>id</th>
      <th>original_language</th>
      <th>original_title</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6388</th>
      <td>4.256173</td>
      <td>324</td>
      <td>296</td>
      <td>en</td>
      <td>Terminator 3: Rise of the Machines</td>
    </tr>
    <tr>
      <th>4020</th>
      <td>4.487138</td>
      <td>311</td>
      <td>318</td>
      <td>en</td>
      <td>The Million Dollar Hotel</td>
    </tr>
    <tr>
      <th>3382</th>
      <td>4.138158</td>
      <td>304</td>
      <td>593</td>
      <td>ru</td>
      <td>Солярис</td>
    </tr>
    <tr>
      <th>938</th>
      <td>4.221649</td>
      <td>291</td>
      <td>260</td>
      <td>en</td>
      <td>The 39 Steps</td>
    </tr>
    <tr>
      <th>5004</th>
      <td>3.706204</td>
      <td>274</td>
      <td>480</td>
      <td>hi</td>
      <td>Monsoon Wedding</td>
    </tr>
  </tbody>
</table>
</div>



###  项目2 bikes

处理实际数据的时候，很多时候时间都花在处理脏数据上。

我们来尝试一个例子，读取一些自行车的数据。

bikes.csv记录了Montreal自行车路线的数据，具体有7条路线，分别记录了每条自行车路线每天有多少人经过。


```python
!head -5../Anaconda3/bikes.csv
```

    'head' is not recognized as an internal or external command,
    operable program or batch file.
    


```python
import pandas as pd
bikes=pd.read_csv("../Anaconda3/bikes.csv")
```


    ---------------------------------------------------------------------------

    UnicodeDecodeError                        Traceback (most recent call last)

    <ipython-input-2-0f82c8c47abd> in <module>()
          1 import pandas as pd
    ----> 2 bikes=pd.read_csv("../Anaconda3/bikes.csv")
    

    D:\anaconda2\lib\site-packages\pandas\io\parsers.py in parser_f(filepath_or_buffer, sep, delimiter, header, names, index_col, usecols, squeeze, prefix, mangle_dupe_cols, dtype, engine, converters, true_values, false_values, skipinitialspace, skiprows, nrows, na_values, keep_default_na, na_filter, verbose, skip_blank_lines, parse_dates, infer_datetime_format, keep_date_col, date_parser, dayfirst, iterator, chunksize, compression, thousands, decimal, lineterminator, quotechar, quoting, escapechar, comment, encoding, dialect, tupleize_cols, error_bad_lines, warn_bad_lines, skipfooter, doublequote, delim_whitespace, low_memory, memory_map, float_precision)
        676                     skip_blank_lines=skip_blank_lines)
        677 
    --> 678         return _read(filepath_or_buffer, kwds)
        679 
        680     parser_f.__name__ = name
    

    D:\anaconda2\lib\site-packages\pandas\io\parsers.py in _read(filepath_or_buffer, kwds)
        438 
        439     # Create the parser.
    --> 440     parser = TextFileReader(filepath_or_buffer, **kwds)
        441 
        442     if chunksize or iterator:
    

    D:\anaconda2\lib\site-packages\pandas\io\parsers.py in __init__(self, f, engine, **kwds)
        785             self.options['has_index_names'] = kwds['has_index_names']
        786 
    --> 787         self._make_engine(self.engine)
        788 
        789     def close(self):
    

    D:\anaconda2\lib\site-packages\pandas\io\parsers.py in _make_engine(self, engine)
       1012     def _make_engine(self, engine='c'):
       1013         if engine == 'c':
    -> 1014             self._engine = CParserWrapper(self.f, **self.options)
       1015         else:
       1016             if engine == 'python':
    

    D:\anaconda2\lib\site-packages\pandas\io\parsers.py in __init__(self, src, **kwds)
       1706         kwds['usecols'] = self.usecols
       1707 
    -> 1708         self._reader = parsers.TextReader(src, **kwds)
       1709 
       1710         passed_names = self.names is None
    

    pandas\_libs\parsers.pyx in pandas._libs.parsers.TextReader.__cinit__()
    

    pandas\_libs\parsers.pyx in pandas._libs.parsers.TextReader._get_header()
    

    UnicodeDecodeError: 'utf-8' codec can't decode byte 0xe9 in position 15: invalid continuation byte



```python
import pandas as pd
bikes=pd.read_csv("../Anaconda3/bikes.csv",encoding="latin-1")
bikes.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date;Berri 1;Brébeuf (données non disponibles);Côte-Sainte-Catherine;Maisonneuve 1;Maisonneuve 2;du Parc;Pierre-Dupuy;Rachel1;St-Urbain (données non disponibles)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01/01/2012;35;;0;38;51;26;10;16;</td>
    </tr>
    <tr>
      <th>1</th>
      <td>02/01/2012;83;;1;68;153;53;6;43;</td>
    </tr>
    <tr>
      <th>2</th>
      <td>03/01/2012;135;;2;104;248;89;3;58;</td>
    </tr>
    <tr>
      <th>3</th>
      <td>04/01/2012;144;;1;116;318;111;8;61;</td>
    </tr>
    <tr>
      <th>4</th>
      <td>05/01/2012;197;;2;124;330;97;13;95;</td>
    </tr>
  </tbody>
</table>
</div>




```python
import pandas as pd
bikes=pd.read_csv("../Anaconda3/bikes.csv",sep=";",parse_dates=["Date"],encoding="latin-1",dayfirst=True,index_col=["Date"])
bikes.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Berri 1</th>
      <th>Brébeuf (données non disponibles)</th>
      <th>Côte-Sainte-Catherine</th>
      <th>Maisonneuve 1</th>
      <th>Maisonneuve 2</th>
      <th>du Parc</th>
      <th>Pierre-Dupuy</th>
      <th>Rachel1</th>
      <th>St-Urbain (données non disponibles)</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
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
      <th>2012-01-01</th>
      <td>35</td>
      <td>NaN</td>
      <td>0</td>
      <td>38</td>
      <td>51</td>
      <td>26</td>
      <td>10</td>
      <td>16</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2012-01-02</th>
      <td>83</td>
      <td>NaN</td>
      <td>1</td>
      <td>68</td>
      <td>153</td>
      <td>53</td>
      <td>6</td>
      <td>43</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2012-01-03</th>
      <td>135</td>
      <td>NaN</td>
      <td>2</td>
      <td>104</td>
      <td>248</td>
      <td>89</td>
      <td>3</td>
      <td>58</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2012-01-04</th>
      <td>144</td>
      <td>NaN</td>
      <td>1</td>
      <td>116</td>
      <td>318</td>
      <td>111</td>
      <td>8</td>
      <td>61</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2012-01-05</th>
      <td>197</td>
      <td>NaN</td>
      <td>2</td>
      <td>124</td>
      <td>330</td>
      <td>97</td>
      <td>13</td>
      <td>95</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
bikes.shape
```




    (310, 9)




```python
bikes.info()
```

    <class 'pandas.core.frame.DataFrame'>
    DatetimeIndex: 310 entries, 2012-01-01 to 2012-11-05
    Data columns (total 9 columns):
    Berri 1                                310 non-null int64
    Brébeuf (données non disponibles)      0 non-null float64
    Côte-Sainte-Catherine                  310 non-null int64
    Maisonneuve 1                          310 non-null int64
    Maisonneuve 2                          310 non-null int64
    du Parc                                310 non-null int64
    Pierre-Dupuy                           310 non-null int64
    Rachel1                                310 non-null int64
    St-Urbain (données non disponibles)    0 non-null float64
    dtypes: float64(2), int64(7)
    memory usage: 24.2 KB
    


```python
bikes.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Berri 1</th>
      <th>Brébeuf (données non disponibles)</th>
      <th>Côte-Sainte-Catherine</th>
      <th>Maisonneuve 1</th>
      <th>Maisonneuve 2</th>
      <th>du Parc</th>
      <th>Pierre-Dupuy</th>
      <th>Rachel1</th>
      <th>St-Urbain (données non disponibles)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>310.000000</td>
      <td>0.0</td>
      <td>310.000000</td>
      <td>310.000000</td>
      <td>310.000000</td>
      <td>310.000000</td>
      <td>310.000000</td>
      <td>310.000000</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>2985.048387</td>
      <td>NaN</td>
      <td>1233.351613</td>
      <td>1983.325806</td>
      <td>3510.261290</td>
      <td>1862.983871</td>
      <td>1054.306452</td>
      <td>2873.483871</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>std</th>
      <td>2169.271062</td>
      <td>NaN</td>
      <td>944.643188</td>
      <td>1450.715170</td>
      <td>2484.959789</td>
      <td>1332.543266</td>
      <td>1064.029205</td>
      <td>2039.315504</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>min</th>
      <td>32.000000</td>
      <td>NaN</td>
      <td>0.000000</td>
      <td>33.000000</td>
      <td>47.000000</td>
      <td>18.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>596.000000</td>
      <td>NaN</td>
      <td>243.250000</td>
      <td>427.000000</td>
      <td>831.000000</td>
      <td>474.750000</td>
      <td>53.250000</td>
      <td>731.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>3128.000000</td>
      <td>NaN</td>
      <td>1269.000000</td>
      <td>2019.500000</td>
      <td>3688.500000</td>
      <td>1822.500000</td>
      <td>704.000000</td>
      <td>3223.500000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>4973.250000</td>
      <td>NaN</td>
      <td>2003.000000</td>
      <td>3168.250000</td>
      <td>5731.750000</td>
      <td>3069.000000</td>
      <td>1818.500000</td>
      <td>4717.250000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>max</th>
      <td>7077.000000</td>
      <td>NaN</td>
      <td>3124.000000</td>
      <td>4999.000000</td>
      <td>8222.000000</td>
      <td>4510.000000</td>
      <td>4386.000000</td>
      <td>6595.000000</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
bikes.dropna()#去掉缺失值
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Berri 1</th>
      <th>Brébeuf (données non disponibles)</th>
      <th>Côte-Sainte-Catherine</th>
      <th>Maisonneuve 1</th>
      <th>Maisonneuve 2</th>
      <th>du Parc</th>
      <th>Pierre-Dupuy</th>
      <th>Rachel1</th>
      <th>St-Urbain (données non disponibles)</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
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
  </tbody>
</table>
</div>




```python
#如果某一行的数值全部缺失，才需要扔掉
bikes.dropna(how="all").head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Berri 1</th>
      <th>Brébeuf (données non disponibles)</th>
      <th>Côte-Sainte-Catherine</th>
      <th>Maisonneuve 1</th>
      <th>Maisonneuve 2</th>
      <th>du Parc</th>
      <th>Pierre-Dupuy</th>
      <th>Rachel1</th>
      <th>St-Urbain (données non disponibles)</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
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
      <th>2012-01-01</th>
      <td>35</td>
      <td>NaN</td>
      <td>0</td>
      <td>38</td>
      <td>51</td>
      <td>26</td>
      <td>10</td>
      <td>16</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2012-01-02</th>
      <td>83</td>
      <td>NaN</td>
      <td>1</td>
      <td>68</td>
      <td>153</td>
      <td>53</td>
      <td>6</td>
      <td>43</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2012-01-03</th>
      <td>135</td>
      <td>NaN</td>
      <td>2</td>
      <td>104</td>
      <td>248</td>
      <td>89</td>
      <td>3</td>
      <td>58</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2012-01-04</th>
      <td>144</td>
      <td>NaN</td>
      <td>1</td>
      <td>116</td>
      <td>318</td>
      <td>111</td>
      <td>8</td>
      <td>61</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2012-01-05</th>
      <td>197</td>
      <td>NaN</td>
      <td>2</td>
      <td>124</td>
      <td>330</td>
      <td>97</td>
      <td>13</td>
      <td>95</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



#### dropna是默认删除行，如果要删除列，就要申明具体是哪一列


```python
bikes.dropna(how="all",axis=1).head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Berri 1</th>
      <th>Côte-Sainte-Catherine</th>
      <th>Maisonneuve 1</th>
      <th>Maisonneuve 2</th>
      <th>du Parc</th>
      <th>Pierre-Dupuy</th>
      <th>Rachel1</th>
    </tr>
    <tr>
      <th>Date</th>
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
      <th>2012-01-01</th>
      <td>35</td>
      <td>0</td>
      <td>38</td>
      <td>51</td>
      <td>26</td>
      <td>10</td>
      <td>16</td>
    </tr>
    <tr>
      <th>2012-01-02</th>
      <td>83</td>
      <td>1</td>
      <td>68</td>
      <td>153</td>
      <td>53</td>
      <td>6</td>
      <td>43</td>
    </tr>
    <tr>
      <th>2012-01-03</th>
      <td>135</td>
      <td>2</td>
      <td>104</td>
      <td>248</td>
      <td>89</td>
      <td>3</td>
      <td>58</td>
    </tr>
    <tr>
      <th>2012-01-04</th>
      <td>144</td>
      <td>1</td>
      <td>116</td>
      <td>318</td>
      <td>111</td>
      <td>8</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2012-01-05</th>
      <td>197</td>
      <td>2</td>
      <td>124</td>
      <td>330</td>
      <td>97</td>
      <td>13</td>
      <td>95</td>
    </tr>
  </tbody>
</table>
</div>




```python
bikes.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Berri 1</th>
      <th>Brébeuf (données non disponibles)</th>
      <th>Côte-Sainte-Catherine</th>
      <th>Maisonneuve 1</th>
      <th>Maisonneuve 2</th>
      <th>du Parc</th>
      <th>Pierre-Dupuy</th>
      <th>Rachel1</th>
      <th>St-Urbain (données non disponibles)</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
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
      <th>2012-01-01</th>
      <td>35</td>
      <td>NaN</td>
      <td>0</td>
      <td>38</td>
      <td>51</td>
      <td>26</td>
      <td>10</td>
      <td>16</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2012-01-02</th>
      <td>83</td>
      <td>NaN</td>
      <td>1</td>
      <td>68</td>
      <td>153</td>
      <td>53</td>
      <td>6</td>
      <td>43</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2012-01-03</th>
      <td>135</td>
      <td>NaN</td>
      <td>2</td>
      <td>104</td>
      <td>248</td>
      <td>89</td>
      <td>3</td>
      <td>58</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2012-01-04</th>
      <td>144</td>
      <td>NaN</td>
      <td>1</td>
      <td>116</td>
      <td>318</td>
      <td>111</td>
      <td>8</td>
      <td>61</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2012-01-05</th>
      <td>197</td>
      <td>NaN</td>
      <td>2</td>
      <td>124</td>
      <td>330</td>
      <td>97</td>
      <td>13</td>
      <td>95</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
bikes.T.fillna(bikes.T.mean()).T.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Berri 1</th>
      <th>Brébeuf (données non disponibles)</th>
      <th>Côte-Sainte-Catherine</th>
      <th>Maisonneuve 1</th>
      <th>Maisonneuve 2</th>
      <th>du Parc</th>
      <th>Pierre-Dupuy</th>
      <th>Rachel1</th>
      <th>St-Urbain (données non disponibles)</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
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
      <th>2012-01-01</th>
      <td>35.0</td>
      <td>25.142857</td>
      <td>0.0</td>
      <td>38.0</td>
      <td>51.0</td>
      <td>26.0</td>
      <td>10.0</td>
      <td>16.0</td>
      <td>25.142857</td>
    </tr>
    <tr>
      <th>2012-01-02</th>
      <td>83.0</td>
      <td>58.142857</td>
      <td>1.0</td>
      <td>68.0</td>
      <td>153.0</td>
      <td>53.0</td>
      <td>6.0</td>
      <td>43.0</td>
      <td>58.142857</td>
    </tr>
    <tr>
      <th>2012-01-03</th>
      <td>135.0</td>
      <td>91.285714</td>
      <td>2.0</td>
      <td>104.0</td>
      <td>248.0</td>
      <td>89.0</td>
      <td>3.0</td>
      <td>58.0</td>
      <td>91.285714</td>
    </tr>
    <tr>
      <th>2012-01-04</th>
      <td>144.0</td>
      <td>108.428571</td>
      <td>1.0</td>
      <td>116.0</td>
      <td>318.0</td>
      <td>111.0</td>
      <td>8.0</td>
      <td>61.0</td>
      <td>108.428571</td>
    </tr>
    <tr>
      <th>2012-01-05</th>
      <td>197.0</td>
      <td>122.571429</td>
      <td>2.0</td>
      <td>124.0</td>
      <td>330.0</td>
      <td>97.0</td>
      <td>13.0</td>
      <td>95.0</td>
      <td>122.571429</td>
    </tr>
  </tbody>
</table>
</div>




```python
#选择哪一列数据
berri_bikes=bikes[["Berri 1"]]
berri_bikes
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Berri 1</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2012-01-01</th>
      <td>35</td>
    </tr>
    <tr>
      <th>2012-01-02</th>
      <td>83</td>
    </tr>
    <tr>
      <th>2012-01-03</th>
      <td>135</td>
    </tr>
    <tr>
      <th>2012-01-04</th>
      <td>144</td>
    </tr>
    <tr>
      <th>2012-01-05</th>
      <td>197</td>
    </tr>
    <tr>
      <th>2012-01-06</th>
      <td>146</td>
    </tr>
    <tr>
      <th>2012-01-07</th>
      <td>98</td>
    </tr>
    <tr>
      <th>2012-01-08</th>
      <td>95</td>
    </tr>
    <tr>
      <th>2012-01-09</th>
      <td>244</td>
    </tr>
    <tr>
      <th>2012-01-10</th>
      <td>397</td>
    </tr>
    <tr>
      <th>2012-01-11</th>
      <td>273</td>
    </tr>
    <tr>
      <th>2012-01-12</th>
      <td>157</td>
    </tr>
    <tr>
      <th>2012-01-13</th>
      <td>75</td>
    </tr>
    <tr>
      <th>2012-01-14</th>
      <td>32</td>
    </tr>
    <tr>
      <th>2012-01-15</th>
      <td>54</td>
    </tr>
    <tr>
      <th>2012-01-16</th>
      <td>168</td>
    </tr>
    <tr>
      <th>2012-01-17</th>
      <td>155</td>
    </tr>
    <tr>
      <th>2012-01-18</th>
      <td>139</td>
    </tr>
    <tr>
      <th>2012-01-19</th>
      <td>191</td>
    </tr>
    <tr>
      <th>2012-01-20</th>
      <td>161</td>
    </tr>
    <tr>
      <th>2012-01-21</th>
      <td>53</td>
    </tr>
    <tr>
      <th>2012-01-22</th>
      <td>71</td>
    </tr>
    <tr>
      <th>2012-01-23</th>
      <td>210</td>
    </tr>
    <tr>
      <th>2012-01-24</th>
      <td>299</td>
    </tr>
    <tr>
      <th>2012-01-25</th>
      <td>334</td>
    </tr>
    <tr>
      <th>2012-01-26</th>
      <td>306</td>
    </tr>
    <tr>
      <th>2012-01-27</th>
      <td>91</td>
    </tr>
    <tr>
      <th>2012-01-28</th>
      <td>80</td>
    </tr>
    <tr>
      <th>2012-01-29</th>
      <td>87</td>
    </tr>
    <tr>
      <th>2012-01-30</th>
      <td>219</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>2012-10-07</th>
      <td>1580</td>
    </tr>
    <tr>
      <th>2012-10-08</th>
      <td>1854</td>
    </tr>
    <tr>
      <th>2012-10-09</th>
      <td>4787</td>
    </tr>
    <tr>
      <th>2012-10-10</th>
      <td>3115</td>
    </tr>
    <tr>
      <th>2012-10-11</th>
      <td>3746</td>
    </tr>
    <tr>
      <th>2012-10-12</th>
      <td>3169</td>
    </tr>
    <tr>
      <th>2012-10-13</th>
      <td>1783</td>
    </tr>
    <tr>
      <th>2012-10-14</th>
      <td>587</td>
    </tr>
    <tr>
      <th>2012-10-15</th>
      <td>3292</td>
    </tr>
    <tr>
      <th>2012-10-16</th>
      <td>3739</td>
    </tr>
    <tr>
      <th>2012-10-17</th>
      <td>4098</td>
    </tr>
    <tr>
      <th>2012-10-18</th>
      <td>4671</td>
    </tr>
    <tr>
      <th>2012-10-19</th>
      <td>1313</td>
    </tr>
    <tr>
      <th>2012-10-20</th>
      <td>2011</td>
    </tr>
    <tr>
      <th>2012-10-21</th>
      <td>1277</td>
    </tr>
    <tr>
      <th>2012-10-22</th>
      <td>3650</td>
    </tr>
    <tr>
      <th>2012-10-23</th>
      <td>4177</td>
    </tr>
    <tr>
      <th>2012-10-24</th>
      <td>3744</td>
    </tr>
    <tr>
      <th>2012-10-25</th>
      <td>3735</td>
    </tr>
    <tr>
      <th>2012-10-26</th>
      <td>4290</td>
    </tr>
    <tr>
      <th>2012-10-27</th>
      <td>1857</td>
    </tr>
    <tr>
      <th>2012-10-28</th>
      <td>1310</td>
    </tr>
    <tr>
      <th>2012-10-29</th>
      <td>2919</td>
    </tr>
    <tr>
      <th>2012-10-30</th>
      <td>2887</td>
    </tr>
    <tr>
      <th>2012-10-31</th>
      <td>2634</td>
    </tr>
    <tr>
      <th>2012-11-01</th>
      <td>2405</td>
    </tr>
    <tr>
      <th>2012-11-02</th>
      <td>1582</td>
    </tr>
    <tr>
      <th>2012-11-03</th>
      <td>844</td>
    </tr>
    <tr>
      <th>2012-11-04</th>
      <td>966</td>
    </tr>
    <tr>
      <th>2012-11-05</th>
      <td>2247</td>
    </tr>
  </tbody>
</table>
<p>310 rows × 1 columns</p>
</div>




```python
berri_bikes.groupby(berri_bikes.index.weekday).mean()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Berri 1</th>
      <th>weekday</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2984.400000</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3075.113636</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3476.636364</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3639.340909</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3222.068182</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2308.590909</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2206.888889</td>
      <td>6.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
berri_bikes.index
```




    DatetimeIndex(['2012-01-01', '2012-01-02', '2012-01-03', '2012-01-04',
                   '2012-01-05', '2012-01-06', '2012-01-07', '2012-01-08',
                   '2012-01-09', '2012-01-10',
                   ...
                   '2012-10-27', '2012-10-28', '2012-10-29', '2012-10-30',
                   '2012-10-31', '2012-11-01', '2012-11-02', '2012-11-03',
                   '2012-11-04', '2012-11-05'],
                  dtype='datetime64[ns]', name='Date', length=310, freq=None)




```python
berri_bikes.index.weekday
```




    Int64Index([6, 0, 1, 2, 3, 4, 5, 6, 0, 1,
                ...
                5, 6, 0, 1, 2, 3, 4, 5, 6, 0],
               dtype='int64', name='Date', length=310)




```python
#增加一列
berri_bikes.loc[:,"weekday"]=berri_bikes.index.weekday
berri_bikes.head()
```

    D:\anaconda2\lib\site-packages\pandas\core\indexing.py:630: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      self.obj[item_labels[indexer[info_axis]]] = value
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Berri 1</th>
      <th>weekday</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2012-01-01</th>
      <td>35</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2012-01-02</th>
      <td>83</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2012-01-03</th>
      <td>135</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2012-01-04</th>
      <td>144</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2012-01-05</th>
      <td>197</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
#计算根据不同的weekday对应的Berri的平均值
weekday_counts=berri_bikes.groupby("weekday").mean()
weekday_counts
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Berri 1</th>
    </tr>
    <tr>
      <th>weekday</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2984.400000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3075.113636</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3476.636364</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3639.340909</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3222.068182</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2308.590909</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2206.888889</td>
    </tr>
  </tbody>
</table>
</div>




```python
weekday_counts.index=["Monday","Tuesday","Wednesday","Thursday","Friday","Saturday","Sunday"]
weekday_counts
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Berri 1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Monday</th>
      <td>2984.400000</td>
    </tr>
    <tr>
      <th>Tuesday</th>
      <td>3075.113636</td>
    </tr>
    <tr>
      <th>Wednesday</th>
      <td>3476.636364</td>
    </tr>
    <tr>
      <th>Thursday</th>
      <td>3639.340909</td>
    </tr>
    <tr>
      <th>Friday</th>
      <td>3222.068182</td>
    </tr>
    <tr>
      <th>Saturday</th>
      <td>2308.590909</td>
    </tr>
    <tr>
      <th>Sunday</th>
      <td>2206.888889</td>
    </tr>
  </tbody>
</table>
</div>




```python
%matplotlib inline
weekday_counts.plot(kind="bar")
```




    <matplotlib.axes._subplots.AxesSubplot at 0x8bf5668>




![png](output_139_1.png)



```python
bikes_avg = bikes.mean(axis=1).to_frame()
bikes_avg
bikes_avg.columns = ["bikes_avg"]
bikes_avg.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>bikes_avg</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2012-01-01</th>
      <td>25.142857</td>
    </tr>
    <tr>
      <th>2012-01-02</th>
      <td>58.142857</td>
    </tr>
    <tr>
      <th>2012-01-03</th>
      <td>91.285714</td>
    </tr>
    <tr>
      <th>2012-01-04</th>
      <td>108.428571</td>
    </tr>
    <tr>
      <th>2012-01-05</th>
      <td>122.571429</td>
    </tr>
  </tbody>
</table>
</div>




```python
bikes_avg.index
bikes_avg.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>bikes_avg</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2012-01-01</th>
      <td>25.142857</td>
    </tr>
    <tr>
      <th>2012-01-02</th>
      <td>58.142857</td>
    </tr>
    <tr>
      <th>2012-01-03</th>
      <td>91.285714</td>
    </tr>
    <tr>
      <th>2012-01-04</th>
      <td>108.428571</td>
    </tr>
    <tr>
      <th>2012-01-05</th>
      <td>122.571429</td>
    </tr>
  </tbody>
</table>
</div>




```python
bikes_avg.index.weekday
```




    Int64Index([6, 0, 1, 2, 3, 4, 5, 6, 0, 1,
                ...
                5, 6, 0, 1, 2, 3, 4, 5, 6, 0],
               dtype='int64', name='Date', length=310)




```python
bikes_avg.loc[:,"weekday"]=bikes_avg.index.weekday
bikes_avg.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>bikes_avg</th>
      <th>weekday</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2012-01-01</th>
      <td>25.142857</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2012-01-02</th>
      <td>58.142857</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2012-01-03</th>
      <td>91.285714</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2012-01-04</th>
      <td>108.428571</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2012-01-05</th>
      <td>122.571429</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
weekday_avg=bikes_avg.groupby("weekday").mean()
weekday_avg.index=["Monday","Tuesday","Wednesday","Thursday","Friday","Saturday","Sunday"]
weekday_avg.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>bikes_avg</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Monday</th>
      <td>2269.723810</td>
    </tr>
    <tr>
      <th>Tuesday</th>
      <td>2268.123377</td>
    </tr>
    <tr>
      <th>Wednesday</th>
      <td>2564.032468</td>
    </tr>
    <tr>
      <th>Thursday</th>
      <td>2691.782468</td>
    </tr>
    <tr>
      <th>Friday</th>
      <td>2398.610390</td>
    </tr>
  </tbody>
</table>
</div>




```python
bikes_avg[["bikes_avg"]].plot()
```




    <matplotlib.axes._subplots.AxesSubplot at 0x8fab128>




![png](output_145_1.png)



```python
bikes.iloc[:50,:].plot()
```




    <matplotlib.axes._subplots.AxesSubplot at 0x8e63128>




![png](output_146_1.png)


###  项目3 股票分析的小项目


```python
goog = pd.read_csv("../Anaconda3/GOOG.csv", index_col=0, parse_dates=["Date"])
goog.index
```




    DatetimeIndex(['2004-08-19', '2004-08-20', '2004-08-23', '2004-08-24',
                   '2004-08-25', '2004-08-26', '2004-08-27', '2004-08-30',
                   '2004-08-31', '2004-09-01',
                   ...
                   '2017-07-07', '2017-07-10', '2017-07-11', '2017-07-12',
                   '2017-07-13', '2017-07-14', '2017-07-17', '2017-07-18',
                   '2017-07-19', '2017-07-20'],
                  dtype='datetime64[ns]', name='Date', length=3253, freq=None)




```python
#取一个字段绘图
goog["Adj Close"].plot(grid=True)
```




    <matplotlib.axes._subplots.AxesSubplot at 0xa0a5da0>




![png](output_149_1.png)



```python
#收盘价绘制图
goog["Close"].plot(grid=True)
```




    <matplotlib.axes._subplots.AxesSubplot at 0xa2fc668>




![png](output_150_1.png)



```python
aapl=pd.read_csv("../Anaconda3/AAPL.csv",index_col=0,parse_dates=[0])
aapl["Adj Close"].plot(grid=True)#显示网格
```




    <matplotlib.axes._subplots.AxesSubplot at 0xbdbf668>




![png](output_151_1.png)



```python
msft=pd.read_csv("../Anaconda3/MSFT.csv",index_col=0,parse_dates=[0])
msft.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
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
      <th>1986-03-13</th>
      <td>0.088542</td>
      <td>0.101563</td>
      <td>0.088542</td>
      <td>0.097222</td>
      <td>0.065242</td>
      <td>1031788800</td>
    </tr>
    <tr>
      <th>1986-03-14</th>
      <td>0.097222</td>
      <td>0.102431</td>
      <td>0.097222</td>
      <td>0.100694</td>
      <td>0.067572</td>
      <td>308160000</td>
    </tr>
    <tr>
      <th>1986-03-17</th>
      <td>0.100694</td>
      <td>0.103299</td>
      <td>0.100694</td>
      <td>0.102431</td>
      <td>0.068737</td>
      <td>133171200</td>
    </tr>
    <tr>
      <th>1986-03-18</th>
      <td>0.102431</td>
      <td>0.103299</td>
      <td>0.098958</td>
      <td>0.099826</td>
      <td>0.066990</td>
      <td>67766400</td>
    </tr>
    <tr>
      <th>1986-03-19</th>
      <td>0.099826</td>
      <td>0.100694</td>
      <td>0.097222</td>
      <td>0.098090</td>
      <td>0.065825</td>
      <td>47894400</td>
    </tr>
  </tbody>
</table>
</div>




```python
#把三张表拼接
stocks=pd.concat([aapl["Adj Close"],goog["Adj Close"],msft["Adj Close"]],axis=1)
stocks.columns=["aapl","goog","msft"]
stocks.head
```




    <bound method NDFrame.head of                   aapl        goog       msft
    Date                                         
    1980-12-12    0.423252         NaN        NaN
    1980-12-15    0.401170         NaN        NaN
    1980-12-16    0.371726         NaN        NaN
    1980-12-17    0.380927         NaN        NaN
    1980-12-18    0.391969         NaN        NaN
    1980-12-19    0.415892         NaN        NaN
    1980-12-22    0.436134         NaN        NaN
    1980-12-23    0.454536         NaN        NaN
    1980-12-24    0.478460         NaN        NaN
    1980-12-26    0.522625         NaN        NaN
    1980-12-29    0.529986         NaN        NaN
    1980-12-30    0.517104         NaN        NaN
    1980-12-31    0.502382         NaN        NaN
    1981-01-02    0.507903         NaN        NaN
    1981-01-05    0.496862         NaN        NaN
    1981-01-06    0.474779         NaN        NaN
    1981-01-07    0.454536         NaN        NaN
    1981-01-08    0.445336         NaN        NaN
    1981-01-09    0.469258         NaN        NaN
    1981-01-12    0.465578         NaN        NaN
    1981-01-13    0.449016         NaN        NaN
    1981-01-14    0.450856         NaN        NaN
    1981-01-15    0.460057         NaN        NaN
    1981-01-16    0.456377         NaN        NaN
    1981-01-19    0.483980         NaN        NaN
    1981-01-20    0.469258         NaN        NaN
    1981-01-21    0.478460         NaN        NaN
    1981-01-22    0.483980         NaN        NaN
    1981-01-23    0.482140         NaN        NaN
    1981-01-26    0.474779         NaN        NaN
    ...                ...         ...        ...
    2017-06-08  154.990005  983.409973  71.949997
    2017-06-09  148.979996  949.830017  70.320000
    2017-06-12  145.419998  942.900024  69.779999
    2017-06-13  146.589996  953.400024  70.650002
    2017-06-14  145.160004  950.760010  70.269997
    2017-06-15  144.289993  942.309998  69.900002
    2017-06-16  142.270004  939.780029  70.000000
    2017-06-19  146.339996  957.369995  70.870003
    2017-06-20  145.009995  950.630005  69.910004
    2017-06-21  145.869995  959.450012  70.269997
    2017-06-22  145.630005  957.090027  70.260002
    2017-06-23  146.279999  965.590027  71.209999
    2017-06-26  145.820007  952.270020  70.529999
    2017-06-27  143.729996  927.330017  69.209999
    2017-06-28  145.830002  940.489990  69.800003
    2017-06-29  143.679993  917.789978  68.489998
    2017-06-30  144.020004  908.729980  68.930000
    2017-07-03  143.500000  898.700012  68.169998
    2017-07-05  144.089996  911.710022  69.080002
    2017-07-06  142.729996  906.690002  68.570000
    2017-07-07  144.179993  918.590027  69.459999
    2017-07-10  145.059998  928.799988  69.980003
    2017-07-11  145.529999  930.090027  69.989998
    2017-07-12  145.740005  943.830017  71.150002
    2017-07-13  147.770004  947.159973  71.769997
    2017-07-14  149.039993  955.989990  72.779999
    2017-07-17  149.559998  953.419983  73.349998
    2017-07-18  150.080002  965.400024  73.300003
    2017-07-19  151.020004  970.890015  73.860001
    2017-07-20  150.339996  968.150024  74.220001
    
    [9231 rows x 3 columns]>




```python
stocks=pd.DataFrame({"AAPL":aapl["Adj Close"].bfill(),"MSFT":msft["Adj Close"].bfill(),"GOOG":goog["Adj Close"].bfill()})
stocks
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>AAPL</th>
      <th>MSFT</th>
      <th>GOOG</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1980-12-12</th>
      <td>0.423252</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1980-12-15</th>
      <td>0.401170</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1980-12-16</th>
      <td>0.371726</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1980-12-17</th>
      <td>0.380927</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1980-12-18</th>
      <td>0.391969</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1980-12-19</th>
      <td>0.415892</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1980-12-22</th>
      <td>0.436134</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1980-12-23</th>
      <td>0.454536</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1980-12-24</th>
      <td>0.478460</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1980-12-26</th>
      <td>0.522625</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1980-12-29</th>
      <td>0.529986</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1980-12-30</th>
      <td>0.517104</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1980-12-31</th>
      <td>0.502382</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1981-01-02</th>
      <td>0.507903</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1981-01-05</th>
      <td>0.496862</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1981-01-06</th>
      <td>0.474779</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1981-01-07</th>
      <td>0.454536</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1981-01-08</th>
      <td>0.445336</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1981-01-09</th>
      <td>0.469258</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1981-01-12</th>
      <td>0.465578</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1981-01-13</th>
      <td>0.449016</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1981-01-14</th>
      <td>0.450856</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1981-01-15</th>
      <td>0.460057</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1981-01-16</th>
      <td>0.456377</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1981-01-19</th>
      <td>0.483980</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1981-01-20</th>
      <td>0.469258</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1981-01-21</th>
      <td>0.478460</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1981-01-22</th>
      <td>0.483980</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1981-01-23</th>
      <td>0.482140</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1981-01-26</th>
      <td>0.474779</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2017-06-08</th>
      <td>154.990005</td>
      <td>71.949997</td>
      <td>983.409973</td>
    </tr>
    <tr>
      <th>2017-06-09</th>
      <td>148.979996</td>
      <td>70.320000</td>
      <td>949.830017</td>
    </tr>
    <tr>
      <th>2017-06-12</th>
      <td>145.419998</td>
      <td>69.779999</td>
      <td>942.900024</td>
    </tr>
    <tr>
      <th>2017-06-13</th>
      <td>146.589996</td>
      <td>70.650002</td>
      <td>953.400024</td>
    </tr>
    <tr>
      <th>2017-06-14</th>
      <td>145.160004</td>
      <td>70.269997</td>
      <td>950.760010</td>
    </tr>
    <tr>
      <th>2017-06-15</th>
      <td>144.289993</td>
      <td>69.900002</td>
      <td>942.309998</td>
    </tr>
    <tr>
      <th>2017-06-16</th>
      <td>142.270004</td>
      <td>70.000000</td>
      <td>939.780029</td>
    </tr>
    <tr>
      <th>2017-06-19</th>
      <td>146.339996</td>
      <td>70.870003</td>
      <td>957.369995</td>
    </tr>
    <tr>
      <th>2017-06-20</th>
      <td>145.009995</td>
      <td>69.910004</td>
      <td>950.630005</td>
    </tr>
    <tr>
      <th>2017-06-21</th>
      <td>145.869995</td>
      <td>70.269997</td>
      <td>959.450012</td>
    </tr>
    <tr>
      <th>2017-06-22</th>
      <td>145.630005</td>
      <td>70.260002</td>
      <td>957.090027</td>
    </tr>
    <tr>
      <th>2017-06-23</th>
      <td>146.279999</td>
      <td>71.209999</td>
      <td>965.590027</td>
    </tr>
    <tr>
      <th>2017-06-26</th>
      <td>145.820007</td>
      <td>70.529999</td>
      <td>952.270020</td>
    </tr>
    <tr>
      <th>2017-06-27</th>
      <td>143.729996</td>
      <td>69.209999</td>
      <td>927.330017</td>
    </tr>
    <tr>
      <th>2017-06-28</th>
      <td>145.830002</td>
      <td>69.800003</td>
      <td>940.489990</td>
    </tr>
    <tr>
      <th>2017-06-29</th>
      <td>143.679993</td>
      <td>68.489998</td>
      <td>917.789978</td>
    </tr>
    <tr>
      <th>2017-06-30</th>
      <td>144.020004</td>
      <td>68.930000</td>
      <td>908.729980</td>
    </tr>
    <tr>
      <th>2017-07-03</th>
      <td>143.500000</td>
      <td>68.169998</td>
      <td>898.700012</td>
    </tr>
    <tr>
      <th>2017-07-05</th>
      <td>144.089996</td>
      <td>69.080002</td>
      <td>911.710022</td>
    </tr>
    <tr>
      <th>2017-07-06</th>
      <td>142.729996</td>
      <td>68.570000</td>
      <td>906.690002</td>
    </tr>
    <tr>
      <th>2017-07-07</th>
      <td>144.179993</td>
      <td>69.459999</td>
      <td>918.590027</td>
    </tr>
    <tr>
      <th>2017-07-10</th>
      <td>145.059998</td>
      <td>69.980003</td>
      <td>928.799988</td>
    </tr>
    <tr>
      <th>2017-07-11</th>
      <td>145.529999</td>
      <td>69.989998</td>
      <td>930.090027</td>
    </tr>
    <tr>
      <th>2017-07-12</th>
      <td>145.740005</td>
      <td>71.150002</td>
      <td>943.830017</td>
    </tr>
    <tr>
      <th>2017-07-13</th>
      <td>147.770004</td>
      <td>71.769997</td>
      <td>947.159973</td>
    </tr>
    <tr>
      <th>2017-07-14</th>
      <td>149.039993</td>
      <td>72.779999</td>
      <td>955.989990</td>
    </tr>
    <tr>
      <th>2017-07-17</th>
      <td>149.559998</td>
      <td>73.349998</td>
      <td>953.419983</td>
    </tr>
    <tr>
      <th>2017-07-18</th>
      <td>150.080002</td>
      <td>73.300003</td>
      <td>965.400024</td>
    </tr>
    <tr>
      <th>2017-07-19</th>
      <td>151.020004</td>
      <td>73.860001</td>
      <td>970.890015</td>
    </tr>
    <tr>
      <th>2017-07-20</th>
      <td>150.339996</td>
      <td>74.220001</td>
      <td>968.150024</td>
    </tr>
  </tbody>
</table>
<p>9231 rows × 3 columns</p>
</div>




```python
stocks.plot(grid=True)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x8f74f98>




![png](output_155_1.png)



```python
#筛选数据
valid_stocks=stocks[stocks.index>=stocks["GOOG"].first_valid_index()]
```


```python
valid_stocks.plot(grid=True)
```




    <matplotlib.axes._subplots.AxesSubplot at 0xa6cd940>




![png](output_157_1.png)



```python
valid_stocks.plot(grid=True)
```




    <matplotlib.axes._subplots.AxesSubplot at 0xaa296a0>




![png](output_158_1.png)



```python
valid_stocks.plot(grid=True)
valid_stocks.dtypes
```




    AAPL    float64
    MSFT    float64
    GOOG    float64
    dtype: object




![png](output_159_1.png)



```python
#画出月k线
monthly_stocks = valid_stocks.resample("M").last()
monthly_stocks.plot()
```




    <matplotlib.axes._subplots.AxesSubplot at 0xbb996d8>




![png](output_160_1.png)



```python

```
