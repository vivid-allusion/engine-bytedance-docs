---
title: "Direct Connect Gateway FAQs"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Direct-Connect-gateway"
---

* [After configuring Direct Connect, how do I test connectivity from a ECS instance to the on-premises IDC?](https://docs.byteplus.com/en/docs/53/10470#.5LiT57q_6L-e5o6l6YWN572u5a6M5oiQ5ZCO77yM5aaC5L2V5rWL6K-V5LqR5LiKRUNT5a6e5L6L5Yiw5pys5ZywSURD55qE6L-e6YCa5oCn77yf)

* [Cloud-to-on-premises configuration is complete, but the network is still not connected. How do I troubleshoot?](https://docs.byteplus.com/en/docs/53/10470#.5bey5a6M5oiQ5LqR5LiK5LqR5LiL6YWN572u77yM5L2G572R57uc5LuN54S25LiN6YCa77yM5aaC5L2V5o6S5p-l77yf)

* [What happens if both static and BGP routes to the same IDC exist on a DC Gateway?](https://docs.byteplus.com/en/docs/53/10470#.5LiT57q_572R5YWz5LiK5ZCM5pe25a2Y5Zyo5YmN5b6A5ZCM5LiA5LiqSURD55qE6Z2Z5oCB6Lev55Sx5ZKMQkdQ6Lev55Sx5oCO5LmI5Yqe77yf)

* [What should I do if the number of route entries exceeds the CEN quota after attaching a DC Gateway to CEN?](https://docs.byteplus.com/en/docs/53/10470#.5LiT57q_572R5YWz5Yqg5YWl5LqR5LyB5Lia572R5ZCO77yM6Lev55Sx5p2h55uu6LaF5Ye65LqR5LyB5Lia572R6YWN6aKd77yM5aaC5L2V5aSE55CG77yf)

* [Does the DC Gateway accept the 0.0.0.0/0 route?](https://docs.byteplus.com/en/docs/53/10470#.5LiT57q_572R5YWz5piv5ZCm5o6l5pS2MC4wLjAuMC8w6Lev55Sx77yf)

* [What is the business impact of disabling IPv6?](https://docs.byteplus.com/en/docs/53/10470#.5YWz6ZetSVB2NuWKn-iDveWvueS4muWKoeacieS7gOS5iOW9seWTje-8nw==)

* [Why can't the on-premises IDC reach the VPC when it advertises public IP routes and accesses the VPC via Direct Connect?](https://docs.byteplus.com/en/docs/53/10470#.5pys5ZywSURD5L2_55So5YWs572R5Zyw5Z2A5Y-R5biD6Lev55Sx77yM6YCa6L-H5LiT57q_6K6_6Zeu5LqR5LiKVlBD77yM5Li65LuA5LmI572R57uc5LiN5LqS6YCa77yf)

* [Why is the added static route for the DC Gateway unavailable when NQA is enabled and the line has no faults?](https://docs.byteplus.com/en/docs/53/10470#.5byA5ZCvTlFB5qOA5rWL5LiU57q_6Lev5peg5pWF6Zqc77yM5Li65LuA5LmI5re75Yqg55qE5LiT57q_572R5YWz6Z2Z5oCB6Lev55Sx5LiN5Y-v55So77yf)

* [Can a DC Gateway be associated with multiple TRs at the same time?](https://docs.byteplus.com/en/docs/53/10470#.5piv5ZCm5pSv5oyB5ZCM5LiA5LiT57q_572R5YWz5ZCM5pe25YWz6IGU5Yiw5aSa5Liq5Lit6L2s6Lev55Sx5Zmo77yf)

* [Can a DC Gateway be associated with both a CEN and a TR at the same time?](https://docs.byteplus.com/en/docs/53/10470#.5piv5ZCm5pSv5oyB5ZCM5LiA5LiT57q_572R5YWz5ZCM5pe25YWz6IGU5LqR5LyB5Lia572R5ZKM5Lit6L2s6Lev55Sx5Zmo77yf)


<span id=".5LiT57q_6L-e5o6l6YWN572u5a6M5oiQ5ZCO77yM5aaC5L2V5rWL6K-V5LqR5LiKRUNT5a6e5L6L5Yiw5pys5ZywSURD55qE6L-e6YCa5oCn77yf"></span>
## After configuring Direct Connect, how do I test connectivity from a ECS instance to the on\-premises IDC?

You can test network connectivity by executing the `ping` command. For procedure, see [Accessing ECS from an on-premises data center via single Direct Connect with static routes](https://docs.byteplus.com/en/docs/directconnect/Best-Practices-4).

<span id=".5bey5a6M5oiQ5LqR5LiK5LqR5LiL6YWN572u77yM5L2G572R57uc5LuN54S25LiN6YCa77yM5aaC5L2V5o6S5p-l77yf"></span>
## Cloud\-to\-on\-premises configuration is complete, but the network is still not connected. How do I troubleshoot?


* **General scenario**

   After completing the configuration in the BytePlus console, the Elastic Compute Service (ECS) instances cannot yet connect to the CIDR block of the data center (IDC). To achieve actual network connectivity between the cloud and on\-premises environments, you must also add the VPC's CIDR block to the routing table of your on\-premises IDC router.

* **Multi\-cloud hybrid deployment scenario**

   The on\-premises IDC and the BytePlus Virtual Private Cloud (VPC) are interconnected via Direct Connect (DC) using BGP routing mode. A third\-party network communicates with the BytePlus VPC by transiting through the on\-premises IDC. If the routes received from the third\-party network have a BGP Community attribute with the "no\-export" value, the BGP routes will not be republished. This will cause network connectivity issues between the third\-party network and BytePlus. Here are two suggested solutions for this situation:

   * Solution 1: Enable the on\-premises data center to receive BGP routes from the third party by adding apply community none using route\-policy.

   * Solution 2: Use Static Routing instead of BGP for the interconnection between the on\-premises IDC and the BytePlus VPC.


<span id=".5LiT57q_572R5YWz5LiK5ZCM5pe25a2Y5Zyo5YmN5b6A5ZCM5LiA5LiqSURD55qE6Z2Z5oCB6Lev55Sx5ZKMQkdQ6Lev55Sx5oCO5LmI5Yqe77yf"></span>
## What happens if both static and BGP routes to the same IDC exist on a DC Gateway?

When both a static route and a BGP route to the same IDC CIDR block exist on a DC Gateway, the BGP route is preferred.

<span id=".5LiT57q_572R5YWz5Yqg5YWl5LqR5LyB5Lia572R5ZCO77yM6Lev55Sx5p2h55uu6LaF5Ye65LqR5LyB5Lia572R6YWN6aKd77yM5aaC5L2V5aSE55CG77yf"></span>
## What should I do if the number of route entries exceeds the CEN quota after attaching a DC Gateway to a CEN?

After a DC Gateway is attached to a Cloud Enterprise Network (CEN), the CEN automatically learns all route entries from the DC Gateway's route table. If the number of learned routes exceeds the CEN route entry quota, the excess DC Gateway route entries will not be learned by the CEN (i.e., they will not appear in the CEN route table).

You can first delete unused or redundant route entries in the CEN to free up quota, and then proceed with either of the following solutions.


* Solution 1: Detach the DC Gateway from the CEN, and then re\-attach it.

* Solution 2: Maintain the attachment between the DC Gateway and the CEN, and reprocess the route entries:

   * Static routes: Delete and then re\-create the static route entries on the DC Gateway side.

   * BGP routes: Re\-publish the BGP routes from the gateway device in your on\-premises IDC.


<span id=".5LiT57q_572R5YWz5piv5ZCm5o6l5pS2MC4wLjAuMC8w6Lev55Sx77yf"></span>
## Does the DC Gateway accept the 0.0.0.0/0 route?

The DC Gateway rejects the default route 0.0.0.0/0 published from the on\-premises IDC side, whether via static or BGP routing.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In addition to 0.0.0.0/0, the following three CIDR blocks are also not supported for publishing from the on\-premises IDC to the DC Gateway. The gateway will directly reject routes for these four segments (including both static and BGP routes).</div>



* <div data-tips="true" data-tips-type="tip">127.0.0.0/8: (127.0.0.0–127.255.255.255)</div>


* <div data-tips="true" data-tips-type="tip">224.0.0.0/4: (224.0.0.0–239.255.255.255)</div>


* <div data-tips="true" data-tips-type="tip">240.0.0.0/4: (240.0.0.0–255.255.255.255)</div>



<span id=".5YWz6ZetSVB2NuWKn-iDveWvueS4muWKoeacieS7gOS5iOW9seWTje-8nw=="></span>
## What is the business impact of disabling IPv6?

The IPv6 feature is currently in beta stage and is only available for trial use by users who have had IPv6 enabled. If you have enabled IPv6, disabling it may affect the IPv6 functionality of your existing instances. It is recommended to delete existing instances before applying to disable IPv6.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If needed, you can contact your account manager to apply for trial access. You can only use the corresponding features and related documentation after your application is approved.</div>


<span id=".5pys5ZywSURD5L2_55So5YWs572R5Zyw5Z2A5Y-R5biD6Lev55Sx77yM6YCa6L-H5LiT57q_6K6_6Zeu5LqR5LiKVlBD77yM5Li65LuA5LmI572R57uc5LiN5LqS6YCa77yf"></span>
## Why can't the on\-premises IDC reach the VPC when it advertises public IP routes and accesses the VPC via Direct Connect?

BytePlus currently does not support the public IP space for private use scenario. Use private IP addresses instead.

<span id=".5byA5ZCvTlFB5qOA5rWL5LiU57q_6Lev5peg5pWF6Zqc77yM5Li65LuA5LmI5re75Yqg55qE5LiT57q_572R5YWz6Z2Z5oCB6Lev55Sx5LiN5Y-v55So77yf"></span>
## Why is the added static route for the DC Gateway unavailable when NQA is enabled and the line has no faults?

In the static route mode with NQA enabled, if the static route on the DC Gateway does not take effect, the reason might be that the Destination CIDR Block of the static route added to the DC Gateway overlaps with the CIDR block of the virtual interface.

You can resolve this by configuring a CIDR block whose subnet mask differs from that of the "DC Virtual Interface Interconnection Address Segment".

<span id=".5piv5ZCm5pSv5oyB5ZCM5LiA5LiT57q_572R5YWz5ZCM5pe25YWz6IGU5Yiw5aSa5Liq5Lit6L2s6Lev55Sx5Zmo77yf"></span>
## Can a DC Gateway be associated with multiple TRs at the same time?

No. After a DC Gateway is attached to a Transit Router (TR), it dynamically learns routes from the TR. If a single DC Gateway is simultaneously attached to multiple TRs, route conflicts may occur.

<span id=".5piv5ZCm5pSv5oyB5ZCM5LiA5LiT57q_572R5YWz5ZCM5pe25YWz6IGU5LqR5LyB5Lia572R5ZKM5Lit6L2s6Lev55Sx5Zmo77yf"></span>
## Can a DC Gateway be associated with both a CEN and a TR at the same time?

No. After a DC Gateway is attached to a CEN or a TR, it dynamically learns routes from them. If a single DC Gateway is simultaneously attached to both a CEN and a TR, route conflicts may occur.
