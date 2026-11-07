---
title: "Creating a Direct Connect Gateway"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Creating-a-Direct-Connect-gateway-1"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

The Direct Connect (DC) Gateway serves as an ingress for an on\-premises data center to access the cloud, and connects a Virtual Private Cloud (VPC) with a DC Connection, enabling mutual access between the data center and the VPC.

When creating a DC Gateway, you can attach a DC Connection at creation or attach one after creation.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have completed real\-name authentication for your account before purchasing DC resources.

* The total value of your account balance (cash balance) and coupons applicable to DC Gateway must be no less than USD 0. You can recharge your account in advance. For procedure, see [Recharge](https://docs.byteplus.com/en/docs/6269/100434).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Direct Connect Gateway console](https://console.byteplus.com/dc/DirectConnectGateway).

2. In the top menu bar, select your target region.

3. On the Direct Connect Gateway page, click **Create DC Gateway**, and configure the DC Gateway parameters in the pop\-up dialog box.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Regions |Select the region where the DC Gateway is deployed. It must match the region of the DC Connection. |China (Beijing) |
   |Name |Set a name for the DC Gateway. |Dcgw\-01 |
   |ASN |Set an ASN for the DC Gateway.<br><br><br>* The valid range for Direct Connect Gateway ASN is 137718, 64512\-65534, and 4200000000\-4294967294, among which 137718 is the ASN of BytePlus.<br><br>* If a DC Gateway is used only in a common scenario (such as an on\-premises data center connecting to a single Virtual Private Cloud resource via DC), use the BytePlus ASN (137718).<br><br>* If a DC Gateway is used in a special scenario (such as an on\-premises data center connecting to multiple CENs via DC), you need to customize an ASN to each DC Gateway and avoid using the BytePlus ASN (137718) to ensure no duplicate ASNs among different DC Gateways. |64512 |
   |IPv6 |Specify whether to enable IPv6. Once enabled, it cannot be disabled.<br><br><br>* Disabling is not supported after enabling IPv6.<br><br>* If the DC Gateway does not have IPv6 enabled, IPv6 is unavailable for its associated DC Virtual Interface. |Enable |
   |Affiliated project |Select the project to which the new DC Gateway belongs. A project refers to a task in your daily work. You can create multiple projects under the same account and create or purchase cloud resources for each project. A resource can only belong to one project. Cloud resources cannot be shared between separate projects.<br><br><br>* After selecting a project, the created DC Gateway can only be used by users with permission for that project.<br><br>* If you select "All Resources" in the top menu bar before entering the creation page, the new DC Gateway belongs to the default project. You can reselect the project when creating a DC Gateway.<br><br>* If you select a specific project in the top menu bar, the new DC Gateway belongs to that project. You cannot modify the project on the creation page. To reselect, cancel the current creation and select your target project and then create a DC Gateway.<br><br>* After adding a DC Gateway to a project, you can transfer the DC Gateway out of the project based on actual business needs. For details, see [Project resource management](https://docs.byteplus.com/en/docs/6649/94337).<br><br>* If no projects are available, you can click "Create Project" to create a new project during the creation of the DC Gateway. |default |
   |Tags |You can configure tags for the DC Gateway below "Advanced Option". A tag consists of a tag key (Key) and a tag value (Value). It can be used to classify and search for DC Gateways.<br><br><br>* Click <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_745f4ea6f3f698cebd9adc96c9240260.png) </span> icon to add multiple tags. You can add up to 20 tags per action, and up to 50 tags for a single DC Gateway.<br><br>* The keys of multiple tags for the same DC Gateway must be unique. Each key can contain only one value.<br><br>* The Key and the Value are case\-sensitive. For example, the Key=tag and the Key=Tag are two different Keys. For more information, see [Tag management](https://docs.byteplus.com/en/docs/directconnect/Tag-management). |key:test |
   |Agreement |Follow the console guidance to review and accept the legal terms. |Check |
   

4. Click **Buy now** to complete the creation, and then click **Go to console** to return to the Direct Connect Gateway console.

5. You can see the new DC Gateway in the list.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next


* [Create a DC Virtual Interface](https://docs.byteplus.com/en/docs/directconnect/Creating-a-virtual-interface-1): After creating a DC Connection and a DC Gateway, you also need to create a DC Virtual Interface to attach the connection and the gateway.

* [Authorize a cross-account CEN](https://docs.byteplus.com/en/docs/directconnect/Cross-account-authorization): If the DC Gateway does not belong to the account where your target Cloud Enterprise Network (CEN) resides, you need to first authorize the CEN's account to allow the CEN using the DC Gateway under your account.


<span id="a8MSXZzu"></span>
## Related actions


* [Enable IPv6 for a DC Gateway](https://docs.byteplus.com/en/docs/directconnect/turn-on-dc-gateway-ipv6): You can enable the IPv6 feature after creating a DC Gateway. A DC Virtual Interface can use the IPv6 feature only after its associated DC Gateway has IPv6 enabled.

* [Load a network instance](https://docs.byteplus.com/en/docs/cen/Network-instances-01): Attach the DC Gateway and other network instances to be interconnected to the same **CEN** instance, enabling network interconnection between the DC Gateway and the VPC.

* [Create a DC Gateway attachment](https://docs.byteplus.com/en/docs/transitrouter/Attachments-dc): Use a DC Gateway to create an attachment that attaches the DC Gateway to the **Transit Router (TR)**  instance, enabling network interconnection between the DC Gateway and the TR.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[CreateDirectConnectGateway](https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectGateway): Create a DC Gateway.
