---
title: "Deprecated and taken down: Spark on Bolt note"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/deprecated_and_taken_down_spark_on_bolt_note"
---

The content has been migrated to [Spark on Native engine: Bolt](https://docs.byteplus.com/docs/E-MapReduce/95198)

<span id="_1-spark-on-bolt简介"></span>
## Introduction to Spark on Bolt

Bolt is a unified lakehouse analytics acceleration C++ engine developed in\-house by the Volcano Engine E\-MapReduce (EMR) team, utilizing acceleration technologies such as vectorized computation and code generation. Spark on Bolt accelerates Spark by combining Gluten and Bolt.

<span id="_2-spark-on-bolt-整体架构"></span>
## Spark on Bolt overall architecture

The overall architecture of Spark on Bolt is as follows:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ecd302b9c9556b690e425bc19ce3c5ce.png) </span>

Its core consists of two parts:


* Transformation and transmission of execution plans. Substrait is used to transmit physical execution plans between JVM and native environments. Substrait can be understood as a cross\-language serialization SDK for relational objects based on Google protobuf. Bolt also supports Substrait as an input for execution plans.

* Data transmission. SparkSQL executes in a row\-based manner, where operators act on Row objects. In the vectorized framework, operators act on ColumnarBatch objects. A ColumnarBatch can contain multiple rows of data, and each field in a ColumnarBatch is structured as a Column Vector.


<span id="_2-1-执行计划转换"></span>
### Execution plan transformation

The transformation of execution plans occurs at the physical execution plan stage. This means that optimization rules related to plans remain effective for Spark on Bolt.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b5f58b2c80837c9a4b98d57d5c220515.png) </span>

<span id="_2-2-统一的内存管理"></span>
### Unified memory management

Spark manages memory and coordinates spill and memory release between different operators through the Unified Memory Manager. Spark on Bolt also integrates and reuses this capability. Bolt provides a Memory Pool to manage native operators' memory allocation and release at runtime, and invokes JNI callbacks to the JVM's Task Memory Consumer by registering a Listener, thereby integrating with Spark's Unified Memory Manager.

For a Spark on Bolt task without operator fallback, its OnHeap usage should be minimal, as all data\-related operators use OffHeap. This also reduces performance loss caused by garbage collection in large memory scenarios.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_45597ad389c7bd85216127b253f9bfe6.png) </span>

<span id="_2-3-runtime"></span>
### Runtime

From the runtime perspective, Spark on Bolt operates as follows

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e556e7f6a3609b77e80155c50cda15b3.png) </span>

At the granularity of each Spark Task, Bolt is invoked via JNI to execute the computation logic of individual tasks. We can still leverage Spark's robust scheduling framework, speculative execution, failure retries at different task and stage granularities, and its rich ecosystem, such as yarn, k8s, and so on.

<span id="_3-bolt使用"></span>
## Bolt usage

Currently, Spark on Bolt can be enabled by adding configuration parameters.

<span id="_3-1-固定参数配置"></span>
### Fixed parameter configuration

```shell
# bolt
set spark.plugins=io.glutenproject.GlutenPlugin;
set spark.shuffle.manager=org.apache.spark.shuffle.gluten.celeborn.CelebornShuffleManager;
set spark.gluten.sql.columnar.numaBinding=false;
set spark.gluten.sql.columnar.coreRange=0-35,72-107|36-71,108-143;
set spark.gluten.sql.columnar.shuffleSplitDefaultSize=8192;
set spark.gluten.sql.columnar.forceShuffledHashJoin=true;
set spark.sql.bucket.union.enable=false;
set spark.sql.optimizer.dynamicDataPruning.enabled=false;
set spark.sql.optimizer.dynamicDataPruning.datasource.enabled=false;
set spark.sql.mergeGetMapValue.enabled=false;
set spark.sql.collapseGetJsonObject.enabled=false;
set spark.sql.CollapseExpensiveExprMode=None;
set spark.sql.execution.useObjectHashAggregateExec=false;
set spark.sql.optimizer.partialAggregationOptimization.enabled=false;
set spark.sql.aggregate.adaptivePartialAggregationThreshold=0;
set spark.gluten.sql.columnar.backend.velox.abandonPartialAggregationMinPct=80;
set spark.gluten.sql.columnar.backend.velox.abandonPartialAggregationMinRows=100000;
set spark.gluten.sql.columnar.maxBatchSize=32768;
set spark.gluten.sql.columnar.maxBatchByteSize=41943040;
set spark.sql.optimizer.excludedRules=org.apache.spark.sql.catalyst.optimizer.RemoveRedundantAggregates,org.apache.spark.sql.hive.auth.GeminiSparkAuthorization;
set spark.sql.gluten.customHadoopConfEnforce.enabled=false;
set spark.kubernetes.driverEnv.CPP_HDFS_CONF=/opt/tiger/hadoop_conf/core-site.xml;
set spark.executorEnv.CPP_HDFS_CONF=/opt/tiger/hadoop_conf/core-site.xml;
set spark.kubernetes.driverEnv.LD_PRELOAD=/opt/tiger/spark_deploy/spark-stable/native_lib/libjemalloc.so;
set spark.executorEnv.LD_PRELOAD=/opt/tiger/spark_deploy/spark-stable/native_lib/libjemalloc.so;
set spark.kubernetes.driverEnv.HADOOP_CONF_DIR=/opt/tiger/hadoop_conf;
set spark.executorEnv.HADOOP_CONF_DIR=/opt/tiger/hadoop_conf;
```


<span id="_3-2-内存配置"></span>
### Memory configuration

Bolt computing uses off\-heap memory, so when Bolt is enabled, you need to adjust Spark memory usage accordingly. By default, we configure the following two parameters:

```shell
// 堆内内存
spark.executor.memory 12G
// 预留非堆内存
spark.executor.memoryOverhead 4096
```


After enabling Bolt, it is recommended to set the parameters as follows:

```shell
// 堆内内存，建议保留原来堆内内存的25%
set spark.executor.memory=3G;
// 预留非堆内存，建议不变
set spark.executor.memoryOverhead=4096;

// 启用offHeap内存
set spark.memory.offHeap.enabled=true;
// offHeap内存大小，建议设置为原来堆内内存的75%
set spark.memory.offHeap.size=9G;

注：启用Bolt后
spark.executor.memory+spark.memory.offHeap.size=原spark.executor.memory
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Because the SQL dedicated resource queue is preheated and started, it does not support reconfiguring memory. To change memory configuration, use a public queue or a queue with general resources, and set the following parameters:</div>


<div data-tips="true" data-tips-type="warning">set tqs.query.engine.type = sparkcli;</div>


<div data-tips="true" data-tips-type="warning">To change memory configuration in the SQL dedicated resource queue, please <a href="https://docs.byteplus.com/docs/E-MapReduce/109489">Deprecated and taken down: Spark on Bolt note</a>contact us.</div>


<span id="7202abc3"></span>
## Spark on Bolt operators and functions

<span id="d5121510"></span>
### Operators

<span id="3b68fc94"></span>
#### Sample


* important notes

   * Currently, Spark on Bolt only supports queries using `TABLESAMPLE(x ROWS)`.

* Example usage

   ```SQL
   set emr.serverless.bolt.enabled=true;
   drop table if exists lt_testdb.test_table;
   create table lt_testdb.test_table AS
   select 
       1 as id,
       'aaa' as name
   union all
   select 
       2 as id,
       'bbb' as name
   union ALL
   select 
       3 as id,
       'ccc' as name;
   
   SELECT * FROM lt_testdb.test_table TABLESAMPLE (1 ROWS);
   ```
   


<span id="7089cfcd"></span>
#### Cache Table


* Example usage

   ```SQL
   set emr.serverless.bolt.enabled=true;
   set spark.gluten.sql.columnar.tableCache=true;
   
   drop table if exists lt_testdb.test_table;
   create table lt_testdb.test_table AS
   select 
       1 as id,
       'aaa' as name
   union all
   select 
       2 as id,
       'bbb' as name
   union ALL
   select 
       3 as id,
       'ccc' as name;
   
   CACHE TABLE testCache OPTIONS ('storageLevel' 'MEMORY_ONLY') SELECT * FROM lt_testdb.test_table;
   ```
   


<span id="0e5722b6"></span>
#### InMemoryTableScan


* important notes

   You need to set `--conf spark.gluten.sql.columnar.tableCache=true` before you can use InMemoryTableScan.

* Example usage

   ```Python
   df = spark.sql("select 1234")
   df.cache()
   a = df.count()
   print(a)
   
   b = df.count()
   print(b)
   ```
   


<span id="73840e1c"></span>
### Functions
