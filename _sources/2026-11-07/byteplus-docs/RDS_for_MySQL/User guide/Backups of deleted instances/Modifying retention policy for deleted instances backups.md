---
title: "Modifying retention policy for deleted instances backups"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_retention_policy_for_deleted_instances_backups"
---

This topic introduces the operation steps for modifying the backup retention policy of deleted instances.

<span id="background"></span>
## Background

When deleting an instance, you can set the retention policy for instance backups. You can choose to keep **The last one** or **All**. If you have selected to keep all backups, you can modify this policy after deleting the instance.

<span id="prerequisites"></span>
## Prerequisites


* The status of the deleted instance backup is **Recycled**.

* The backup retention policy of the deleted instance is **All**.


<span id="steps"></span>
## Steps


1. Log on to the [RDS for MySQL console](https://console.volcengine.com/db/rds-mysql).

2. In the top menu bar on the upper left, select the region.

3. On the left navigation bar, select **MySQL** \> **Backups**.

4. On the **Backups of deleted instances** page, click **Modify retention policy**.

5. On the popped\-up **Modify policy** page, enter the ID of the instance to which the target backup file belongs to search for the instance.

6. After setting the backup retention policy to **The last one**, click **Next step**.

7. On the **Confirm policy** page, after confirming that the modification content is correct, click **OK**.
