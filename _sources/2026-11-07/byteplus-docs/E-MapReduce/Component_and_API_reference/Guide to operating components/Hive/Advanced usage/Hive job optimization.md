---
title: "Hive job optimization"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Hive_job_optimization"
---

This article introduces how to optimize Hive jobs by adjusting memory, CPU, and the number of tasks.

<span id="_1-调优方案总览"></span>
## 1 Overview of optimization solutions


|Optimization direction |Optimization plan |
|---|---|
|Code optimization |Code optimization |
|Parameter tuning |* Memory parameter<br><br>* CPU parameter<br><br>* Enable vectorization<br><br>* Optimization of the number of tasks<br><br>* Merge small files |


<span id="_2-代码优化"></span>
## 2 Code optimization

<span id="_2-1-数据清洗"></span>
### 2.1 Data cleansing


* Filter data before performing JOIN operations.

* When reusing data, avoid redundant computations by creating intermediate tables and reusing them.

* Apply partition filtering when reading tables to avoid full table scans.


<span id="_2-2-多-distinct-优化"></span>
### 2.2 Optimization for multiple distinct operations


* Code before optimization

   ```sql
   SELECT g,
          COUNT(DISTINCT CASE WHEN a > 1 THEN user_id) cnt_user1,
          COUNT(DISTINCT CASE WHEN a > 2 THEN user_id) cnt_user2,
          COUNT(DISTINCT CASE WHEN a > 3 THEN user_id) cnt_user3,
          COUNT(DISTINCT CASE WHEN a > 4 THEN user_id) cnt_user4
   FROM tbl 
   GROUP BY g
   ```
   

   When using multiple distinct operations, the data volume expands during computation.

* Code after optimization

   ```sql
   SELECT g,
          SUM(CASE WHEN user1 > 0 THEN 1 END) as cnt_user1,
          SUM(CASE WHEN user2 > 0 THEN 1 END) as cnt_user2,
          SUM(CASE WHEN user3 > 0 THEN 1 END) as cnt_user3,
          SUM(CASE WHEN user4 > 0 THEN 1 END) as cnt_user4
   FROM 
           (SELECT g,user_id,
                   COUNT(CASE WHEN a > 1 THEN user_id) user1,
                   COUNT(CASE WHEN a > 2 THEN user_id) user2,
                   COUNT(CASE WHEN a > 3 THEN user_id) user3,
                   COUNT(CASE WHEN a > 4 THEN user_id) user4
           FROM tbl
           GROUP BY g,user_id  
           ) tmp 
   GROUP BY g
   ```
   

   Replace distinct operations with two group by steps: use the inner group by to deduplicate and reduce data volume, and the outer group by to sum, achieving the effect of distinct.


<span id="_2-3-数据倾斜"></span>
### 2.3 Data skew

Data skew typically occurs during group by or large table join operations, where certain keys have significantly larger data volumes, causing some operators to process much more data than others.


* Hotspots in group by:

   1. First, enable aggregation on the Map side.

   ```sql
   SET hive.map.aggr=true;
   SET hive.groupby.mapaggr.checkinterval=200000; （用于设定Map端进行聚合操作的条目数，视场景而定）
   ```
   

   2. Randomize and scatter keys, and aggregate multiple times.

   ```sql
   SET hive.groupby.skewindata=true;
   ```
   

   When hive.groupby.skewindata is set to true, the generated execution plan contains two MapReduce jobs.

   * In the first MapReduce job, the output result set from the Map phase is randomly distributed to the Reduce phase, where each part is aggregated and outputs results. This results in the same group by key possibly being distributed to different Reduce nodes, achieving load balancing.

   * The second MapReduce job redistributes the preprocessed data results to Reduce nodes based on the group by key, completing the final aggregation calculation.

* Hotspots in large table joins:

   The strategy is to randomize hotspot keys.

   For example, the event table contains many records where user_id is null, but the users table does not have records with null user_id. You can randomize null values before joining, which prevents all null values from being sent to a single Reduce task.

   ```sql
   SELECT * FROM event a LEFT OUTER 
   JOIN users b ON 
       CASE WHEN a.user_id IS NULL THEN CONCAT(‘dp_hive’,RAND()) 
       ELSE a.user_id=b.user_id 
       END;
   ```
   


<span id="_3-参数调优"></span>
## 3 Parameter optimization

<span id="_3-1-内存参数"></span>
### 3.1 Memory parameters

In the **EMR** cluster's **MapReduce2** service, you can adjust the memory for the Map and Reduce phases by setting the following parameters:


* Map

   
   |**Parameter** |**Description** |**Example** |
   |---|---|---|
   |**mapreduce.map.java.opts** |Default parameter, indicates JVM heap memory. |\-Xmx2048m |
   |**mapreduce.map.memory.mb** |Default parameter, indicates the total memory used by the JVM process. The calculation method is heap memory + off\-heap memory = 2048 + 256. |2304 |
   

* Reduce

   
   |**Parameter** |**Description** |**Example** |
   |---|---|---|
   |**mapreduce.reduce.java.opts** |Default parameter, indicates JVM heap memory. |\-Xmx2048m |
   |**mapreduce.reduce.memory.mb** |Default parameter, indicates the total memory used by the JVM process. The calculation method is heap memory + off\-heap memory = 2048 + 256. |2304 |
   


<span id="_3-2-cpu-参数"></span>
### 3.2 CPU parameters

You can optimize the CPU for Map and Reduce tasks by setting the following parameters.


|**Parameter** |**Description** |
|---|---|
|**mapreduce.map.cpu.vcores** |The maximum number of CPU cores available for each Map task. |
|**mapreduce.reduce.cpu.vcores** |The maximum number of CPU cores available to each Reduce task. Note: This setting does not take effect in fair queues. Typically, vCores are used in larger clusters to limit CPU usage by different users or applications. |


<span id="_3-3-开启向量化"></span>
### 3.3 Enable vectorization


|**Parameter** |**Description** |
|---|---|
|**hive.vectorized.execution.enabled** |The default value is false. Indicates whether to enable the vectorized query switch. It is recommended to set the parameter value to true during performance testing. |
|**hive.vectorized.execution.reduce.enabled** |The default value is false. Indicates whether to enable vectorized execution mode for Reduce tasks. It is recommended to set the parameter value to true during performance testing. |


<span id="_3-4-task-数量优化"></span>
### 3.4 Optimization of task count

<span id="_3-4-1-map-task-数量优化"></span>
#### 3.4.1 Optimization of Map task count

In distributed computing, the original data is a key factor in determining the number of Map tasks. Optimization strategies include:


* When there are a large number of original data files and each file is very small, the initial number of Map tasks can be reduced to minimize wasted computing resources.

* If there are fewer files but each file is large, the number of Map tasks can be increased to reduce the load on individual tasks.


The parameters that determine the number of Map tasks are:


* **mapred.map.tasks**

* **mapred.min.split.size**

* **dfs.block.size**

1. Initial default Map task count calculation logic

   ```Plain
   default_mapper_num = total_size/dfs.block.size
   ```
   

   If Hive files are stored on HDFS. Because files in HDFS are stored in blocks, the number of blocks for specific Hive data files on HDFS may correspond to the default number of Map tasks.

2. split_num calculation logic

   ```Plain
   default_split_size = max(mapred.min.split.size, 
                         min(mapred.max.split.size, dfs.block.size))
   split_num = total_size/default_split_size；
   ```
   

3. Map task count calculation logic

   ```Plain
   map_task_num = min(split_num, max(mapred.map.tasks, default_mapper_num))
   ```
   

   To increase the number of tasks, decrease the value of **mappred.min.split.size**, and within a certain range, reduce the value of **default_split_size** to increase the value of **split_num** and raise the number of **mapred.map.tasks**.


<span id="_3-4-2-reduce-task-数量优化"></span>
#### 3.4.2 Reduce task count optimization


* Control the number of bytes processed by each Reduce task using the **hive.exec.reducers.bytes.per.reducer** parameter.

   The calculation method for Reduce is as follows:

   ```sql
   reducer_num = min(
       total_size/hive.exec.reducers.bytes.per.reducers, 
       hive.exec.reducers.max)。
   ```
   

* Set the number of Reduce tasks using the **mapred.reduce.tasks** parameter.

   Too many Reduce tasks increase startup time and consume cluster resources. The number of Reduce tasks determines the number of output files. If many small files are generated, and these small files are used as input for the next task, it can lead to the problem of excessive small files.


<span id="_3-5-合并小文件"></span>
### 3.5 Merge small files

A large number of small files can easily cause bottlenecks at the file storage end and affect processing efficiency. This can be addressed by merging the result files from Map and Reduce.


|**Parameter** |**Description** |
|---|---|
|**hive.merge.mapfiles** |The default value is true. Indicates whether to merge Map output files. |
|**hive.merge.mapredfiles** |The default value is false. Indicates whether to merge Reduce output files. |
|**hive.merge.size.per.task** |The default value is 256000000 bytes. Indicates the size of the merged file. |
