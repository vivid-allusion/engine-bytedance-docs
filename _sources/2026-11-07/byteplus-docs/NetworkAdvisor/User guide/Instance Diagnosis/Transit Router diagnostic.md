---
title: "Transit Router diagnostic"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/Transit_Router_diagnostic_items"
---

This topic introduces the diagnostics for Transit Router (TR).


|**Module** |**Item Category Name** |**Item Name** |**Abnormal Result** |**Item Status** |**Recommendation** |
|---|---|---|---|---|---|
|Instance Information Diagnosis |Resource status |Check TR instance status<br><br> |Available |Pass |\-\- |
||||Deleting |Notice |Resource is in intermediate state. Please try again later. |
||||Configuring |Notice ||
||||Creating |Notice ||
||Arrears alert |Check if TR instance is suspended due to arrears, check if associated bandwidth package is in arrears |Not overdue |Pass |\-\- |
||||Instance overdue and suspended |Severe<br><br> |Account overdue, please recharge promptly to ensure normal resource usage. [Cost Center - Account Recharge](https://console.byteplus.com/finance/fund/recharge) |
||||*Instance overdue and reclaimed* |Severe ||
||Expiration warning |Check if bandwidth package instance expires within 7 days / is already expired<br><br> |Instance expiration \> 7 days |Pass |\-\- |
||||3 < Instance expiration ≤ 7 days |Notice |Instance expiring soon. Please renew promptly to ensure normal resource usage. [Cost Center - Renewal Management](https://console.byteplus.com/finance/renew/) |
||||Instance expires in < 3 days |General ||
||||Instance expired and suspended |Severe |Instance expired, please recharge promptly to ensure normal resource usage. [Cost Center - Renewal Management](https://console.byteplus.com/finance/renew/) |
||||Instance expired and reclaimed |Severe ||
||Quota check |Check if TR route entries exceed quota \>=80% |Gateway route entry quota =100%<br><br> |Serious |Route count exceeds quota. Merge CIDRs or increase route quota, otherwise routes will be lost. [Quota Center](https://console.byteplus.com/quota/productList) |
||||Gateway route entry quota \>=80% |General |Increase quota promptly to avoid route loss. [Quota Center](https://console.byteplus.com/quota/productList) |
||||Gateway route entry quota <80% |Pass |\-\- |
|Configuration Diagnosis |Connection check |Check if any network instance connections exist under the instance |Transit Router instance has network instance connections created |Pass |\-\- |
||||Transit Router instance has no network instance connections created<br><br> |Notice |Create a network instance connection; otherwise TR cannot function properly. |
||Associated forwarding check<br><br> |Check if network instance connection has associated forwarding configured<br><br> |Network instance connection with associated forwarding configured |Pass |\-\- |
||||Network instance connection with no associated forwarding configured |Notice |Some TR connections are not associated with a route table. TR will discard traffic from those connections. <br><br> |
||Route learning check |Check if network instance connection has route learning configured |Network instance connection configured with route learning |Pass |\-\- |
||||Network instance connection has no route learning configured<br><br> |Notice |Some TR route tables are not configured with route learning. Without static routes, TR will discard traffic from those connections.  |
||Inter\-region bandwidth configuration |Check if cross\-region network instance connection is configured with a bandwidth package |Cross\-region network instance connection has bandwidth package configured |Pass |\-\- |
||||Cross\-region network instance connection has no bandwidth package configured<br><br> |General |Cross\-region connection has no bandwidth package configured, cross\-region traffic may be dropped.  |
||Route diagnosis |Conflicting or overlapping routes<br><br> |No route table entry conflicts |Pass |\-\- |
||||Route table entry conflicts detected |General |Route conflict detected.  |
|Specification Exceedance Diagnosis<br><br> |Bandwidth utilization<br><br> |Inter\-region bandwidth in/out utilization \>=80%<br><br> |Inbound and outbound bandwidth utilization <=80% |Pass |\-\- |
||||Outbound bandwidth utilization \>80% |Serious |Cross\-region bandwidth over\-limit may cause random packet loss. Upgrade your bandwidth. See [Modifying bandwidth for a package bandwidth](https://docs.byteplus.com/en/docs/transitrouter/TR-bandwidth-packages-02) for details. |
||||Inbound bandwidth utilization \>80% |Serious ||
|||TR connection inbound/outbound bandwidth utilization \>=80% |Inbound and outbound bandwidth utilization <=80% |Pass |\-\- |
||||Outbound bandwidth utilization \>80%<br><br> |Serious |TR connection bandwidth over\-limit may cause random packet loss. Submit a ticket to upgrade the TR rate limit for normal operation. |
||||Inbound bandwidth utilization \>80% |Serious ||
||Rate limiting packet loss |Check for cross\-region bandwidth rate limiting packet loss |No inter\-region bandwidth rate limiting packet loss in past 30 mins |Pass |\-\- |
||||Inter\-region bandwidth rate limiting packet loss occurred in past 30 mins |Serious |Inter\-region bandwidth is experiencing rate\-limited packet loss. Increase inter\-region bandwidth allocation. |
||Route matching failure packet loss |Check for route matching failure packet loss |No route match failure packet loss in past 30 minutes |Pass |\-\- |
||||Route match failure packet loss occurred in past 30 minutes<br><br> |Serious |Packet loss due to no matching route. Check route configuration and consider enabling route synchronization. |
