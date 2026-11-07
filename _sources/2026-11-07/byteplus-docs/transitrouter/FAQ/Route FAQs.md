---
title: "Route FAQs"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Routing-faq"
---

<span id=".572R57uc5a6e5L6L6L-e5o6l5bey5byA5ZCv6Lev55Sx5ZCM5q2l77yM5Li65LuA5LmI5rKh5pyJ6Lev55Sx5ZCM5q2l5YiwVlBD6Lev55Sx6KGo5Lit77yf"></span>
## Why does the route not synchronize to the VPC route table when the network instance attachment has enable Auto Publish Route?

Possible causes include:


* There are no routes in the TR route table that require synchronization.

   The system automatically synchronizes TR routes to the VPC route table only if the following conditions are met:

   * The network instance attachment has been configured with associated forwarding.

   * The associated forwarding TR route table contains route entries.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If only some of the above conditions are met, routes will not be synchronized. Check and complete the missing configurations. The system will trigger route synchronization after all conditions are met.   </div>
   

* Routes to be synchronized conflict with existing routes in the VPC.

   * The destination CIDR blocks of both are exactly the same.

   * The TR route overlaps with an existing subnet route in the VPC, with a longer mask.

   * The route published by the TR to the VPC direction is denied by the outbound route policy attached to the TR route table.

* The number of route entries in the VPC route table exceeds the quota limit.

   * If the VPC route entries exceed the quota before enabling Auto Publish Route, no routes will be synchronized to the VPC route table after enabling it.

   * If the VPC route entries do not exceed the quota limit before enabling Auto publish route, but adding new routes after enabling causes the quota to be exceeded, some routes will synchronize successfully while those exceeding the quota will fail.


<span id=".6Lev55Sx562W55Wl5LiO6L2s5Y-R562W55Wl5pyJ5LuA5LmI5Yy65Yir77yf"></span>
## What is the difference between route policy and forwarding policy?

Route policy and forwarding policy work independently. Their differences are as follows:


* Route policy applies during the route propagation stage and affects the propagation scope and attributes. The route propagation scope includes routes in the TR route table and network instance route tables.

   * Configure inbound policies to allow or deny network instance routes from being published to the TR route.

   * Configure outbound policies to allow or deny TR routes from being published to VPC or Direct Connect Gateway routes.

* The forwarding policy applies during traffic forwarding, affecting the forwarding path of access requests.

   For example, configuring forwarding policies allows two subnets in a VPC to forward traffic based on different TR route tables.


<span id=".VFLku47kuJPnur_lkoxWUE7lrabkuaDliLDmnaXoh6rlkIzkuIDkupHkuItJREPnmoTot6_nlLHvvIzkuLrku4DkuYhWUE7ot6_nlLHkvJjlhYjnlJ_mlYjvvJ_lpoLkvZXkvJjlhYjnlJ_mlYjkuJPnur_ot6_nlLHvvJ8="></span>
## TR learns routes from both Direct Connect and VPN under the same on\-premises IDC; why do VPN routes take priority? How to prioritize Direct Connect routes?

Routes learned by TR from Direct Connect and VPN include static and BGP routes. Static routes have no AsPath attribute. The AsPath of BGP routes is as follows:


* BGP routes from IDC add the ASN of the Direct Connect Gateway, such as `137718`, to the AsPath when passing through Direct Connect.

* BGP routes from IDC keep their AsPath unchanged when passing through VPN.


Therefore, when the TR learns BGP routes from the direct connect, the AsPath of direct connect routes is longer than VPN routes, so VPN routes take precedence.

If direct connect routes should take precedence, please [create a route policy](https://docs.byteplus.com/en/docs/transitrouter/Creating-a-routing-policy) to adjust the AsPath so that the direct connect route's AsPath is shorter than or equal to the VPN route's.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The TR feature to learn VPN routes is in beta. If you need to use it, contact your customer service support.</div>


<span id=".572R57uc5a6e5L6L6L-e5o6l5bey5byA5ZCv6Lev55Sx5a2m5Lmg77yM5Li65LuA5LmIVFLot6_nlLHooajmsqHmnInku45WUE7lrabkuaDliLDku7vkvZXot6_nlLHvvJ8="></span>
## How does a TR prevent routing loops?

The TR prevents routing loops through the following mechanisms:

**AS Path** ** setting**:​ Each TR must be configured with an ASN, and different TRs should use different ASNs. The AS Path mechanism identifies potential loops and restricts them accordingly.


   * When advertising routes, the TR appends its own ASN to the AS Path.

   * When receiving routes, if the TR detects that the AS Path contains its own ASN or the AS Path length exceeds 30, the route is discarded.

* **Route policy control**:​ Route policies limit the route advertisement scope. Routes are published only to target network instances that require connectivity.​ This reduces unnecessary route propagation.

* **TTL decrement**:​ TR supports Time To Live (TTL) decrement by default. When the TTL of a packet decrements to 0, the TR automatically discards the packet. This prevents infinite traffic amplification caused by loops.


<span id="hKaInNVJ"></span>
## Why doesn't a TR route table learn any routes from a VPN attachment even though route learning is enabled for the attachment?

The VPN route propagation mode is Static Route. If you want to learn VPN routes, change the VPN route propagation mode to Dynamic routing.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Dynamic route propagation for VPN Connect is in the beta stage. To request a trial, please contact your account manager.</div>
