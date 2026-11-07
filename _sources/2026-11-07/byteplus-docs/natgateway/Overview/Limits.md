---
title: "Limits"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Limits"
---

This topic describes the quota limits for NAT Gateway.

## Shared quota

The shared quota for Internet NAT Gateway and VPC NAT Gateway is as follows:

|Quota parameter |Description |Default maximum |Upgradeable |Adjusted quota |
|---|---|---|---|---|
|vpc/nat |Maximum number of NAT Gateways supported per VPC |3 |No |\- |
|nat/snat |Maximum number of SNAT entries supported per NAT Gateway |40 |Yes, go to [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=NATGW) to apply for an increase |200 |
|nat/dnat |The maximum number of DNAT rules that a single NAT Gateway supports creating |100 |Yes, go to [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=NATGW) to apply for an increase |200 |

## Other quotas

### Internet NAT Gateway

|Quota parameter |Description |Default maximum |Upgradeable |Adjusted quota |
|---|---|---|---|---|
|\- |Number of public IPs supported per SNAT entry |40 |No |\- |
|nat/eip |Number of public IPs supported for association on a single Internet NAT Gateway |10 |Yes, go to [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=NATGW) to apply for an increase |100 |
|nat/iplimitrule |Maximum number of rate limiting rules per Internet NAT Gateway​ |20 ||100 |
|nat/qosqueue |Maximum number of traffic queues for scheduling policies per Internet NAT Gateway​ |64 |No |\- |
|nat_proxy/rule |Maximum number of proxy rules per Web proxy |100 |Yes. Go to [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=NATGW) to apply for a quota increase. |500 |
|nat_proxy/port |Maximum number of listening ports per Web proxy |5 |No |\- |
|nat_proxy/rule/source |Maximum number of access source entries per Web proxy rule​ |100 |No |\- |
|nat_proxy/rule/destination |Maximum number of access destination entries per Web proxy rule​ |500 |No |\- |

> **tip**

> The Web Proxy feature is in the Invite\-only Beta stage. To request a trial, pleascontact your account manager.

### VPC NAT Gateway

|Quota parameter |Description |Default maximum |Upgradeable |
|---|---|---|---|
|nat/cidr/ip |Number of NAT IP addresses supported for adding on a single VPC NAT Gateway |50 |No |
|\- |The number of NAT IP addresses supported to attach to a single SNAT entry |1 |No |
