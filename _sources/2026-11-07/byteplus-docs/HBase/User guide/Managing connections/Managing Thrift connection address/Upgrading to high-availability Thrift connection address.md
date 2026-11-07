---
title: "Upgrading to high-availability Thrift connection address"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Upgrading_to_high-availability_Thrift_connection_address"
---

Existing instances using the legacy Thrift2 connection address can be upgraded to the new high\-availability Thrift connection address. This article describes how to upgrade to a high\-availability Thrift connection address.

<span id=""></span>
## Background

To provide a more reliable and stable service, HBase has upgraded its Thrift service to offer high\-availability Thrift. The legacy Thrift2 version provides basic multi\-language access but does not support the flexible configuration of Thrift Server node specifications and quantity. Instances with the legacy Thrift2 enabled can continue to be used for free. The new high\-availability Thrift offers improved availability and stability. It supports the flexible configuration of Thrift Server node specifications and quantity based on your business needs, and billing is based on the selected configuration.

Since the launch of high\-availability Thrift, applications for legacy Thrift2 connection addresses are no longer supported. Existing instances using the legacy Thrift2 connection address can be upgraded to the high\-availability Thrift connection address. The usage is the same for both the new and old versions. After the upgrade, you only need to replace the connection address in your application configuration with the high\-availability Thrift connection address.

<span id="LxVjkhqJ"></span>
## Prerequisites


* The instance has already been assigned a legacy Thrift2 connection address.

* The HBase database version must be 2.3.x or later. If you cannot enable a high\-availability Thrift connection address due to an unsupported instance version, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support for an upgrade.


<span id="rVt4GL4h"></span>
## Billing instructions


* The legacy Thrift2 connection address is free to use. After you upgrade to the new high\-availability Thrift connection address, HBase will be billed based on the specifications and quantity of the high\-availability Thrift Server nodes selected during the upgrade. For details about the billing rules and prices of Thrift Server, see [Billing items and prices](https://docs.byteplus.com/en/docs/HBase/Billing_items_and_prices).

* Upgrading to a high\-availability Thrift connection address is a configuration change. Therefore, fees for the Thrift Server configuration are calculated based on the configuration change order. For billing rules regarding configuration changes, see [Fee description for Modify Instance Spec](https://docs.byteplus.com/en/docs/HBase/Subscription_cancellation_or_instance_specification_modification).

* You cannot select a billing type when upgrading to a high\-availability Thrift connection address. By default, the billing method will match that of the HBase instance.


<span id="6J3kTi0W"></span>
## Procedure


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click **Connectivity**.

5. In the **Private network access** area, click **Upgrade to high availability Thrift connection address** next to the **Thrift2 connection address**.

6. In the pop\-up panel, select a **High availability Thrift Server configuration** based on the instance specifications.

   
   |**Name** |**Description** |
   |---|---|
   |Thrift Server node specifications<br><br> |Select the Thrift Server node specifications. For more information about Thrift Server node specifications, see [Product specifications](https://docs.byteplus.com/en/docs/HBase/Product_specifications). |
   |Number of Thrift Server nodes |Select the number of Thrift Server nodes. The value must be between 2 and 100. |
   

7. In the lower\-right corner of the page, click **Confirm order**.

8. On the **Confirm order** page, confirm the instance order details, read and select the terms of service, and then click **Submit the order**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When the instance status changes from <strong>Changing configuration</strong> to <strong>Running</strong>, the high\-availability Thrift connection address takes effect. You can get the high\-availability Thrift connection address on the Connectivity tab.   </div>
   

<span id="vB9EJFl4"></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[UpgradeDBInstanceThriftServer](https://docs.byteplus.com/en/docs/HBase/UpgradeDBInstanceThriftServer) |Call the UpgradeDBInstanceThriftServer API to upgrade a legacy Thrift2 connection address to high\-availability Thrift mode. |
