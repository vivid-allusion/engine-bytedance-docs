---
title: "Viewing instance list"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_instance_list"
---

The instance list displays the basic information of all instances under the primary account. By viewing the instance list, you can have a preliminary understanding of the information of all instances. This article describes the steps to view the instance list.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

The instance list displays information such as instance name/ID, running status, availability zone, virtual private cloud, compatible version, tag, instance specification, specification type, storage type, used storage space, storage space, calculate billing type, storage billing type, affiliated project, creation time, and supported operations.

The **Actions** column of the instance list provides shortcuts to the following operations:


* [Changing instance configuration](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Changing_node_specifications)

* [Restarting instances](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Restarting_instances)

* [Deleting or unsubscribing an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Deleting_or_unsubscribing_an_instance)

* [Changing billing method to Subscription](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Changing_billing_method_to_Subscription)

* [Creating a data backup manually](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_a_data_backup_manually)

* [Managing parameters](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_parameters)

* [Viewing monitoring information](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Monitoring_metrics)

* [Managing accounts](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Account_and_access_authorization)

* [Managing databases](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Managing_databases)


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. Click **Instances** on the left navigation bar to view the instance list.

4. (Optional) Customize the display column of the instance list. Click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ad31d166c8d6a2f8b75e8a2fbdcd2298.jpg) </span>icon in the upper right corner of the instance list to customize the display of the columns in the instance list. Except for the **Instance name/ID** and **Actions** columns, the remaining columns can be customized to display.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[DescribeDBInstances](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances) |Call the DescribeDBInstances to query the instance list. |
