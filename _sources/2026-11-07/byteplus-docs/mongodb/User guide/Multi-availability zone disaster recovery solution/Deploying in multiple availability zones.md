---
title: "Deploying in multiple availability zones"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/deploy-multi-az"
---

Document Database for MongoDB supports single availability zone deployment and multi\-availability zone deployment. This topic contains instructions on how to deploy MongoDB instances in multiple availability zones.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Multiple availability zone deployment is only supported in regions with 3 or more availability zone resources. Currently, only the following regions support 3 or more availability zone resources:

   * China (Shanghai)

   * China (Beijing)

   * China (Guangzhou)

* FlexPL volumes currently support multi\-AZ deployment in China (Shanghai) and single\-AZ deployment in China (Beijing) and China (Guangzhou).

* Deployment across availability zones can improve availability, but there may be a network latency of 2 ms to 3 ms.


<span id=".6K6h6LS56K-05piO"></span>
## Billing instruction

When creating an instance, selecting the multi\-availability zone deployment option will only incur the fees for creating the instance, and the multi\-availability zone functionality can be used free of charge.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can set the multi\-availability zone deployment solution to:</div>



* <div data-tips="true" data-tips-type="tip">Creating instance</div>


* <div data-tips="true" data-tips-type="tip">Restore to new instance by backup file</div>


* <div data-tips="true" data-tips-type="tip">Restore to new instance by point in time</div>


1. Log on to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the top menu bar, select the project and region for the instance.

3. Refer to the procedures of [Creating instance](https://docs.byteplus.com/en/docs/mongodb/creating_an_instance), [Recovery from backup files](https://docs.byteplus.com/en/docs/mongodb/recovery-from-backup-file) or [Recovery by time point](https://docs.byteplus.com/en/docs/mongodb/recovery-by-time-point) based on your scenario, enter the **Create instance** or **Recovery instance** page, and set the **Deployment method** as follows:

   1. Select **Deployment method** as **Multiple availability zone deployment**.

   2. From the **Availability Zone** dropdown list, set the desired availability zone for the primary node and each secondary node, and choose whether to add read\-only nodes based on your business needs.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Only replica set instances and Shard in sharding cluster instances support adding read\-only nodes.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Each instance (or each Shard) can add up to 5 read\-only nodes. For more details on read\-only node feature introduction and limits, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/managing_read_only_nodes">MongoDB read\-only nodes</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Deployment across availability zones can improve availability, but there may be a network latency of 2 ms to 3 ms.   </div>
   

4. After setting **Deployment method**, proceed to set other parameters for the instance and buy the instance by reference to the creating instance or restoring instance operation guidance.
