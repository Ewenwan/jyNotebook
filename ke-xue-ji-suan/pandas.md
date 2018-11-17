### 关键缩写和包导入

##### 声明

* df:任意的pandas DataFrame对象
* s:任意的pandas Series对象

##### 导入包

```
import pandas as pd
import numpy as np
```

### 导入数据

* pandas.read\_csv\(filename,sep,header,names\):从csv文件导入数据
  * filename:csv文件名
  * sep:如果不指定参数，则尝试使用逗号分隔符
  * header:指定函数用来作为列名，数据开始行数。如果文件中没有列名，则默认为0\[第一行数据\],否者设置为None
  * names:用于结果的列名列表，如果数据文件中没有列标题行，就需要执行header=None，names属性在header之前运行
  * prefix:在没有列标题时，也就是header设定为None，给列添加前缀，例如prefix='x'==&gt;x0
  * skip\_blank\_lines:如果为True，则跳过空行；否则记为NaN
* pandas.read\_table\(filename,na\_values\):从限定分隔符的文本文件导入数据,默认分隔符为"\t"
  * filename:文件名
  * 缺失值处理:na\_values= \["null"\]，用null字符替换缺失值
* pd.read\_excel\(filename,sheetname,header\):从excel文件导入数据

  * filename:excel文件名

  * sheetname:表名

* pd.read\_sql\(sql,conn\):从sql表/库导入数据

  * sql:将要查询的语句即"select \* from table"

  * conn:sql对象即conn = pymysql.connect\(\)

* pd.read\_sql\_table\(table\_name,conn\):将sql数据库表读入DataFrame

  * table\_name:表名

  * conn:sql对象

  ```
  import pandas as pd
  import pymysql
  from sqlalchemy import create_engine

  con = create_engine('mysql+pymysql://user_name:password@127.0.0.1:3306/database_name')
  data = pd.read_sql_table("table_name", con)
  data.to_csv("table_name.csv")
  ```

* pd.read\_json\(json\_string\):从json格式的字符串导入数据

  * json\_string:文件名/json数据

* pd.read\_html\(url\)：解析URL、字符串或者HTML文件，抽取其中的tables表格

* pd.read\_clipboard\(\)：从你的粘贴板获取内容，并传给read\_table\(\)

* pd.DataFrame\(dict\)：从字典对象导入数据，Key是列名，Value是数据

### 导出数据

* df.to\_csv\(filename\)：导出数据到CSV文件

* df.to\_excel\(filename\)：导出数据到Excel文件

* df.to\_sql\(table\_name, connection\_object\)：导出数据到SQL表

  * table\_name:表名
  * connection\_object:sql连接对象

* df.to\_json\(filename\)：以Json格式导出数据到文本文件

### pandas对象

* Series：有序，有索引（一维数据结构）

* Dataframe：有序，有索引（二维数据结构）

  * pd.DataFrame\(data,columns\)

    * data:数组

    * columns:列索引

* index 对象：即 Series 和 DataFrame 的索引

### 查看、检查数据

* df.head\(n\):查看DataFrame对象的前n行
* df.tail\(n\):查看DataFrame对象的最后n行
* df.shape\(\):查看行数和列数
* df.info\(\):查看索引、数据类型和内存信息
* df.describe\(\):查看数值型列的汇总统计
* s.value\_counts\(dropna=False\):查看series对象的唯一值和计数
* df.apply\(pd.Series.value\_counts\):查看DataFrame对象中每一列的唯一值和计数

  ```
  train['Has_Cabin'] = train["Cabin"].apply(lambda x: 0 if type(x) == float else 1)

  传入一个函数，应用于一个列
  ```

### 获取数据

* df.columns = \['a','b','c'\]:重命名列名
* pd.isnull\(\):检查DataFrame对象中的空值，并返回一个Boolean数组
* pd.notnull\(\):检查DataFrame对象中的非空值，并返回一个Boolean数组
* df.dropna\(\):删除所有包含空值的行
* df.dropna\(axis=1\):删除所有包含空值的列
* df.dropna\(axis=1,thesh=n\):删除所有小与n个非空值的行
* df.fillna\(x\):用x替换DataFrame对象中所有的空值
* s.astype\(float\):将Series中的数据类型更改为float类型
* s.replace\(1,'one'\):用'one'代替所有等于1的值
* s.replace\(\[1,3\],\['one','three'\]\):用'one'代替1，用'three'代替3
* df.rename\(columns=lambda x:x+1\):批量更改列名
* df.rename\(columns={'old\_name':'new\_game'}\):选择性更改列名
* df.set\_index\('column\_one'\):更改索引列
* df.rename\(index=lambda x: x + 1\)：批量重命名索引
* df.loc\(value\):返回列值value相同的行数据
* df.loc\[col\_value,\[A,B\]\]:返回A,B列相同col\_value的列值

* ```
  print(df.loc['20130102'])
  """
  A    4
  B    5
  C    6
  D    7
  Name: 2013-01-02 00:00:00, dtype: int64
  """

  print(df.loc[:,['A','B']]) 
  """
               A   B
  2013-01-01   0   1
  2013-01-02   4   5
  2013-01-03   8   9
  2013-01-04  12  13
  2013-01-05  16  17
  2013-01-06  20  21
  """

  print(df.loc['20130102',['A','B']])
  """
  A    4
  B    5
  Name: 2013-01-02 00:00:00, dtype: int64
  """
  ```
* df.iloc\[x,y\]:选中行，再选中列

```
dates = pd.date_range('20130101', periods=6)
df = pd.DataFrame(np.arange(24).reshape((6,4)),index=dates, columns=['A','B','C','D'])

>>> df
             A   B   C   D
2013-01-01   0   1   2   3
2013-01-02   4   5   6   7
2013-01-03   8   9  10  11
2013-01-04  12  13  14  15
2013-01-05  16  17  18  19
2013-01-06  20  21  22  23
>>> df.iloc[3,1]
13
>>> df.iloc[3]
A    12
B    13
C    14
D    15
Name: 2013-01-04 00:00:00, dtype: int32
# 选中3,4行，再选中1,2列
>>> df.iloc[3:5,1:3]
             B   C
2013-01-04  13  14
2013-01-05  17  18
# 选中1,3,5行，然后再选中1,2列
>>> df.iloc[[1,3,5],1:3]
             B   C
2013-01-02   5   6
2013-01-04  13  14
2013-01-06  21  22
```

* df.ix:混合选择

```
>>> df.ix[:2]
            A  B  C  D
2013-01-01  0  1  2  3
2013-01-02  4  5  6  7
>>> df.ix[:2,['A','B']]
            A  B
2013-01-01  0  1
2013-01-02  4  5
```

### 数据处理

* df\[df\[col\]&gt;0.5\]:选择col列的值大于0.5的行

* df.sort\_values\(col1\):按照列col1排序数据，默认升序排列

* df.sort\_values\(col2,ascending=False\):按照列col2降序排列数据

* df.sort\_values\(\[col1,col2\],ascending=\[True,False\]\):先按列col1升序排列，后按col2降序排列数据

* df.groupby\(col\):返回一个按列col进行分组的Groupby对象

* df.groupby\(\[col1,col2\]\):返回一个按多列进行分组的Groupby对象

* df.groupby\(col1\)\[col2\]:返回按列col1进行分组后，列col2的均值

* df.pivot\_table\(index=col1,values=\[col2,col3\],aggfunc=max\):创建一个按列col1进行分组，并计算col2和col3的最大值的数据透视表
* df.groupby\(col1\).agg\(np.mean\):返回按列col1分组的所有列的均值
* data.apply\(np.mean\):对DataFrame中的每一列应用函数np.mean
* data.apply\(np.max,axis=1\):对DataFrame中的每一行应用函数np.max
* factorize\(\):将字符数据字符化，一个字符对应一个数字

  ```
  dic = {"X": ["a", "a", "b", "c"], "Y": [1, 2, 3, 4]}
  df = pd.DataFrame(dic)

  pd.factorize(df['X'])[0]

  Output:
  array([0, 0, 1, 2], dtype=int64)
  ```

### 数据合并

* df1.append\(df2\):将df2中的行添加到df1的尾部
* df.concat\(\[df1,df2\],axis,join\):将df2中的列添加到df1的尾部
  * axis=1,concat就是行对齐，将不同列名称的两张表合并
  * join
    * inner:内连接
    * outer:外连接
* df1.join\(df2,on=col1,how='inner'\):对df1的列和df2的列执行SQL形式的join

## 数据统计

* df.describe\(\):查看数据值列的汇总统计
* df.mean\(\):返回所有列的均值
* df.corr\(\):返回列与列之间的相关系数
* df.count\(\):返回每一列中的非空值的个数
* df.max\(\):返回每一列的最大值
* df.min\(\):返回每一列的最小值
* df.median\(\):返回每一列的中位数
* df.std\(\):返回每一列的标准差



