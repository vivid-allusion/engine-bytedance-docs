---
title: "Managing association forwarding"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Route-tables-07"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

The association forwarding feature specifies the TR route table for the Transit Router (TR) to forward traffic from a network instance. To change path selection of the TR, you can create or modify an association forwarding rule for a network instance attachment.

<span id=".5Yib5bu65YWz6IGU6L2s5Y-R"></span>
## Create an association forwarding rule

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each network instance attachment can be associated with only one TR route table for traffic forwarding.</div>



1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the zone below **Basic information**, select the **Route Table** tab.

4. Select the target route table and click the **Association forwarding** tab.

5. Click **Create association forwarding**, and select the target network instance attachment according to the attachment type.

6. Click **Create** to complete the action.


<span id=".5Yig6Zmk5YWz6IGU6L2s5Y-R"></span>
## Delete an association forwarding rule

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Once an association forwarding rule is deleted, the network instance cannot communicate with other network instances via the TR. Proceed with caution.</div>


* <div data-tips="true" data-tips-type="warning">After you delete an association forwarding rule, the system automatically withdraws all routes that were synchronized from the TR to any network instance that has auto publishing enabled.</div>


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the zone below **Basic information**, select the **Route Table** tab.

4. Select the target route table and click the **Association forwarding** tab.

5. Click **Delete** to the right of the target association forwarding rule, and confirm resource information.

6. Click **Delete** to complete the action.


<span id=".5L-u5pS55YWz6IGU6L2s5Y-R6Lev55Sx6KGo"></span>
## Modify an associated forwarding route table

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For attachments with auto publishing enabled, modifying an association forwarding route table may change the path selection for the network instance, causing seconds of service disruption. We recommend scheduling this action during off\-peak hours.</div>



1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the area under **Basic information**, select the ** Intra\-region attachments** tab.

4. Click the name of the target attachment.

5. Click **Modify** next to **Associated forwarding route table**, and reselect your target associated route table as needed.

6. Click **Save** to complete the modification.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation


* [AssociateTransitRouterAttachmentToRouteTable](https://docs.byteplus.com/en/docs/transitrouter/AssociateTransitRouterAttachmentToRouteTable): Associate a specified route table with a network instance attachment.

* [DescribeTransitRouterRouteTableAssociations](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteTableAssociations): Query network instance attachments associated with a specified route table.

* [DissociateTransitRouterAttachmentFromRouteTable](https://docs.byteplus.com/en/docs/transitrouter/DissociateTransitRouterAttachmentFromRouteTable): Disassociate a specified route table from a network instance attachment.

* [ModifyTransitRouterRouteTableAssociationAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterRouteTableAssociationAttributes): Modify a route table associated with a specified network instance attachment.
