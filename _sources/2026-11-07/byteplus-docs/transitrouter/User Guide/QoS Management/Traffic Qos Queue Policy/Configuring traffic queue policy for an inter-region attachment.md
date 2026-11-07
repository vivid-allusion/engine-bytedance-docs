---
title: "Configuring traffic queue policy for an inter-region attachment"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Configuring-a-qos-queue-policy-for-inter-region-attachment"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

The traffic queue policy applies to inter\-region attachments and allows forwarding different business traffic with varying bandwidths. If bandwidth allocation to each business is unnecessary, turn off the traffic queue policy.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the modified bandwidth is insufficient for actual business requirements, normal service forwarding may be impacted.​</div>


<span id=".5ZCv55So5rWB6Zif5YiX"></span>
## Enable traffic queue policy


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter). 

2. Click the name of the target TR instance.

3. In the section below **Basic information**, select the **Inter\-region attachment** tab.

4. Click  **··· \> Configure traffic queue policy** to the right of the target inter\-region attachment, turn on the traffic queue policy switch, and select a traffic queue policy.

5. Click **OK** to complete the action.


<span id=".5YWz6Zet5rWB6Zif5YiX"></span>
## Disable traffic queue policy


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter). 

2. Click the name of the target TR instance.

3. In the section below **Basic information**, select the **Inter\-region attachment** tab.

4. Click  **··· \> Configure traffic queue policy** to the right of the target inter\-region attachment, turn off the traffic queue policy switch.

5. Click **OK** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation


* [AssociateTransitRouterTrafficQosQueuePolicyToAttachment](https://docs.byteplus.com/en/docs/transitrouter/AssociateTransitRouterTrafficQosQueuePolicyToAttachment): Enable traffic queue policy for a TR attachment.

* [DissociateTransitRouterTrafficQosQueuePolicyFromAttachment](https://docs.byteplus.com/en/docs/transitrouter/DissociateTransitRouterTrafficQosQueuePolicyFromAttachment): Disable a traffic queue policy of a TR attachment.

* [ModifyTransitRouterTrafficQosQueuePolicyAssociation](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterTrafficQosQueuePolicyAssociation): Modify a traffic queue policy associated with a TR attachment.
