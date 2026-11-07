---
title: "Configuring forwarding policy for a network instance attachment"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Enabling-Disabling-Modifying-forwarding-policy"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

A created forwarding policy must be associated with a network instance attachment for use.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Service traffic forwarding may be affected by enabling, disabling, or modifying a forwarding policy. Proceed with caution.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the area under **Basic information**, select the ** Intra\-region attachments** tab.

4. Click **Configure forwarding policy** to the right of the target resource, and then enable, disable, or modify a forwarding policy for the specified resource as needed.

   * **Enable a forwarding policy**: Set the feature status to **Enable** and select your target forwarding policy.

   * **Disable a forwarding policy**: Set the feature status to **Disabled**.

   * **Modify a forwarding policy**: Keep setting the feature status to **Enable** and reselect a forwarding policy to be associated.

5. Click **Save** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation


* [ModifyTransitRouterForwardPolicyTableAssociation](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterForwardPolicyTableAssociation): Modify a network instance attachment that the specified forwarding policy is associated with.

* [AssociateTransitRouterForwardPolicyTableToAttachment](https://docs.byteplus.com/en/docs/transitrouter/AssociateTransitRouterForwardPolicyTableToAttachment): Associate a specified forwarding policy with a specified network instance attachment.

* [DissociateTransitRouterForwardPolicyTableFromAttachment](https://docs.byteplus.com/en/docs/transitrouter/DissociateTransitRouterForwardPolicyTableFromAttachment): Disassociate a specified forwarding policy from a specified network instance attachment.
