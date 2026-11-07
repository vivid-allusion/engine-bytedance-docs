---
title: "AssociateRouteTable - Attaching a route table"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/AssociateRouteTable"
---

Call the AssociateRouteTable API to associate a subnet with a specified route table.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* The subnet and route table to be associated must be in the same VPC.

* A subnet must be associated with exactly one route table. After creation, a subnet is automatically associated with the system route table by default.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=AssociateRouteTable&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String </span><span data-api-tag="require|9WNLom">必选</span> `Example value: AssociateRouteTable`

The interface name. The current API name is `AssociateRouteTable`.



**Version ** <span data-label="purple"> String </span><span data-api-tag="require|WjgbL7">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**RouteTableId ** <span data-label="purple"> String  </span><span data-api-tag="require|iAyWoX">必选</span> `Example value: vtb-2fdzao4h726f45******`

Route table ID.

You can call the [DescribeRouteTableList](https://docs.byteplus.com/en/docs/vpc/DescribeRouteTableList) API to query the route table ID.



**SubnetId ** <span data-label="purple">String </span>`optional` `Example: subnet-2fdzaou4liw3k5oxruv******`

ID of the subnet to be associated.

You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API to query the subnet ID.



**GatewayType ** <span data-label="purple"> String  </span>`optional` `Example value: 123e4567-e89b-12d3-a456-42665544****`

Gateway type. Valid values:


* Ipv4Gateway: IPv4 Gateway

* Ipv6Gateway: IPv6 Gateway



**GatewayId** <span data-label="purple">String</span> `optional` `Example value: ipv4gw-bp1fgnh68xyz9****`

Gateway ID.


* You can call the [DescribeIpv4Gateways](https://docs.byteplus.com/en/docs/vpc/DescribeIpv4Gateways) API to query the IPv4 Gateway ID.

* You can call the [DescribeIpv6Gateways](https://docs.byteplus.com/en/docs/IPv6/DescribeIpv6Gateways) API to query the ID of IPv6 Gateway.



**ClientToken ** <span data-label="purple"> String </span>`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

Client Token that is used to ensure the request idempotency.


* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple"> String </span>`optional` `Example value: 2021062415303301022514515207C4****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=AssociateRouteTable&Version=2020-04-01&RouteTableId=vtb-2fdzao4h726f45****&SubnetId=subnet-2fdzaou4liw3k5oxruv**** HTTP/1.1
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
        "Action": "AssociateRouteTable",
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


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidGatewayType.Malformed |The specified gateway type is malformed. |The specified gateway type is invalid. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidRouteTable.VpcMismatch |The specified route table and subnet are in different VPC. |The specified route table and subnet are not in the same VPC. |
|400 |InvalidRouteTableAssociateGateway.Malformed |The specified gateway route table cannot be associated with the gateway. IPv4 gateway and IPv6 gateway must be associated with the same gateway route table. |The specified gateway route table cannot be bound to this gateway. Both the IPv4 gateway and IPv6 gateway must be bound to the same gateway route table. |
|400 |InvalidRouteTableAssociateType.Malformed |The specified route table associate type is malformed. |The specified route table binding type is invalid. |
|400 |InvalidRouteTableGateway.VpcMismatch |The specified route table and gateway are in different VPC. |The specified route table and gateway are not in the same VPC. |
|400 |InvalidSubnet.InvalidStatus |The specified subnet is not in the correct status for the request. |The specified subnet is in a state that cannot process this request. |
|400 |InvalidVpc.InvalidStatus |The specified VPC is not in the correct status for the request. |The specified VPC is in a state that cannot respond to this request. |
|403 |Forbidden |You are not authorized to perform operations on the specified gateway. The specified gateway is associated with a route table. |No sufficient permissions to perform this operation on the specified gateway. The specified gateway is already associated with a route table. |
|403 |Forbidden |You are not authorized to perform operations on the specified route table. The specified route table is associated with the gateway. |No sufficient permissions to perform this operation on the specified route table. The specified route table is already bound to a gateway. |
|403 |Forbidden |You are not authorized to perform operations on the specified route table. The specified route table is associated with this subnet. |No sufficient permissions to perform this operation on the specified route table. The specified route table is already bound to the specified subnet. |
|404 |InvalidIpv4Gateway.NotFound |The specified Ipv4Gateway does not exist. |The specified IPv4 gateway does not exist. |
|404 |InvalidIpv6Gateway.NotFound |The specified Ipv6Gateway does not exist. |The specified IPv6 Gateway does not exist. |
|404 |InvalidRouteTable.NotFound |The specified route table does not exist. |The specified route table does not exist. |
|404 |InvalidSubnet.NotFound |The specified subnet does not exist. |The specified subnet does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
