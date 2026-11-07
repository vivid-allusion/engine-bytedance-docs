---
title: "ModifyIpv6AddressBandwidth - Modifying IPv6 Internet bandwidth"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/ModifyIpv6AddressBandwidth"
---

Call the ModifyIpv6AddressBandwidth API to modify the bandwidth cap of an IPv6 Internet bandwidth.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Decreasing bandwidth cap may affect business traffic and lead to packet loss. Evaluate the possible impacts of the action on your business and proceed with caution.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|QX2eCj">必选</span> `Example: ModifyIpv6AddressBandwidth`

The action to perform. Value: **ModifyIpv6AddressBandwidth**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|6f8q60">必选</span> `Example: 2020-04-01`

The API version. The current version is **2020\-04\-01**.



**AllocationId ** <span data-label="purple">String </span><span data-api-tag="require|qjrJ8f">必选</span> `Example: eip-2zaiwb7ujxscd****`

The ID of the IPv6 Internet bandwidth.



**Bandwidth ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The bandwidth cap of the IPv6 Internet bandwidth. Unit: Mbps.


* Pay\-by\-data\-transfer: Value ranges from 1 to 200.

* Pay\-by\-bandwidth\-cap: Value ranges from 1 to 1000.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 2021062415303301022514515207C4****`

The request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=ModifyIpv6AddressBandwidth&Version=2020-04-01&AllocationId=eip-2zaiwb7ujxscd****&Bandwidth=100 HTTP/1.1
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
        "Action": "ModifyIpv6AddressBandwidth",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****"
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
|400 |InvalidAlb.InvalidStatus |The specified ALB is not in the correct status for the request. Current ALB has been frozen. |The specified Application Load Balancer (ALB) cannot respond to this request due to its status. The current ALB is frozen. |
|400 |InvalidBandwidth.Malformed |The specified bandwidth is malformed.Ensure that bandwidth is not smaller than 1. |The specified bandwidth is invalid. Ensure the value is not less than 1 when specifying bandwidth. |
|400 |InvalidClb.InvalidStatus |The specified CLB is not in the correct status for the request. Current CLB has been frozen. |The specified Classic Load Balancer (CLB) cannot respond to this request due to its status. The current CLB is frozen. |
|400 |InvalidEip.InUse |The specified EIP is being operated by another request. |The specified Elastic IP Address (EIP) is being processed by another request. Try again later. |
|400 |InvalidInstance.InvalidStatus |The specified ECS is not in the correct status for the request. Current ECS has been frozen. |The specified Elastic Compute Service (ECS) instance cannot respond to this request due to its status. The current ECS is frozen. |
|400 |InvalidIpv6.InUse |The specified IPv6 address bandwidth is being operated by another request. |The specified IPv6 Internet bandwidth is being processed by another request. Try again later. |
|400 |InvalidIpv6.InvalidStatus |The specified IPv6 address bandwidth is not in the correct status for the request. The specified IPv6 address bandwidth is in freeze. |The specified IPv6 Internet bandwidth or VPC cannot respond to this request due to its status. The current Internet bandwidth is frozen. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format specified for CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |LimitExceeded.BandwidthPerEip |You've reached the limit on the bandwidth of elastic ip that you can create. |The EIP bandwidth cap has been reached. |
|400 |LimitExceeded.Ipv6 |You've reached the limit on the bandwidth of IPv6 address that you can create. |IPv6 address bandwidth cap has been reached.​ |
|400 |MissingParameter |The request is missing a required parameter. |This request does not contain the required parameter. |
|400 |OrderError |Failed to create an order in one step. |Failed to create and pay for the order. |
|400 |PreOrderError |Failed to create pre order. |Failed to create configuration order. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is rejected because the sum of both account balance and available coupons are less than USD 100. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account balance and available vouchers are less than 100 yuan in total. |The action request on this instance is denied because the account is in arrears. |
|403 |Forbidden |You are not authorized to perform operations on the specified EIP. The specified EIP is a service\-managed EIP. |No permission to manage the specified EIP. The specified EIP is managed by the cloud product. |
|404 |InvalidEip.GetInstanceDetail |Get instance detail failed. |Failed to retrieve instance information |
|404 |InvalidInstance.NotFound |The specified instance does not exist. |The specified instance does not exist. |
|404 |InvalidIpv6.NotFound |The specified IPv6 address bandwidth does not exist. |The specified IPv6 Internet bandwidth does not exist. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
