---
title: "Create storage-compute separation clusters"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Create_storage-compute_separation_clusters"
---

**Storage\-compute separation** refers to deploying compute resources (such as Spark, Hive, and other compute engines) separately from business data storage, with business data uniformly stored in object storage (such as TOS). EMR on ECS clusters support using the **TOS path** as the **cluster storage root path** (only supported in EMR\-4.0.0 and later versions) and the **Hive root path**, enabling the creation of **storage\-compute separation clusters.**  This article introduces the methods for creating storage\-compute separation clusters.

<span id="b40974f6"></span>
# Prerequisites

Account preparation and EMR service activation have been completed. For details, see [Preparation](https://docs.byteplus.com/docs/E-MapReduce/Preparation_sq).

<span id="f9dc67b9"></span>
# Preparation

Before creating a storage\-compute separation cluster, you need to create a TOS bucket for subsequent storage of business data, job logs, and temporary data. Ensure that the TOS bucket's region matches the EMR cluster VPC's **region**. For detailed instructions, see [Creating buckets](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When the EMR cluster accesses TOS, ensure that the <strong>role</strong> bound to the cluster has permission to access TOS. The default EMR cluster role has access permission to TOS. For details, see <a href="https://docs.byteplus.com/docs/E-MapReduce/EMR_service_role">EMR service role</a>.</div>


* <div data-tips="true" data-tips-type="tip">It is recommended to create a TOS hierarchical namespace bucket as storage for separating compute and storage in the data lake, to achieve optimal performance. For information about TOS hierarchical namespaces, refer to <a href="https://docs.byteplus.com/en/docs/tos/What-is-hierarchical-namespace">Hierarchical Namespace</a>.</div>


* <div data-tips="true" data-tips-type="tip">Data stored in TOS will not be automatically deleted when the data lake cluster is deleted. To delete data in TOS, you must manually delete it in the TOS console or by executing a delete command.</div>



<span id="6c1e62b6"></span>
# EMR\-4.0.0 and later versions

<span id="352c3bcd"></span>
## Context


|**Terminology** |**Concept note** |
|---|---|
|HadoopCommon |The foundational dependency base for Hadoop ecosystem clusters, applicable to all EMR on ECS clusters running on the Hadoop framework, including Hadoop\-type clusters and custom clusters with Hadoop framework components installed. |
|Cluster storage root path |Configure the cluster's default storage root path, which is used to store job logs, temporary data, and other information.<br><br>Supports local HDFS paths or TOS paths, available for use by components such as Hive.<br><br>This item can be configured after enabling the HadoopCommon service. |
|Hive root path |Configure the root path information for Hive, that is, the default table creation location for Hive. This can be modified after the cluster is created.<br><br>You can select either a local HDFS path or a TOS path. |



* The cluster does not deploy the HDFS service and only supports the TOS path as the **cluster storage root path** and **Hive root path**, achieving storage\-compute separation in the cluster.

* The cluster deploys the HDFS service, and both the **cluster storage root path** and **Hive root path** support selecting either the built\-in HDFS path or the TOS path.

   * Selecting the HDFS path: integrated storage and compute.

   * Selecting the TOS path: storage\-compute separation. Retaining the HDFS service is suitable for transitional scenarios such as historical data migration or when some components depend on HDFS.


<span id="e9999bfb"></span>
## Limits

Only **EMR\-4.0.0** and later versions are supported, for **data lake clusters and custom clusters** running on the Hadoop framework.

<span id="bee8c768"></span>
## procedure

For detailed creation entry and parameter descriptions, see [Procedure](https://docs.byteplus.com/docs/E-MapReduce/ecs_create_a_cluster_3190_and_later#7b3a7437)Create a cluster. To create a storage\-compute separation cluster, configure the following parameters in **Software settings**:


|**Parameters** |**Configuration guide** |
|---|---|
|Analytics scenarios |Please select **Data Lake** or **Custom Cluster.**  |
|Product version |Please select EMR\-4.0.0 or later. |
|Optional services(Custom Cluster only) |Ensure that the HadoopCommon service is selected. |
|Hive root path |* When HDFS is not enabled: Only TOS paths are supported as the **cluster storage root path.** <br><br>* When enabling the HDFS service: You can choose either the cluster's built\-in HDFS directory or TOS as the **cluster storage root path**. |
|Cluster storage root path |* When HDFS is not enabled: Only TOS paths are supported as the **cluster storage root path.** <br><br>* When enabling the HDFS service: You can choose either the cluster's built\-in HDFS directory or TOS as the **cluster storage root path**. |


<span id="8c056b3b"></span>
# Versions earlier than EMR\-4.0.0

<span id="6808028f"></span>
## Context


|**Terminology** |**Concept note** |
|---|---|
|Hive root path |Configure the root path information for Hive, that is, the default table creation location for Hive. This can be modified after the cluster is created.<br><br>You can select either a local HDFS path or a TOS path. |


<span id="3945330c"></span>
## Limits

Only versions earlier than **EMR\-4.0.0** are supported, for **data lake clusters and custom clusters** running on the Hadoop framework.

<span id="7f08fd21"></span>
## procedure

For detailed creation entry and parameter descriptions, see [Procedure](https://docs.byteplus.com/docs/E-MapReduce/ecs_create_a_cluster_3190_and_later#7b3a7437)Create a cluster. To create a storage\-compute separation cluster, configure the following parameters in **Software settings**:


|**Parameters** |**Configuration guide** |
|---|---|
|Analytics scenarios |Please select **Data Lake** or **Custom Cluster.**  |
|Product version |Please select a version earlier than EMR\-4.0.0. |
|Hive root path |* Select HDFS: Store Hive table data in the local HDFS path, with **integrated storage and compute**.<br><br>* Select TOS or TOS Calculator: Store Hive table data in the TOS path, with **storage and compute separation**. |


<span id="f1fd35b8"></span>
# Related operations

<span id="9d54fdfb"></span>
## Switch Hive data storage to TOS

Go to the cluster details page, click **Service list\>Hive\>Service parameters**, and modify the values of `hive.metastore.warehouse.external.dir` and `hive.metastore.warehouse.dir` parameters to the TOS bucket path.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c03271fa57244579b1cd9f934572e6db~tplv-goo7wpa0wc-image.image) </span>


|**Parameters** |**Note** |
|---|---|
|`hive.metastore.warehouse.external.dir` |The default storage root path for Hive external tables (External Tables). After the path is changed to a TOS bucket path, the default data path for newly created external tables will point to TOS.<br><br>Example value: `tos://<your_tos_bucket>/<your_tos_dir>/hive/warehouse/external`. |
|`hive.metastore.warehouse.dir` |The default storage path for Hive managed tables (Managed Tables). When creating a managed table, if LOCATION is not specified, data will be written to this path. After the path is changed to a TOS bucket path, newly created managed table data will be stored in TOS.<br><br>Example value: `tos://<your_tos_bucket>/<your_tos_dir>/hive/warehouse/managed`. |


<span id="9dd6abc5"></span>
## Add the HDFS service

For EMR\-4.0.0 and later clusters without the HDFS service installed, you can add it when **adding services.** 


1. to the [EMR Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?), click the target cluster name to enter the cluster overview page.

2. Click the **Service list**left panel and then the **Add service**upper right corner. On the **Add service**page, select HDFS, click **Confirm**, submit the task, and when the service status changes to **Normal**, it indicates that the service has been installed successfully.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/182cad124c7d4d9e9ffaa8c30876f82c~tplv-goo7wpa0wc-image.image) </span>
