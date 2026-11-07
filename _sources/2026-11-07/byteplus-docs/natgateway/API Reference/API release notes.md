---
title: "API release notes"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/API-release-notes"
---

This article introduces the API updates of the NAT gateway.

<span id="b4TQHJqz"></span>
## July 2025


|API |Release note |Associated features |
|---|---|---|
|CreateNatGateway |Added new error code: `InvalidNatGateway.NoSubnetInRegion`. |NAT Gateway |
|DeleteNatGateway |Added new error code: `InvalidNatGateway.InUse`. ||
|DeleteDnatEntry |Added new error codes: `InvalidDnatEntry.InvalidStatus`, `InvalidNatGateway.NotFound`. |DNAT rules<br><br> |
|ModifyDnatEntryAttributes |Add error code: `InvalidDnatEntry.InvalidStatus`. ||
|DescribeDnatEntries |Add error code: `MissingParameter`. ||
|DeleteNatIp |Added error codes: `InvalidNatIp.InvalidStatus` and `InvalidNatGateway.NotFound`. |Bandwidth limit |
|ModifyNatIpAttributes |||
|DescribeNatIpAttributes |Added new error code: `InvalidNatGateway.NotFound`. ||
|DeleteSnatEntry |Added new error codes: `InvalidSnatEntry.InvalidStatus` and `InvalidNatGateway.NotFound`. |SNAT rules |
|ModifySnatEntryAttributes |||
|DescribeSnatEntryAttributes |Added new error code: `InvalidNatGateway.NotFound`. ||
|CreateNatIpLimitRule |Add interface to manage bandwidth speed limit.<br><br> |Bandwidth limit |
|ModifyNatIpLimitRuleAttributes |||
|DeleteNatIpLimitRule |||
|DescribeNatIpLimitRules |||
