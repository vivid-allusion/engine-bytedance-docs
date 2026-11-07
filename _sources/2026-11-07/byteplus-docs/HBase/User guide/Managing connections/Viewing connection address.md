---
title: "Viewing connection address"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Viewing_connection_address"
---

Table Storage for HBase provides a ZK private connection address by default and also supports instance access via a Thrift address. You can choose a suitable connection address to access and manage the HBase instance based on your business needs. This article describes how to view HBase connection addresses in the console.

<span id=".6K6_6Zeu5pa55byP"></span>
## Access method

HBase provides private and public network access methods. The following table compares the two access methods.


|Access method |Description |Precautions |
|---|---|---|
|Private network access |* Accessing your HBase instance via a private network connection provides maximum security and performance.<br><br>* When you create an HBase instance, a ZK connection address for private network access is provided by default.<br><br>* You can also request a high availability connection address for private network access to your HBase instance based on your business needs. For detailed steps, see [Enable high-availability Thrift connection address](https://docs.byteplus.com/en/docs/HBase/Enabling_or_disabling_high-availability_Thrift_connection_address). |None |
|Public network access |You can apply for a public connection address for your HBase instance to allow access from devices outside the VPC. |* Public network connections pose security risks. By default, public network connection addresses are not enabled for HBase. You can apply for one manually in the console. To enable public network access, see [Enabling public network access](https://docs.byteplus.com/en/docs/HBase/Enabling_public_network_access).<br><br>* When you apply for a public IP address, it will be bound to your Elastic IP Address (EIP), and fees are charged by EIP. For more details, see [Billing overview](https://docs.byteplus.com/en/docs/eip/Billing-overview).<br><br>* When devices outside the VPC no longer need to access the HBase instance, we recommend that you promptly disable public network access. To disable public network access, see [Disabling public network access](https://docs.byteplus.com/en/docs/HBase/Disabling_public_network_access). |


<span id=".6L-e5o6l5Zyw5Z2A57G75Z6L"></span>
## Connection address type

The supported access methods vary depending on the HBase connection address type.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The symbols in the following table are described as follows:</div>



* <div data-tips="true" data-tips-type="tip">✔️: Supports applying for or releasing the connection address.</div>


* <div data-tips="true" data-tips-type="tip">❌: Applying for or releasing this connection address is not supported.</div>




|Connection address type ||ZK connection address |High availability Thrift connection address |
|---|---|---|---|
|Private network address |Support application |❌<br><br>Application is not required. Each HBase instance includes a ZK private network access address by default. |✔️<br><br>To apply for the high\-availability Thrift private network connection address, see [Enable high-availability Thrift connection address](https://docs.byteplus.com/en/docs/HBase/Enabling_or_disabling_high-availability_Thrift_connection_address#mCRFE24r). |
||Support release |❌<br><br>The default ZK private network access address cannot be released. |✔️<br><br>To release the high\-availability Thrift private network connection address, see [Disable high-availability Thrift connection address](https://docs.byteplus.com/en/docs/HBase/Enabling_or_disabling_high-availability_Thrift_connection_address#36GlpPI4). |
|Public network address |Support application |✔️<br><br>Enabling public network access automatically generates a public network address. To enable public network access, see [Enabling public network access](https://docs.byteplus.com/en/docs/HBase/Enabling_public_network_access).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Enabling public network access requires you to select and bind two EIPs. One EIP is bound to the ZK node, while the other is shared by other components in the instance, such as RS and Master nodes.</div><br> |✔️<br><br>Enabling public network access automatically generates a public network address. To enable public network access, see [Enabling public network access](https://docs.byteplus.com/en/docs/HBase/Enabling_public_network_access).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You must apply for a high availability private network access address before applying for a public network access address.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You only need to select and bind one EIP to enable public network access.</div><br> |
||Support release |✔️<br><br>The public network address is automatically released after public network access is disabled. To disable public network access, see [Disabling public network access](https://docs.byteplus.com/en/docs/HBase/Disabling_public_network_access). |✔️<br><br>The public network address is automatically released after public network access is disabled. To disable public network access, see [Disabling public network access](https://docs.byteplus.com/en/docs/HBase/Disabling_public_network_access). |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click **Connectivity**.

5. On the **Connectivity** tab, you can view information about the corresponding ZK or high availability connection addresses in the **Private network access** and **Public network access** areas.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">By default, HBase only provides a ZK private connection address. To view high availability or public connection addresses, you need to first apply for a high availability connection address or enable public access. For instructions, see <a href="https://docs.byteplus.com/en/docs/HBase/Enabling_or_disabling_high-availability_Thrift_connection_address">Enable high\-availability Thrift connection address</a> and <a href="https://docs.byteplus.com/en/docs/HBase/Enabling_public_network_access">Enabling public network access</a>.   </div>
