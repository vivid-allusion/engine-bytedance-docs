---
title: "Enabling or disabling public network resolution"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Enabling_or_disabling_public_network_resolution"
---

The VPC domain name of HBase can be resolved to a private IP address in the internet environment. This article describes the steps to enable or disable public network resolution.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

Table Storage for HBase provides access points for a variety of protocols that you can use for connection. When you access a VPC access point, you should resolve the private domain name. However, the private domain name must be in the private environment of BytePlus by default so that it can be successfully resolved to a private IP address. Therefore, you can enable public network resolution for instance so that you can successfully resolve a private domain name to a private IP address even over the Internet. Public network resolution is suitable for scenarios in test environments and other non\-production environments, such as direct connections from test environments to HBase instances, and access of personal devices to private domain names.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Enabling or disabling public network resolution applies to both the **ZK connection address** and the **High availability Thrift connection address**. If you enabled public network resolution before applying for a high\-availability Thrift connection address, the address will also automatically support public network resolution after you apply.

* A BytePlus private IP address is obtained through the public network resolution of a private domain name. Your local environment should support BytePlus private network through VPN or other means, otherwise you cannot successfully access the private IP address.

* Due to the complexity of the internet environment, the accuracy and timeliness of domain name resolution cannot be ensured. Therefore, the internet DNS resolution function **only applies to non\-production environments**. The DNS Forward solution is strongly recommended for the production environment. You can configure Forward to BytePlus DNS in the local DNS Server to implement private domain name resolution.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/HBase/Creating_an_instance_1).

* To enable public network resolution for a high\-availability Thrift connection address, you must first apply for the address. For instructions, see [Enable high-availability Thrift connection address](https://docs.byteplus.com/en/docs/HBase/Enabling_or_disabling_high-availability_Thrift_connection_address#mCRFE24r).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. On the **Summary** page, click the **Connectivity** tab.

5. In the **Private network access** area of the **Connectivity** tab, enable or disable public network resolution.

   * Enable public network resolution

      Click the **Enable public network resolution**, and confirm the domain name involved in this operation in the pop\-up dialog box, and then click **OK**.

   * Disable public network resolution

      Click the **Disable public network resolution**, and confirm the domain name involved in this operation in the pop\-up dialog box, and then click **OK**.
