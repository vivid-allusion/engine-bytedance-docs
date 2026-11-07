---
title: "ReleaseIpv6AddressBandwidth - Releasing IPv6 Internet bandwidth"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/ReleaseIpv6AddressBandwidth"
---

Call the ReleaseIpv6AddressBandwidth API to release a specified IPv6 Internet bandwidth.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

You cannot manually disable IPv6 Internet bandwidth for public dual\-stack Application Load Balancer (ALB) instance. When [deleting a public dual-stack ALB instance](https://docs.byteplus.com/en/docs/clb/Managing-instances), the system automatically deletes its IPv6 Internet bandwidth.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|uV0V9r">必选</span> `Example: ReleaseIpv6AddressBandwidth`

The action to perform. Value: **ReleaseIpv6AddressBandwidth**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|QYowPE">必选</span> `Example: 2020-04-01`

The API version. The current version is **2020\-04\-01**.



**AllocationId ** <span data-label="purple">String </span>`optional` `Example: eip-2zaiwb7ujxscd****`

The ID of the IPv6 Internet bandwidth.



**AllocationIds.N ** <span data-label="purple">String </span>`optional` `Example: eip-2zaiwb7ujxscd****`

IPv6 Internet bandwidth IDs to batch release.


* N represents the sequence number of a tag key. Valid range: 1–100.

* Separate multiple parameters with ampersands (&).



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 2021062415303301022514515207C4****`

The request ID.



**PreOrderNumber ** <span data-label="purple">String </span>`Example: BO702327073660581****`

The order ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=ReleaseIpv6AddressBandwidth&Version=2020-04-01&AllocationId=eip-2zaiwb7ujxscd**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: vpc
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "ReleaseIpv6AddressBandwidth",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****",
        "PreOrderNumber": "BO702327073660581****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

For more information, see [Common error codes](https://docs.byteplus.com/en/docs/IPv6/Public_error_codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvaildIpv4.NotSupport |The specified IPv4 address does not support this operation. |The specified IPv4 address does not support this action. |
|400 |InvalidEip.InUse |The specified EIP has dependent resource of a bandwidth package. |The specified EIP is being processed by another request. Try again later. |
|400 |InvalidEip.InUse |The specified EIP is being operated by another request. |The specified EIP cannot be released because it is referenced by a Bandwidth Package. |
|400 |InvalidIpv6.InUse |The specified IPv6 address bandwidth is being operated by another request. |The specified IPv6 Internet bandwidth is being processed by another request. Try again later. |
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |This request contains an invalid or unsupported parameter. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format specified for CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |MissingParameter |The request is missing a required parameter. |This request does not contain the required parameter. |
|400 |OrderError |Failed to create an order in one step. |Failed to create and pay for the order. |
|400 |PreOrderError |Failed to create pre order. |Failed to create configuration order. |
|400 |QuotaExceeded.IPv6Bandwidth |You've reached the limit on the number of IPv6 bandwidth that you can create. |You have reached the maximum number of IPv6 Internet bandwidths that can be enabled. |
|400 |QuotaExceeded.PremiumBGPEip |Premium BGP EIP number exceeded quota. |You have reached the maximum of EIPs with premium BGP that can be applied for. |
|403 |Forbidden |You are not authorized to perform operations on the specified IPv6 address which is managed by ALB. |No permission to manage the specified Elastic IP Address (EIP). The specified EIP is managed by the cloud product. |
|403 |Forbidden |You are not authorized to perform operations on the specified EIP. The specified EIP is a service\-managed EIP. |No permission to manage the IPv6 address of the ALB. |
|404 |InvalidIpv6.NotFound |The specified IPv6 address bandwidth does not exist. |The specified IPv6 Internet bandwidth does not exist. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
