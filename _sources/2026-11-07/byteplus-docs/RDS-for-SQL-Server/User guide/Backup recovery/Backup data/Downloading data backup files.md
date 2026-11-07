---
title: "Downloading data backup files"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/downloading-data-backup-files"
---

RDS for SQL Server allows you to download unencrypted data backups to archive and restore your data. This topic describes how to download data backup files of a single database, multiple databases, or all databases.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have created an instance and its status is **Running**. For detailed instructions, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide).

* You have created a data backup, and its status is Success. For detailed instructions, see [Creating data backup manually](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-data-backup-manually).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The download link is valid for 7 days. After the link expires, you must obtain a new Intranet or Extranet address to download the backup files.

* The Intranet is safer, faster, and more stable than the Extranet. We recommend using the Intranet address to download data backup files.


<span id=".6LS555So"></span>
## Cost

The fees for downloading data are as follows:


* Intranet address download: Free.

* Extranet address download: Currently free.


<span id="VDuWZgbs"></span>
## Operation steps


1. Log in to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper\-left corner of the top menu bar, select the project and region of the instance.

3. On the **Instances** page, click the name of the target instance.

4. On the **Summary** page, click **Backups**.

5. On the **Basic backup list** tab, click **Download backup file** in the **Actions ** column of the target data backup.

6. In the **Download backup file** panel, copy the download address as follows:

   * Copy the download address of a single database: In the **Download Address** column for the target database, click the copy icon for **Intranet address** or **Extranet Address**.

   * Copy the download address of multiple or all databases: After selecting the target databases, click **Copy intranet address** or **Copy extranet address** to the right of **Select n items** below.

   7. Download the file using the copied **Intranet address** or **Extranet address** as follows:

      * (Recommended) Download through the **Intranet address**: You can download the file through intranet address ** ** when your BytePlus ECS instance and RDS for SQL Server instance can communicate over the intranet. Copy the **Intranet address** to a private network environment, such as an ECS instance in the same VPC, to download the file. For details on how to log in to an ECS instance, see [Login Overview](https://docs.byteplus.com/en/docs/ecs/Overview-1#.55m75b2V5pa55byP).

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Resources can only communicate within the same region. Cross\-region access via Private network is not supported.      </div>
      

      * Download through the **Extranet address**: If you cannot access RDS for SQL Server from a private network, you can download backup files using a extranet address. Copy the **Extranet address** to your browser to download the backup files.


<span id="faq"></span>
## FAQ

Q: Why doesn't the download link contain the file I want?

A: This may be because the target database had not been created when the instance was backed up. Therefore, the download link does not contain the file you need. You can get a download link from another backup set to download the backup.
