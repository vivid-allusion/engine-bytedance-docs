---
title: "UnassignIpv6Addresses - Deleting an IPv6 private IP address"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/UnassignIpv6Addresses"
---

Call the UnassignIpv6Addresses API to release the private IPv6 address from the specified network interface.

<div data-tips="true" data-tips-type="default">Description</div>


<div data-tips="true" data-tips-type="default">IPv6 is currently in Beta stage. If you need a trial, please contact your account manager.</div>


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=UnassignIpv6Addresses&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|rjlfDy">必选</span> `Example value: UnassignIpv6Addresses`

The interface name. The current API name is `UnassignIpv6Addresses`.



**Version ** <span data-label="purple"> string  </span><span data-api-tag="require|800HBn">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**NetworkInterfaceId ** <span data-label="purple"> String  </span><span data-api-tag="require|iZ1kPD">必选</span> `Example value: eni-bp1fg655nh68xyz9****`

Network Interface ID.

You can call the [DescribeNetworkInterfaces](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces) API to query the network interface ID.



**Ipv6Address.N ** <span data-label="purple"> String  </span><span data-api-tag="require|pr2ag5">必选</span> `Example value: 2408:4008:55b:XXXX:XXXX:922:96c4:e0`

Private IPv6 address to be released.


* Parameter \- N: Indicates the serial number of the private IPv6 address. The value range depends on the number of private IPv6 addresses currently assigned to the network interface.

* Separate multiple private IPv6 addresses with ampersands ( & ).



**ClientToken ** <span data-label="purple"> String  </span>`optional` `Example value: 123e4567-e89b-12d3-a456-42665544****`

Client Token that is used to ensure the request idempotency.


* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple"> String </span>`optional` `Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=UnassignIpv6Addresses&Version=2020-04-01&NetworkInterfaceId=eni-bp1fg655nh68xyz9****&Ipv6Address.1=2408:4008:55b:XXXX:XXXX:922:96c4:e0&Ipv6Address.2=2408:4008:55b:XXXX:XXXX:5eb5:eadc:cda1 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UnassignIpv6Addresses",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |InvalidEip.InUse |The specified EIP is being operated by another request. |The specified EIP is being operated by another request. Try again later. |
|400 |InvalidEni.InvalidStatus |The specified elastic network interface is not in the correct status for the request. |The specified Elastic Network Interface is not in a status that can respond to this request. |
|400 |InvalidEni.InvalidType |The type of specified elastic network interface is illegal for the request. |The specified type of elastic network interface cannot process this request. |
|400 |InvalidEni.UnassignFirstIPv6Address |The first IPv6 address of ipv6 only ENI is forbidden to unassign. |The first IPv6 address of an IPv6\-only ENI cannot be deleted. |
|400 |InvalidEni.UnassignIPv6AddressAsNextHop |The IPv6 address of ENI as next hop is forbidden to unassign. |The IPv6 address of an ENI cannot be deleted if it is configured as a route next hop. |
|400 |InvalidIpv6.Malformed |The specified IPv6 address is malformed. |The specified IPv6 address is invalid. |
|400 |InvalidIpv6Prefix.Malformed |The specified ipv6 prefix is malformed. |The specified IPv6 prefix is invalid. |
|400 |InvalidPrivateIp.Malformed |The specified private ip is malformed. |The specified private IP address is invalid. |
|400 |InvalidVpcEip.InUse |The specified vpc eip is being operated by another request. |The specified EIP is being operated by another request. Try again later. |
|400 |OrderError |Failed to create an order in one step. |Failed to create and pay for the order. |
|400 |QuotaExceeded.BandwidthPackage |You've reached the limit on the EIP number of that you can add to bandwidth package. |The maximum EIPs that you can add to the Bandwidth Package have been reached. |
|400 |QuotaExceeded.IPv6Gateway |You've reached the limit on the number of IPv6 egress only rule per IPv6 gateway that you can create. |The maximum number of Egress Only rules allowed per IPv6 Gateway has been reached. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic network interface. The owner of the specified elastic network interface is not in sharing. |No permission to perform actions on the specified elastic network interface. The specified Elastic Network Interface (ENI) is not owned by a user in the sharing list. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic network interface. The specified elastic network interface is a service\-managed elastic network interface. |No permission to perform actions on the specified elastic network interface. The specified elastic network interface is managed by a cloud product. |
|404 |InvalidEniId.NotFound |The specified elastic network interface does not exist. |The specified elastic network interface does not exist. |
|409 |InvalidIPv6Prefix.Conflict |The specified IPv6 prefix is in use. |The specified IPv6 prefix is currently in use. |
