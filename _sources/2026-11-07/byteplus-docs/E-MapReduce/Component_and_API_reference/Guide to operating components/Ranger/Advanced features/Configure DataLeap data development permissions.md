---
title: "Configure DataLeap data development permissions"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Configure_DataLeap_data_development_permissions"
---

DataLeap is a one\-stop big data platform solution independently developed by ByteDance, integrating data integration, development, operations, governance, and asset management capabilities. For more information, see [DataLeap overview](https://www.volcengine.com/docs/6260/65391).

DataLeap supports accessing EMR in secure mode or quick mode, and uses engines such as Hive and Spark in EMR to execute jobs. For details on using DataLeap with EMR, see [DataLeap on EMR 快速入门](https://docs.byteplus.com/docs/undefined/68da347342e561058e056b4e).

When using quick mode, there is no need to configure Ranger. In secure mode, fine\-grained authorization for Ranger is required to ensure jobs can run successfully.

In secure mode, EMR matches and executes tasks using users whose names match those in DataLeap, enabling more granular permission control. When EMR and DataLeap are bound in secure mode, user permission configuration is required in Ranger:


1. Import users to EMR via the EMR portal console: [User management](https://docs.byteplus.com/docs/E-MapReduce/105426).

2. Log in to Ranger Admin: [Overview](https://docs.byteplus.com/docs/E-MapReduce/109411).

3. Configure permissions for relevant components.


HDFS permission settings:

To grant full path permissions to an account, directly edit the all\-path policy and add the account name in Select User.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_a847faaf3f7ffe1daccdb42e85fff733.png) </span>

For more granular control, create a new policy.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_4427d2f18ec4818def998e2907e995d4.png) </span>

Add commonly used directories such as /tmp, /app\-logs, /apps, and any directories required for your business, and grant the corresponding read, write, and execute permissions.

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_e51bf75018cf44df18c966d676da9748.png) </span>

YARN permission settings:

By default, only the yarn and hive users have permission to submit jobs. To allow your own user to submit jobs directly to Yarn, click the default_yarn policy.

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_4dc530adfa4a24ff010b2d78bd452cb9.png) </span>

Add the corresponding account to the all\-queue policy.

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_9fc89e2510bd2cc7f23ce89f181bb7f1.png) </span>

HIVE permission settings:

Click the HIVE permission configuration entry, Hadoop SQL, and then click default_hive.

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_63a4b12295cd85a8bded280d65184e0b.png) </span>

Edit the all\-database, table, and column policy to add the user and grant all permissions, or adjust permissions based on your business needs.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_b096174e4108192f625ba8e277537cb9.png) </span>

DataLeap tasks write intermediate results to HDFS, so the user needs to be added to the all\-url policy.

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_b70c6c96aed8491e37cb407ac5d95463.png) </span>

DTS data integration permission configuration:


1. In Ranger's built\-in user management interface, click Add New User to create the root user and set the corresponding password.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_606fcf1eb6fe588444f30e0fa2b08ef2.png) </span>

2. Grant the root user HDFS all\-path policy permissions.

3. Grant the root user all\-database, table, and column policy permissions.
