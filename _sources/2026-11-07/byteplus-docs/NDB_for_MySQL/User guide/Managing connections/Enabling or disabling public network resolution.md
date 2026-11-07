---
title: "Enabling or disabling public network resolution"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Enabling_or_disabling_public_network_resolution"
---

The VPC domain name of NDB for MySQL can be resolved to a private IP address in the internet environment. This article describes the steps to enable or disable public network resolution.

<span id="背景信息"></span>
## Background

NDB for MySQL provides access points for a variety of protocols that you can use for connection. When you access a VPC access point, you should resolve the private domain name. However, the private domain name must be in the private environment of BytePlus by default so that it can be successfully resolved to a private IP address. Therefore, you can enable public network resolution for instance so that you can successfully resolve a private domain name to a private IP address even over the Internet. Public network resolution is suitable for scenarios in test environments and other non\-production environments, such as direct connections from test environments to NDB for MySQL instances, and access of personal devices to private domain names.

<span id="注意事项"></span>
## Precautions


* A BytePlus private IP address is obtained through the public network resolution of a private domain name. Your local environment should support BytePlus private network through VPN or other means, otherwise you cannot successfully access the private IP address.

* Due to the complexity of the internet environment, the accuracy and timeliness of domain name resolution cannot be ensured. Therefore, the internet DNS resolution function **only applies to non\-production environments**. The DNS Forward solution is strongly recommended for the production environment. You can configure Forward to BytePlus DNS in the local DNS Server to implement private domain name resolution.


<span id="前提条件"></span>
## Prerequisites

The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://www.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

<span id="操作步骤"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. On the **Summary** page, click the **Connectivity** tab.

5. On the **Connectivity** tab, click **Edit** in the destination endpoint area.

6. In the **Connection information** area of the **Modify endpoint** sidebar, enable or disable **public network resolution**.

   * **Enable public network resolution**: Click the **Enable public network resolution**, and confirm the domain name involved in this operation in the pop\-up dialog box, and then click **OK**.

   * **Disable public network resolution**: Click the **Disable public network resolution**, and confirm the domain name involved in this operation in the pop\-up dialog box, and then click **Confirm to disable**.
