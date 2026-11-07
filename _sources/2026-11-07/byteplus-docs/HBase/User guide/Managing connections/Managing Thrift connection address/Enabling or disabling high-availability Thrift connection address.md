---
title: "Enabling or disabling high-availability Thrift connection address"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Enabling_or_disabling_high-availability_Thrift_connection_address"
---

By default, Table Storage for HBase provides a ZK connection address for accessing instances and supports Thrift connections to meet multi\-language development needs. Thrift is a built\-in service component in standard HBase instances. Developed on the Apache Thrift communication framework, it allows access from multiple programming languages. This article describes how to enable and disable high\-availability Thrift connection addresses in the console.

<span id="fErXcejK"></span>
## Background

To provide a more reliable and stable service, HBase has upgraded its Thrift service to offer high\-availability Thrift. The legacy Thrift2 version provides basic multi\-language access but does not support the flexible configuration of Thrift Server node specifications and quantity. Instances with the legacy Thrift2 enabled can continue to be used for free. The new high\-availability Thrift offers improved availability and stability. It supports the flexible configuration of Thrift Server node specifications and quantity based on your business needs, and billing is based on the selected configuration.

Since the launch of high\-availability Thrift, applications for legacy Thrift2 connection addresses are no longer supported. Existing instances using the legacy Thrift2 connection address can be upgraded to the high\-availability Thrift connection address. The usage is the same for both the new and old versions. After the upgrade, you only need to replace the connection address in your application configuration with the high\-availability Thrift connection address.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The HBase database version must be 2.3.x or later. If you cannot enable a high\-availability Thrift connection address due to an unsupported instance version, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support for an upgrade.

* The protocol version for the high\-availability Thrift connection address provided by Table Storage for HBase is Thrift2, and the Thrift client version must be v0.13.0.


<span id=".5pON5L2c5q2l6aqk"></span>
## Billing instructions


* For details about the billing rules and prices of Thrift Server, see [Billing items and prices](https://docs.byteplus.com/en/docs/HBase/Billing_items_and_prices).

* You cannot select a billing type when enabling a high\-availability Thrift connection address. By default, the billing method is the same as the HBase instance's.

* Enabling a high\-availability Thrift connection address is a configuration change. Therefore, fees for the Thrift Server configuration are calculated based on the configuration change order. For billing rules regarding configuration changes, see [Fee description for Modify Instance Spec](https://docs.byteplus.com/en/docs/HBase/Subscription_cancellation_or_instance_specification_modification).


<span id="mCRFE24r"></span>
## Enable high\-availability Thrift connection address


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click **Connectivity**.

5. In the **Connectivity** area, click **Enable** next to **High availability Thrift connection address**.

6. In the pop\-up panel, select a **High availability Thrift Server configuration** based on the instance specifications.

   
   |**Name** |**Description** |
   |---|---|
   |Thrift Server node specifications<br><br> |Select the Thrift Server node specifications. For more information about Thrift Server node specifications, see [Product specifications](https://docs.byteplus.com/en/docs/HBase/Product_specifications). |
   |Number of Thrift Server nodes |Select the number of Thrift Server nodes. The value must be between 2 and 100. |
   

7. In the lower\-right corner of the page, click **Confirm order**.

8. On the **Confirm order** page, confirm the instance order details, read and select the terms of service, and then click **Submit the order**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When the instance status changes from <strong>Changing configuration</strong> to <strong>Running</strong>, the high\-availability Thrift connection address takes effect. You can get the high\-availability Thrift connection address on the Connectivity tab.   </div>
   

<span id="36GlpPI4"></span>
## Disable high\-availability Thrift connection address


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. You can disable high\-availability Thrift through any of the following methods.

   * Method 1

      On the **Summary** page, in the **Configuration** area, click **Disable** in the actions column for **High availability Thrift Server**.

   * Method 2

      On the **Connectivity** page, in the **Private network access** area, click **Disable** for **High availability Thrift connection address**.

5. In the dialog box, confirm the current configuration of the instance, read and select the checkbox for the shutdown risk warning, and then click **Confirm order**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After the high availability Thrift Server is disabled, the high availability Thrift connection address is reclaimed, and applications can no longer access the HBase instance through the Thrift connection address. Ensure that the Thrift connection address configured in your application is changed to the ZK connection address.   </div>
   

<span id="pqThOUx8"></span>
## Subsequent operations


* [Access an HBase instance from a Java program using a Thrift2 address](https://docs.byteplus.com/en/docs/HBase/Access_an_HBase_instance_from_a_Java_program_using_a_Thrift2_address)

* [Access an HBase instance from a Python program using a Thrift2 address](https://docs.byteplus.com/en/docs/HBase/Access_an_HBase_instance_from_a_Python_program_using_a_Thrift2_address)

* [Access an HBase instance from a Go program via a Thrift2 address](https://docs.byteplus.com/en/docs/HBase/Access_an_HBase_instance_from_a_Go_program_via_a_Thrift2_address)


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[EnableDBInstanceThriftServer](https://docs.byteplus.com/en/docs/HBase/EnableDBInstanceThriftServer) |Call the EnableDBInstanceThriftServer API to enable the high\-availability Thrift connection address. |
|[DisableDBInstanceThriftServer](https://docs.byteplus.com/en/docs/HBase/DisableDBInstanceThriftServer) |Call the DisableDBInstanceThriftServer API to disable the high\-availability Thrift connection address. |
|[StopThrift2](https://docs.byteplus.com/en/docs/HBase/StopThrift2) |Call the StopThrift2 interface to delete the Thrift2 private network connection address of the instance. |
