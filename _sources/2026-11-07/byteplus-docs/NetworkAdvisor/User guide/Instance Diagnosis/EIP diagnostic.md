---
title: "EIP diagnostic"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/EIP_diagnostic_items"
---

This topic introduces diagnostic items for EIPs.

|**Diagnostic category** |**Diagnostic​**  |**Diagnostic item description** |**Diagnostic conditions** |**Diagnostic results** |**Recommendations** |
|---|---|---|---|---|---|
|Instance information diagnosis |Resource status |Instance status check |Available |Pass |\-\- |
||||Attached |||
||||Pending \- Instance operation in progress |Note |The resource is in an intermediate state. Please try again later. |
||||Attaching \- Instance associating |||
||||Detaching \- Instance disassociating |||
||Overdue alert |Verify if the instance has overdue payments |No overdue payments |Pass |\-\- |
||||The instance has overdue payments but is not yet suspended |Severe |Account overdue. Please recharge promptly to ensure normal resource usage. [Billing center - Account recharge](https://console.byteplus.com/finance/fund/recharge) |
||||Instance suspended due to overdue payment |Critical ||
||Expiration warning |Check if the instance has expired |Expiration date \> 7 days |Pass |\-\- |
||||3 days < instance expiration date ≤ 7 days |Note |The instance is about to expire. Please renew it in time to ensure normal resource usage. [Billing center - Renewal management](https://console.byteplus.com/finance/renew/) |
||||Instance expiration time < 1 day |General ||
||||The instance has expired but has not been shut down |SEVERE |The instance has expired. Please recharge as soon as possible to ensure normal resource usage. [Billing center - Renewal management](https://console.byteplus.com/finance/renew/) |
||||The instance has been shut down because it expired |Critical ||
||Instance binding status check |Check the resource information bound to the EIP instance |EIP instance is not associated with any resource |Note |EIP instance is not currently associated with any resource. |
||||EIP instance is associated with resources |Pass |\-\- |
|Capacity overrun diagnosis |Bandwidth utilization |EIP instance inbound/outbound bandwidth utilization check |Outbound bandwidth utilization of the EIP instance ≤ 80% |||
||||Inbound bandwidth utilization of the EIP instance ≤ 80% |||
||||Outbound bandwidth utilization of the EIP instance \> 80% |SEVERE |If the bandwidth limit is exceeded, it may cause random packet loss. To ensure normal service operation, upgrading your bandwidth specification is recommended. For instructions on upgrading bandwidth, see [EIP - Specification change](https://docs.byteplus.com/en/docs/eip/Bandwidth-modifications). |
||||Inbound bandwidth utilization of the EIP instance \> 80% |||
|Security policy diagnosis |Security protection status |EIP security protection status check |Default protection |Pass |\-\- |
||||Default protection \- Added to DDoS Native Protection (Premium) |||
||||Enhanced protection \- Added to Anti\-DDoS Origin (Enterprise Edition) |||
||||The Enhanced Protection EIP is not added to Anti\-DDoS Origin (Enterprise Edition) |Note |The Enhanced Protection EIP instance is not yet added to DDoS Native Protection. Please bind a security protection plan promptly. |
||Security lock check |Check if the EIP is locked due to risk control reasons |EIP instance is not security blocked |Pass |\-\- |
||||The EIP instance is security blocked |Critical |EIP has been security blocked due to violations. Operations are prohibited. Please monitor your service status promptly. |
