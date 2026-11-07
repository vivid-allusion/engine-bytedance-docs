---
title: "API overview"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/API-overview-1"
---

This topic lists the OpenAPIs for NAT Gateway as follows.

## NAT Gateway

|API name |Feature |
|---|---|
|[CreateNatGateway](https://docs.byteplus.com/en/docs/natgateway/CreateNatGateway) |Create a new NAT Gateway instance. |
|[ModifyNatGatewayAttributes](https://docs.byteplus.com/en/docs/natgateway/ModifyNatGatewayAttributes) |Modify the specification, name, and description of a NAT Gateway. |
|[DescribeNatGateways](https://docs.byteplus.com/en/docs/natgateway/DescribeNatGateways) |Query NAT Gateways that meet the specified conditions. |
|[DescribeNatGatewayAttributes](https://docs.byteplus.com/en/docs/natgateway/DescribeNatGatewayAttributes) |View the details of a NAT Gateway. |
|[DeleteNatGateway](https://docs.byteplus.com/en/docs/natgateway/DeleteNatGateway) |Delete a specified NAT Gateway. |
|[ListNatGatewayAvailableZones](https://docs.byteplus.com/en/docs/natgateway/ListNatGatewayAvailableZones) |Query the availability zones where NAT Gateways are deployed in the current region.​ |

## SNAT rule

|API name |Feature |
|---|---|
|[CreateSnatEntry](https://docs.byteplus.com/en/docs/natgateway/CreateSnatEntry) |Create a new SNAT rule. |
|[ModifySnatEntryAttributes](https://docs.byteplus.com/en/docs/natgateway/ModifySnatEntryAttributes) |Modify the name and associated EIP of an SNAT rule. |
|[DescribeSnatEntries](https://docs.byteplus.com/en/docs/natgateway/DescribeSnatEntries) |Query SNAT rules that meet the specified conditions. |
|[DescribeSnatEntryAttributes](https://docs.byteplus.com/en/docs/natgateway/DescribeSnatEntryAttributes) |View the details of an SNAT rule. |
|[DeleteSnatEntry](https://docs.byteplus.com/en/docs/natgateway/DeleteSnatEntry) |Delete a specified SNAT rule. |

## DNAT rule

|API name |Feature |
|---|---|
|[CreateDnatEntry](https://docs.byteplus.com/en/docs/natgateway/CreateDnatEntry) |Create a new DNAT rule. |
|[ModifyDnatEntryAttributes](https://docs.byteplus.com/en/docs/natgateway/ModifyDnatEntryAttributes) |Modify a DNAT rule. |
|[DescribeDnatEntries](https://docs.byteplus.com/en/docs/natgateway/DescribeDnatEntries) |Query DNAT rules that meet the specified conditions. |
|[DescribeDnatEntryAttributes](https://docs.byteplus.com/en/docs/natgateway/DescribeDnatEntryAttributes) |View the details of a DNAT rule. |
|[DeleteDnatEntry](https://docs.byteplus.com/en/docs/natgateway/DeleteDnatEntry) |Delete a DNAT rule. |

## NAT IP

|API name |Feature |
|---|---|
|[CreateNatIp](https://docs.byteplus.com/en/docs/natgateway/CreateNatIp) |Add a NAT IP. |
|[ModifyNatIpAttributes](https://docs.byteplus.com/en/docs/natgateway/ModifyNatIpAttributes) |Modify a NAT IP. |
|[DescribeNatIps](https://docs.byteplus.com/en/docs/natgateway/DescribeNatIps) |Query NAT IPs that meet the specified conditions. |
|[DescribeNatIpAttributes](https://docs.byteplus.com/en/docs/natgateway/DescribeNatIpAttributes) |View the details of a NAT IP. |
|[DeleteNatIp](https://docs.byteplus.com/en/docs/natgateway/DeleteNatIp) |Delete a NAT IP. |

## IP rate limiting

|API name |Feature |
|---|---|
|[CreateNatIpLimitRule](https://docs.byteplus.com/en/docs/natgateway/CreateNatIpLimitRule) |Create a rate limiting rule. |
|[DescribeNatIpLimitRules](https://docs.byteplus.com/en/docs/natgateway/DescribeNatIpLimitRules) |Query bandwidth limit rules. |
|[ModifyNatIpLimitRuleAttributes](https://docs.byteplus.com/en/docs/natgateway/ModifyNatIpLimitRuleAttributes) |Modify a rate limiting rule. |
|[DeleteNatIpLimitRule](https://docs.byteplus.com/en/docs/natgateway/DeleteNatIpLimitRule) |Delete a bandwidth limit rule. |

## Resource tag

|API name |Feature |
|---|---|
|[TagResources](https://docs.byteplus.com/en/docs/natgateway/TagResources) |Batch add tags to a resource. |
|[UntagResources](https://docs.byteplus.com/en/docs/natgateway/UntagResources) |Batch remove tags from a resource. |
|[ListTagsForResources](https://docs.byteplus.com/en/docs/natgateway/ListTagsForResources) |Query tags that meet the specified conditions. |

## Session log

|API name |Feature |
|---|---|
|[CreateSessionLog](https://docs.byteplus.com/en/docs/natgateway/CreateSessionLog) |Create a NAT session log. |
|[DescribeSessionLogs](https://docs.byteplus.com/en/docs/natgateway/DescribeSessionLogs) |Query session logs. |
|[ModifySessionLog](https://docs.byteplus.com/en/docs/natgateway/ModifySessionLog) |Modify a NAT session log. |
|[EnableSessionLog](https://docs.byteplus.com/en/docs/natgateway/EnableSessionLog) |Enable NAT session log. |
|[DisableSessionLog](https://docs.byteplus.com/en/docs/natgateway/DisableSessionLog) |Disable NAT session log. |
|[DeleteSessionLog](https://docs.byteplus.com/en/docs/natgateway/DeleteSessionLog) |Delete a NAT session log. |
