---
title: "PrivateLink diagnostic"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/PrivateLink_diagnostic_items"
---

This topic introduces the diagnostic items for PrivateLink.

|**Module** |**Item Category Name** |**Item Name** |**Abnormal Result** |**Item Status** |**Recommendation** |
|---|---|---|---|---|---|
|Instance Information Diagnosis |Resource status<br><br> |Endpoint and endpoint service status |Available |Pass |\-\- |
||||Deleting |Notice |Resource is in intermediate state. Please try again later. |
||||Configuring |Notice ||
||||Creating |Notice ||
|||Connection status check<br><br> |Connected |Pass |\-\- |
||||Disconnecting |Notice |Resource is in intermediate state. Please try again later. |
||||Connecting |Notice ||
||||Waiting for connection |Notice |Connection status abnormal. You may choose to [accept the endpoint connection](https://docs.byteplus.com/en/docs/privatelink/Accepting-Rejecting-endpoint-connection). |
||||Connection refused |General ||
||||Connection failed |General ||
||||Partial connection failed |General ||
||Arrears alert |Check if instance is in arrears |Not overdue |Pass |\-\- |
||||Instance overdue and suspended |Severe<br><br> |Account overdue, please recharge promptly to ensure normal resource usage.[ ](https://console.byteplus.com/finance/fund/recharge)[Cost Center - Account Recharge](https://console.byteplus.com/finance/fund/recharge) |
||||Instance overdue and reclaimed |Severe ||
||Quota check |Number of service resources addable per endpoint service per availability zone |Service resource quota =100%<br><br> |Serious |The number of service resources per availability zone for a single endpoint service has reached the limit. Increase quota promptly. [Cost Center](https://console.byteplus.com/quota/productList)<br><br> |
||||Service resource quota \>=80% |General |Increase your quota promptly to avoid service disruption. [Cost Center](https://console.byteplus.com/quota/productList)<br><br> |
||||Service resource quota <80% |Pass |\-\- |
|Specification Exceedance Diagnosis |Rate limiting packet loss check |Endpoint rate limiting packet loss detection |No endpoint inbound/outbound packet loss in past 30 mins |Pass |\-\- |
||||Endpoint inbound/outbound packet loss occurred in past 30 mins<br><br> |Notice |Rate limit packet loss detected in past 30 mins.  |
|Configuration Diagnosis |ACL configuration check |Check if PrivateLink connections are blocked by VPC ACL<br><br> |All traffic allowed in ACL |Pass |\-\- |
||||PL\-related routes blocked by ACL |General |ACL rules block partial traffic. Adjust network ACL rules. |
