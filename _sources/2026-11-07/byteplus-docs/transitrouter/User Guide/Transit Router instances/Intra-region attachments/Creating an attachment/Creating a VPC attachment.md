---
title: "Creating a VPC attachment"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Attachments-vpc"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

Establish a connection between a Virtual Private Cloud (VPC) and a Transit Router (TR), enabling intercommunication between VPCs' and TRs' private networks.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Ensure you have created a TR instance. For procedure, see [Creating a Transit Router instance](https://docs.byteplus.com/docs/transitrouter/TransitRouter-instances-01).

* Ensure your VPC to be connected contains at least one subnet and one available IP address in the required availability zone.

* Before creating a cross\-account intra\-region network instance attachment, ensure you have [accepted a sharing invitation](https://docs.byteplus.com/docs/transitrouter/Cross-account-Transit-Router-sharing#kFuWwFWD). The target TR instance is not suspended due to overdue payment.

* If the VPC to be connected requires IPv6 communication via the TR, ensure that IPv6 is enabled on the VPC instance and that the IPv6 feature is activated for the TR.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The TR IPv6 feature is in the beta stage. If you need a trial, please contact your account manager.   </div>
   

<span id=".5pON5L2c6K-05piO"></span>
## Instructions


* By default, a single TR instance supports a maximum of 200 VPC attachments. If this quota is insufficient, you can request an increase through the [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=Auto_Scaling), up to an absolute upper limit of 1,000 attachments.

* You can attach the same VPC to five TR instances concurrently.

* After the TR forwards traffic to a VPC, the VPC's routing subsystem performs a second route lookup. This lookup queries the route table of the specific subnet where the attachment point resides. The subsystem then applies the Longest Prefix Match (LPM) rule to select the most specific route from that subnet's route table.


<span id="xR6e61YE"></span>
## Precautions


* Enabling path consistent mode may change the availability zone attachment point selected when forwarding traffic to the VPC, which could affect the traffic. Proceed with caution.

* Enabling route learning at the VPC CIDR granularity will forward traffic belonging to the VPC CIDR block but not to any subnet within that VPC to the TR, causing changes in traffic forwarding paths. Carefully assess and decide.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the section below **Basic information**, select the **Intra\-region attachment** tab.

4. Click **Create attachment**, and complete the basic configuration based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |**Basic information** |||
   |TR |Defaults to the selected TR instance, requiring no manual configuration. |tr01 |
   |Region |Defaults to the same region as the TR instance. No manual configuration required. |China (Guangzhou) |
   |Fee payer |Default to the same fee payer as the TR instance. No manual configuration required. This parameter is displayed only when the TR instance is shared. |Network instance account |
   |Name |The name for the network instance attachment to be created. |attach\-vpc01 |
   |**Network instance** |||
   |Network instance type |Select the type of network instance. This example only demonstrates configuration parameters for VPC attachments. |VPC |
   |VPC |Select the VPC instance to be attached based on the project. |vpc01 |
   |IPv6 |Specify whether to enable IPv6. If you need to achieve IPv6 communication between VPCs through a TR, enable IPv6. |Unchecked |
   |**Attachment point configuration** |||
   |Availability Zone and Subnet |Select the availability zone for the attachment point and specify the subnet. The subnet is used to assign a private IP address to the attachment point (i.e., the network interface).<br><br>If traffic originating from VPC Availability Zone *X* cannot be matched to a corresponding zone upon arrival at the TR, it must be forwarded via the default availability zone.<br><br>For example, if the attachment points of a VPC attachment are configured in Availability Zone A (designated as default) and Availability Zone B, traffic from VPC Availability Zone A is forwarded via TR Availability Zone A; traffic from VPC Availability Zone B is forwarded via TR Availability Zone B; and traffic from VPC Availability Zone C is forwarded via the default availability zone (i.e., Availability Zone A).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">We recommend configuring attachment points in multiple availability zones for higher availability.</div><br><br><br>* <div data-tips="true" data-tips-type="default">After enabling IPv6, all selected subnets must have IPv6 CIDR blocks.</div><br> |Availability Zone A, subnet01 |
   |Path consistent mode |Specify whether to enable path consistent mode.<br><br>After enabling, TR will use the same availability zone attachment point to forward both the request and response traffic when routing to this VPC attachment. For example, traffic from vpc01 to vpc02 is forwarded by the transit router to vpc03 for security protection. The specific traffic path is shown in the figure below.<br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4fb9f31a491e6d02ca36d702f0e89728.png) </span><br><br> |Disabled |
   

5. Complete the route configuration and advanced options based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |**Route configuration** |||
   |Association forwarding |Specify whether to enable association forwarding for this attachment.<br><br><br>* **Enable**: Select the TR route table. This means traffic from the previously selected VPC will be forwarded according to routes in this TR route table.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Shared User does not need to select a TR route table when creating a cross\-account attachment with association forwarding enabled. The default is the target TR instance’s system route table. To modify this, contact Owner.   </div><br>   <br><br>* **Disable**: The TR cannot forward traffic from this VPC. After the attachment creation is completed, configure association forwarding for it based on [Create an associated forwarding rule](https://docs.byteplus.com/docs/transitrouter/Route-tables-07). |Enable |
   |Route learning |Specify whether to enable route learning for this attachment.<br><br><br>* **Enable**: Select the TR route table. The route table will automatically learn subnet routes of the VPC by default and generate corresponding routes. The destination CIDR block of this route is the subnet CIDR block, and its next hop is this attachment.<br><br>   * In scenarios where VPC contains a large number of subnets, to simplify route management and maintenance, you can configure the **learning granularity** to **VPC CIDR** so that the TR automatically learns routes of the VPC CIDR block and generates corresponding routes. The destination CIDR block of this route is the VPC CIDR block (including the primary CIDR block and the IPv4/IPv6 secondary CIDR block), and its next hop is this attachment.<br><br>   * Once the learning granularity is configured, it cannot be modified. You can only delete the current route learning configuration and set up a new one. For traffic forwarding limits when the learning granularity is set to VPC CIDR, see [Precautions](https://docs.byteplus.com/en/docs/transitrouter/Attachments-vpc?TagIDs=2,105,104,95,94&lang=zh#xR6e61YE).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Shared User does not need to select a TR route table when creating a cross\-account attachment with route learning enabled. The default is the target TR instance’s system route table. To modify this, contact the Owner.</div><br><br><br><br>* **Disable**: The TR route table will not automatically learn routes of this VPC, and the TR will be unable to forward received requests to it. After the attachment creation is completed, configure route learning for it based on [Create a route learning rule](https://docs.byteplus.com/docs/transitrouter/Route-tables-06). |Enable |
   |Auto Publish Route |Specify whether to enable route publishing for this attachment.<br><br><br>* **Enable**: The system will automatically propagate routes from the TR route table associated with this attachment to all route tables of the selected VPC. These synchronized routes are marked as system routes.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If association forwarding is not enabled, enabling route publishing will not add any routes to the VPC route table. Route publishing is only triggered when you enable association forwarding.   </div><br>   <br><br>* **Disable**: The system will not automatically propagate TR routes to the VPC route table. You need to manually add custom routes to the VPC route table. For procedure, see [Add a route](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry). |Enabled |
   |**Advanced options** |||
   |Tag |A tag consists of a key\-value pair and is used for categorizing and searching resources. [Learn more](https://docs.byteplus.com/docs/transitrouter/Tags)<br><br>Click **Add tag**, type the tag key and tag value to add tags for the attachment. |* Tag key: attach\-k1<br><br>* Tag value: attach\-v1 |
   

6. Click **Buy now** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[CreateTransitRouterVpcAttachment](https://docs.byteplus.com/docs/transitrouter/CreateTransitRouterVpcAttachment): Create a VPC attachment.
