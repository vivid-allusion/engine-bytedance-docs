---
title: "View Cerebro details"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/View_Cerebro_details"
---

You can view Cerebro details in the console, including basic information, network information, access information, and payment information. This article explains how to view Cerebro details.

<span id="vdTaBzXo"></span>
## Prerequisites

Cerebro is created. For specific operations, refer to [Create Cerebro](https://docs.byteplus.com/en/docs/cloudsearch/Create_Cerebro).

<span id="dGo0k8KB"></span>
## Procedure


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. Select **Cerebro** in the left navigation bar to view the following information on the **Cerebro** page.

   
   |**Category** |**Description** |
   |---|---|
   |Basic information |* Instance ID: Cerobro’s identifier. You can click the Copy button to copy the ID.<br><br>* Username: the login username for Cerobro, default is **admin**.<br><br>* Password: the user’s password. If you forget or need to change the password, click **Reset password**, enter and confirm the new password in the pop\-up dialog, then click **OK**.<br><br>* Node specifications: Cerobro’s node specifications.<br><br>* Availability zone: the availability zone where Cerebro is located. |
   |Network information |* Virtual Private Cloud: the virtual private cloud the instance belongs to.<br><br>* Subnet: the subnet to which the instance belongs. |
   |Access information |* Public network access: you can turn public network access on or off. When enabled, the instance can be accessed via the specified public address. You can also click to change bandwidth configuration to adjust Cerebro’s public network bandwidth. The interface provides 1 to 200 Mbps of public network bandwidth. Set it as needed.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you need to set bandwidth over 200 Mbps, please <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000255">submit a ticket</a> for approval.   </div><br>   <br><br>* Public access address: the address used to access Cerebro over the public network. You can click **IP allowlist configuration** to set IP addresses allowed to access Cerebro through the public network.<br><br>* Private network access address: the address used to access Cerebro within the VPC. By default, all devices within the same VPC can access the instance. You can also click **IP allowlist configuration** to set IP addresses allowed to access Cerebro within the VPC. If you need to access the instance via a private network address using dedicated lines, enable public resolution for the private address. For detailed steps, refer to [Configure Cerebro private address public resolution](https://docs.byteplus.com/en/docs/cloudsearch/Configure_Cerebro_private_network_address_public_network_resolution).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The allowlist supports uploading up to 300 IP addresses or IP address ranges.</div><br><br><br>* <div data-tips="true" data-tips-type="default"><code>127.0.0.1</code> represents blocking all IPv4 addresses, while <code>0.0.0.0/0</code> represents allowing all IPv4 addresses to access.</div><br><br><br>* <div data-tips="true" data-tips-type="default">From a security perspective, it is not recommended to configure access for all IP addresses.</div><br> |
   |Payment information |* Creation time: the time when Cerebro was created.<br><br>* Billing type: the billing method for Cerebro. |
