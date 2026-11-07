---
title: "Configuring local remaining available space protection"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/configuring_local_remaining_space_protection"
---

This topic describes how to configure local remaining available space protection in the console.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

RDS for PostgreSQL supports local remaining available space protection. after enabling this feature, the instance automatically clears the earliest local WAL log when storage usage exceeds 80% or remaining space is less than 5 GB, until usage drops below 80% and remaining space exceeds 5 GB, preventing abnormalities such as instance read\-only due to high storage usage.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* After enabling local remaining available space protection, the instance clears WAL logs in chronological order from oldest to recent. After clearing the WAL, there might be issues such as the range of selectable time for instance point\-in\-time recovery having discontinuities, and logical replication slots becoming invalid. Proceed with caution.

* Due to active logical replication slots not consuming in time, WAL logs may not be cleared promptly, causing storage space to not be released timely. If storage usage remains high for a long time after enabling this feature, monitor the accumulation of WAL logs in the instance's logical replication slots. For more details on clearing logical replication slots, refer to [How to troubleshoot and handle inactive logical replication slots in instances](https://docs.byteplus.com/en/docs/RDS_for_PG/How_to_troubleshoot_and_resolve_inactive_logical_replication_slots_in_an_instance).


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An instance is created and in the **Running** state. For more details, refer to [Creating an instanc](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance)e.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name.

5. At the top of the page, click **Backups**.

6. In the **Backups** tab, click the **WAL management** sub\-tab, then click **Backup settings**.

7. In the pop\-up **Backup settings** window, click the switch button under **Local remaining available space protection** to turn this feature on or off.


<span id=".55u45YWzIEFQSQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[DescribeBackupPolicy](https://docs.byteplus.com/en/docs/RDS_for_PG/describebackuppolicy) |Call DescribeBackupPolicy API to query the backup policy. |
|[ModifyBackupPolicy](https://docs.byteplus.com/en/docs/RDS_for_PG/modifybackuppolicy) |Call ModifyBackupPolicy API to modify the backup policy. |
