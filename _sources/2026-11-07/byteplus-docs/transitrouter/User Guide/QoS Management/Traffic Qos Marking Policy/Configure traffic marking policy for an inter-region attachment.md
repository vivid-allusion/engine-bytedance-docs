---
title: "Configure traffic marking policy for an inter-region attachment"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Configuring-a-qos-marking-policy-for-inter-region-attachment"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

The traffic marking policy applies to inter\-region peering attachments and can classify outbound data transfer. Turn off the traffic marking policy when data transfer classification is no longer needed.

<span id=".5pON5L2c6K-05piO"></span>
## Instructions

Enabling or disabling the traffic marking policy affects data transfer marking. If the bandwidth of the scheduling queue matched by the data transfer marking is less than the actual business demand, it will affect active forwarding.

<span id=".5ZCv55So5rWB5qCH6K6w"></span>
## Enable traffic marking policy


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the section below **Basic information**, select the **Inter\-region attachment** tab.

4. Click  **··· \> Configure traffic marking policy** to the right of the target inter\-region attachment, turn on the traffic marking policy switch, and select a traffic marking policy.

5. Click **OK** to complete the action.


<span id=".5YWz6Zet5rWB5qCH6K6w"></span>
## Disable traffic marking policy


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the section below **Basic information**, select the **Inter\-region attachment** tab.

4. Click  **··· \> Configure traffic marking policy** to the right of the target inter\-region attachment and turn off the traffic marking policy switch.

5. Click **OK** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation


* [AssociateTransitRouterTrafficQosMarkingPolicyToAttachment](https://docs.byteplus.com/en/docs/transitrouter/AssociateTransitRouterTrafficQosMarkingPolicyToAttachment): Enable traffic marking policy for a TR attachment.

* [DissociateTransitRouterTrafficQosMarkingPolicyFromAttachment](https://docs.byteplus.com/en/docs/transitrouter/DissociateTransitRouterTrafficQosMarkingPolicyFromAttachment): Disable traffic marking policy for a TR attachment.

* [ModifyTransitRouterTrafficQosMarkingPolicyAssociation](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterTrafficQosMarkingPolicyAssociation): Modify a traffic marking policy associated with a TR attachment.
