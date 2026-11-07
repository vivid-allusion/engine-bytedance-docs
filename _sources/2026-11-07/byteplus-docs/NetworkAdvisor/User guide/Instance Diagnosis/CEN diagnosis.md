---
title: "CEN diagnosis"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/CEN-diagnosis"
---

This topic introduces the Cloud Enterprise Network (CEN) diagnosis items.

|Module |**Diagnostic category**<br><br> **(ItemCategoryName)**  |**Diagnostic​** <br><br>(**ItemName)**  |**Diagnostic conditions**<br><br>(**AbnormalResult)**  |**Diagnostic results**<br><br> **(ItemStatus)**  |**Recommendations**<br><br> **(Recommendation)**  |
|---|---|---|---|---|---|
|Instance information diagnosis |Resource status |Check CEN instance status |Available |<br>Pass<br> |\-\- |
||||Deleting |<br>Notice<br> |The resource is in an intermediate state. Please try again later.<br><br> |
||||Pending |<br>Notice<br> ||
||||Creating |<br>Notice<br> ||
||Overdue alert |Check whether the bandwidth package instance associated with CEN is overdue |No overdue payments |<br>Pass<br> |\-\- |
||||The instance has overdue payments but is not yet suspended |<br>Severe<br> |Account overdue. Please recharge promptly to ensure normal resource usage. [Billing center - Account recharge](https://console.byteplus.com/finance/fund/recharge) |
||||Instance suspended due to overdue payment |<br>Serious<br> ||
||Expiration warning |Check whether the bandwidth package instance expires within 7 days/has already expired |Expiration date \> 7 days |<br>Pass<br> |\-\- |
||||3 days < instance expiration date ≤ 7 days |<div style="text-align: center"><br>Notice</div><br> |The instance is about to expire. Please renew it in time to ensure normal resource usage. [Billing center - Renewal management](https://console.byteplus.com/finance/renew/) |
||||Instance expiration time < 3 day |<div style="text-align: center"><br>General</div><br> ||
||||The instance has expired but has not been shut down |<br>Severe<br> |The instance has expired. Please recharge as soon as possible to ensure normal resource usage. [Billing center - Renewal management](https://console.byteplus.com/finance/renew/) |
||||The instance has been shut down because it expired |<br>Serious<br> ||
||Quota check |Check whether the quota number of route entries used by CEN ≥80% |Gateway route entry quota = 100% |<br>Severe<br> |The number of routes has exceeded the quota. Please go to the Quota Center to increase the route quota; otherwise, route loss may occur. [Quota Center](https://console.byteplus.com/quota/productList) |
||||Gateway route entry quota ≥ 80% |<br>General<br> |Please increase the quota promptly to avoid route loss. [Quota Center](https://console.byteplus.com/quota/productList) |
||||Quota usage for route entries on the gateway is < 80% |<div style="text-align: center"><br>Pass</div><br> |\-\- |
|Capacity overrun diagnosis |Rate limiting packet loss |Packet loss due to cross\-region bandwidth rate limiting |No packet loss due to inter\-region bandwidth rate limiting in the last 30 minutes |<br>Pass<br> |\-\- |
||||Packet loss due to inter\-region bandwidth rate limiting occurred in the last 30 minutes |<br>Severe<br> |Packet loss due to rate limiting on inter\-region bandwidth. Please increase the inter\-region bandwidth allocation. See [Modifying an inter-region bandwidth](https://docs.byteplus.com/en/docs/cen/Inter-region-bandwidth-02). |
|Configuration diagnosis |Inter\-region bandwidth configuration |Cross\-region scenario: No inter\-region bandwidth configured |CEN instance has a bandwidth package bound but no inter\-region bandwidth allocated |<br>Severe<br> |Please allocate inter\-region bandwidth to the CEN instance promptly; otherwise, traffic may not function properly. See [Modifying an inter-region bandwidth](https://docs.byteplus.com/en/docs/cen/Inter-region-bandwidth-02). |
||||CEN instance has a bandwidth package bound and inter\-region bandwidth allocated |<br>Pass<br> |\-\- |
||Route diagnosis |Route overlapping |No routing table entry conflict exists |<br>Pass<br> |\-\- |
||||A routing table entry conflict exists |<br>Severe<br> |A route conflict exists. Please adjust the route promptly. |
