---
title: "Creating an IP address pool"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Create_an_IP_address_pool"
---

<span id=".5pON5L2c6K-05piO"></span>
## Instructions

This topic describes how to create an IP Address Pool. For related use limits and billing notes, see [IP Address Pool overview](https://docs.byteplus.com/en/docs/eip/IP_address_pool_overview).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in [to the EIP console](https://console.byteplus.com/eip/eips).

2. In the top menu bar, select the target region and project.

3. In the left navigation pane, select **Access to Internet \> IP Address Pool**.

4. Click **Create IP Address Pool** and fill in the parameters.

   
   |Parameters |Description |Example |
   |---|---|---|
   |**Basic information** |||
   |Billing method |Currently only Pay\-as\-you\-go is supported. |Pay\-as\-you\-go |
   |Region |Refers to different geographical regions where physical data centers are located.<br><br>Changing the Region is not supported. Please ensure that the Region of the IP address pool matches the Region of the allocated Elastic IP (EIP). |China (Beijing) |
   |Name |Name of the IP address pool. |IPpool01 |
   |**Line configuration** |||
   |ISP |Select the ISP for the IP Address Pool. BGP (multi\-line) is recommended. If you need another ISP, please contact your account manager. |BGP (multi\-line) |
   |Add CIDR block |Add a CIDR block to the IP address pool as needed.<br><br><br>* Off: Do not add CIDR blocks. You can [add CIDR blocks](https://docs.byteplus.com/en/docs/eip/Manage_IP_address_pools#.5re75Yqg572R5q61) anytime after creating the IP Address Pool.<br><br>* On: Select a method for CIDR block allocation. |Checked |
   |CIDR block allocation |Configure this parameter only when **Add CIDR block** is enabled.<br><br><br>* Mask: Select a mask for the IP address to allow the system to automatically assign the IP address CIDR block. Value range: 24–28.<br><br>* CIDR block: Enter the IP address CIDR block. Currently, only adding IPv4 CIDR blocks is supported. The mask value range is 23–30 and cannot start with 0.<br><br>   > When selecting the CIDR block method, we recommend that you first communicate with your account manager regarding the needed IP address CIDR block. Otherwise, allocation may fail. |Mask: /28 |
   |**More information** |||
   |Affiliated project |Select the project to which the IP address pool belongs. For more information, see [Project management](https://docs.byteplus.com/en/docs/eip/Managing-projects).<br><br><br>* If you select All Resources in the top menu bar before going to the Apply for EIP page, you can select an existing project from the drop\-down list.<br><br>* If you select a target project in the top menu bar before going to the Apply for EIP page, you can only select that project.<br><br>   After the IP Address Pool is created, if you need to switch projects, see [Transfer resources to a project](https://docs.byteplus.com/en/docs/6649/94337). |project\-1 |
   |Tag |Add one or more custom tags to the IP address pool as needed.<br><br>A tag consists of a tag key and a tag value. The tag can be used as a key\-value pair for IP address pool classification and search. For more information, see [Tag Management](https://docs.byteplus.com/en/docs/eip/Managing-tags).<br><br><br>* Click the<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_745f4ea6f3f698cebd9adc96c9240260.png) </span> icon to add multiple tags, and an IP address pool can have up to 20 tags.<br><br>* The Keys of multiple tags in the same IP address pool cannot be duplicated, and each Tag key can only have one Tag value.<br><br>* The Key and the Value are case\-sensitive. For example, Key=tag and Key=Tag are two different Tag keys. |ippool1:v1 |
   

5. Follow the console guidance to review and confirm the legal terms.

6. Click **Buy now** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## What to do next


* [Add a CIDR block](https://docs.byteplus.com/en/docs/eip/Manage_IP_address_pools#.5re75Yqg572R5q61): Add new CIDR blocks to expand the IP Address Pool.

* [Apply for an EIP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP): When creating an EIP, you can choose to start the IP Address Pool. The EIP IP address will be allocated from the specified IP Address Pool, and the IP config fee for the EIP will be waived.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[CreateIpAddressPool](https://docs.byteplus.com/en/docs/eip/CreateIpAddressPool): Create an IP Address Pool.
