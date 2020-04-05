
# Pandas教程

目录
+ numpy速成
+ Series
+ DataFrame
+ index
+ 文件读写


```python
Pandas简介
-python数据分析library
--基于numpy (对ndarray的操作)
有一种用python做Excel/SQL/R的感觉

为什么要学习pandas?
-pandas和机器学习的关系，数据预处理，feature engineering。
-pandas的DataFrame结构和大家在大数据部分见到的spark中的DataFrame非常类似。
```

# Numpy

Numpy是Python语言的一个library 
Numpy主要支持矩阵操作和运算
现在比较流行的机器学习框架（例如Tensorflow/PyTorch等等），语法都与Numpy比较接近


```python
Numpy速成
+ array数组
+ 数据索引和切片
+ 数学运算
+ 广播特性
+ 统计数学运算
++ 乘法（点乘，逐元素相乘）
```

## Array数组


```python
%config ZMQInteractiveShell.ast_node_interactivity='all'
%pprint
import numpy as np
```

    Pretty printing has been turned ON
    


```python
#嵌套list转numpy array
a = np.array([[1,2,3],[4,5,6]])
a
type(a)
```




    array([[1, 2, 3],
           [4, 5, 6]])






    numpy.ndarray




```python
# 随机生成array
b=np.random.random((2,2))
b
```




    array([[0.40785995, 0.46300156],
           [0.11046077, 0.79346652]])




```python
# 通过shape查看维度
a=np.array([[[1,2,3],[4,5,6]],[[1,2,3],[2,4,5]]])
a
a.shape
```




    array([[[1, 2, 3],
            [4, 5, 6]],
    
           [[1, 2, 3],
            [2, 4, 5]]])






    (2, 2, 3)




```python
print(a.shape, b.shape, a.dtype, b.dtype)
```

    (2, 2, 3) (2, 2) int32 float64
    


```python
# astype做类型转换
a.astype(np.float)
```




    array([[[1., 2., 3.],
            [4., 5., 6.]],
    
           [[1., 2., 3.],
            [2., 4., 5.]]])



## 数组索引与切片/Array indexing and slicing


```python
a
#在第一个维度上取下标为0的元素，在第二个维度上取下标为1的元素
a[0,1]
```




    array([[[1, 2, 3],
            [4, 5, 6]],
    
           [[1, 2, 3],
            [2, 4, 5]]])






    array([4, 5, 6])




```python
a
a[:, 1:3]
```




    array([[[1, 2, 0],
            [0, 0, 0]],
    
           [[1, 2, 0],
            [2, 0, 0]]])






    array([[[0, 0, 0]],
    
           [[2, 0, 0]]])




```python
a.size
```




    12



boolean indexing


```python
a
a>2 #判断true or false
```




    array([[[1, 2, 0],
            [0, 0, 0]],
    
           [[1, 2, 0],
            [2, 0, 0]]])






    array([[[False, False, False],
            [False, False, False]],
    
           [[False, False, False],
            [False, False, False]]])




```python
a [a>2] 
```




    array([], dtype=int32)




```python
a[a>2] = 0 #根据条件赋值
a
```




    array([[[1, 2, 0],
            [0, 0, 0]],
    
           [[1, 2, 0],
            [2, 0, 0]]])



## 数学运算


```python
a.shape #查看维度
a
```




    (2, 2, 3)






    array([[[1, 2, 0],
            [0, 0, 0]],
    
           [[1, 2, 0],
            [2, 0, 0]]])




```python
c = np.random.random((2,3)) #取（2,3）之间的随机数
c
c.shape #查看维度
```




    array([[0.31494218, 0.6071922 , 0.31817351],
           [0.15481804, 0.04829196, 0.27493966]])






    (2, 3)




```python
a+c
```




    array([[[1.31494218, 2.6071922 , 0.31817351],
            [0.15481804, 0.04829196, 0.27493966]],
    
           [[1.31494218, 2.6071922 , 0.31817351],
            [2.15481804, 0.04829196, 0.27493966]]])




```python
a-c
```




    array([[[ 0.68505782,  1.3928078 , -0.31817351],
            [-0.15481804, -0.04829196, -0.27493966]],
    
           [[ 0.68505782,  1.3928078 , -0.31817351],
            [ 1.84518196, -0.04829196, -0.27493966]]])




```python
a*c
```




    array([[[0.31494218, 1.21438441, 0.        ],
            [0.        , 0.        , 0.        ]],
    
           [[0.31494218, 1.21438441, 0.        ],
            [0.30963607, 0.        , 0.        ]]])




```python
a/c
```




    array([[[ 3.17518601,  3.29384994,  0.        ],
            [ 0.        ,  0.        ,  0.        ]],
    
           [[ 3.17518601,  3.29384994,  0.        ],
            [12.91839146,  0.        ,  0.        ]]])



## 广播特性


```python
a
a+2
```




    array([[[1, 2, 0],
            [0, 0, 0]],
    
           [[1, 2, 0],
            [2, 0, 0]]])






    array([[[3, 4, 2],
            [2, 2, 2]],
    
           [[3, 4, 2],
            [4, 2, 2]]])




```python
import numpy as np
c = np.random.random((2,3))
c
```




    array([[0.68210808, 0.5906167 , 0.82365369],
           [0.87371658, 0.48402846, 0.20838049]])




```python
a
a+c
```




    array([[[1, 2, 0],
            [0, 0, 0]],
    
           [[1, 2, 0],
            [2, 0, 0]]])






    array([[[1.68210808, 2.5906167 , 0.82365369],
            [0.87371658, 0.48402846, 0.20838049]],
    
           [[1.68210808, 2.5906167 , 0.82365369],
            [2.87371658, 0.48402846, 0.20838049]]])




```python
a=np.random.random((8,1,6))
b=np.random.random((1,6,1))
(a+b).shape
```




    (8, 6, 6)




```python
当操作两个array时，numpy会逐个dimension比较它们的shape，在下述情况下，两arrays会兼容和输出broadcasting结果：

相等
其中一个为1，（进而可进行拷贝拓展已至，shape匹配）
当两个ndarray的维度不完全相同的时候，rank较小的那个ndarray会被自动在前面加上一个一维维度，直到与另一个ndarray rank相同再检查是否匹配
比如求和的时候有：
```

Image (3d array):  256 x 256 x 3
Scale (1d array):              3
Result (3d array): 256 x 256 x 3

A      (4d array):  8 x 1 x 6 x 1
B      (3d array):      7 x 1 x 5
Result (4d array):  8 x 7 x 6 x 5

A      (2d array):  5 x 4
B      (1d array):      1
Result (2d array):  5 x 4

A      (2d array):  15 x 3 x 5
B      (1d array):  15 x 1 x 5
Result (2d array):  15 x 3 x 5

## 统计数学运算


```python
a
np.sum(a) #全部元素求和
```




    array([[[0.299323  , 0.16209028, 0.26781003, 0.50055941, 0.28798051,
             0.68223228]],
    
           [[0.45291006, 0.36393098, 0.78294897, 0.26542374, 0.76473769,
             0.65729997]],
    
           [[0.12514212, 0.85186248, 0.57476725, 0.48624224, 0.74364581,
             0.81320181]],
    
           [[0.8096316 , 0.04156333, 0.39141841, 0.97276423, 0.93446199,
             0.58501471]],
    
           [[0.43599753, 0.77333741, 0.69217109, 0.96785717, 0.64064523,
             0.42573816]],
    
           [[0.00219661, 0.69052674, 0.81087502, 0.55670143, 0.18325122,
             0.27356429]],
    
           [[0.4835367 , 0.66443635, 0.63198413, 0.83366485, 0.30526176,
             0.83838393]],
    
           [[0.69527304, 0.37254991, 0.70026954, 0.93577787, 0.87991597,
             0.04625285]]])






    26.6571316971363




```python
np.sum(a,axis=0) #按照第一个维度汇总求和
```




    array([[3.30401067, 3.92029748, 4.85224444, 5.51899094, 4.73990018,
            4.321688  ]])




```python
np.sum(a,axis =2)#按照第三个维度汇总求和
```




    array([[2.19999551],
           [3.28725141],
           [3.59486172],
           [3.73485427],
           [3.93574658],
           [2.51711531],
           [3.75726773],
           [3.63003917]])




```python
np.mean(a,axis =2)#按照第三个维度汇总求均值
```




    0.5553569103570063



### 乘法

np.dot是点乘

|A B| . |E F| = |A*E+B*G A*F+B*H|
|C D|   |G H|   |C*E+D*G C*F+D*H|

np.multiply 逐元素乘法

|A B| ⊙ |E F| = |A*E B*F|
|C D|   |G H|   |C*G D*H|


```python
a = np.array([[1,2],[3,4]])
b = np.array([[1,2],[2,3]])
a
b
```




    array([[1, 2],
           [3, 4]])






    array([[1, 2],
           [2, 3]])




```python
np.dot(a,b)
```




    array([[ 5,  8],
           [11, 18]])




```python
np.multiply(a,b)
```




    array([[ 1,  4],
           [ 6, 12]])



# Panda数据结构Series


```python
-构造和初始化series
--series是一维数据结构，只有一个方括号
--用dictionary构造series
--改变默认索引
--用numpy ndarray构造series
-选择数据
-series赋值
--切片
--字典的键对应字典的值
--判断某元素在不在series里
--series元素赋值
```

## 构造和初始化Series


```python
import pandas as pd
```


```python
pd.__version__
```




    '0.23.4'



Series是一个一维的数据结构，下面是一些初始化Series的方法。


```python
s = pd.Series([7, 'Beijing', 2.17, -12344, 'Happy Birthday!'])
s
```




    0                  7
    1            Beijing
    2               2.17
    3             -12344
    4    Happy Birthday!
    dtype: object




```python
s = pd.Series([7, 'Beijing', 2.17, -12344, 'Happy Birthday!'])
s
```




    0                  7
    1            Beijing
    2               2.17
    3             -12344
    4    Happy Birthday!
    dtype: object



pandas会默认用0到n-1来作为Series的index，但是我们也可以自己指定index。index我们可以把它理解为dict里面的key。


```python
s = pd.Series([7,"Beijing",2.17,-12345,"Happy Birthday!"],index=["A","B","C","D","E"])
s
```




    A                  7
    B            Beijing
    C               2.17
    D             -12345
    E    Happy Birthday!
    dtype: object



还可以用dictionary来构造一个Series，因为Series本来就是key value pairs


```python
cities = {'Beijing': 55000, 'Shanghai': 60000, 'Shenzhen': 50000, 'Hangzhou': 20000, 'Guangzhou': 25000, 'Suzhou': None}
apts = pd.Series(cities, name="price")
apts
```




    Beijing      55000.0
    Shanghai     60000.0
    Shenzhen     50000.0
    Hangzhou     20000.0
    Guangzhou    25000.0
    Suzhou           NaN
    Name: price, dtype: float64



numpy ndarray构建一个Series


```python
import numpy as np
s = pd.Series(np.random.random(5), index=['a', 'b', 'c', 'd', 'e'])
s
```




    a    0.777576
    b    0.120963
    c    0.108663
    d    0.058646
    e    0.427640
    dtype: float64



## 选择数据

我们可以像对待一个list一样对待Series


```python
apts[1:] #切片
```




    Shanghai     60000.0
    Shenzhen     50000.0
    Hangzhou     20000.0
    Guangzhou    25000.0
    Suzhou           NaN
    Name: price, dtype: float64




```python
apts[:-1] #切片
```




    Beijing      55000.0
    Shanghai     60000.0
    Shenzhen     50000.0
    Hangzhou     20000.0
    Guangzhou    25000.0
    Name: price, dtype: float64




```python
apts[[4,3,1]] #这种写法是Series独有而list不具备的
```




    Guangzhou    25000.0
    Hangzhou     20000.0
    Shanghai     60000.0
    Name: price, dtype: float64




```python
apts[1:] + apts[:-1] #注意，在相加的时候，其实是index对齐的方式相加的
```




    Beijing           NaN
    Guangzhou     50000.0
    Hangzhou      40000.0
    Shanghai     120000.0
    Shenzhen     100000.0
    Suzhou            NaN
    Name: price, dtype: float64



Series就像一个dict，前面定义的index就是用来选择数据的


```python
apts["Hangzhou"]
```




    20000.0




```python
apts[["Hangzhou", "Beijing", "Shenzhen"]]
```




    Hangzhou    20000.0
    Beijing     55000.0
    Shenzhen    50000.0
    Name: price, dtype: float64



boolean值


```python
"Hangzhou" in apts #判断是否有这个index
```




    True




```python
"Chongqing" in apts
```




    False



比较安全的用key读取value的方法如下


```python
apts.get("Chongqing", 55) #和字典类似，默认值放在后面
```




    55




```python
apts.get("Hangzhou",9)
```




    20000.0



下面这种写法，如果key不存在，就可能会报错了


```python
# apts["Chongqing"]
```


```python
apts[apts < 50000] #条件选择
```




    Hangzhou     20000.0
    Guangzhou    25000.0
    Name: price, dtype: float64




```python
apts.median() #中位数，统计计算
```




    50000.0




```python
apts[apts > apts.median()] #借助于统计计算的数据选择
```




    Beijing     55000.0
    Shanghai    60000.0
    Name: price, dtype: float64



下面我再详细展示一下这个boolean indexing是如何工作的


```python
less_than_50000 = apts < 50000
less_than_50000 #实际上拿到的是一个True or False的series
```




    Beijing      False
    Shanghai     False
    Shenzhen     False
    Hangzhou      True
    Guangzhou     True
    Suzhou       False
    Name: price, dtype: bool




```python
print(apts[less_than_50000])
```

    Hangzhou     20000.0
    Guangzhou    25000.0
    Name: price, dtype: float64
    

## Series元素赋值

Series的元素可以被赋值


```python
#根据index赋值
print("Old value: ", apts['Shenzhen'])
apts['Shenzhen'] = 55000
print("New value: ", apts['Shenzhen'])
```

    Old value:  50000.0
    New value:  55000.0
    

前面讲过的boolean indexing在赋值的时候也可以用


```python
# 条件选择赋值
print(apts[apts < 50000])
print()
apts[apts <= 50000] = 40000
print(apts[apts < 50000])
```

    Hangzhou     20000.0
    Guangzhou    25000.0
    Name: price, dtype: float64
    
    Hangzhou     40000.0
    Guangzhou    40000.0
    Name: price, dtype: float64
    

## 数学运算


```python
apts/2 #广播特性
```




    Beijing      27500.0
    Shanghai     30000.0
    Shenzhen     27500.0
    Hangzhou     20000.0
    Guangzhou    20000.0
    Suzhou           NaN
    Name: price, dtype: float64




```python
apts **2
```




    Beijing      3.025000e+09
    Shanghai     3.600000e+09
    Shenzhen     3.025000e+09
    Hangzhou     1.600000e+09
    Guangzhou    1.600000e+09
    Suzhou                NaN
    Name: price, dtype: float64



numpy的运算可以被运用到pandas上去


```python
np.square(apts)
```




    Beijing      3.025000e+09
    Shanghai     3.600000e+09
    Shenzhen     3.025000e+09
    Hangzhou     1.600000e+09
    Guangzhou    1.600000e+09
    Suzhou                NaN
    Name: price, dtype: float64




```python
cars = pd.Series({'Beijing': 300000, 'Shanghai': 400000, 'Shenzhen': 300000, \
                      'Tianjin': 200000, 'Guangzhou': 200000, 'Chongqing': 150000})
cars
```




    Beijing      300000
    Shanghai     400000
    Shenzhen     300000
    Tianjin      200000
    Guangzhou    200000
    Chongqing    150000
    dtype: int64




```python
print(cars + apts * 100) #注意广播特性与index对齐求和
```

    Beijing      5800000.0
    Chongqing          NaN
    Guangzhou    4200000.0
    Hangzhou           NaN
    Shanghai     6400000.0
    Shenzhen     5800000.0
    Suzhou             NaN
    Tianjin            NaN
    dtype: float64
    

# 数据结构Dataframe


```python
-DataFrame的构造
---用字典构造dataframe
---columns的名字和顺序可以指定
---index可以指定
--用几个series构造dataframe
--用lists of dicts 构造dataframe
-DataFrame的赋值
--loc（）方法取行和列
--用Series来指定需要修改的index以及相对应的value
```

一个Dataframe就是一张表格，Series表示的是一维数组，Dataframe则是一个二维数组，可以类比成一张excel的spreadsheet。也可以把Dataframe当做一组Series的集合

## 创建一个DataFrame

dataframe可以由一个dictionary构造得到


```python
import pandas as pd
data = {'city': ['Beijing', 'Shanghai', 'Guangzhou', 'Shenzhen', 'Hangzhou', 'Chongqing'],
       'year': [2016,2017,2016,2017,2016, 2016],
       'population': [2100, 2300, 1000, 700, 500, 500]}
pd.DataFrame(data)
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
      <th>city</th>
      <th>year</th>
      <th>population</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Beijing</td>
      <td>2016</td>
      <td>2100</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Shanghai</td>
      <td>2017</td>
      <td>2300</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Guangzhou</td>
      <td>2016</td>
      <td>1000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Shenzhen</td>
      <td>2017</td>
      <td>700</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Hangzhou</td>
      <td>2016</td>
      <td>500</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Chongqing</td>
      <td>2016</td>
      <td>500</td>
    </tr>
  </tbody>
</table>
</div>



columns的名字和顺序可以指定


```python
pd.DataFrame(data, columns=['year', 'city', 'population'])
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
      <th>year</th>
      <th>city</th>
      <th>population</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2016</td>
      <td>Beijing</td>
      <td>2100</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2017</td>
      <td>Shanghai</td>
      <td>2300</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2016</td>
      <td>Guangzhou</td>
      <td>1000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2017</td>
      <td>Shenzhen</td>
      <td>700</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2016</td>
      <td>Hangzhou</td>
      <td>500</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2016</td>
      <td>Chongqing</td>
      <td>500</td>
    </tr>
  </tbody>
</table>
</div>



index也可以指定


```python
frame = pd.DataFrame(data, columns = ['year', 'city', 'population'],
                     index = ['one', 'two', 'three', 'four', 'five', 'six'])
frame
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
      <th>year</th>
      <th>city</th>
      <th>population</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>2016</td>
      <td>Beijing</td>
      <td>2100</td>
    </tr>
    <tr>
      <th>two</th>
      <td>2017</td>
      <td>Shanghai</td>
      <td>2300</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2016</td>
      <td>Guangzhou</td>
      <td>1000</td>
    </tr>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>Shenzhen</td>
      <td>700</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2016</td>
      <td>Hangzhou</td>
      <td>500</td>
    </tr>
    <tr>
      <th>six</th>
      <td>2016</td>
      <td>Chongqing</td>
      <td>500</td>
    </tr>
  </tbody>
</table>
</div>



也可以从几个Series构建一个DataFrame


```python
cities = {'Beijing': 55000, 'Shanghai': 60000, 'Shenzhen': 50000, 'Hangzhou': 20000, 'Guangzhou': 25000, 'Suzhou': None}
apts = pd.Series(cities)
apts
```




    Beijing      55000.0
    Shanghai     60000.0
    Shenzhen     50000.0
    Hangzhou     20000.0
    Guangzhou    25000.0
    Suzhou           NaN
    dtype: float64




```python
cars = pd.Series({'Beijing': 300000, 'Shanghai': 400000, 'Shenzhen': 300000, \
                      'Tianjin': 200000, 'Guangzhou': 200000, 'Chongqing': 150000})
cars
```




    Beijing      300000
    Shanghai     400000
    Shenzhen     300000
    Tianjin      200000
    Guangzhou    200000
    Chongqing    150000
    dtype: int64




```python
apts+cars
```




    Beijing      355000.0
    Chongqing         NaN
    Guangzhou    225000.0
    Hangzhou          NaN
    Shanghai     460000.0
    Shenzhen     350000.0
    Suzhou            NaN
    Tianjin           NaN
    dtype: float64




```python
#index要对齐
df=pd.DataFrame({"apts":apts,"cars":cars})
df
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
      <th>Beijing</th>
      <td>55000.0</td>
      <td>300000.0</td>
    </tr>
    <tr>
      <th>Chongqing</th>
      <td>NaN</td>
      <td>150000.0</td>
    </tr>
    <tr>
      <th>Guangzhou</th>
      <td>25000.0</td>
      <td>200000.0</td>
    </tr>
    <tr>
      <th>Hangzhou</th>
      <td>20000.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Shanghai</th>
      <td>60000.0</td>
      <td>400000.0</td>
    </tr>
    <tr>
      <th>Shenzhen</th>
      <td>50000.0</td>
      <td>300000.0</td>
    </tr>
    <tr>
      <th>Suzhou</th>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Tianjin</th>
      <td>NaN</td>
      <td>200000.0</td>
    </tr>
  </tbody>
</table>
</div>



也可以用一个list of dicts来构建DataFrame


```python
data = [{"BOSS":999999,"Han":1000,"Jason":50000},{"BOSS":99999,"Han":200,"Jason":8000}]
df=pd.DataFrame(data,columns=["BOSS","Han","Jason"])
df
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
      <th>BOSS</th>
      <th>Han</th>
      <th>Jason</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>999999</td>
      <td>1000</td>
      <td>50000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>99999</td>
      <td>200</td>
      <td>8000</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.DataFrame(data, index=["salary", "bonus"])

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
      <th>BOSS</th>
      <th>Han</th>
      <th>Jason</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>salary</th>
      <td>999999</td>
      <td>1000</td>
      <td>50000</td>
    </tr>
    <tr>
      <th>bonus</th>
      <td>99999</td>
      <td>200</td>
      <td>8000</td>
    </tr>
  </tbody>
</table>
</div>




```python
df=pd.DataFrame({"apts":apts,"cars":cars})
df
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
      <th>Beijing</th>
      <td>55000.0</td>
      <td>300000.0</td>
    </tr>
    <tr>
      <th>Chongqing</th>
      <td>NaN</td>
      <td>150000.0</td>
    </tr>
    <tr>
      <th>Guangzhou</th>
      <td>25000.0</td>
      <td>200000.0</td>
    </tr>
    <tr>
      <th>Hangzhou</th>
      <td>20000.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Shanghai</th>
      <td>60000.0</td>
      <td>400000.0</td>
    </tr>
    <tr>
      <th>Shenzhen</th>
      <td>50000.0</td>
      <td>300000.0</td>
    </tr>
    <tr>
      <th>Suzhou</th>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Tianjin</th>
      <td>NaN</td>
      <td>200000.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df["apts"]
```




    Beijing      55000.0
    Chongqing        NaN
    Guangzhou    25000.0
    Hangzhou     20000.0
    Shanghai     60000.0
    Shenzhen     50000.0
    Suzhou           NaN
    Tianjin          NaN
    Name: apts, dtype: float64




```python
import pandas as pd
data = {'city': ['Beijing', 'Shanghai', 'Guangzhou', 'Shenzhen', 'Hangzhou', 'Chongqing'],
       'year': [2016,2017,2016,2017,2016, 2016],
       'population': [2100, 2300, 1000, 700, 500, 500]}
pd.DataFrame(data)
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
      <th>city</th>
      <th>year</th>
      <th>population</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Beijing</td>
      <td>2016</td>
      <td>2100</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Shanghai</td>
      <td>2017</td>
      <td>2300</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Guangzhou</td>
      <td>2016</td>
      <td>1000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Shenzhen</td>
      <td>2017</td>
      <td>700</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Hangzhou</td>
      <td>2016</td>
      <td>500</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Chongqing</td>
      <td>2016</td>
      <td>500</td>
    </tr>
  </tbody>
</table>
</div>




```python
df["total_cost"]=df["apts"]*100 +df["cars"]
df
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
      <th>total_cost</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Beijing</th>
      <td>55000.0</td>
      <td>300000.0</td>
      <td>5800000.0</td>
    </tr>
    <tr>
      <th>Chongqing</th>
      <td>NaN</td>
      <td>150000.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Guangzhou</th>
      <td>25000.0</td>
      <td>200000.0</td>
      <td>2700000.0</td>
    </tr>
    <tr>
      <th>Hangzhou</th>
      <td>20000.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Shanghai</th>
      <td>60000.0</td>
      <td>400000.0</td>
      <td>6400000.0</td>
    </tr>
    <tr>
      <th>Shenzhen</th>
      <td>50000.0</td>
      <td>300000.0</td>
      <td>5300000.0</td>
    </tr>
    <tr>
      <th>Suzhou</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Tianjin</th>
      <td>NaN</td>
      <td>200000.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 注意一下Series与DataFrame的区别
frame['city'] #Series
type(frame['city'])
frame[['city']] #DataFrame
type(frame[['city']])
```




    pandas.core.frame.DataFrame




```python
frame[["city","year"]]
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
      <th>city</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>Beijing</td>
      <td>2016</td>
    </tr>
    <tr>
      <th>two</th>
      <td>Shanghai</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>three</th>
      <td>Guangzhou</td>
      <td>2016</td>
    </tr>
    <tr>
      <th>four</th>
      <td>Shenzhen</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>five</th>
      <td>Hangzhou</td>
      <td>2016</td>
    </tr>
    <tr>
      <th>six</th>
      <td>Chongqing</td>
      <td>2016</td>
    </tr>
  </tbody>
</table>
</div>



loc方法可以拿到行


```python
# loc+index取出行
frame.loc['three']
type(frame.loc['three'])
```




    pandas.core.series.Series




```python
frame.loc[["one","two"],["city","year"]]
type (frame.loc[["one","two"],["city","year"]])
```




    pandas.core.frame.DataFrame



iloc方法可以拿到行和列，把pandas dataframe当做numpy的ndarray来操作


```python
frame.head()
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
      <th>year</th>
      <th>city</th>
      <th>population</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>2016</td>
      <td>Beijing</td>
      <td>2100</td>
    </tr>
    <tr>
      <th>two</th>
      <td>2017</td>
      <td>Shanghai</td>
      <td>2300</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2016</td>
      <td>Guangzhou</td>
      <td>1000</td>
    </tr>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>Shenzhen</td>
      <td>700</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2016</td>
      <td>Hangzhou</td>
      <td>500</td>
    </tr>
  </tbody>
</table>
</div>



## DataFrame数据选择与赋值

大多数情况下，我们的赋值操作都是在数据选择之后进行赋值的，DataFrame的数据选择有很多不同的函数，相对比较自由。但是建议大家使用loc函数进行数据选择。

具体的语法为df.loc[行条件,列条件]


```python
frame
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
      <th>year</th>
      <th>city</th>
      <th>population</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>2016</td>
      <td>Beijing</td>
      <td>2100</td>
    </tr>
    <tr>
      <th>two</th>
      <td>2017</td>
      <td>Shanghai</td>
      <td>2300</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2016</td>
      <td>Guangzhou</td>
      <td>1000</td>
    </tr>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>Shenzhen</td>
      <td>700</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2016</td>
      <td>Hangzhou</td>
      <td>500</td>
    </tr>
    <tr>
      <th>six</th>
      <td>2016</td>
      <td>Chongqing</td>
      <td>500</td>
    </tr>
  </tbody>
</table>
</div>




```python
frame.loc["one","population"]=2200
frame
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
      <th>year</th>
      <th>city</th>
      <th>population</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>2016</td>
      <td>Beijing</td>
      <td>2200</td>
    </tr>
    <tr>
      <th>two</th>
      <td>2017</td>
      <td>Shanghai</td>
      <td>2300</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2016</td>
      <td>Guangzhou</td>
      <td>1000</td>
    </tr>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>Shenzhen</td>
      <td>700</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2016</td>
      <td>Hangzhou</td>
      <td>500</td>
    </tr>
    <tr>
      <th>six</th>
      <td>2016</td>
      <td>Chongqing</td>
      <td>500</td>
    </tr>
  </tbody>
</table>
</div>




```python
frame.loc[:,"debt"]=100
frame
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
      <th>year</th>
      <th>city</th>
      <th>population</th>
      <th>debt</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>2016</td>
      <td>Beijing</td>
      <td>2200</td>
      <td>100</td>
    </tr>
    <tr>
      <th>two</th>
      <td>2017</td>
      <td>Shanghai</td>
      <td>2300</td>
      <td>100</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2016</td>
      <td>Guangzhou</td>
      <td>1000</td>
      <td>100</td>
    </tr>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>Shenzhen</td>
      <td>700</td>
      <td>100</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2016</td>
      <td>Hangzhou</td>
      <td>500</td>
      <td>100</td>
    </tr>
    <tr>
      <th>six</th>
      <td>2016</td>
      <td>Chongqing</td>
      <td>500</td>
      <td>100</td>
    </tr>
  </tbody>
</table>
</div>




```python
frame.loc["six","city"]=0
frame
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
      <th>year</th>
      <th>city</th>
      <th>population</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>2016</td>
      <td>Beijing</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>two</th>
      <td>2017</td>
      <td>Shanghai</td>
      <td>200.0</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2016</td>
      <td>Guangzhou</td>
      <td>300.0</td>
    </tr>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>Shenzhen</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2016</td>
      <td>Hangzhou</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>six</th>
      <td>2016</td>
      <td>0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



我们可以给定多个条件进行组合，选择对应的数据。每个条件用小括号包裹，同时通过&(与) |(或) ~(非)进行组合。


```python
frame.loc[:]
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
      <th>year</th>
      <th>city</th>
      <th>population</th>
      <th>debt</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>2016</td>
      <td>Beijing</td>
      <td>2200</td>
      <td>100</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2016</td>
      <td>Guangzhou</td>
      <td>1000</td>
      <td>100</td>
    </tr>
  </tbody>
</table>
</div>




```python
frame.loc[(frame["year"]==2016)|(frame["city"]!="Shanghai")&(frame["population"]==1000),["population","debt"]]
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
      <th>population</th>
      <th>debt</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>2200</td>
      <td>100</td>
    </tr>
    <tr>
      <th>three</th>
      <td>1000</td>
      <td>100</td>
    </tr>
    <tr>
      <th>five</th>
      <td>500</td>
      <td>100</td>
    </tr>
  </tbody>
</table>
</div>



还可以用Series来指定需要修改的index以及相对应的value，没有指定的默认用NaN.


```python
import pandas as pd
data = {'city': ['Beijing', 'Shanghai', 'Guangzhou', 'Shenzhen', 'Hangzhou', 'Chongqing'],
       'year': [2016,2017,2016,2017,2016, 2016],
       'population': [2100, 2300, 1000, 700, 500, 500]}
pd.DataFrame(data)
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
      <th>city</th>
      <th>year</th>
      <th>population</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Beijing</td>
      <td>2016</td>
      <td>2100</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Shanghai</td>
      <td>2017</td>
      <td>2300</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Guangzhou</td>
      <td>2016</td>
      <td>1000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Shenzhen</td>
      <td>2017</td>
      <td>700</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Hangzhou</td>
      <td>2016</td>
      <td>500</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Chongqing</td>
      <td>2016</td>
      <td>500</td>
    </tr>
  </tbody>
</table>
</div>




```python
frame = pd.DataFrame(data, columns = ['year', 'city', 'population'],index = ['one', 'two', 'three', 'four', 'five', 'six'])
val = pd.Series([100, 200, 300], index=['two', 'three', 'five'])
frame['debt'] = val
frame
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
      <th>year</th>
      <th>city</th>
      <th>population</th>
      <th>debt</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>2016</td>
      <td>Beijing</td>
      <td>2100</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>two</th>
      <td>2017</td>
      <td>Shanghai</td>
      <td>2300</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2016</td>
      <td>Guangzhou</td>
      <td>1000</td>
      <td>200.0</td>
    </tr>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>Shenzhen</td>
      <td>700</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2016</td>
      <td>Hangzhou</td>
      <td>500</td>
      <td>300.0</td>
    </tr>
    <tr>
      <th>six</th>
      <td>2016</td>
      <td>Chongqing</td>
      <td>500</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
frame=pd.DataFrame(data,columns=["year","city","population"],index=["one","two","three","four","five","six"])
val=pd.Series([100,200,300],index=["one","two","three"])
frame["population"]=val
frame
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
      <th>year</th>
      <th>city</th>
      <th>population</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>2016</td>
      <td>Beijing</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>two</th>
      <td>2017</td>
      <td>Shanghai</td>
      <td>200.0</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2016</td>
      <td>Guangzhou</td>
      <td>300.0</td>
    </tr>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>Shenzhen</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2016</td>
      <td>Hangzhou</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>six</th>
      <td>2016</td>
      <td>Chongqing</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
val=pd.Series([100,200,300],index=["one","two","three"])
frame["population"]=val
frame
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
      <th>year</th>
      <th>city</th>
      <th>population</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>2016</td>
      <td>Beijing</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>two</th>
      <td>2017</td>
      <td>Shanghai</td>
      <td>200.0</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2016</td>
      <td>Guangzhou</td>
      <td>300.0</td>
    </tr>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>Shenzhen</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2016</td>
      <td>Hangzhou</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>six</th>
      <td>2016</td>
      <td>Chongqing</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



选择数据

想知道有哪些列


```python
frame.index
```




    Index(['one', 'two', 'three', 'four', 'five', 'six'], dtype='object')



想知道有哪些行


```python
frame.columns
```




    Index(['year', 'city', 'population'], dtype='object')



转置DataFrame


```python
frame.T
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
      <th>one</th>
      <th>two</th>
      <th>three</th>
      <th>four</th>
      <th>five</th>
      <th>six</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>year</th>
      <td>2016</td>
      <td>2017</td>
      <td>2016</td>
      <td>2017</td>
      <td>2016</td>
      <td>2016</td>
    </tr>
    <tr>
      <th>city</th>
      <td>Beijing</td>
      <td>Shanghai</td>
      <td>Guangzhou</td>
      <td>Shenzhen</td>
      <td>Hangzhou</td>
      <td>Chongqing</td>
    </tr>
    <tr>
      <th>population</th>
      <td>300</td>
      <td>400</td>
      <td>500</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



# csv文件读写

-read_csv
-to_csv


```python
import pandas as pd
pokemon = pd.read_csv("../Anaconda3/Pokemon.csv")
pokemon.head(10)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>318</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>405</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>525</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>625</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>309</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Charmeleon</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>405</td>
      <td>58</td>
      <td>64</td>
      <td>58</td>
      <td>80</td>
      <td>65</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Charizard</td>
      <td>Fire</td>
      <td>Flying</td>
      <td>534</td>
      <td>78</td>
      <td>84</td>
      <td>78</td>
      <td>109</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>7</th>
      <td>6</td>
      <td>CharizardMega Charizard X</td>
      <td>Fire</td>
      <td>Dragon</td>
      <td>634</td>
      <td>78</td>
      <td>130</td>
      <td>111</td>
      <td>130</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>8</th>
      <td>6</td>
      <td>CharizardMega Charizard Y</td>
      <td>Fire</td>
      <td>Flying</td>
      <td>634</td>
      <td>78</td>
      <td>104</td>
      <td>78</td>
      <td>159</td>
      <td>115</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>9</th>
      <td>7</td>
      <td>Squirtle</td>
      <td>Water</td>
      <td>NaN</td>
      <td>314</td>
      <td>44</td>
      <td>48</td>
      <td>65</td>
      <td>50</td>
      <td>64</td>
      <td>43</td>
      <td>1</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
#describe可以帮我们了解数据的统计特性
pokemon.describe()
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
      <th>#</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>800.000000</td>
      <td>800.00000</td>
      <td>800.000000</td>
      <td>800.000000</td>
      <td>800.000000</td>
      <td>800.000000</td>
      <td>800.000000</td>
      <td>800.000000</td>
      <td>800.00000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>362.813750</td>
      <td>435.10250</td>
      <td>69.258750</td>
      <td>79.001250</td>
      <td>73.842500</td>
      <td>72.820000</td>
      <td>71.902500</td>
      <td>68.277500</td>
      <td>3.32375</td>
    </tr>
    <tr>
      <th>std</th>
      <td>208.343798</td>
      <td>119.96304</td>
      <td>25.534669</td>
      <td>32.457366</td>
      <td>31.183501</td>
      <td>32.722294</td>
      <td>27.828916</td>
      <td>29.060474</td>
      <td>1.66129</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000000</td>
      <td>180.00000</td>
      <td>1.000000</td>
      <td>5.000000</td>
      <td>5.000000</td>
      <td>10.000000</td>
      <td>20.000000</td>
      <td>5.000000</td>
      <td>1.00000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>184.750000</td>
      <td>330.00000</td>
      <td>50.000000</td>
      <td>55.000000</td>
      <td>50.000000</td>
      <td>49.750000</td>
      <td>50.000000</td>
      <td>45.000000</td>
      <td>2.00000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>364.500000</td>
      <td>450.00000</td>
      <td>65.000000</td>
      <td>75.000000</td>
      <td>70.000000</td>
      <td>65.000000</td>
      <td>70.000000</td>
      <td>65.000000</td>
      <td>3.00000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>539.250000</td>
      <td>515.00000</td>
      <td>80.000000</td>
      <td>100.000000</td>
      <td>90.000000</td>
      <td>95.000000</td>
      <td>90.000000</td>
      <td>90.000000</td>
      <td>5.00000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>721.000000</td>
      <td>780.00000</td>
      <td>255.000000</td>
      <td>190.000000</td>
      <td>230.000000</td>
      <td>194.000000</td>
      <td>230.000000</td>
      <td>180.000000</td>
      <td>6.00000</td>
    </tr>
  </tbody>
</table>
</div>




```python
pokemon.loc[:50,["HP","Ddfense"]].to_csv("../Anaconda3/pokemon_tmp.csv")
```

    D:\anaconda2\lib\site-packages\pandas\core\indexing.py:1472: FutureWarning: 
    Passing list-likes to .loc or [] with any missing label will raise
    KeyError in the future, you can use .reindex() as an alternative.
    
    See the documentation here:
    https://pandas.pydata.org/pandas-docs/stable/indexing.html#deprecate-loc-reindex-listlike
      return self._getitem_tuple(key)
    

# 数据缺失


```python
reference
```


```python
pokemon.loc[10:16,:]
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10</th>
      <td>8</td>
      <td>Wartortle</td>
      <td>Water</td>
      <td>NaN</td>
      <td>405</td>
      <td>59</td>
      <td>63</td>
      <td>80</td>
      <td>65</td>
      <td>80</td>
      <td>58</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>11</th>
      <td>9</td>
      <td>Blastoise</td>
      <td>Water</td>
      <td>NaN</td>
      <td>530</td>
      <td>79</td>
      <td>83</td>
      <td>100</td>
      <td>85</td>
      <td>105</td>
      <td>78</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>12</th>
      <td>9</td>
      <td>BlastoiseMega Blastoise</td>
      <td>Water</td>
      <td>NaN</td>
      <td>630</td>
      <td>79</td>
      <td>103</td>
      <td>120</td>
      <td>135</td>
      <td>115</td>
      <td>78</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>13</th>
      <td>10</td>
      <td>Caterpie</td>
      <td>Bug</td>
      <td>NaN</td>
      <td>195</td>
      <td>45</td>
      <td>30</td>
      <td>35</td>
      <td>20</td>
      <td>20</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>14</th>
      <td>11</td>
      <td>Metapod</td>
      <td>Bug</td>
      <td>NaN</td>
      <td>205</td>
      <td>50</td>
      <td>20</td>
      <td>55</td>
      <td>25</td>
      <td>25</td>
      <td>30</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>15</th>
      <td>12</td>
      <td>Butterfree</td>
      <td>Bug</td>
      <td>Flying</td>
      <td>395</td>
      <td>60</td>
      <td>45</td>
      <td>50</td>
      <td>90</td>
      <td>80</td>
      <td>70</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>16</th>
      <td>13</td>
      <td>Weedle</td>
      <td>Bug</td>
      <td>Poison</td>
      <td>195</td>
      <td>40</td>
      <td>35</td>
      <td>30</td>
      <td>20</td>
      <td>20</td>
      <td>50</td>
      <td>1</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
#判断数据是否有缺失
pokemon.isnull()
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>5</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>6</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>7</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>8</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>9</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>10</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>11</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>12</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>13</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>14</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>15</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>16</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>17</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>18</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>19</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>20</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>21</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>22</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>23</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>24</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>25</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>26</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>27</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>28</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>29</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
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
    </tr>
    <tr>
      <th>770</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>771</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>772</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>773</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>774</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>775</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>776</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>777</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>778</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>779</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>780</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>781</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>782</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>783</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>784</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>785</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>786</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>787</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>788</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>789</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>790</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>791</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>792</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>793</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>794</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>795</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>796</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>797</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>798</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>799</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
<p>800 rows × 13 columns</p>
</div>




```python
# 判断数据是否无缺失
```


```python
pokemon.notnull()
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>4</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>5</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>6</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>7</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>8</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>9</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>10</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>11</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>12</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>13</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>14</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>15</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>16</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>17</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>18</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>19</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>20</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>21</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>22</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>23</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>24</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>25</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>26</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>27</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>28</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>29</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
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
    </tr>
    <tr>
      <th>770</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>771</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>772</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>773</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>774</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>775</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>776</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>777</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>778</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>779</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>780</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>781</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>782</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>783</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>784</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>785</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>786</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>787</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>788</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>789</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>790</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>791</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>792</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>793</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>794</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>795</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>796</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>797</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>798</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>799</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
<p>800 rows × 13 columns</p>
</div>




```python
cities = {'Beijing': 55000, 'Shanghai': 60000, 'Shenzhen': 50000, 'Hangzhou': 20000, 'Guangzhou': 25000, 'Suzhou': None}
apts = pd.Series(cities)
apts
```




    Beijing      55000.0
    Shanghai     60000.0
    Shenzhen     50000.0
    Hangzhou     20000.0
    Guangzhou    25000.0
    Suzhou           NaN
    dtype: float64




```python
print(apts[apts.isnull()])#判断数据是否缺失
```

    Suzhou   NaN
    dtype: float64
    


```python
print(apts[apts.isnull()== False]) #根据数据是否缺失选择数据
```

    Beijing      55000.0
    Shanghai     60000.0
    Shenzhen     50000.0
    Hangzhou     20000.0
    Guangzhou    25000.0
    dtype: float64
    


```python
import numpy as np
df = pd.DataFrame(np.random.rand(10,4),columns=list("abcd"))
df
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
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.751859</td>
      <td>0.684991</td>
      <td>0.527920</td>
      <td>0.500135</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.053578</td>
      <td>0.262967</td>
      <td>0.749619</td>
      <td>0.347938</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.359095</td>
      <td>0.430271</td>
      <td>0.233142</td>
      <td>0.016490</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.024023</td>
      <td>0.868547</td>
      <td>0.482118</td>
      <td>0.133838</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.811960</td>
      <td>0.783656</td>
      <td>0.054895</td>
      <td>0.952696</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.448678</td>
      <td>0.333494</td>
      <td>0.216211</td>
      <td>0.277872</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0.167217</td>
      <td>0.531840</td>
      <td>0.520069</td>
      <td>0.752797</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0.515915</td>
      <td>0.633703</td>
      <td>0.070737</td>
      <td>0.960054</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0.379936</td>
      <td>0.722115</td>
      <td>0.352121</td>
      <td>0.346624</td>
    </tr>
    <tr>
      <th>9</th>
      <td>0.422430</td>
      <td>0.745857</td>
      <td>0.867953</td>
      <td>0.742086</td>
    </tr>
  </tbody>
</table>
</div>



## 数据删除


```python
import pandas as pd
data = {'city': ['Beijing', 'Shanghai', 'Guangzhou', 'Shenzhen', 'Hangzhou', 'Chongqing'],
       'year': [2016,2017,2016,2017,2016, 2016],
       'population': [2100, 2300, 1000, 700, 500, 500]}
frame = pd.DataFrame(data, columns = ['year', 'city', 'population'],index = ['one', 'two', 'three', 'four', 'five', 'six'])
frame
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
      <th>year</th>
      <th>city</th>
      <th>population</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>2016</td>
      <td>Beijing</td>
      <td>2100</td>
    </tr>
    <tr>
      <th>two</th>
      <td>2017</td>
      <td>Shanghai</td>
      <td>2300</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2016</td>
      <td>Guangzhou</td>
      <td>1000</td>
    </tr>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>Shenzhen</td>
      <td>700</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2016</td>
      <td>Hangzhou</td>
      <td>500</td>
    </tr>
    <tr>
      <th>six</th>
      <td>2016</td>
      <td>Chongqing</td>
      <td>500</td>
    </tr>
  </tbody>
</table>
</div>




```python
frame.drop(["one","two"])
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
      <th>year</th>
      <th>city</th>
      <th>population</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>three</th>
      <td>2016</td>
      <td>Guangzhou</td>
      <td>1000</td>
    </tr>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>Shenzhen</td>
      <td>700</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2016</td>
      <td>Hangzhou</td>
      <td>500</td>
    </tr>
    <tr>
      <th>six</th>
      <td>2016</td>
      <td>Chongqing</td>
      <td>500</td>
    </tr>
  </tbody>
</table>
</div>




```python
frame.drop("city",axis=1)#删除第二个维度的元素
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
      <th>year</th>
      <th>population</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>2016</td>
      <td>2100</td>
    </tr>
    <tr>
      <th>two</th>
      <td>2017</td>
      <td>2300</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2016</td>
      <td>1000</td>
    </tr>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>700</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2016</td>
      <td>500</td>
    </tr>
    <tr>
      <th>six</th>
      <td>2016</td>
      <td>500</td>
    </tr>
  </tbody>
</table>
</div>


