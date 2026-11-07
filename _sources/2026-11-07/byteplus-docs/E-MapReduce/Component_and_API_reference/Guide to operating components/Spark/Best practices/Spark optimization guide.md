---
title: "Spark optimization guide"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Spark_optimization_guide"
---

<span id="8324a3b1"></span>
## 1 CPU and memory configuration

Configure the number of Spark executors (set `--num-executors`) and executor settings (configure `--executor-cores`, `--executor-memory`) appropriately based on task requirements and hardware resources.

For CPU\-intensive tasks (commonly seen in data science scenarios), the total task parallelism should be set to the total number of cores (or total cores minus one to prevent the system from being unable to respond to other tasks).

For memory\-intensive tasks (most Spark SQL jobs fall into this category), configure the memory size of each executor appropriately according to the memory available in Yarn. Caution, `--executor-memory` refers to JVM heap memory, and its actual usage depends on the situation:


1. If it is only a Scala/Java job, or the Python operator part of a PySpark job does not have additional memory consumption, the total memory usage is approximately 1.1 times the heap memory (refer to the official documentation for `spark.executor.memoryOverhead`).

2. If it is a PySpark job and there are data structures within the Python operator, this portion of memory is not managed by Spark. In this case, it is necessary to estimate Python's memory usage appropriately.


<span id="9f383d63"></span>
## 2 Parallelism configuration

This mainly involves two parameters.


1. `spark.default.parallelism`: affects the parallelism of Spark RDD jobs

2. `spark.sql.shuffle.partitions`: affects the parallelism of Spark SQL/streaming jobs


Caution, the above parameters are only a reference for Spark and do not necessarily guarantee that the actual number of tasks equals the configured parallelism.

<span id="0c0fd504"></span>
## 3 Handling data skew:

When data skew exists, the following methods can be used to address it:


* Use an appropriate data partitioning strategy to distribute data evenly across all nodes.

* Use Spark's mechanisms for resolving data skew, such as `repartition()`, optimizations for `groupBy()`, and more.

* If it is an SQL job, data skew can be optimized by adding a salt attribute.

* Enable Adaptive Query Execution (AQE, enabled by default in version 3.5.1).


<span id="b24b8cc6"></span>
## 4 Caching and persistence

Spark uses a lazy execution mechanism. When a transformation operation on a dataframe is too long, the entire DAG chain becomes lengthy, and some parts may be reusable. This leads to two issues:


1. Reusable operators can completely avoid redundant computation.

2. When the DAG is very complex, the effectiveness of Spark's optimizer is reduced, and automatic operator reuse may fail.


In this scenario, the following optimization methods are commonly used:


1. When memory capacity is sufficient, you can use the `cache()` operator to temporarily cache computation results in memory

2. When memory is limited, you can use the `persist()` operator to persist computation results

3. Use temporary tables to split the original, relatively complex DAG/pipeline by writing the results to temporary tables. This approach, on one hand, provides more stable performance; on the other hand, it makes troubleshooting easier when jobs fail


<span id="b0cd7386"></span>
## 5 JVM configuration

Configure appropriate parameters for the driver and executor JVMs using the following two parameters, such as setting the GC algorithm, enabling GC logging, and so on

```Bash
spark.driver.extraJavaOptions
spark.executor.extraJavaOptions
```


<span id="6b6f11ce"></span>
## 6 Remove Shuffle Service（RSS）

Compared to Spark's native shuffle, Remote Shuffle Service offers a series of advantages, including


1. Performance improvement: RSS uses push\-based shuffle, which allows data to be stored remotely during computation. Remote data storage is partition\-contiguous, effectively avoiding a large number of random reads and improving shuffle efficiency

2. Improved job execution stability: In traditional shuffle processes, if a node fails, it may cause the entire task to fail. With RSS, even if a node fails, other nodes can continue processing data, thereby improving job stability. Additionally, push\-based shuffle can reduce memory pressure on the executor side, further enhancing job stability

3. Reduced network transmission pressure: In traditional shuffle processes, data transmission between nodes can reach up to M \* N. Using RSS reduces this complexity to M + N, thereby alleviating network transmission pressure.

4. Supports large\-scale data processing: Because RSS can distribute data across different nodes, it can support large\-scale data processing tasks, which is not possible with traditional shuffle methods.
