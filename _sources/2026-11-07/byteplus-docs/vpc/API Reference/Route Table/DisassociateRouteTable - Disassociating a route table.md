---
title: "DisassociateRouteTable - Disassociating a route table"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DisassociateRouteTable"
---

Call the DisassociateRouteTable API to disassociate the route table.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* System route tables cannot be disassociated from subnets using this API. You can call the [AssociateRouteTable](https://docs.byteplus.com/en/docs/vpc/AssociateRouteTable) API to associate a subnet with a custom route table. After association, the subnet is automatically disassociated from the system route table.

* When a subnet is disassociated from a custom route table, it is automatically reassociated with the system route table.

* Gateway route table is currently in Beta stage. If you need a trial, please contact your account manager.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DisassociateRouteTable&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String </span><span data-api-tag="require|oASPIb">必选</span> `Example value: DisassociateRouteTable`

The interface name. The current API name is `DisassociateRouteTable`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|LkjuEM">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**RouteTableId ** <span data-label="purple"> String  </span><span data-api-tag="require|igTHIC">必选</span> `Example value: vpc-2fdz8g5nruzuo5oxr******`

Route table ID

You can call the [DescribeRouteTableList](https://docs.byteplus.com/en/docs/vpc/DescribeRouteTableList) API to query the route table ID.



**SubnetId ** <span data-label="purple"> String </span>`optional` `Example value: subnet-2fdzaou4liw3k5o******`

The ID of the subnet.

You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API to query the subnet ID.



**GatewayType ** <span data-label="purple"> String  </span>`optional` `Example value: Ipv4Gateway`

Gateway type. Valid values:


* Ipv4Gateway: IPv4 Gateway

* Ipv6Gateway: IPv6 Gateway


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">IPv4 Gateway and IPv6 Gateway are currently in Beta stage. If you need a trial, please contact your account manager.</div>




**GatewayId ** <span data-label="purple"> String  </span>`optional` `Example value: ipv4gw-bp1fgnh68xyz9****`

Gateway ID.


* You can call the [DescribeIpv4Gateways](https://docs.byteplus.com/en/docs/vpc/DescribeIpv4Gateways) API to query the IPv4 Gateway ID.

* You can call the [DescribeIpv6Gateways](https://docs.byteplus.com/en/docs/IPv6/DescribeIpv6Gateways) API to query the ID of IPv6 Gateway.



**ClientToken ** <span data-label="purple">String </span>`optional` `Example value: 123e4567-e89b-12d3-a456-42665544****`

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
GET /?Action=DisassociateRouteTable&Version=2020-04-01&RouteTableId=vpc-2fdz8g5nruzuo5oxr******&SubnetId=subnet-2fdzaou4liw3k5o****** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DisassociateRouteTable",
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


|**Status code** |**Error codes** |**Error message** |**Explain** |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidGatewayType.Malformed |The specified gateway type is malformed. |The specified gateway type is invalid. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidRouteTable.GatewayMismatch |The specified route table is not associated with the specified gateway. |The specified route table is not associated with the specified gateway. |
|400 |InvalidRouteTable.VpcMismatch |The specified route table and subnet are in different VPC. |The specified route table and subnet are not in the same VPC. |
|400 |InvalidRouteTableAssociateType.Malformed |The specified route table associate type is malformed. |The specified route table binding type is invalid. |
|400 |InvalidSubnet.InvalidStatus |The specified subnet is not in the correct status for the request. |The specified subnet is in a state that cannot process this request. |
|400 |InvalidVpc.InvalidStatus |The specified VPC is not in the correct status for the request. |The specified VPC is in a state that cannot respond to this request. |
|400 |OperationUnsupported.RouteTable |The route table can not be disassociated. |Specified route tables cannot be disassociated. |
|400 |OperationUnsupported.SystemRouteTable |System route table can not be disassociated. |System route tables cannot be disassociated. |
|404 |InvalidRouteTable.NotFound |The specified route table does not exist. |The specified route table does not exist. |
|404 |InvalidSubnet.NotFound |The specified subnet does not exist. |The specified subnet does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
