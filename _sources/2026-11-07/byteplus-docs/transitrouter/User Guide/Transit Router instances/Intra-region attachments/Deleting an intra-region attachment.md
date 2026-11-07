---
title: "Deleting an intra-region attachment"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Attachments-03"
---

<span id=".5pON5L2c6K-05piO"></span>
## Instructions


* Deleting a network instance attachment will remove the association between the network instance and the Transit Router (TR) instance, causing communication failure between network instances. Proceed with caution.

* Deleting the same account attachments allows batch deletion of associated resources with one click. Before deleting a cross\-account attachment, refer to [Deleting associated forwarding](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-07), [Deleting route learning](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-06), [Deleting static routes](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-05), and [Deleting VPC custom route entries](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry) to manually remove associated resources.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the area under **Basic information**, select the ** Intra\-region attachments** tab.

4. Click **Delete** to the right of the target attachment, and confirm resource information.

5. Check **I have confirmed that the deletion of the above ** ***XX*** ** items will not affect the stability of services and can be proceeded**.

   Here, *XX* represents the total number of attachments and other associated resources to be deleted.

6. Click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [DeleteTransitRouterVpcAttachment](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterVpcAttachment): Delete a specified VPC attachment.

* [DeleteTransitRouterVpnAttachment](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterVpnAttachment): Delete a specified VPN attachment.

* [DeleteTransitRouterDirectConnectGatewayAttachment](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterDirectConnectGatewayAttachment): Delete a specified DC Gateway attachment.
