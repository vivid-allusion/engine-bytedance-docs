---
title: "Delete a read-only instance"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/Delete_a_read-only_instance"
---

This topic describes how to delete a read\-only instance in the RDS for SQL Server console.

<span id="2t2J4Nc3"></span>
## Prerequisites

An RDS for SQL Server instance has been created and meets the following conditions. For more information about how to create an instance, see [Create an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance).


* Compatible versions: SQL Server 2019 Enterprise Edition or SQL Server 2022 Enterprise Edition.

* Instance type: Cluster.

* Status: running.


<span id="94W8eJo2"></span>
## Precautions

When you delete a read\-only instance, the only backup policy option is to not retain backups.

<span id="L7tWwvjs"></span>
## Procedure


1. Log in to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper\-left corner of the top menu bar, select the project and region of the instance.

3. In the left navigation pane, click **Instances**.

4. On the **Instances** page, click the icon to the left of the target instance<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a57c22996bba4b36ea00244ed553e862.png) </span>to expand and view the read\-only instances under it.

5. In the **Actions** column of the target read\-only instance, click  **··· ** \> ** Delete an instance**.

6. In the **Are you sure you want to delete the selected instance?**  dialog box, confirm the information of the target read\-only instance and enter the name of the instance to be deleted.

7. Click the **Delete ** button to delete the read\-only instance.
