---
title: "Configuring route policy for a TR route table"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Binding-Unbinding-Modifying-routing-policy-for-TR-route-table"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

After being associated with a TR route table, a route policy filters the routes that the table learns from network instances and publishes to other network instances.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Service traffic forwarding may be affected by associating, disassociating, or modifying a route policy for a TR route table. Proceed with caution.</div>


<span id=".VFLot6_nlLHooajnu5Hlrprot6_nlLHnrZbnlaU="></span>
## Associate a route policy with a TR route table

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each TR route table supports associating a maximum of one inbound and one outbound route policy at the same time.</div>



1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the zone below **Basic information**, select the **Route Table** tab.

4. Click the target TR route table and select the **Associated route policy** tab.

5. Click **Associate route policy** and select your target route policy.

6. Click **Save** to complete the action.


<span id=".VFLot6_nlLHooajop6Pnu5Hot6_nlLHnrZbnlaU="></span>
## Disassociate a route policy from a TR route table


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the zone below **Basic information**, select the **Route Table** tab.

4. Click the target TR route table and select the **Associated route policy** tab.

5. Click **Disassociate** and confirm the resource information.

6. Click **Save** to complete the action.


<span id=".VFLot6_nlLHooajkv67mlLnot6_nlLHnrZbnlaU="></span>
## Modify a route policy for a TR route table

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Service traffic forwarding may be affected by modifying a route policy for a TR route table. Proceed with caution.</div>



1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the zone below **Basic information**, select the **Route Table** tab.

4. Click the target TR route table and select the **Associated route policy** tab.

5. Click **Modify** to the right of the target policy and reselect a route policy.

6. Click **Save** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation


* [ModifyTransitRouterRoutePolicyAssociation](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterRoutePolicyAssociation): Modify a TR route table associated with a route policy.

* [AssociateTransitRouterRoutePolicyToRouteTable](https://docs.byteplus.com/en/docs/transitrouter/AssociateTransitRouterRoutePolicyToRouteTable): Associate a specified route policy with a designated TR route table.

* [DissociateTransitRouterRoutePolicyTableFromRouteTable](https://docs.byteplus.com/en/docs/transitrouter/DissociateTransitRouterRoutePolicyFromRouteTable): Disassociate a route policy from a TR route table.
