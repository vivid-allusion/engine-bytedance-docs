---
title: "Instance diagnostic overview"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/Instance-Diagnostic-item"
---

## Diagnostic status

|Status |Explanation |Example |
|---|---|---|
|Pass |Indicates the service is available and no issues are detected |Instance expiration date \> 7 days |
|Notice |Indicates service is available, and identified issue does not affect service operation |3 days < instance expiration date ≤ 7 days |
|General |Indicates the service is available, but an issue may potentially impact it soon |Instance expiration time < 3 day |
|SEVERE |Indicates service is available, but an issue poses a significant risk to the service |The instance has expired but has not been shut down |
|Critical |Indicates service unavailable |The instance has been shut down because it expired |

## Diagnostics overview

|Diagnosed type |Instance Diagnostic item |
|---|---|
|Elastic IP Address |For details, see [EIP diagnostic](https://docs.byteplus.com/en/docs/NetworkAdvisor/EIP_diagnostic_items). |
|NAT Gateway |For details, see [NAT Gateway diagnostic](https://docs.byteplus.com/en/docs/NetworkAdvisor/NAT_Gateway_diagnostic_items). |
|CLB |For details, see [CLB diagnostic](https://docs.byteplus.com/en/docs/NetworkAdvisor/CLB_diagnostic_items). |
|VPN |For details, see [VPN diagnostic](https://docs.byteplus.com/en/docs/NetworkAdvisor/VPN_gateway_diagnostic_items). |
|TR type IPsec\-VPN connection | |
|Transit Router |For details, see [TR diagnostic](https://docs.byteplus.com/en/docs/NetworkAdvisor/Transit_Router_diagnostic_items). |
|Direct Connect (DC) |For details, see [DC diagnostic](https://docs.byteplus.com/en/docs/NetworkAdvisor/Direct_Connect_diagnostic_items). |
|Endpoint |For details, see [PrivateLink diagnostic](https://docs.byteplus.com/en/docs/NetworkAdvisor/PrivateLink_diagnostic_items). |
|Cloud Enterprise Network (CEN)  |For details, see [CEN diagnosis](https://docs.byteplus.com/en/docs/NetworkAdvisor/CEN-diagnosis). |
