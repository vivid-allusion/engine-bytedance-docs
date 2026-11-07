---
title: "Proton overview"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Proton_overview"
---

<span id="_1-介绍"></span>
## 1 Introduction

Proton is an acceleration engine developed by the Volcano Engine E\-MapReduce (EMR) team for storage\-compute separation scenarios. Its deeply optimized TOS access capabilities, JobCommitter functionality, and caching capabilities can significantly improve the execution efficiency of computing tasks.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08cecec0ea914802a1124f4e891ea5ad~tplv-goo7wpa0wc-image.image) </span>

<span id="_1-1-存算分离-vs-存算一体"></span>
### 1.1 Storage\-compute separation vs integrated storage\-compute

Hadoop big data components (including Hive, Spark, Yarn, HBase, Presto/Trino, and more) generally access the underlying distributed file system based on the HDFS standard API. The solution where storage services (HDFS) and compute services (Yarn) are deployed in a single cluster is referred to as the integrated storage\-compute solution, while switching storage services to Volcano Engine Object Storage Service (TOS) is referred to as the storage\-compute separation solution.

Compared to TOS (storage\-compute separation solution), HDFS clusters (that is, the integrated storage\-compute solution) have several obvious shortcomings:


* HDFS clusters use more storage resources and less compute resources. Users typically deploy compute components and HDFS components together on the same set of nodes to fully reuse storage and compute resources, but this results in a deep coupling between the cluster's storage and compute capabilities.

   For example, a business may have 1 PB of data and only run offline computations once a week. Using Hadoop mixed deployment means the user must pay expensive compute resource costs for this 1 PB of data. By adopting the storage\-compute separation model, users only need to pay for the storage costs of 1 PB of data and a small amount of compute resource costs, greatly reducing expenses.

* Users need to reserve idle storage space in advance for HDFS clusters (for example, reserving about 30% idle space for future use), whereas Volcano Engine TOS is billed on demand, and users do not need to pay for reserved storage resources.

* The open\-source version of HDFS cold data storage ([HDFS Erasure Coding](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HDFSErasureCoding.html)) has a high threshold for use and maintenance, and maintaining cold data in a self\-built HDFS cluster is a significant challenge for operations personnel. In contrast, the cold data storage capabilities of Volcano Engine Object Storage Service have been tested in internal and external scenarios, making them relatively mature. According to the [TOS pricing documentation](https://www.volcengine.com/pricing?product=TOS&tab=1), the cold archive storage capacity fee (that is, cold data storage) is much lower per unit than the standard storage capacity fee. Therefore, for large volumes of cold data with infrequent access, users can leverage TOS cold data storage capabilities in the cloud to significantly reduce storage costs.


While the TOS object storage service provides many conveniences and cost optimizations for Hadoop big data users, it also presents several challenges:


* The Rename operation in TOS object storage is time\-consuming, and it is difficult to guarantee atomic semantics.

* The List operation in TOS object storage is more time\-consuming compared to HDFS.


The Proton component built into Volcano Engine EMR effectively addresses the above issues, enabling users to smoothly migrate the Hadoop big data ecosystem from self\-built HDFS clusters to the TOS object storage service in the cloud. Here is an introduction to the basic concepts of Proton's non\-cache mode and cache mode, as well as their similarities and differences.

<span id="_1-2-无缓存模式"></span>
### 1.2 Non\-cache mode

The Proton component in non\-cache mode only includes one SDK jar file, which is placed in the Hadoop classpath. By implementing the HDFS standard API, it maps file system access to TOS access. Additionally, TOS read and write capabilities are deeply optimized for big data analytics scenarios. In offline scenarios, the read and write performance of Proton in non\-cache mode can match the performance of self\-built HDFS.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5cafb1b3c328a2050bb6ad6777ac298b.png) </span>

For common analytics engines (Hive, Spark, Presto/Trino), Proton provides a deeply optimized Job Committer feature, which doubles the performance of storage\-compute separation compared to directly using open\-source solutions. For more information about JobCommitter, please refer to: [EMR storage-compute separation Job Committer best practices](https://docs.byteplus.com/docs/undefined/69a967fa10be4d05382fdc16).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e1bf2c3eb89524f93ca383fb5e0d93c3.png) </span>

<span id="_1-3-有缓存模式"></span>
### 1.3 Cache mode

In addition to non\-cache mode, Proton also offers cache mode, which caches metadata and data to EMR nodes, providing better performance than accessing TOS directly. Non\-cache mode and cache mode are compatible, and users can switch between the two modes as needed.

Cache mode includes a set of highly available MetaServers with three replicas and several collections of DataServers (in the EMR cluster, MetaServer nodes are deployed by default on Master nodes, while DataServer nodes are deployed on Core nodes). MetaServer is responsible for caching metadata, DataServer is responsible for caching TOS object data, and DataServer communicates with MetaServer via heartbeat. After cache acceleration is enabled, users' metadata requests are sent directly to MetaServer, while data IO requests are sent to DataServer. Taking data reading as an example, the client first sends a metadata request to MetaServer, which includes the file path to be read. MetaServer returns to the client the address of the DataServer where the corresponding blocks of the file are located. The client then sends a data IO request to DataServer to read the file data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3069b897121149bdae45c83a1fb03d1b~tplv-goo7wpa0wc-image.image) </span>

<span id="_1-4-两种模式对比"></span>
### 1.4 Comparison of two modes


| |**No cache mode** |**Cache mode** |
|---|---|---|
|Storage\-compute separation |Supported |Supported |
|Service deployment |No additional deployment required |MetaServer and DataServer deployment required |
|Resource requirements |None |Local disks required, local SSD recommended |
|Authentication methods |AssumeRole, static AKSK, environment variable AKSK |AssumeRole, static AKSK, environment variable AKSK |
|Availability |High |High, automatically falls back to TOS when the cache service is unavailable |
|Number of TOS requests |Many |Few |
|List performance |Slow |Fast |
|Read throughput |Low |* On a cache miss, performance is consistent with "no cache mode"<br><br>* On a cache hit, performance is greatly improved |


<span id="_2-版本说明"></span>
## 2 Version information

For version information, please refer to: [Proton release versions](https://docs.byteplus.com/docs/E-MapReduce/109371)

<span id="_3-生态集成"></span>
## 3 Ecosystem integration

Proton currently supports four engine types: Hadoop MR, Hive, Spark, and Flink. For configuration instructions for each engine, please refer to the linked documentation:


* Hadoop:[Hadoop uses Proton](https://docs.byteplus.com/docs/undefined/69a96941fbfc73052b82bac5)

* Hive:[Hive uses Proton](https://docs.byteplus.com/docs/undefined/69a968e1ff63760531155dc9)

* Spark:[Spark uses Proton](https://docs.byteplus.com/docs/undefined/69a9688bf1381a04fe14776b)

* Flink:[Flink uses Proton](https://docs.byteplus.com/docs/undefined/69a968c59a03a004ffa95f10)


<span id="_4-参数调优"></span>
## 4 Parameter tuning

Proton provides a wide range of parameters to facilitate user\-driven tuning. For EMR clusters, users can configure parameters in **EMR cluster console \> Cluster details \> HDFS service parameters**, with the configuration file being `core-site.xml`. If the cluster is user\-built, configuration can be performed directly in `core-site.xml`.

Parameter list: [Proton parameter configuration](https://docs.byteplus.com/docs/undefined/69a967da949de005696297bc)

<span id="_5-使用须知"></span>
## 5 Usage notes

When creating an EMR cluster, regardless of whether the Proton service is selected for installation, the EMR cluster will integrate the Proton SDK required for no cache mode. When the Proton service is installed, cache mode is enabled by default.

After cache mode is enabled, the EMR cluster cannot access historical data stored in TOS by default. To access this historical data, you must first perform the Load operation to batch synchronize the metadata of historical data, or enable automatic metadata synchronization. For specific instructions, please refer to [Proton metadata synchronization](https://docs.byteplus.com/docs/undefined/69a967bc537eb3050706b5f7).
