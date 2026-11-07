---
title: "Editing attachment point for a VPC attachment"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Attachments-02"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

After completing the creation of a VPC attachment, you can edit its attachment point based on your actual needs. For more about attachment points, see [Components](https://docs.byteplus.com/en/docs/transitrouter/Product-Overview-01#.57uE5oiQ6YOo5YiG).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Modification of attachment points is only available for VPC attachments created by this account. To modify the attachment point of cross\-account attachments, use the account of the Recipient to perform.</div>


<span id=".5pON5L2c6K-05piO"></span>
## Instructions


* When you modify the availability zone and subnet, the system automatically creates or deletes a network interface. This interface functions as the ingress point for connectivity between the Transit Router (TR) and the Virtual Private Cloud (VPC).

* You must select at least one availability zone to create an attachment point for the same VPC. Only one subnet can be selected per availability zone.

* After the attachment creation is completed, all subnets in all availability zones within the VPC's region can communicate with the TR.

* When enabling IPv6 for a VPC attachment, all selected subnets must have IPv6 CIDR blocks.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The IPv6 feature of TR is in the beta stage. If you need a trial, please contact your account manager.   </div>
   

<span id="R8GMddDO"></span>
## Precautions


* When modifying the subnet of an availability zone where an attachment point is established, the system will delete the network interface from the original subnet and recreate it in the new subnet. This may cause traffic interruption. Proceed with caution.

* Enabling path consistent mode may change the availability zone attachment point selected when forwarding traffic to the VPC, which could affect the traffic. Proceed with caution.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the area under **Basic information**, select the ** Intra\-region attachments** tab.

4. Click the name of the target attachment.

5. Click **Edit attachment point** to reselect the availability zone and subnet for the attachment point.

   
   |Parameter |Description |Example |
   |---|---|---|
   |AZs and Subnets |All availability zones under the target VPC's region are displayed by default. Select as needed.<br><br><br>* **Add an attachment point**: Check the availability zone where you want to establish a new attachment point, and select the subnet for it.<br><br>   The subnet assigns a private IP address to the attachment point.​​ If no available subnets exist under the availability zone for the attachment point to be created, expand the subnet dropdown and click **Create Subnet** below to create a subnet for that zone. For detailed steps, see [Creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If IPv6 is enabled, all selected subnets must have IPv6 CIDR blocks.   </div><br>   <br><br>* **Delete an attachment point**: Uncheck the availability zone where creating the attachment point is no longer needed.<br><br>   Each attachment must have at least one attachment point. Therefore, you cannot uncheck the last remaining attachment point on an attachment.<br><br>* **Modify a subnet**: Reselect the subnet for the checked availability zone.<br><br>* **Modify Default AZ**: Check the target availability zone and then click **Set as Default** to configure it as the default availability zone. |Availability Zone A, Subnet A |
   |IPv6 |Specify whether to enable IPv6. |Disable |
   |Path consistent mode |Describe whether to enable path consistency mode.<br><br>After enabling, TR will use the same availability zone attachment point to forward both the request and response traffic when routing to this VPC attachment. |Disable |
   

6. Click **OK** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[ModifyTransitRouterVpcAttachmentAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterVpcAttachmentAttributes): Modify the name, description, and attachment point of a specified VPC attachment, and enable or disable route publishing for the specified VPC attachment.
