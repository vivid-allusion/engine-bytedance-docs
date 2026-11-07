---
title: "Reconfigure a cluster"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/reconfigure-a-cluster"
---

ByteHouse Enterprise Edition supports modifying the configuration of existing clusters, allowing changes to cluster specifications or node counts through either vertical or horizontal reconfiguration. This text will introduce the methods and points of attention for configuration changes in ByteHouse.

<span id="1025050f"></span>
# Background information: vertical and horizontal reconfiguration

Configuration changes in ByteHouse generally entail two types: vertical reconfiguration and horizontal reconfiguration.


|Contrast Analysis |Horizontal Scaling |Vertical Scaling |
|---|---|---|
|Meaning of Scaling |Horizontal scaling (scale out/in) refers to increasing or decreasing the number of nodes in a cluster to enhance or reduce the overall performance of the cluster.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/afb276e3771b47019dcf74f9cc165320~tplv-goo7wpa0wc-image.image) </span> |Vertical scaling (scale up/down) involves adjusting the specifications of each node in the cluster to increase or decrease the overall performance of the cluster.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb506f9ae992438aa0741dfac5836e59~tplv-goo7wpa0wc-image.image) </span> |
|Suitable Scenarios |Scenes where vertical scaling reaches the configuration cap of virtual machines. |Scenes with demands for configuration enhancement. |
|Scaling for performance improvement |* CPU: Less than linear;<br><br>* Disk/Network Throughput: Close to linear; |* CPU: Close to linear;<br><br>* Disk Throughput: Depends on the virtual machine's disk bandwidth allocation and disk bandwidth impact;<br><br>* Network Throughput: Depends on the virtual machine's network bandwidth allocation; |
|Expansion Duration |From 10 minutes to hourly |Every min |
|Impact of Expansion |* The table being redistributed is read only<br><br>* Cluster query performance will be affected during expansion |* Each cluster node will restart sequentially |


<span id="2b5a51b4"></span>
# Restriction

If you need to use the horizontal scaling\-down (reducing the number of nodes) feature, please submit a work order or contact the ByteHouse team to obtain whitelist permission.

<span id="a368cad8"></span>
# Cautions


* Currently, the horizontal scaling function is in Beta status, and it is recommended to back up critical data before expansion.

* Ensure all distributed tables of the HaUnique unique key table in the cluster have specified a shardKey (sharding method).

* Ensure the following cluster Parameters are in the terminated state.

   1. enable_sharding_optimize=0

   2. distributed_perfect_shard_in_optimizer=0

   3. enable_single_shard_property=0

* Each old node needs to reserve the maximum capacity of a single table for storage.


For instance, if the total size of the table is 100GB, with 10 nodes currently, reducing to 5 nodes would mean reserving more than 20GB of storage expansion per old node.


* During horizontal reconfiguration and redistribution, the usage of DDL / DML statements to adjust metadata, such as creating tables, modifying table structure, changing users, etc., is prohibited.

* The time for expansion is related to the number of nodes, network speed, and disk speed. The time displayed on the ByteHouse product interface is only forreference.

* During data redistribution, tables will enterstate one by one, and the cluster's computational and IO load will be higher, generally leading to unstable and deteriorated reading performance.


<span id="f53340e8"></span>
# Vertical scaling

<span id="6de58732"></span>
## Prerequisites

Permission Requirements: Cluster Administrator or System Administrator

<span id="bb3d8f33"></span>
## Operation Steps


1. In the ByteHouse interface, go to: Manage clusters \> Cluster list, click Show more \> Change specifications on the corresponding cluster's action column.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8fdc5897f56944808de0fea2b263b6d9~tplv-goo7wpa0wc-image.image) </span>

2. Select "Changing Vertical" for "Change specification type".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/621cba43c00045d4be53e5629e21b2cc~tplv-goo7wpa0wc-image.image) </span>

3. Adjust the specifications of computing resources and the size of storage resources.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When performing vertical scaling, storage space can only be expanded, not reduced.</div>


<div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a4ada8f5a9d4807b4b77adbe5fb71c9~tplv-goo7wpa0wc-image.image" width="273px" /></div>



4. The changes in costs are displayed in real\-time on the interface, for more details refer to [Billing details about specification changes](https://docs.byteplus.com/docs/bytehouse/billing-details-about-specification-changes).

5. Click the Confirm button, the node will Restart and the configuration will activate afterwards.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Expansion is estimated to take 1\-5 minutes; the more nodes, the longer the expansion will take.</div>


<div data-tips="true" data-tips-type="tip">Cluster operations will stop during the expansion of a single\-copy cluster. It is advisable to carry out expansions during off\-peak business hours.</div>


<span id="3f544f13"></span>
# Horizontal scaling [Beta]

<span id="ef330ec7"></span>
## Prerequisites


* Permission Requirements: Cluster Administrator or System Administrator.

* Version requirement: ByteHouse 2.2.1.130 or higher.


You can check if your current engine version meets the requirements under Manage Clusters \> Cluster List \> Cluster Details \> Basic Information \> Engine Version in ByteHouse. If the version is too low, the interface will indicate that the horizontal scaling feature cannot be used.

<span id="ba37a94a"></span>
## Operation Steps


1. Access ByteHouse interface: Manage Clusters \> Cluster List, and click Show More \> Change Specification on the corresponding cluster's actions column.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8fdc5897f56944808de0fea2b263b6d9~tplv-goo7wpa0wc-image.image) </span>

2. Select “Changing Horizontal” for "Change Specification Type" and configure the horizontal scaling parameters.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ae6f2de60ce4565bdbbf226d5717ce8~tplv-goo7wpa0wc-image.image) </span>



|Parameter |Configuration Description |
|---|---|
|Horizontal reconfiguration type |Currently supports two methods: adjusting the number of nodes and the number of copies.<br><br><br>* Node quantity: change the number of nodes, the number of copies remains the same.<br><br>* Number of Copies: Modifying the number of copies will automatically adjust the number of nodes accordingly. |
|Computing Resources |Configuration of nodes/copy number after level adjustment.<br><br>In a level adjustment scenario, the number of nodes can be increased (scaled up) or decreased (scaled down).<br><br><br>* If you have increased the number of nodes.<br><br>   * While scaling up, all table data will be automatically redistributed. If some tables fail to redistribute, it won't affect the scaling process, and you can use the "Redistribution" function later to independently redistribute these tables.<br><br>   * If the current cluster contains a HaUniqueMergeTree table, after scaling up, the table topology does not change, new nodes have no data, and the import task is unaffected; or if you need improved read/write performance after scaling up, it is suggested you manually redistribute the data upon completion of the scale\-up.<br><br><br>For manual redistribution operation details, please see [Data redistribution](https://docs.byteplus.com/docs/bytehouse/data-redistribution).<br><br><br>* If you have decreased the number of nodes, you also need to configure redistribution and advanced settings at the bottom of the page. |
|Redistribution Settings & Advanced Settings<br><br>(Optional) |If you reduce the number of nodes, you must also configure redistribution settings and advanced settings.<br><br><br>* Redistribution: Choose whether to enable the redistribution setting switch according to circumstances. After turning on the switch, you can view all the tables that need redistribution at the bottom of the page. After submitting the horizontal scale\-in configuration and completing the specification changes, all data tables are automatically redistributed.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, only the redistribution of all tables is supported; partial table data redistribution (which may lead to data loss) is not supported. If you only want to redistribute part of the table data, please submit a ticket to contact BytePlus RD support personnel for manual processing.</div><br><br><br><br>* Advanced settings: Configure the minimum read\-only mode for redistribution, set the active partition range, and during the subsequent redistribution data, only the data within the active partition range will be prohibited from writing. This significantly reduces the read\-only time of tables by prohibiting new data writings only during the active partition period of redistribution. |
|Scaling duration |The interface will provide the Estimated time for scaling/data redistribution. You can issue an Announcement based on the actual situation.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The actual time consumption is related to the number of nodes, network rate, and disk rate. The time displayed here is only for estimated reference.</div><br> |
|Change Fee |Show you the cost changes caused by this configuration change, refer to [Billing details about specification changes](https://docs.byteplus.com/docs/bytehouse/billing-details-about-specification-changes).<br><br>. |



3. Click **Confirm** at the bottom of the page, which redirects to the configuration order confirmation page. Complete payment according to the on\-screen instructions, and the cluster will start horizontal scaling.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8745687c6a244b9590c7ac18b3c6821e~tplv-goo7wpa0wc-image.image) </span>

When the cluster is in the "Horizontal Resizing" state, the background task procedure is as follows:


|Expansion Situation |Reduction Situation |
|---|---|
|When new nodes are added, they are actually initialized, and new metadata is created on the new nodes. This stage does not affect cluster read/write performance.<br><br>If the cluster has HaUnique tables:<br><br><br>* Automatically created virtual clusters, and all HaUnique tables are automatically mounted to the virtual cluster, ensuring that the node topology and data distribution do not change before and after the expansion.<br><br>* Meanwhile, the synchronization tasks such as Kafka sync, offline sync, and Flink sync corresponding to the HaUnique tables remain unchanged, and the new nodes will not create the HaKafka and View tables corresponding to the HaUnique tables. |1. Phase 1: Redistribute all tables one by one.<br><br><br>**This stage is redistributing tables on a read\-only state while the cluster's computational and IO load will be higher, estimated read performance will drop and be unstable.**  **If part of the table redistribution fails, the scaling down will not proceed and the mission will terminate**.<br><br><br>2. Phase Feb: Reduce nodes.<br><br><br>This phase does not affect cluster read and write performance. |



4. Once the above steps are completed, the cluster returns to the "Running" status.
