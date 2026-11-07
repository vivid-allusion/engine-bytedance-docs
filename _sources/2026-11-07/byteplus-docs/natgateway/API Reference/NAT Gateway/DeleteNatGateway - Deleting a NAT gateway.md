---
title: "DeleteNatGateway - Deleting a NAT gateway"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/DeleteNatGateway"
---

Call the DeleteNatGateway API to delete a NAT gateway instance.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

To delete a NAT gateway using this API, all the following conditions must be met:


* The NAT gateway is a Pay\-as\-you\-go instance or an expired Subscription instance. Subscription NAT gateways cannot be deleted before expiration. To release a gateway early, you must unsubscribe it. For details, see Unsubscription.

* The NAT gateway contains no SNAT entries. For details, see [DescribeSnatEntries](https://docs.byteplus.com/en/docs/natgateway/DescribeSnatEntries) and [DeleteSnatEntry](https://docs.byteplus.com/en/docs/natgateway/DeleteSnatEntry).

* The NAT gateway contains no DNAT entries. For details, see [DescribeDnatEntries](https://docs.byteplus.com/en/docs/natgateway/DescribeDnatEntries) and [DeleteDnatEntry](https://docs.byteplus.com/en/docs/natgateway/DeleteDnatEntry).

* The NAT gateway has no elastic IP address (EIP) associated. For details, see [DescribeNatGatewayAttributes](https://docs.byteplus.com/en/docs/natgateway/DescribeNatGatewayAttributes) and [DisassociateEipAddress](https://docs.byteplus.com/en/docs/eip/DisassociateEipAddress).

* The NAT gateway is not managed by other cloud services. If it is managed, first confirm that the NAT gateway is no longer needed according to the managed system tag and the corresponding cloud service, and then release the management.

> When a NAT gateway is managed by a cloud service, that service can utilize the gateway's capabilities and control its permissions. Specifically, users can only view and modify the managed NAT gateway; they cannot delete it.

> During management, the NAT gateway is tagged by a management system tag with the key as volc:{ServiceCode}:ServiceManagedis. An example of such a key is volc:vke:ServiceManaged.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteNatGateway&groupName=NAT%E7%BD%91%E5%85%B3&serviceCode=natgateway&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|NwKSzq">必选</span> `Example: DeleteNatGateway`

The action that you want to perform. Value: DeleteNatGateway.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|qruebD">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**NatGatewayId ** <span data-label="purple">string </span><span data-api-tag="require|inMuKH">必选</span> `Example: ngw-vv3t043k05sm****`

ID of the NAT gateway.

You can call the [DescribeNatGateways](https://docs.byteplus.com/en/docs/natgateway/DescribeNatGateways) API to query the NAT gateway ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 2021062415303301022514515207C4****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DeleteNatGateway&Version=2020-04-01&NatGatewayId=ngw-vv3t043k05sm**** HTTP/1.1
Host: natgateway.cn-beijing.byteplusapi.com.cn
Service: natgateway
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DeleteNatGateway",
        "Version": "2020-04-01",
        "Service": "natgateway",
        "Region": "cn-beijing"
    },
    "Result":{
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/natgateway/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. |This request does not contain required parameters. |
|400 |InvalidNatGateway.InvalidBillingType |The specified NAT gateway is not in the correct billing type for the request. |The specified NAT gateway cannot respond to this request due to its billing method. |
|400 |InvalidNatGateway.InvalidStatus |The specified NAT gateway is not in the correct status for the request. |The specified NAT gateway cannot respond to this request due to its status. |
|400 |InvalidNatGateway.InUse |The specified NAT gateway has dependent resource of an EIP. |The specified NAT gateway is associated with the EIP and cannot be deleted. |
|400 |InvalidNatGateway.InUse |The specified NAT gateway has dependent resource of ip bandwidth limit rule. |The specified NAT gateway cannot be deleted because it still has IP rate\-limiting rules configured. |
|403 |Forbidden |You are not authorized to perform operations on the specified NAT gateway. The specified NAT gateway is a service\-managed NAT gateway. |No permission to perform actions on the specified NAT gateway. The specified NAT gateway is managed by a service. |
|404 |InvalidNatGateway.NotFound |The specified NAT gateway does not exist. |The specified NAT gateway does not exist. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|412 |InvalidNatGateway.DependenceDnatEntryExist |The specified NAT gateway has a dependency on DNAT entry. |The request cannot be processed because the specified NAT gateway has dependencies on DNAT rules. |
|412 |InvalidNatGateway.DependenceSnatEntryExist |The specified NAT gateway has a dependency on SNAT entry. |The request cannot be processed because the specified NAT gateway has dependencies on SNAT rules. |
|412 |InvalidNatGateway.DependenceNatIPExist |The specified NAT gateway has a dependency on nat ip. |The request cannot be processed because the specified NAT gateway has dependencies on NAT IP addresses. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
