---
title: "Deleting an inter-region attachment"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Inter-region-peering-attachments-04"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Instructions


* When deleting a same\-account inter\-region attachment with associated resources, you can delete them in batch during the deletion of the attachment or manually delete associated resources based on [Delete an association forwarding rule](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-07#.5Yig6Zmk5YWz6IGU6L2s5Y-R), [Delete a route learning rule](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-06#.5Yig6Zmk6Lev55Sx5a2m5Lmg), [Delete a static route](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-05#.5Yig6Zmk6Z2Z5oCB6Lev55Sx), and [Delete a route entry](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry#.5Yig6Zmk6Lev55Sx5p2h55uu).

* When deleting a cross\-account inter\-region attachment, contact the peer account to delete any associated resources first.

* Deleting an inter\-region attachment automatically disassociates its traffic marking and traffic queue policies.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the section below **Basic information**, select the **Inter\-region attachment** tab.

4. Click **Delete** to the right of the target attachment, and confirm resource information.

5. Check **I have confirmed that the deletion of the above ** ***XX*** ** items will not affect the stability of services and can be proceeded.** 

6. Click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[DeleteTransitRouterPeerAttachment](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterPeerAttachment): Delete a specified inter\-region attachment.
