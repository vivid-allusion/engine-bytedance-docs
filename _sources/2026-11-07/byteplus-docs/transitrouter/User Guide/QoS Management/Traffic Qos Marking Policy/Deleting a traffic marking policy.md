---
title: "Deleting a traffic marking policy"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Deleting-a-qos-marking-policy"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Instructions

Traffic marking may be impacted by deleting a traffic marking policy. If the bandwidth allocated to the scheduling queue matched by the traffic marking is insufficient for actual business requirements, normal service forwarding may be impacted.​

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The traffic marking policy is not used by an inter\-region attachment. If in use, [disable the traffic marking policy for the attachment](https://docs.byteplus.com/en/docs/transitrouter/Configuring-a-qos-marking-policy-for-inter-region-attachment#.5YWz6Zet5rWB5qCH6K6w).

* No marking entries exist in the traffic marking policy. If present, delete the marking entries first.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. Select the **Traffic marking policy** tab under **Basic information**.

4. Click **Delete** to the right of the target traffic marking policy, then confirm the resource information.

5. Click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[DeleteTransitRouterTrafficQosMarkingPolicy](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterTrafficQosMarkingPolicy): Delete a traffic marking policy.
