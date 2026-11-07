---
title: "Deleting a custom route table"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Route-tables-09"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

You can delete custom route tables that are no longer needed, but cannot delete system route tables.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Deleting a route table may affect service running. Proceed with caution.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Ensure no association forwarding is created in the route table. If created, first [delete the associated forwarding rule](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-07#.5Yig6Zmk5YWz6IGU6L2s5Y-R).

* Ensure no route learning is created in the route table. If created, first [delete the route learning rule](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-06#.5Yig6Zmk6Lev55Sx5a2m5Lmg).

* Ensure no static route is created in the route table. If created, first [delete the static route](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-05#.5Yig6Zmk6Z2Z5oCB6Lev55Sx).

* Ensure the route table is not referenced by any forwarding policy entries. If referenced, first [delete the forwarding policy entry](https://docs.byteplus.com/en/docs/transitrouter/Managing-forwarding-policy-entries#.5Yig6Zmk6L2s5Y-R562W55Wl5p2h55uu).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the Transit Router  console](https://console.byteplus.com/tr/transitRouter).

2. In the top menu bar, select your target region.

3. Click the name of the target TR instance.

4. In the zone below **Basic information**, select the **Route Table** tab.

5. Click **Delete** to the right of the target route table and confirm the resource information.

6. Click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[DeleteTransitRouterRouteTable](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterRouteTable): Delete a specified custom route table.
