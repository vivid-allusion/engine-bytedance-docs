---
title: "NAT Gateway diagnostic"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/NAT_Gateway_diagnostic_items"
---

This topic introduces the NAT Gateway diagnostic items.


|**Module** |**Item Category Name** |**Item Name** |**Abnormal Result** |**Item Status** |**Recommendation** |
|---|---|---|---|---|---|
|Instance Information Diagnosis |Resource status |Check instance status |Available |Pass |\-\- |
||||Creating |Notice |Resource is in intermediate state. Please try again later. |
||||Operating |||
||||Deleting |||
||Arrears alert |Check if instance is in arrears |Not overdue |Pass |\-\- |
||||Instance overdue and suspended |Severe |Account overdue, please recharge promptly to ensure normal resource usage.[ Cost Center - Account Recharge](https://console.byteplus.com/finance/fund/recharge) |
||||*Instance overdue and reclaimed* |Severe ||
||Expiration warning |Check if instance is expired |Instance expiration \> 7 days |Pass |\-\- |
||||3 < Instance expiration ≤ 7 days |Notice |Instance expiring soon. Please renew promptly to ensure normal resource usage. [Cost Center - Renewal Management](https://console.byteplus.com/finance/renew/) |
||||Instance expires in < 3 days |General ||
||||Instance expired and suspended |Severe |Instance expired, please recharge promptly to ensure normal resource usage. [Cost Center - Renewal Management](https://console.byteplus.com/finance/renew/) |
||||Instance expired and reclaimed |Severe ||
||Quota check |Check number of EIPs supportable per NAT instance |NAT EIP binding quota utilization <=80% |Pass |\-\- |
||||NAT EIP binding quota utilization \>80% |General |Increase quota promptly to avoid business impact [NAT - Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=NATGW)<br><br> |
||||NAT EIP binding quota 100% allocated |Serious ||
|||Check number of SNAT rules supported per NAT instance |NAT SNAT rule creation quota utilization <=80% |Pass |\-\- |
||||NAT SNAT rule creation quota utilization <=80% |General |Increase quota promptly to avoid business impact [NAT - Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=NATGW) |
||||NAT SNAT rule creation quota 100% allocated |Serious ||
|||Check number of DNAT rules supported per NAT instance |NAT DNAT rule creation quota utilization <=80% |Pass |\-\- |
||||NAT DNAT rule creation quota utilization \>80% |General |Increase quota promptly to avoid business impact [NAT - Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=NATGW) |
||||NAT DNAT rule creation quota 100% allocated |Serious ||
|Specification Exceedance Diagnosis<br><br> |NAT bandwidth utilization |Check NAT instance bandwidth utilization |NAT instance inbound and outbound bandwidth utilization ≤80% |Pass<br><br> |\-\- |
||||NAT instance outbound bandwidth utilization \>80% |Serious |Bandwidth over\-limit may cause random packet loss. Plan your service usage appropriately. |
||||NAT instance inbound bandwidth utilization \>80% |||
|||Check if SNAT source ports are exhausted |SNAT source ports not exhausted |Pass |\-\- |
||||SNAT source port allocation failed<br><br> |Severe |A single EIP offers limited SNAT ports. Increase the number of EIPs in SNAT rules. |
|Configuration Diagnosis |Route configuration check<br><br> |Check if route entry pointing to NAT instance exists in VPC route table |Route entry pointing to NAT instance exists in VPC route table |Pass |\-\- |
||||No route to NAT instance in VPC route table |Severe |Add a route to the NAT instance in the VPC route table to ensure connectivity. |
||SNAT/DNAT configuration check |Check if NAT instance SNAT and DNAT use the same EIP |NAT instance SNAT and DNAT configured with same EIP |Notice |Avoid using the same EIP for SNAT and DNAT rules to prevent business contention. |
||||NAT instance SNAT and DNAT not configured with same EIP |Pass |\-\- |
|||Check if backend ECS instances have both an EIP and a NAT gateway configured |Backend ECS instances have both an EIP and a NAT gateway configured |Notice |Avoid configuring both EIP and NAT gateway for the same ECS instance, as traffic will use the EIP. |
||||Backend ECS instance not configured with both EIP and NAT gateway |Pass |\-\- |
|Security Policy Diagnosis |EIP security lock check |Check if EIP bound to NAT instance is locked due to risk control |EIPs bound to NAT instance are not blocked for security |Pass |\-\- |
||||NAT instance not bound to an EIP |Pass |\-\- |
||||EIPs bound to NAT instance are blocked for security |Severe |EIP bound to NAT instance is blocked due to violations. Operations prohibited. Monitor service status |
