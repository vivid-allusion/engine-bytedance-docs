---
title: "Deleting a Transit Router instance"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/TransitRouter-instances-04"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Instructions

The Shared User cannot delete shared Transit Router (TR) instances. To delete them, contact the Owner for assistance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Ensure no TR attachments exist in the TR. If present, first [delete the network instance attachment](https://docs.byteplus.com/en/docs/transitrouter/Attachments-03) or [delete the inter-region attachment](https://docs.byteplus.com/en/docs/transitrouter/Inter-region-peering-attachments-04).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the existing attachment is a cross\-account attachment, contact the Recipient to delete it.   </div>
   

* Ensure no custom route tables exist in the TR. If present, first [delete the custom route table](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-09).

* Ensure no route policies or forwarding policies exist in the TR. If present, first [delete the route policy](https://docs.byteplus.com/en/docs/transitrouter/Deleting-a-routing-policy) or [delete the forwarding policy](https://docs.byteplus.com/en/docs/transitrouter/Deleting-a-forwarding-policy).

* Ensure no traffic marking policies or traffic queue policies exist in the TR. If present, first [delete the traffic marking policy](https://docs.byteplus.com/en/docs/transitrouter/Deleting-a-qos-marking-policy) or [delete the traffic queue policy](https://docs.byteplus.com/en/docs/transitrouter/Deleting-a-qos-queue-policy).

* Ensure the TR is not shared with other accounts. If shared, first [delete the shared unit](https://docs.byteplus.com/en/docs/resourcemanagement/Shared_by_Me_Management#deleting-shared-unit).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the Transit Router  console](https://console.byteplus.com/tr/transitRouter).

2. In the top menu bar, select the target project and region.

3. Click **Delete** to the right of the target TR instance, and confirm resource information.

4. Click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[DeleteTransitRouter](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouter): Delete a specified TR instance.
