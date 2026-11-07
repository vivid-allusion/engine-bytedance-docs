---
title: "Basic usage of PySpark"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Basic_usage_of_PySpark"
---

<span id="75816d94"></span>
## 1 Introduction

PySpark is the Python API for Apache Spark, allowing big data processing using the Python language. PySpark supports a variety of data processing tasks, including SQL queries, stream processing, machine learning, and many other tasks.

<span id="819d75f1"></span>
## 2 Installing PySpark and configuring the environment

PySpark is already included by default in the EMR environment, so no additional installation is required.

The environment used by PySpark is specified by `PYSPARK_PYTHON` by default. Users can configure this by navigating to "EMR Console \-\> Cluster \-\> Service List \-\> Spark". The configuration file is `spark-env.sh`.

<span id="804c2a41"></span>
## 3 Starting/stopping SparkSession

Starting PySpark initializes a SparkSession, which is the entry point for data processing with PySpark. There are two ways to use PySpark: non\-interactive (code) and interactive. An example of creating a SparkSession in code is as follows:

```Python
from pyspark.sql import SparkSession

# 创建 sparkSession
spark = SparkSession.builder \
    .appName("MyApp") \
    .getOrCreate()
    
# your code here...
# your code here...
# your code here...

# 停止 sparkSession
spark.stop()
```


The interactive command\-line startup is as follows:

```Python
pyspark --name "MyApp" --master yarn --num-executors 2 <other options>
```


After startup, a SparkSession named `spark` is initialized by default.

<span id="a267bfea"></span>
## 4 Basic operations

<span id="c938de26"></span>
### 4.1 RDD

```Python
# 使用 Python 集合创建 RDD
rdd = spark.sparkContext.parallelize([1, 2, 3, 4, 5])
print(rdd.collect())
# [1, 2, 3, 4, 5]

# 对其中每个元素乘 2
mapped_rdd = rdd.map(lambda x: x * 2)
print(mapped_rdd.collect())
# [2, 4, 6, 8, 10]
```


<span id="c504e14a"></span>
### 4.2 DataFrame

```Python
from pyspark.sql import DataFrame

# 将 RDD 转换为 DataFrame
rdd = spark.sparkContext.parallelize([("Sam", 28, 88), ("Flora", 28, 90), ("Run", 1, 60)])
df = rdd.toDF(["name", "age", "score"])
df.show()
# +-----+---+-----+
# | name|age|score|
# +-----+---+-----+
# |  Sam| 28|   88|
# |Flora| 28|   90|
# |  Run| 10|   60|
# +-----+---+-----+

# 从基础数据结构创建 DataFrame
df = spark.createDataFrame([
    ("Sam", 28, 88),
    ("Flora", 28, 90),
    ("Run", 10, 60)
], schema='name string, age int, score int')
df

# 从其他数据结构创建 DataFrame，比如 pandas
import pandas as pd
pandas_df = pd.DataFrame([['Sam', 28, 88], ['Flora', 28, 90], ['Run', 10, 60]],
                  columns=['name', 'age', 'score'])
df = spark.createDataFrame(pandas_df)

# 查询
df.select("name", "age").show()
# +-----+---+
# | name|age|
# +-----+---+
# |  Sam| 28|
# |Flora| 28|
# |  Run| 10|
# +-----+---+

# 转换
df.selectExpr("name", "score-10").show()
# +-----+-----+
# | name|score|
# +-----+-----+
# |  Sam|   78|
# |Flora|   80|
# |  Run|   50|
# +-----+-----+
```


<span id="fd40470b"></span>
### 4.3 Data reading and writing

PySpark supports reading from and writing to a variety of data sources, including CSV, JSON, Parquet, JDBC, and many other sources.


* **Reading data**


```Python
# 从 CSV 文件读取数据
csv_df = spark.read.csv("people.csv", header=True, inferSchema=True)
csv_df.show()

# 从 Parquet 文件读取数据
parquet_df = spark.read.parquet("data.parquet")
parquet_df.show()
```



* **Writing data**


```Python
# 将 DataFrame 写入 CSV 文件
df.write.csv("people_output.csv", header=True)

# 将 DataFrame 写入 Parquet 文件
df.write.parquet("people_output.parquet")
```


<span id="c4806123"></span>
## 5 Pandas API

Compared to the PySpark API, data scientists or machine learning practitioners are often more familiar with the Pandas API. For this reason, Spark introduced the Pandas API starting from version 3.2, and has made significant improvements and enhancements in subsequent versions. As of now (3.5.1), most Pandas APIs are supported in PySpark. There is little difference between using the Pandas API in Spark and using Pandas itself. In most cases, only the import statement needs to be changed:

```Python
import pyspark.pandas as ps
```


**Basic usage**

```Python
import pandas as pd
import numpy as np
import pyspark.pandas as ps
from pyspark.sql import SparkSession

# 创建一个 "pandas" Series
s = ps.Series([1, 3, 5, np.nan, 6, 8])
print(type(s))
# <class 'pyspark.pandas.series.Series'>

# 创建一个 "pandas" DataFrame
psdf = ps.DataFrame(
    {'a': [1, 2, 3, 4, 5, 6],
     'b': [100, 200, 300, 400, 500, 600],
     'c': ["one", "two", "three", "four", "five", "six"]},
    index=[10, 20, 30, 40, 50, 60])
print(type(psdf)
# <class 'pyspark.pandas.frame.DataFrame'>

# 基于一个 pandas DataFrame 创建一个 "pandas" DataFrame
pdf = pd.DataFrame()
psdf = ps.from_pandas(pdf)

# 将一个 "pandas DataFrame" 转化为 pandas DataFrame (注意由于 pandas 为单机引擎，这个操作会把 pyspark dataframe 的所有数据拉到本地)
pdf = psdf.to_pandas()

# 将一个 PySpark DataFrame 转化为 "pandas" DataFrame
sdf = spark.range(10)
psdf = sdf.pandas_api()

# 创建 "pandas" DataFrame 之后，就可以像 pandas 那样操作该 DataFrame 了
```


<span id="d18bd4a9"></span>
## 6 Important notes

The working principle of PySpark is that Python functions are translated into Scala functions via `py4j` and executed on the JVM. However, sometimes users have custom Python code to run. In such cases, Spark will start an additional Python process outside the Executor process to execute this code. This leads to two consequences:


1. There is inter\-process communication between the JVM and Python, which reduces computational efficiency compared to Scala programs.

2. By default, memory management for Python code must be handled by the developer, as Spark cannot manage this memory. Excessive usage may cause the process to be killed by Yarn or the operating system. In this case, configure `spark.executor.memoryOverhead` to request additional memory from Yarn.
