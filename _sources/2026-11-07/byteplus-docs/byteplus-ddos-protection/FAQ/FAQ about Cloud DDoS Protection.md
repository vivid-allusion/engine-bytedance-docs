---
title: "FAQ about Cloud DDoS Protection"
product: "DDoS Protection"
product_code: "byteplus-ddos-protection"
source: "https://docs.byteplus.com/en/docs/byteplus-ddos-protection/FAQ_about_Cloud_DDoS_Protection"
---

This document answers frequently asked questions (FAQs) about the Cloud DDoS Protection service. It covers key topics such as the billing differences between protection plans and the steps to take if your Elastic IP (EIP) is blackholed.

<span id="e227af36"></span>
# What is the difference in billing between Cloud DDoS Protection and DDoS Advanced Protection?

Billing for Cloud DDoS Protection and DDoS Advanced Protection includes both basic billing items and additional billing items. The table below shows the differences between the basic billing items and extensible billing items of different protection services.


|Item |DDoS Advanced Protection |Cloud DDoS Protection |
|---|---|---|
|Basic billing items |* Minimum guaranteed protection bandwidth (various optional configurations available)<br><br>* Elastic bandwidth protection (available in different configurations)<br><br>* Default protection package: 100 Mbps business bandwidth + 60 protected ports + 60 protected domains |* Maximum protection capability<br><br>* Default protected IP count (50)<br><br>* Default business bandwidth (50 Mbps)<br><br><br> |
|Additional billing items |The following billing items can be added to the base package:<br><br><br>* Service bandwidth (an additional charge applies for each 50 Mbps increase)<br><br>* Number of protected ports (an additional charge applies for each increment of 10 ports)<br><br>* Number of protected domains (additional charge for every 10 domains added) |The following billing items can be added to the base package:<br><br><br>* Number of protected IPs (each additional IP incurs an extra charge)<br><br>* Service bandwidth (an additional charge applies for each 50 Mbps increase) |


For more information about billing, see the following documents:


* [Billing details of Advanced DDoS Protection](https://docs.byteplus.com/docs/byteplus-ddos-protection/docs-pricing)

* [Billing details of Cloud DDoS Protection](https://docs.byteplus.com/docs/byteplus-ddos-protection/Billing_details_of_Cloud_DDoS_Protection)


<span id="62302281"></span>
# What should I do if a protected EIP is blackholed?

After an EIP instance is blackholed, you can unblock the EIP using the following methods.

<span id="a4ba44db"></span>
## Automatic unblocking

In the protection resource list, hover over the icon next to an EIP that has a **Blackholing** status to see the scheduled automatic unblock time. In general, the EIP is automatically unblocked about 2 hours after an attack ends, but the actual unblocking time may vary depending on the frequency of attacks. In some cases, the unblocking time may be extended to 24 hours or even longer.

For more details, refer to [Automatic unblocking](https://docs.byteplus.com/docs/byteplus-ddos-protection/DDoS_blackholing_policy#24ccb4c3).

<span id="e856d522"></span>
## Manually unblocking

In the protection resources list, click **Unblock** in the Actions column to manually unblock the EIP.


* If the DDoS attack does not end after manual unblocking, the EIP may be blackholed again.

* If your instance is frequently blackholed, it is recommended that you increase your plan's protection bandwidth level.

* You have a limited number of manual unblocking attempts per instance each day. This limit resets daily at 02:00, and unused attempts do not carry over. The number of available attempts varies by instance specification.


For more details, refer to [Manual unblocking](https://docs.byteplus.com/docs/byteplus-ddos-protection/DDoS_blackholing_policy#49e4bd31).
