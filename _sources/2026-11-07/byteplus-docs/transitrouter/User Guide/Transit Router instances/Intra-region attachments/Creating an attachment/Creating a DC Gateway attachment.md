---
title: "Creating a DC Gateway attachment"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Attachments-dc"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

Establish a connection between a Direct Connect (DC) Gateway and a Transit Router (TR), enabling intercommunication between the DC\-connected and TR's networks.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Ensure you have created a TR instance. For procedure, see [Creating a Transit Router instance](https://docs.byteplus.com/docs/transitrouter/TransitRouter-instances-01).

* Ensure you have added a Virtual Interface and configured on\-premises routing for the target DC Gateway. This DC Gateway is not attached to a Cloud Enterprise Network (CEN) instance or other TR instances.

* Before creating a cross\-account intra\-region attachment, ensure you have [accepted a sharing invitation](https://docs.byteplus.com/docs/transitrouter/Cross-account-Transit-Router-sharing#kFuWwFWD). The target TR instance is not suspended due to overdue payment.


<span id=".5pON5L2c6K-05piO"></span>
## Instructions

By default, a single TR instance supports a maximum of 10 DC Gateway attachments. If this quota is insufficient, you can request an increase through the [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=Auto_Scaling), up to an absolute upper limit of 16 attachments.

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
   |Fee payer |Defaults to the same fee payer as the TR instance. No manual configuration required. This parameter is displayed only when the TR instance is shared. |Network instance account |
   |Name |The name for the network instance attachment to be created. |attach01 |
   |**Instance** |||
   |Attachment type |Select the type of network instance. This example only demonstrates configuration parameters for DC Gateway attachments. |DC Gateway |
   |DC Gateway |Select the DC Gateway instance to be connected based on the project.<br><br>To ensure the mutual route learning between the TR and DC Gateway, we recommend avoiding the use of the same ASN for both the DC Gateway and the TR instance. |dcgw01 |
   

5. Complete the route configuration and advanced options based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |**Route configuration** |||
   |Association forwarding |Specify whether to enable association forwarding for this attachment.<br><br><br>* Enable: Select the TR route table. This means traffic from the previously selected network instance will be forwarded according to routes in this TR route table.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When a Recipient creates a cross\-account attachment and enables association forwarding, the only option is the target TR instance’s system route table by default. To modify this, contact the Owner.   </div><br>   <br><br>* Disable: After the attachment creation is completed, you also need to specify the TR route table that forwards traffic for this attachment by seeing [Create an association forwarding rule](https://docs.byteplus.com/docs/transitrouter/Route-tables-07#.5Yib5bu65YWz6IGU6L2s5Y-R). Otherwise, the TR will be unable to forward traffic from the attachment. |Enable |
   |Route learning |Specify whether to enable route learning for this attachment.<br><br><br>* Enable: Select the TR route table. This means this TR route table will automatically learn routes from the selected DC Gateway, and generate routes with the destination CIDR block set as the CIDR block of the on\-premises data center connected via the DC Gateway and the next hop set as this attachment.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When a Recipient creates a cross\-account attachment and enables route learning, the only option is the target TR instance’s system route table by default. To modify this, contact the Owner.   </div><br>   <br><br>* Disable: The TR route table will not automatically learn routes of this DC Gateway. After the attachment creation is completed, configure route learning for it based on [Create a route learning rule](https://docs.byteplus.com/docs/transitrouter/Route-tables-06#.5Yib5bu66Lev55Sx5a2m5Lmg). Otherwise, the TR will be unable to forward received requests to this DC Gateway. |Enable |
   |**Advanced options** |||
   |Tag |A tag consists of a key\-value pair and is used for categorizing and searching resources. [Learn more](https://docs.byteplus.com/docs/transitrouter/Tags)<br><br>Click **Add tag**, type the tag key and tag value to add tags for the attachment. |* Tag key: attach\-k1<br><br>* Tag value: attach\-v1 |
   

6. Click **Buy now** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[CreateTransitRouterDirectConnectGatewayAttachment](https://docs.byteplus.com/docs/transitrouter/CreateTransitRouterDirectConnectGatewayAttachment): Create a DC Gateway attachment.
