---
title: "Deleting a route policy"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Deleting-a-routing-policy"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Instructions


* A route policy cannot be deleted while it is associated with a Transit Router (TR) route table. To delete, first [disassociate the TR route table](https://docs.byteplus.com/en/docs/transitrouter/Binding-Unbinding-Modifying-routing-policy-for-TR-route-table).

* When you delete a route policy, all policy entries within it are automatically deleted.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the section below **Basic information**, select the **Route policy** tab.

4. Click **Delete** to the right of the target route policy, and confirm resource information.

5. Check **I have confirmed that the deletion of the above XX items will not affect the stability of services and can be proceed.** 

6. Click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[DeleteTransitRouterRoutePolicyTable](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterRoutePolicyTable): Delete a specified route policy.
