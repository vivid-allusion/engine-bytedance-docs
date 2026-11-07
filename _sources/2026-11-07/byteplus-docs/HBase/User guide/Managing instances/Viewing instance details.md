---
title: "Viewing instance details"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Viewing_instance_details"
---

You can view the basic information, configuration information, and billing details of the instance on the console. This article describes how to view detailed information about an HBase instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An instance has been created. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/HBase/Creating_an_instance_1).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. On the **Summary** tab, you can view the following information about the HBase instance.

   
   |Classification |Description |
   |---|---|
   |**Basic information** |You can view information such as instance ID, instance name, subnet, project, creation time, deletion protection status, availability zone, tag, private network.<br><br>You can also modify the instance name, enable or disable instance deletion protection, manage tags, and perform other operations in this area. For detailed steps, see:<br><br><br>* [Instance deletion protection](https://docs.byteplus.com/en/docs/HBase/Instance_deletion_protection)<br><br>* [Managing tags](https://docs.byteplus.com/en/docs/HBase/Managing_tags_1) |
   |**Configuration** |You can view information such as database version, instance type, node specification, number of nodes, storage type, storage space,.<br><br>You can also change node specifications, add or remove nodes, and change storage size in this area. For detailed steps, see:<br><br><br>* [Adding or removing nodes](https://docs.byteplus.com/en/docs/HBase/Adding_or_removing_nodes)<br><br>* [Changing node specifications](https://docs.byteplus.com/en/docs/HBase/Changing_node_specifications)<br><br>* [Changing storage size](https://docs.byteplus.com/en/docs/HBase/Changing_storage_size) |
   |**Billing information** |Supports viewing instance billing type information.<br><br><br>* For pay\-as\-you\-go instances, you can click **Recharge** to top up your account before it becomes delinquent. |
   


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/HBase/DescribeDBInstanceDetail) |Call the DescribeDBInstanceDetail interface to query detailed information about a specified instance. |
