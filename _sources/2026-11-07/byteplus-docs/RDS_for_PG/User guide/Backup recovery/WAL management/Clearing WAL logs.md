---
title: "Clearing WAL logs"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/clearing_wal_logs"
---

This topic describes how to clear local WAL logs in the console.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

RDS for PostgreSQL supports the local remaining available space protection feature, which can automatically clean up local WAL logs when the storage space usage of an instance exceeds a certain threshold. In addition to the automatic cleanup, RDS for PostgreSQL also supports manual cleanup of local WAL logs for deeper management of instance storage.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

If you select the **Clear all WAL** level while clearing WAL logs, it may cause problems such as the optional time range generating breakpoints and logical replication slots failing when the instance recovers by point in time, so proceed with caution.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An instance is created and in the **Running** state. For more details, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name.

5. At the top of the page, click **Backups**.

6. In the **Backups** tab, click the ** WAL management** sub\-tab, then click **Clear WAL**.

7. In the popped\-up **Clear WAL** window, select **Clearance level**, and then click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can choose either <strong>Clear backed up WAL</strong> or <strong>Clear all WAL</strong>.   </div>
