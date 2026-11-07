---
title: "Direct Connect diagnostic"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/Direct_Connect_diagnostic_items"
---

This topic introduces Direct Connect diagnostic items.


|**Module** |**Item Category Name** |**Item Name** |**Abnormal Result** |**Item Status** |**Recommendation** |
|---|---|---|---|---|---|
|Instance Information Diagnosis |Resource status |DC connection, DC gateway, virtual interface instance status diagnosis |Available |Pass |\-\- |
||||Deleting |Notice |Resource is in intermediate state. Please try again later. |
||||Configuring |Notice ||
||||Creating |Notice ||
||Arrears alert |DC gateway billing status diagnosis |Not overdue |Pass |\-\- |
||||Instance overdue and suspended |Severe<br><br> |Account overdue, please recharge promptly to ensure normal resource usage. [Cost Center - Account Recharge](https://console.byteplus.com/finance/fund/recharge) |
||||Instance overdue and reclaimed |Severe ||
||Expiration warning |Check if DC gateway/DC connection expires within 7 days or has expired |Instance expiration \> 7 days |Pass |\-\- |
||||3 < Instance expiration ≤ 7 days |Notice |Instance expiring soon. Please renew promptly to ensure normal resource usage. [Cost Center - Renewal Management](https://console.byteplus.com/finance/renew/) |
||||Instance expires in < 3 days |Normal ||
||||Instance expired and suspended |Severe |Instance expired, please recharge promptly to ensure normal resource usage. [Cost Center - Renewal Management](https://console.byteplus.com/finance/renew/) |
||||Instance expired and reclaimed |Severe ||
||Quota check |BGP route quota usage<br><br> |Gateway route entry quota =100% |General |Route quota exceeded. Increase your route quota in the Quota Center to avoid route loss. [Quota Center](https://console.byteplus.com/quota/productList)<br><br> |
||||Gateway route entry quota \>=80% |Normal |Increase quota promptly to avoid route loss. [Quota Center](https://console.byteplus.com/quota/productList) |
||||Gateway route entry quota <80% |Pass |\-\- |
|Configuration Diagnosis |Route configuration |To/from\-cloud route configuration |Virtual interface not configured |Notice |From\-cloud route not configured. Configure virtual interface. |
||||CEN not configured and TR not configured<br><br> |Notice |To\-cloud route not configured. Associate with CEN or TR. |
||||\-\- |Pass |\-\- |
||BGP session abnormal |BGP session status |Normal |Pass |\-\- |
||||Faulty |General |BGP session abnormal. Check network configuration. |
|Specification Exceedance Diagnosis |Rate limiting packet loss |Check for virtual interface rate limiting packet loss |No virtual interface rate limiting packet loss in past 30 mins |Pass |\-\- |
||||Virtual interface rate limiting packet loss occurred in past 30 mins |General |Virtual interface has rate limiting packet loss. Please increase virtual interface bandwidth limit.<br><br> |
