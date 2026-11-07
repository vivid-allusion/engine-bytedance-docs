---
title: "DDoS blackholing strategy"
product: "DDoS Protection"
product_code: "byteplus-ddos-protection"
source: "https://docs.byteplus.com/en/docs/byteplus-ddos-protection/DDoS_blackholing_policy"
---

DDoS blackholing is a security policy that temporarily blocks all inbound traffic to a protected resource when a high\-volume attack exceeds its defense capacity, protecting it from further damage. This guide explains the blackhole mechanism, details the automatic and manual methods for restoring your services, and provides strategies to prevent future incidents.

<span id="08821ae8"></span>
## How to unblock an EIP from blackholing?

After your resource triggers the blackhole blocking policy, the system provides both automatic and manual methods for unblocking.

<span id="24ccb4c3"></span>
### Automatic unblocking

Automatic unblocking of blackholes occurs in the following two scenarios:

<span id="0ec714d3"></span>
#### **Being blackholed when integrated into Cloud DDoS Protection**

When an IP under basic protection is added to Cloud DDoS Protection, if the IP is being blackholed, the system automatically performs an unblocking action. The maximum number of automatic unblocking actions for a single instance is equal to the quota of purchased protected IPs.

For example, if you purchase a subscription\-based Cloud DDoS Protection instance and select 100 protected IPs, the instance will have a quota of 100 automatic unblocking attempts. You then add three EIPs (A, B, and C), two of which (B and C) are currently blackholed. After they are successfully added, Cloud DDoS Protection automatically unblocks B and C. This uses two attempts from your quota, leaving 98.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">Removing an IP address will not restore the quota that has already been consumed.</div>


<span id="255a218c"></span>
#### **Blackholing after Integration with DDoS Protection**

After your resources are connected to DDoS protection services (including basic protection, advanced protection, and cloud protection), if the attack traffic exceeds the protection capacity limit, the system will trigger blackhole routing to drop all traffic onto the resource. After the attack ends, the system will continue to monitor for a period of time and will only lift the black hole state after confirming that services have returned to normal.

Under normal circumstances, the black hole state will be automatically lifted approximately two hours after the attack ends. However, the actual unblocking time will be dynamically adjusted based on the frequency of attacks: it may be shortened to 1 hour, or extended to 24 hours or even longer.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">If you have a paid subscription for DDoS Advanced Protection or Native Protection services, you can view the scheduled automatic unblocking time for blackhole events in the protection resource list in the console.</div>


In this scenario, the blackhole's automatic unblocking time is primarily affected by the following factors:


* **Ongoing attacks**: If the attack continues, the automatic unblocking time for the blackhole will be extended, and the unblocking time will be recalculated starting from the moment of extension.

* **Attack frequency**:

   * If an asset is attacked for the first time, the automatic unblocking time for its blackhole will be shorter.

   * If an asset is frequently attacked, the automatic blackhole unblocking time will be extended, because the probability of continued attacks on this resource is higher.


<span id="49e4bd31"></span>
### Manual unblocking

To urgently restore business operations, you can manually unblock the resource from the DDoS console.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">We recommend enhancing your protection configuration (such as baseline or flexible protection rules) before unblocking the resource to prevent it from being blackholed again by a subsequent attack.</div>


<span id="2d001acf"></span>
#### Constraints


* Only paid subscriptions for Advanced DDoS Protection and Cloud DDoS Protection support manual unblocking.

* Manual unblocking is not supported by Cloud DDoS Protection_ Basic or for free trial instances.


<span id="118e75db"></span>
#### Important notes


* If the DDoS attack has not ended after manual unblocking, the asset may enter the blackhole state again.

* The quota for manual unblocking attempts resets daily at 2:00 AM, and unused attempts do not carry over.

* The number of manual unblocking attempts varies by instance type:

   
   |Instance specifications |Manual unblocking count |
   |---|---|
   |Cloud DDoS Protection_Basic |Manual unblocking is not supported |
   |Advanced DDoS Protection |5 times per day |
   |Cloud DDoS Protection |5 times per day |
   


<span id="3c261265"></span>
#### How to unblock manually


* **Cloud DDoS Protection_Basic**: Manual unblocking is not currently supported.

* **Advanced DDoS Protection**: Go to **Advanced DDoS Protection \> Protection policy \> DDoS attack protection**, then select **Unblock**. 

* **Cloud DDoS Protection**: Go to the **Cloud DDoS Protection \> Protection resources**, select the blocked EIP instance, and click **Unblock**.


<span id="4b08d614"></span>
## How to prevent blackholing?

Blackhole blocking is triggered only when the peak bandwidth of a DDoS attack exceeds the DDoS protection capability of the asset. The stronger an asset's defense capability, the less likely it is to be blackholed by a DDoS attack. To prevent frequent blackholing, we recommend increasing your plan's protection bandwidth. This enhances your asset's DDoS protection capability, also known as the blackhole threshold.

<span id="53f90221"></span>
##
