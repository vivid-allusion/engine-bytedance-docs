---
title: "OLAP data disaster recovery best practices"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/OLAP_data_disaster_recovery_best_practices"
---

<span id="0203385c"></span>
## Disaster recovery overview

Disaster recovery refers to the ability to promptly restore business operations and ensure no data loss when the system encounters an exception. **National Standard GB/T 20988—2007** defines the levels of information system disaster recovery capability, recovery time objective (RTO), and recovery point objective (RPO) as follows.


|Disaster recovery capability levels |RTO |RPO |
|---|---|---|
|1 |More than 2 days |1 to 7 days |
|2 |More than 24 hours |1 to 7 days |
|3 |More than 12 hours |Several hours to 1 day |
|4 |Several hours to 2 days |Several hours to 1 day |
|5 |Several minutes to 2 days |0 to 30 minutes |
|6 |Several minutes |0 |


<span id="8e5bc110"></span>
## Active\-active cluster solution (meets disaster recovery levels 5 and 6)

EMR cluster deployment in both the same region and remote regions with identical specifications to achieve a dual\-location, triple\-center architecture. There are two approaches for building disaster recovery clusters: **dual\-write** and **replication**. This section introduces both approaches.


* **Dual\-write approach (high real\-time performance and fast switchover) (recommended)** 


Build disaster recovery clusters using the dual\-write approach. Each link is relatively independent, can actively detect cluster availability, and enables business link switchover. Achieves RTO in seconds and 0 RPO at best.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f0bec9deb2204d4390224bf7ec41a41c~tplv-goo7wpa0wc-image.image) </span>


* **Replication approach (replication has latency, requires a switchover plan)** 


Use [Doris CCR (Cross Cluster Replication)](https://doris.apache.org/zh-CN/docs/admin-manual/data-admin/ccr) for cross\-cluster data copying. A comprehensive switchover plan must be developed to ensure timely business switchover in case of failures. Typically achieves minute\-level RTO and RPO.

Doris CCR：https://doris.apache.org/zh\-CN/docs/admin\-manual/data\-admin/ccr

SR cluster\-sync：https://docs.starrocks.io/zh/docs/administration/data_migration_tool/

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48079301cc1a466c9a1d91b997fe585b~tplv-goo7wpa0wc-image.image" width="1062px" /></div>


<span id="7505a09f"></span>
## Data disaster recovery solution (meets disaster recovery levels 1–4)

Periodically perform cold backups of data to TOS. In the event of a failure, create a new cluster and restore the data. Cluster creation typically takes about 5 minutes; data recovery time depends on the amount of data to be restored. Overall, this approach meets the RTO and RPO requirements for levels 1–4.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca5bc5bbc0a84b4d866c9706e23511c3~tplv-goo7wpa0wc-image.image" width="458px" /></div>


<span id="ada1abe6"></span>
## Pre\-positioned cache (disaster recovery capability depends on the amount of pre\-positioned cache data)

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e42704f601e148469d415f4741d00705~tplv-goo7wpa0wc-image.image" width="1308px" /></div>


<span id="e434be27"></span>
## Data snapshots (can be performed offline; real\-time data may not be recoverable due to compaction)

Use disk snapshots to periodically take snapshots of disks, which can prevent data loss in the event of a disaster\-level exception.

For detailed operations, refer to: [Snapshot operations guide](https://www.volcengine.com/docs/26444/434968).
