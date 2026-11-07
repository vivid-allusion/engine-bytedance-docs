---
title: "Basic usage of Spark RDD"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Basic_usage_of_Spark_RDD"
---

<span id="dc5c2c4e"></span>
## **1 What is Spark RDD**

`RDD` (Resilient Distributed Dataset) is the most fundamental data abstraction in Spark. It represents a fault\-tolerant, parallelizable collection. `RDD` consists of a series of partitions (`Partition`), each of which can be processed independently. `RDD` also provides a series of operations (operators) for various data transformations and manipulations.

<span id="61116c90"></span>
## **2 Creating RDDs**

In Spark, `RDD` can be created in multiple ways, such as reading data from local files, HDFS, Kafka, and other data sources, or by transforming an existing `RDD` to obtain a new `RDD`. The following are several common ways to create `RDD`:


1. **Create RDD from local files**


```Python
from pyspark.sql import SparkSession
spark = SparkSession.builder.appName("LocalFileRDD").getOrCreate()
# 读取本地文件，创建 RDD
data = spark.read.text("path/to/file.txt")
```



2. **Create RDD from HDFS**


```Python
from pyspark.sql import SparkSession
spark = SparkSession.builder.appName("HDFSRDD").getOrCreate()
# 读取 HDFS 文件，创建 RDD
data = spark.read.csv("hdfs://localhost:9000/path/to/file.csv")
```



3. **Transform an existing RDD to obtain a new RDD**


```Python
from pyspark.sql import SparkSession
spark = SparkSession.builder.appName("TransformRDD").getOrCreate()
# 创建一个整数类型的 RDD
intRDD = spark.range(1, 10)
# 将 intRDD 转换为字符串类型的 RDD
strRDD = intRDD.map(lambda x: str(x))
# 打印 strRDD 的内容
strRDD.collect()
```


<span id="1f7bcad7"></span>
## **3 RDD operators**

`RDD` provides a series of operators for various data transformations and manipulations. The following are several common `RDD` operators:


1. **map() operator**: Applies a mapping operation to each element in the `RDD` and returns a new `RDD`.


```Python
from pyspark.sql import SparkSession
spark = SparkSession.builder.appName("MapOperator").getOrCreate()
# 创建一个整数类型的 RDD
intRDD = spark.range(1, 10)
# 将 intRDD 中的每个元素加 1，返回一个新的 RDD
resultRDD = intRDD.map(lambda x: x + 1)
# 打印结果 RDD 的内容
resultRDD.collect()
```



2. **filter() operator**: Applies a filtering operation to each element in the `RDD` and returns a new `RDD`.


```Python
from pyspark.sql import SparkSession
spark = SparkSession.builder.appName("FilterOperator").getOrCreate()
# 创建一个整数类型的 RDD
intRDD = spark.range(1, 10)
# 过滤出偶数，返回一个新的 RDD
evenRDD = intRDD.filter(lambda x: x % 2 == 0)
# 打印偶数 RDD 的内容
evenRDD.collect()
```



3. **reduce() operator**: Performs an aggregation operation on each partition in the `RDD` and returns a new `RDD`.


```Python
from pyspark.sql import SparkSession
spark = SparkSession.builder.appName("ReduceOperator").getOrCreate()
# 创建一个整数类型的 RDD
intRDD = spark.range(1, 10)
# 对每个分区的元素进行求和，返回一个新的 RDD
resultRDD = intRDD.reduce(lambda x, y: x + y)
# 打印结果 RDD 的内容
resultRDD.collect()
```



4. **groupByKey() operator**: Groups the data in the `RDD` by the specified key and returns a new `RDD`, where each element is a `Tuple2` containing the grouping key and the collection of grouped elements.


```Python
from pyspark.sql import SparkSession
# 创建 SparkSession 实例
spark = SparkSession.builder.appName("GroupByKeyOperator").getOrCreate()
# 创建一个示例 RDD
data = [("A", 1), ("B", 2), ("A", 3), ("B", 4), ("A", 5)]
rdd = spark.sparkContext.parallelize(data)
# 使用 groupByKey() 进行分组
grouped_rdd = rdd.groupbyKey(lambda x: x[0])
# 打印分组结果
for key, group in grouped_rdd.collect():
    print(f"Key: {key}, Values: {group}")
```


<span id="1c915d99"></span>
## **4 RDD persistence**

In Spark, the computation of `RDD` is memory\-based. If the data volume in `RDD` is large, it may lead to insufficient memory and affect computational performance. To address this issue, Spark provides RDD persistence functionality, which allows the data in `RDD` to be persisted to disk to free up memory. The following are several common `RDD` persistence methods:


1. **cache() method**: Caches the `RDD` data in memory to accelerate subsequent computations.


```Python
from pyspark.sql import SparkSession
spark = SparkSession.builder.appName("CacheRDD").getOrCreate()
# 创建一个整数类型的 RDD
intRDD = spark.range(1, 10)
# 将 intRDD 数据缓存到内存中
intRDD.cache()
```



2. **persist() method**: Persists the `RDD` data to disk to free up memory.


```Python
from pyspark.sql import SparkSession
spark = SparkSession.builder.appName("PersistRDD").getOrCreate()
# 创建一个整数类型的 RDD
intRDD = spark.range(1, 10)
# 将 intRDD 数据持久化到磁盘上
intRDD.persist()
```
