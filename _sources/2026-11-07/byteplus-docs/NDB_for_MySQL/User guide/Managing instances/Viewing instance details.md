---
title: "Viewing instance details"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_instance_details"
---

The instance information page shows basic information about the instance. This article describes the steps to view basic information about an instance.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the **Summary** tab, you can view the instance's **Basic information**, **Configuration** and **Billing information**.

   
   |**Information classification** |**Description** |
   |---|---|
   |Basic information |Basic information includes instance name, instance ID, creation time, primary instance availability zone, virtual private cloud/subnet, affiliated project, maintenance window, tag, and deletion protection. |
   |Configuration |Configuration includes compatible version, kernel version, node specification, node configuration, number of nodes, used space, specification type, storage type, and compressed data space. |
   |Billing information |The billing information includes the computing billing type of the instance, the storage billing type, and whether to enable automatic renewal (subscription instance). |
   


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstanceDetail) |Call the DescribeDBInstanceDetail to query the instance details. |
