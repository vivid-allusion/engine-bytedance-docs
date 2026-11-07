---
title: "View migration results"
product: "Data Migration Service"
product_code: "dms"
source: "https://docs.byteplus.com/en/docs/dms/View-migration-results"
---

After the data migration is completed, you can view the detailed information of the data migration through the migration report and migration list. This article explains how to view the migration report, migration list, and the parameters explanation of the migration list.

<span id="f000b542"></span>
## Background Information

After the completion of data migration, the storage migration service will generate migration reports and migration lists, as explained below:


* Migration report: The migration report includes information such as migration tasks, migration target site, and migration source site. The report is named `dms-<account ID>-<task name>_<source bucket name>_<destination bucket name>_report.pdf`. You can obtain the migration report from the Storage Migration Service console or the destination storage bucket for data migration.

* Migration list: Includes information such as the name, size, and migration result of the migrated objects. You can obtain the migration list in the destination storage bucket for data migration. If there is no permission for the source objects or if the migration fails to retrieve archived objects, the migration will fail. The names of the successful and failed migration lists are different, as explained below:

   * Migration Success List: The name is`dms-<account id>-<task name>_<source bucket name>_<destination bucket name>_success`.

   * Migration Failure List: The name is `dms-<account id>-<task name>_<source bucket name>_<destination bucket name>_failed`.


<span id="6d6efa5f"></span>
## Prerequisite

Data migration has been completed or finished.

<span id="353b003b"></span>
## Precautions

When migrating data, only the latest version of objects will be migrated, and the historical versions of objects will not be migrated. If the source objects contain historical versions, there will be an inconsistency between the number of source objects and the number of objects in the destination storage bucket after migration.

<span id="fe085729"></span>
## View migration report


1. Log on to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Bucket List**. In the **displayed bucket list**, click the target bucket name.

3. Find the file named `dms-<account id>-<task name>_<source bucket name>_<destination bucket name>_report.pdf` in the root directory, and click **Download** option under the **Operation** column of that file.


<span id="8f61c9c0"></span>
## View migration list


1. Log on to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Bucket List**. In the **displayed bucket list**, click the target bucket name.

3. Find the file named `dms-<account id>-<task name>_<source bucket name>_<destination bucket name>_success` or `dms-<account id>-<task name>_<source bucket name>_<destination bucket name>_failed` in the root directory, and click **Download** option under the **Operation** column of that file.

   After downloading the migration list to the local device, it can be viewed locally. The migration list includes file names, file sizes, and other information, as shown in the diagram below.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24aa410ac61b43a9b9d9e48163abfa61~tplv-goo7wpa0wc-image.image) </span>

   Migration list parameter description is as follows:

   
   |Parameters |Instructions |
   |---|---|
   |key |File name. |
   |size |File size. |
   |state |Migration result, corresponding value explanations are as follows:<br><br><br>* `success`: The object migration is successful.<br><br>* `failed`: The object migration failed.<br><br>* `skip`: During migration, skip the object, i.e., do not migrate the object.<br><br>* `notExist`: The object does not exist. When migrating data, the source object is deleted, and then the problem with the object not existing occurs. |
   |crc64 |CRC64 checksum of the object. |
   |completedTime |Migration completion time. |
   |message |Migration failure details. For example, when migrating data while maintaining the original storage attributes, if TOS does not support a certain storage type of another cloud vendor's object, the storage type of the object will be set to standard storage by default, and the message will indicate unknown storage class, upload with default standard storage class. |
