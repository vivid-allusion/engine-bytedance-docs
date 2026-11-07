---
title: "API release notes"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/API-release-notes"
---

This topic describes updates to the APIs for Elastic IP Address (EIPs).

<span id="march-2025"></span>
## March 2025


|API |Modify Record |Attach function |
|---|---|---|
|ModifyEipAddressAttributes |New error codes `InvalidDirectModeEip.IPv4GatewayEnabled`, `InvalidEip.NotSupported`, `InvalidModeEip.DirectMode`. |Changes the name, description, and maximum bandwidth of an EIP. |
|* DescribeEipAddresses<br><br>* DescribeEipAddressAttributes |Added back parameter `VpcId`. |Queries the EIPs that meet the specified conditions. |
|AssociateEipAddress |* Adds new request parameters: `InstanceType` and `VpcId`.<br><br>* Adds a new value for the request parameter InstanceType: IpAddress (trial).<br><br>* Adds new error codes: `InvalidDirectModeEip.IPv4GatewayEnabled`, `InvalidEip.PrivateAddressConflict`, `InvalidModeEip.DirectMode`, `InvalidPrivateIp.IPFormatError`, `InvalidVpc.IPv4GatewayDisabled`, `InvalidVpc.InvalidStatus`, `Forbidden`, `InvalidNatGateway.NotFound`, `InvalidVpc.NotFound`. |Associates an EIP with a cloud resource. |
|DisassociateEipAddress |* Adds a new value for the request parameter `InstanceType`: IpAddress (trial).<br><br>* Adds new error codes: `InvalidNatBindEip.NotFound`, `InvalidNatGateway.NotFound`, `InvalidNatGateway.UnSupportAction`. |Unbinds an elastic IP address from a cloud resource. |
|ReleaseEipAddress |Added error codes `InvalidEipOrNat.InvalidStatus`, `InvalidNatGateway.UnSupportAction`, `InvalidNatBindEip.NotFound`, and `InvalidNatGateway.NotFound` |Releases a specified EIP. |


<span id="january-2025"></span>
## January 2025


|API |Modify Record |Attach function |
|---|---|---|
|DeleteIpAddressPool |Error code deleted`QuotaExceeded.IPPool`、`QuotaExceeded.IPPoolIP`. |Delete an IP address pool |


<span id="november-2024"></span>
## November 2024


|API |Release time |Modify Record |Attach function |
|---|---|---|---|
|[AssociateEipAddress](https://docs.byteplus.com/en/docs/eip/AssociateEipAddress) |2024\-11 |* Add request argument`DirectMode`(Beta,Optional argument).<br><br>* Error code added`InvalidDirectModeEip.InvalidBindInstanceType`、`InvalidInstance.IPv4Disabled`、`InvalidDirectModeEip.InstanceMismatch、Forbidden`。<br><br>* Error code deleted`InvalidEni.IPv4Disabled`。 |Applying for an EIP |
|* [DescribeEipAddresses](https://docs.byteplus.com/en/docs/eip/DescribeEipAddresses)<br><br>* [DescribeEipAddressAttributes](https://docs.byteplus.com/en/docs/eip/DescribeEipAddressAttributes) ||New request parameter`DirectMode`。 |Configure the direct mode of an EIP |
|[ModifyEipAddressAttributes](https://docs.byteplus.com/en/docs/eip/ModifyEipAddressAttributes) ||* Add request argument`DirectMode`(Beta,Optional argument).<br><br>* Error code added：`InvalidDirectModeEip.InvalidBindInstanceType`、`InvalidEni.InvalidStatus`、`InvalidDirectModeEip.InvalidStatus`、`InvalidDirectModeEip.InstanceMismatch`、`Forbidden`。 ||


<span id="_17-july-2024"></span>
## 17 July 2024


|API |Release time |Modify Record |Attach function |
|---|---|---|---|
|[AllocateEipAddress](https://docs.byteplus.com/en/docs/eip/AllocateEipAddress) |2024\-07\-17 |Add request argument `InvalidRenewType.Malformed`。 |Applying for an EIP |


<span id="_28-may-2024"></span>
## 28 May 2024


|API |Release time |Modify Record |Attach function |
|---|---|---|---|
|[AllocateEipAddress](https://docs.byteplus.com/en/docs/eip/AllocateEipAddress) |2024\-05\-28 |* Add request argument`IpAddress`。<br><br>* Request argument `Period`, increase the range of values.<br><br>* Error code added:`InvalidEip.Allocated`、`InvalidIPAddress.NotSupported`、`InvalidEip.IPFormatError`、`InvalidEip.ISPMismatch`、`InvalidParameter`、`LimitExceeded.MonthlyAddressRetrieveQuota`、`UnsupportedOperation.AllocateHistoricalEIP` |Applying for an EIP |
|[DisassociateEipAddress](https://docs.byteplus.com/en/docs/eip/DisassociateEipAddress) ||Error code deleted`InvalidEni.InvalidStatus`。 |Disassociating Cloud Resource from an EIP |
|[AssociateEipAddress](https://docs.byteplus.com/en/docs/eip/AssociateEipAddress) ||Error code added`InvalidEni.IPv4Disabled`。 |Associating Cloud Resources with an EIP |
|[ReleaseEipAddress](https://docs.byteplus.com/en/docs/eip/ReleaseEipAddress) ||Error code added`InvalidEip.InUse`、`IdempotentParameterMismatch`、`InvalidParameter.ClientTokenMalformed`、`IdempotentProcessing`。<br><br><br>* New request parameter `ClientToken`, which is an optional parameter. |Releasing an EIP |


<span id="_30-march-2024"></span>
## 30 March 2024


|Module |API |Release Note |Region |
|---|---|---|---|
|EIP |All |The first release of all OpenAPI of EIP. |All |
