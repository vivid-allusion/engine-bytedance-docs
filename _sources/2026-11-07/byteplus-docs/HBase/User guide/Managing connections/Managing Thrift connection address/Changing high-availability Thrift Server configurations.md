---
title: "Changing high-availability Thrift Server configurations"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Changing_high-availability_Thrift_Server_configurations"
---

You can flexibly modify the Thrift Server configuration based on changes in your business volume. This article describes how to modify the high\-availability Thrift Server configuration.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A high\-availability Thrift connection address is enabled for the instance. For details, see [Enable high-availability Thrift connection address](https://docs.byteplus.com/en/docs/HBase/Enabling_or_disabling_high-availability_Thrift_connection_address) or [Upgrade to high-availability Thrift connection address](https://docs.byteplus.com/en/docs/HBase/Upgrading_to_high-availability_Thrift_connection_address).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Billing instructions

After you modify the high\-availability Thrift Server configuration, you will be charged based on the new configuration's price. For more information about billing for configuration changes, see [Fee description for Modify Instance Spec](https://docs.byteplus.com/en/docs/HBase/Subscription_cancellation_or_instance_specification_modification).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. You can modify the high\-availability Thrift configuration using one of the following methods.

   * Method 1

      On the **Summary** page, in the **Configuration** section, click **Configuration change** in the actions column for **High availability Thrift Server**.

   * Method 2

      On the **Connectivity** page, in the **Private network access area**, click **Configuration change** for **High availability Thrift connection address**.

5. In the pop\-up panel, reselect a **High availability Thrift Server configuration** based on the instance specifications.

   
   |**Name** |**Description** |
   |---|---|
   |Thrift Server node specifications<br><br> |Select the Thrift Server node specifications. For more information about Thrift Server node specifications, see [Product specifications](https://docs.byteplus.com/en/docs/HBase/Product_specifications). |
   |Number of Thrift Server nodes |Select the number of Thrift Server nodes. The value must be between 2 and 100. |
   

6. In the lower\-right corner of the page, click **Confirm order**.

7. On the **Confirm order** page, review the updated order details, read and agree to the terms of service, and click **Submit the order**.


<span id="Eo8Bhxr1"></span>
## Related APIs


|API |Description |
|---|---|
|[ModifyDBInstanceThriftServerSpec](https://docs.byteplus.com/en/docs/HBase/ModifyDBInstanceThriftServerSpec) |Call ModifyDBInstanceThriftServerSpec to modify the node specifications or number of nodes of a high\-availability Thrift server. |
