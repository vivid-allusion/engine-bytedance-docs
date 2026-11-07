---
title: "Enabling public network access"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Enabling_public_network_access"
---

You can apply for a public network address for an HBase instance in the console to allow devices outside the VPC to access the instance. This article describes how to apply for a public network address for an HBase instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The instance must be in the **Running** state.

* You must bind an Elastic IP (EIP) when applying for a public network address. You need to apply for a public IP first. For specific instructions, see [Applying for an EIP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP).

* Before enabling public network access for a Thrift2 connection address, you must first apply for a private network connection address for Thrift2. For detailed steps, see [Applying for Thrift2 connection address](https://docs.byteplus.com/en/docs/HBase/Enabling_or_disabling_high-availability_Thrift_connection_address).

* If a sub\-user is applying for a public network address, you must first configure the `EIPReadOnlyAccess` and `EIPFullAccess` permission policies for the sub\-user.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limitation

Enabling public network access for both ZK and Thrift2 connection addresses simultaneously is not supported.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Public network connections pose security risks. If devices outside the VPC no longer need to access the HBase instance, disable public network access promptly. To disable public network access, see [Disabling public network access](https://docs.byteplus.com/en/docs/HBase/Disabling_public_network_access).

<span id=".6LS555So6K-05piO"></span>
## Billing instructions


* A public address is associated with an Elastic IP Address (EIP). Using an EIP incurs charges at EIP billing rates. For more information about public IP address billing, refer to [Billing overview](https://docs.byteplus.com/en/docs/eip/Billing-overview).

* After a payment is overdue for two hours, a pay\-as\-you\-go EIP enters the **Closed** state, stops providing service, and is automatically unbound from its associated resource. If your HBase instance is bound to a pay\-as\-you\-go EIP, monitor your account balance and top it up promptly to prevent the instance's public access address from becoming unavailable due to overdue payments. For more details, see [Arrears](https://docs.byteplus.com/en/docs/eip/Arrears).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click **Connectivity**.

5. On the **Connectivity** tab, in the **Public network access** area, perform the required action based on the connection address type.

   
   |Connection address type |Procedure |
   |---|---|
   |ZK connection address |1. Click to Enable public network access.<br><br>2. In the pop\-up panel, select the EIPs you want to bind, and then click OK.<br><br>   You need to select two EIPs. One EIP is required for the ZK node, and the other EIP is shared by other components in the instance (such as RS and Master nodes). |
   |Thrift2 connection address |1. Click to Enable public network access.<br><br>2. In the pop\-up panel, select the EIPs you want to bind, and then click OK.<br><br>   You can only select one EIP.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You must apply for a Thrift2 private network access address before applying for a public network access address. For instructions on how to request a Thrift2 connection address, see <a href="https://docs.byteplus.com/en/docs/HBase/Enabling_or_disabling_high-availability_Thrift_connection_address">Applying for Thrift2 connection address</a>.</div><br> |
   


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations


* After the application is complete, you need to add the client device's IP address to the instance's IP allowlist. For more information, see [Creating an allowlist](https://docs.byteplus.com/en/docs/HBase/Creating_an_allowlist).

* You can use the new public address to access the HBase instance. See the following documents for connection methods:

   * [Access an HBase instance from a Java program using a Thrift2 address](https://docs.byteplus.com/en/docs/HBase/Access_an_HBase_instance_from_a_Java_program_using_a_Thrift2_address)

   * [Access an HBase instance from a Python program using a Thrift2 address](https://docs.byteplus.com/en/docs/HBase/Access_an_HBase_instance_from_a_Python_program_using_a_Thrift2_address)

   * [Connecting to the instance using the Java API](https://docs.byteplus.com/en/docs/HBase/Connecting_to_the_instance_using_the_Java_API)

   * [Connecting to the instance using the HBase Shell](https://docs.byteplus.com/en/docs/HBase/Connecting_to_the_instance_using_the_HBase_Shell)


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[CreateDBEndpoint](https://docs.byteplus.com/en/docs/HBase/CreateDBEndpoint) |Call the CreateDBEndpoint API to enable public access for the specified connection address. |
