---
title: "Compute groups overview"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Overview_of_computation_groups"
---

A compute group is a further subdivision of queue resources, designed to execute specific tasks more efficiently, optimize resource allocation, and ensure resource isolation. All queries and tasks must be submitted to a compute group under the queue.

<span id="dffe8185"></span>
# Compute group types and resource allocation logic

<span id="a1dbb8b2"></span>
## Types of computing groups

After the queue is created, a Default general compute group is automatically created for you. You can also plan and create custom compute groups based on subsequent job requirements. Compute groups help users achieve more efficient task execution by providing customized resource configuration and management for different types of tasks. Compute groups can be divided into:


* **General compute groups** (including the Default general compute group created automatically and custom general compute groups), suitable for a wide range of task types.

* **Dedicated compute groups** (including Spark SQL Warehouse, Presto SQL Warehouse, Ray Cluster, and more). Dedicated compute groups provide optimized resource configurations for specific task types, ensuring tasks can be executed efficiently.


The following sections introduce the detailed types of compute groups and their resource allocation methods.


|Types of computing groups |Note |Resource allocation methods for computing groups |
|---|---|---|
|General computing group \- Default |The default computing group is automatically created by the queue. |The resource amount of the Default general computing group is dynamic. Its available resources are the remaining available resources in the queue after custom computing groups have been created. |
|Custom computing groups |Supports the creation of various types of custom computing groups, including general computing groups, SparkSQL Warehouse, PrestoSQL Warehouse, and more. |In custom computing groups:<br><br><br>* Custom\-general computing group: The resources of the computing group are allocated using a 'logical allocation' method. That is, after a custom general computing group is created, resources in the queue are not immediately isolated and allocated to the corresponding custom general computing group. Instead, resources are allocated only when a job is running in this computing group.<br><br>* Other types of custom computing groups: After other types of custom computing groups are created, resources in the queue are immediately isolated and allocated to the corresponding computing group according to the resource allocation configuration results of the computing group. |


Based on the above:


* The actual available resources in the queue are the resources of the Default compute group. If a new compute group is created, resources will be allocated from the Default compute group.

* During the creation of a compute group, if a job happens to be running in the Default compute group and occupies part of its resources, it is possible that resources intended for the new compute group are temporarily occupied. In this case, the "resource preemption policy" configured when creating the new compute group will be used to handle resources temporarily occupied by jobs running in the Default compute group.


<span id="7f3b6062"></span>
# When to use compute groups

Compute groups are particularly suitable for the following scenarios, especially dedicated compute groups:


* **Resource requirements for PrestoSQL tasks**

   PrestoSQL requires a resident coordinator to initiate tasks. Therefore, it is not possible to execute PrestoSQL tasks in the general computing group (Default computing group). At this point, by creating a Presto SQL Warehouse computing group and reserving resident resources for PrestoSQL tasks, you can ensure the execution of PrestoSQL.

* **Tasks with higher performance requirements**

   For tasks such as SparkSQL, the Spark SQL Warehouse computing group reduces task execution latency by warming up resources, enabling tasks to start within seconds. This is especially suitable for ad hoc query tasks that require rapid response.

* **Tasks that require execution with dedicated resources**

   The computing group divides the queue's resources into multiple independent units, providing dedicated resources for different types of tasks. This division effectively avoids resource contention and ensures that each task receives a reasonable allocation based on its resource requirements. It is particularly suitable for tasks that require guaranteed resources.


The differences between the general computing group (Default computing group) and dedicated computing groups (Spark SQL Warehouse, Presto SQL Warehouse, Ray Cluster) are as follows.


|**Features** |**General computing group (Default computing group)**  |**Dedicated computing group (Spark SQL Warehouse, Presto SQL Warehouse, Ray Cluster)**  |
|---|---|---|
|**Applicable tasks** |SparkSQL, SparkJar, PySpark, RayJob, HiveSQL, CustomJob |SparkSQL（Spark SQL Warehouse）、PrestoSQL（Presto SQL Warehouse）、RayJob（Ray Cluster） |
|**Resource management** |Resources are dynamically allocated, multiple jobs share the resource pool, and resources are allocated at the job level. |Manages its own resources independently, supports resident resources, on\-demand resources, and others.<br><br>Resource specifications are fixed, resources are already pre\-launched, and job\-level resource customization is ineffective. |
|**Task flexibility** |High, supports multiple job types |Only supports specific types of tasks, but can provide more efficient execution performance |
|**Latency optimization** |Relatively high, dynamic resource requests may cause latency |Relatively low, reduces pre\-launch time |
|**Advantages** |High flexibility, supports multiple job types |Provides resource optimization for specific tasks |
|**Disadvantages** |Resources need to be requested dynamically, which takes some time (about 30 seconds) |Lower flexibility, suitable for specific types of tasks, cannot support the execution of multiple task types |
|**Use cases** |Production and large\-scale tasks |Ad hoc and other latency\-sensitive queries (Spark SQL Warehouse/Presto SQL Warehouse)<br><br>Ray jobs that require resource isolation and guarantees (Ray Cluster) |


<span id="a815afae"></span>
# Operation guide

After the queue is created, based on your job plan, you can create computing groups and allocate queue resources appropriately. You can also view the resource consumption of computing groups and the status of job instances in real time during subsequent job execution. For details, see [Create and manage compute groups](https://docs.byteplus.com/docs/E-MapReduce/Create_and_manage_compute_groups).
