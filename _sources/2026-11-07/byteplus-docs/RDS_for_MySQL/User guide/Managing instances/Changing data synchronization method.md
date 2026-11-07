---
title: "Changing data synchronization method"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_sync_mode"
---

This topic describes how to modify the data synchronization method for an RDS for MySQL instance.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

RDS for MySQL instances support two data synchronization methods: semisynchronous and asynchronous.


* Semisynchronous

   After an application adds, deletes, or modifies data on the primary node, the primary node immediately copies the data to the secondary node. After the secondary node receives the data and writes it to the relay log (execution is not required), it returns a success message to the primary node. The primary node returns a response to the application only after receiving the success message from the secondary node.

   If data replication becomes abnormal, for example, if the secondary node is unavailable or a network failure occurs, the primary node pauses responses to the application and downgrades the data synchronization method to asynchronous. After data replication returns to normal, the data synchronization method is restored to semisynchronous.

* Asynchronous

   When an application sends a request to add, delete, or modify data, the primary node returns a response to the application immediately after the operation is complete and then copies the data to the secondary node.

   When using asynchronous synchronization, the primary node does not wait for a response from the secondary node during data updates, which often results in higher instance performance and ensures that an unavailable secondary node does not impact the primary node. However, since data from the primary node is not synchronized to the secondary node in real\-time, there is a small probability of data inconsistency if a failure occurs during replication latency.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Precautions

Single\-node instances do not support changing the data synchronization method.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.</div>



3. Click **Instances** in the left\-side navigation bar.

4. On the **Instances** page, click the target instance name.

5. On the **Summary** tab, in the **Configuration** section, click the button after **Data synchronization method**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Alternatively, on the <strong>Service availability</strong> tab, in the <strong>Instance availability</strong> section, click the Edit button after <strong>Data synchronization method</strong>.   </div>
   

6. Modify the synchronization method, and then click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[ModifyDBInstanceSyncMode](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstancesyncmode) |Call the ModifyDBInstanceSyncMode API to modify the data synchronization mode of an instance. |
