---
title: "Creating an IPv6 Gateway"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/Creating_an_IPv6_gateway_instance"
---

This topic describes how to create an IPv6 Gateway and associate it with a Virtual Private Cloud (VPC).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When you <a href="https://docs.byteplus.com/en/docs/IPv6/Enable_IPv6_for_private_networks">enable IPv6 for a VPC</a>, the system automatically creates an IPv6 Gateway for the VPC.</div>


<span id=".57qm5p2f6ZmQ5Yi2"></span>
## Limits

You can attach an IPv6 Gateway to only one VPC, and associate a VPC with only one IPv6 Gateway.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [IPv6 Gateway console](https://console.byteplus.com/eip/ipv6s).

2. In the top menu bar, select your target region.

3. Click **Create IPv6 Gateway** to pop up the Create IPv6 Gateway window.

4. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Name |Type the name for the IPv6 Gateway instance. |Ipv6GW\-01 |
   |VPC |Select a VPC to associate from the dropdown.<br><br><br>* VPC without IPv6 enabled: The system automatically enables IPv6 and assigns a `/56` IPv6 CIDR block, supporting IPv6 intranet communication.<br><br>* VPC with IPv6 enabled: Do not reassign a new IPv6 CIDR block. |vpc\-01 |
   |Subnet IPv6 |Specify whether to check **Automatically enable IPv6 for all subnets in the VPC**. You need to configure this parameter only when attaching a VPC without IPv6 enabled.<br><br><br>* Check: Assign a `/64` IPv6 CIDR block to each subnet by default.<br><br>* Uncheck: You can [enable IPv6 for the specified subnet](https://docs.byteplus.com/en/docs/IPv6/Enable_IPv6_for_private_networks#.5a2Q572R5byA5ZCvSVB2Ng==) later. |Uncheck |
   |Affiliated project |Select the project for the IPv6 Gateway. For more information, see [Project management](https://docs.byteplus.com/en/docs/IPv6/Managing_projects).<br><br><br>* If you select All Resources in the top menu bar, you can select one of existing projects from the project drop\-down list for this parameter.<br><br>* If you select a target project in the top menu bar, you can only select the target project for this parameter.<br><br><br>If you want to switch the IPv6 Gateway to another project after creation, see [Transfer resources in project](https://docs.byteplus.com/en/docs/6649/94337). |default |
   |Tags |Add one or more custom tags to the IPv6 Internet bandwidth as needed. A tag consists of a key\-value pair and is used for categorizing and searching resources. For more information, see [Tag management](https://docs.byteplus.com/en/docs/IPv6/Managing_tags).<br><br>Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e69956428611ee87141a75073bce3c8a.png) </span> icon, enter tag key and tag value to add tags to the IPv6 Gateway instance. |* Tag key: ipv6\-key<br><br>* Tag value: ipv6\-v1 |
   

5. Click **OK** to complete the action.


<span id="WxSHuOFL"></span>
## What to do next

[Enable IPv6 Internet bandwidth](https://docs.byteplus.com/en/docs/IPv6/Enable_IPv6_internet_bandwidth): IPv6 addresses without enabled IPv6 Internet bandwidth do not have the capability to communicate with the Internet. You need to enable IPv6 Internet bandwidth for them.

<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[CreateIpv6Gateway](https://docs.byteplus.com/en/docs/IPv6/CreateIpv6Gateway): Create an IPv6 Gateway instance.
