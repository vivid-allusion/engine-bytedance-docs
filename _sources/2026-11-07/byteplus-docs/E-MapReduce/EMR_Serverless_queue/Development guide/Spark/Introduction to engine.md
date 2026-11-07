---
title: "Introduction to engine"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Engine_introduction"
---

Spark is an open\-source distributed computing framework designed for large\-scale data analytics and processing. By leveraging in\-memory computing technology and directed acyclic graphs (DAG), it delivers faster analytics and processing capabilities than the MapReduce engine. It provides multiple computing packages, including Spark SQL, Spark Streaming, MLlib, and Graphx, which can be used for large\-scale data analytics and processing, real\-time computing, machine learning, graph computation, and many other scenarios.

Based on full compatibility with open\-source Spark, EMR Spark has been customized and optimized to provide the following capabilities:

<span id="_1-uiservice：云原生-spark-history-server"></span>
## 1 UIService: Cloud\-native Spark History Server

The native Spark History Service has the following issues:


1. High storage space overhead


Spark's event system is highly detailed, resulting in a large number of events recorded in the event log. For UI display, most events are unnecessary. Additionally, the event log is typically stored in plain Json format, which occupies significant space.


2. Poor replay efficiency and high latency


The History Server restores the Spark UI by replaying and parsing the event log, which incurs substantial computational overhead. When tasks are large, there is noticeable response latency. After a large job completes, users may have to wait ten minutes or even half an hour to view job history through the History Server, significantly impacting user experience.


3. Poor scalability


Before replaying and parsing files, the History Server's FsHistoryProvider must first scan the configured event log path, traverse the event logs, and load the metadata of all files into memory, making the native service stateful. Therefore, each time the service restarts, it must reload the entire path before it can provide external service. After each task completes, it also needs to wait for the next scan cycle before it can be accessed. It is difficult to scale horizontally conveniently.


4. Not cloud\-native


Spark History Server is not a cloud\-native service. Workload differences among tenants are significant, and the cost of modification and maintenance is high in public cloud scenarios.

To address the aforementioned issues, we attempted to modify the History Server.

Whether running Spark Driver or History Server, both listen to events and reflect task change information into instances of several UI\-related classes, then store them in KVStore for UI rendering. In other words, KVStore stores all the complete information required for UI display. For users of the History Server, in most cases, we only care about the final state of the task and do not need to pay attention to the specific events that cause state changes. Therefore, we can persist only the KVStore without storing a large amount of redundant event information. In addition, KVStore natively supports Kryo serialization, which offers significantly better performance than JSON serialization. Based on this idea, we developed a new History Server system named UIService.

By building UIService, we greatly reduced the storage space required for Spark UI\-related events and effectively improved UI access latency. Architecturally, we also implemented multi\-tenant access isolation, cloud\-native capabilities, and elastic scaling based on UIService.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0b496db2cd5edb826b58465d02235cd1.png) </span>

<span id="_2-falcon：remote-shuffle-service"></span>
## 2 Falcon：Remote Shuffle Service

In addition to UIService, optimization at the Shuffle layer is also a topic worth highlighting. Shuffle is the process in Spark jobs used to connect upstream and downstream data interactions. The Remote Shuffle Service (RSS) framework allows the Shuffle Service to run outside of Spark, decoupling storage and compute, and providing better availability and performance.

Falcon is the Remote Shuffle Service on EMR Serverless Spark, adopting a highly available architecture with separation of storage and compute. It supports Spark engine to read and write remote Shuffle data, and can be deployed and applied in cloud environments. For more details, see: [Data shuffle](https://docs.byteplus.com/docs/E-MapReduce/Data_shuffle)

<span id="_3-bolt：spark-native-engine"></span>
## 3 Bolt：Spark Native Engine

Bolt is ByteDance's self\-developed engine for accelerating data processing and analysis. It addresses performance issues in the field of big data processing and analysis, providing faster, more reliable, and more flexible and easy\-to\-use acceleration for analytics. Bolt uses a vectorized execution engine implemented in C++, combined with runtime LLVM Codegen technology, significantly improving parallel execution efficiency on multi\-core CPUs. On the distributed SQL query engine Spark, replacing the traditional Java engine with Bolt can greatly increase query speed and reduce resource costs. When users leverage Bolt's acceleration capabilities, they pay the corresponding acceleration fees based on the actual CUH consumed by their jobs. For detailed billing rules, please refer to [Bolt acceleration engine pricing details](https://docs.byteplus.com/docs/E-MapReduce/Billing_for_Bolt).

Spark on Bolt uses the Gluten plugin as the binding layer between the framework and the native engine. It mainly consists of several parts: the Conversion component, which converts the Spark Physical Plan into a Substrait Plan. Memory Manager: Bolt operates independently from the JVM, so Bolt's memory must be handed over to Spark for unified management to prevent memory overflow. Bolt reports the allocated memory to the Task Memory Manager. When the Executor's memory is insufficient, Spark triggers the Bolt Spill logic to release memory or write part of the memory to disk. Columnar Shuffle: Spark's native shuffle is row\-based, so it needs to be extended to support columnar shuffle, including columnar data splitting, serialization, compression, and other methods. Memory usage during columnar shuffle is reduced through delayed allocation, sampling prediction, and other methods. Fallback component: Spark supports many operator expressions. When Bolt does not support certain cases, execution falls back to the native JVM engine. There is a unified function signature registration mechanism to reduce the implementation cost of scalar and aggregate functions. Functions required by different frameworks can be reused and overridden. Data transfer: Data is transferred between the JVM and Bolt via JNI calls. The data returned by Bolt is stored as Block Columnar Vector, which facilitates subsequent computation.

For more information and usage, see: [Spark on Native engine: Bolt](https://docs.byteplus.com/docs/E-MapReduce/sq_spark_on_native_engine)

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_682f16e714ee9490bc96b2e41b39d907.png) </span>

<span id="_4-tpc-ds-优化"></span>
## 4 TPC\-DS optimization

The TPC\-DS test suite, launched by the TPC organization, is a benchmark based on decision support systems. It simulates a complex data warehouse environment, covers multiple business domains, and effectively tests and evaluates the performance and efficiency of OLAP engines in handling different business scenarios, making performance comparisons between OLAP engines more fair and reliable.

EMR Serverless Spark delivers significant performance improvements compared to the community version. Some of these improvements come from internal performance optimizations at ByteDance, such as AdaptiveShuffledHashJoin and AdaptiveFileSplit, while others result from research and exploration of the TPC\-DS dataset. In testing and researching the TPC\-DS workload, we have implemented rule optimization, cache optimization, and runtime optimization at the engine level.

After optimization, compared to the community version, performance on the TPC\-DS 1T dataset shows that version 3.0 achieves 2.1x the performance of the community 3.0 version, and version 3.2 achieves 2.5x the performance of the community 3.2 version with the same hardware resources.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cc344907d52e7937eaa41575f863b095.jpg) </span>

<span id="406ee288"></span>
## 5 Spark 4 version enhancements

Apache Spark 4 is a major version upgrade following the 3.x series in the Spark community, featuring enhancements in semi\-structured data processing, SQL usability, Python ecosystem, connectivity, and runtime infrastructure. For scenarios such as lakehouse analytics, real\-time data processing, interactive development, and large\-scale SQL jobs, Spark 4 further improves development efficiency and complex data processing capabilities.

Spark 4 mainly provides the following capabilities:


1. VARIANT: Enhanced semi\-structured data processing

   In scenarios such as log analysis, event tracking analysis, and user behavior analysis, semi\-structured data like JSON is typically stored as String type. Traditional methods require repeatedly parsing JSON strings during queries using functions such as `get_json_object`, making it difficult to fully leverage structured data optimization features like column pruning and predicate pushdown. When the data volume is large or the field hierarchy is deep, this can result in additional parsing overhead.

   Spark 4 introduces the VARIANT data type for storing and processing semi\-structured data. VARIANT uses an internal representation that is more suitable for querying, reducing repeated parsing overhead when accessing JSON fields and supporting path expressions for query optimization. For business data containing a large number of dynamic fields, VARIANT can retain a flexible schema while improving the efficiency of field filtering, field projection, and nested structure queries.

2. SQL capability enhancements: SQL UDF and PIPE syntax

   Spark 4 enhances native SQL expressiveness, reducing the development and maintenance costs of complex SQL jobs.

   SQL UDF supports defining reusable functions directly within SQL. Compared to writing UDFs in Python or Java, SQL UDFs are more easily recognized and optimized by the Catalyst optimizer, making them suitable for encapsulating common cleansing logic, field normalization logic, and business rule expressions.

   The PIPE syntax uses `|>` to chain multi\-step SQL processing in execution order. For SQL statements involving multiple stages such as filtering, aggregation, and sorting, the PIPE syntax can reduce deeply nested subqueries, making the reading order of SQL closer to the actual processing flow and facilitating troubleshooting and maintenance.

   Example:

   ```SQL
   FROM sales
   |> WHERE region = 'east'
   |> AGGREGATE COUNT(*) AS cnt, SUM(amount) AS gmv
      GROUP BY product_id
   |> ORDER BY gmv DESC;
   ```
   

3. PySpark ecosystem enhancements

   Spark 4 continues to enhance PySpark capabilities, providing Python users with a more comprehensive data processing and development experience. PySpark now supports custom data sources, allowing users to connect to external systems or implement custom input and output logic using Python. At the same time, Spark 4 also improves the visualization capabilities of PySpark DataFrame, making it easier to quickly observe data distribution and processing results in interactive analysis, notebook debugging, and exploratory data processing scenarios.

   For teams that use Python as their primary development language, Spark 4 reduces the cost of migrating from local analysis and notebook development to production jobs, enabling better continuity for PySpark in batch processing, interactive analysis, and data science scenarios.

4. Spark Connect and client compatibility enhancements

   Spark Connect continues to be enhanced in Spark 4. With Spark Connect, client applications can be decoupled from the Spark Driver and use standardized protocols to remotely connect to Spark clusters. This model helps reduce the coupling between client environments and cluster runtime environments, improving maintainability for multi\-language clients, remote development, and interactive analysis scenarios.

   For scenarios where Spark computing capabilities need to be accessed in notebooks, application services, or local development environments, Spark Connect can reduce local dependency conflicts and increase the flexibility of client and cluster upgrades.

5. Changes in runtime environment and compatibility

   Spark 4 also adjusts requirements for runtime environment and compatibility. The community version has upgraded underlying dependencies and runtime requirements. For example, version requirements for JDK, Scala, Python, and others have changed compared to Spark 3.x. At the same time, Spark 4 enhances ANSI SQL behavior, error handling, and some default configurations. Some existing SQL jobs may expose compatibility issues such as type conversion, division by zero, overflow, or reserved keywords after upgrading.

   Therefore, when migrating from Spark 3.x to Spark 4, it is recommended to first perform regression validation of core jobs in a test environment, with particular attention to changes in SQL semantics, UDF compatibility, dependency package versions, and JDK and Python runtime environments. For production jobs, it is recommended to perform a gradual upgrade in conjunction with version notes, and explicitly configure key compatibility parameters based on the specifics of your jobs. For the community's official upgrade instructions, refer to [Spark Migration Guide](https://spark.apache.org/docs/latest/migration-guide.html).
