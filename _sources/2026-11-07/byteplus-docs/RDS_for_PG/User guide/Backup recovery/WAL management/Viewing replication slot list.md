---
title: "Viewing replication slot list"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/view_replication_slot_list"
---

RDS for PostgreSQL displays all replication slots of instances on the console. this topic describes the procedure to view the instance replication slot list on the console.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Replication slot is a unique mechanism of PostgreSQL databases that prevents data loss or duplicate replication during streaming replication, enhancing data replication reliability.

RDS for PostgreSQL provides a replication slot list on the console to easily view relevant information of instance replication slots, such as name, type, used extension, database the slot is located, temporary slot or not, state, IP address source of the slot, WAL accumulation, and supported actions.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Instances have been created and the instance is in **Running** state, for more details please see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name.

5. At the top of the page, click **Backups**.

6. On the **Backups** tab, click the **WAL management** sub\-tab to view the replication slot list.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the replication slot list, you can filter and view slots by the <strong>Slot type</strong>, <strong>Temporary slot or not</strong>, and <strong>State</strong> columns, and search for target extensions, target databases, or related source replication slots in the <strong>Used extension</strong>, <strong>Database the slot is located</strong>, and <strong>IP address</strong> columns.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When a PostgreSQL instance serves as the replication source for a Volc DTS task, DTS also creates corresponding replication slots. These replication slot names start with <code>_volc_dts_logical_replica_</code>. In the replication slot list, click the name of such replication slots to view<img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dce7002e5f8f75ded2ea9a106e7db3b8.png" width="20px" />, you can retrieve the ID of the DTS task associated with this replication slot. You can use this ID to check the task progress in the <a href="https://console.byteplus.com/dts">DTS console</a>.   </div>
   


<span id=".55u45YWzIEFQSQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[DescribeSlots](https://docs.byteplus.com/en/docs/RDS_for_PG/describeslots) |Call DescribeSlots API to query the instance replication slots. |
