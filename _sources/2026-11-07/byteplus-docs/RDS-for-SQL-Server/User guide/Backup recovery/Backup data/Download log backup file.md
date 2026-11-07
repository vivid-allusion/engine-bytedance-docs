---
title: "Download log backup file"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/downloading-log-backups-files"
---

RDS for SQL Server provides a log backup feature to ensure the integrity and consistency of your instance data. This topic describes how to download log backup files.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An instance has been created and the instance state is Running. For detailed operations, see [Create an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The download link is valid for 12 hours. After the link expires, you need to get a new one to download the file. Note that if a log backup download task is initiated while the download link is valid, the task will continue until completion and is not affected by the link's expiration.

* We recommend using the internal network to download backup files because it is more secure, faster, and more stable than the public network.


<span id=".6LS555So"></span>
## Billing

The following fees apply to data downloads:


* Private network download: Free.

* Public network download: Currently free.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper\-left corner of the top menu bar, select the project and region where the instance is located.

3. On the **Instances** page, click the name of the target instance.

4. On the **Summary** page, click **Backups**.

5. On the **Backup and Restore** tab, click the **Log backup** sub\-tab under **Basic backup list**.

6. On the **Log backup** subtab, click **Download backup file** in the **Actions** column of the target log backup.

7. In the **Backup download address** dialog box, select a download method as needed:

      * Download via private network address(Recommended) : You can use this method when your BytePlus ECS and RDS for SQL Server instances are in the same VPC and can communicate over the internal network. Copy the **private network address** to a private network environment, such as an ECS instance in the same VPC, to download the file. To learn how to log in to an ECS instance, see [Log overview](https://docs.byteplus.com/en/docs/ecs/Overview-1#.55m75b2V5pa55byP).

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Description      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Resources can only communicate with each other within the same region. Cross\-region access via private IP addresses is not supported.      </div>
      

      * Download via public network address: If you cannot access the RDS for SQL Server instance through the private network, you can use the public network for the download. Copy the **public network address** to your browser to download the backup file.
