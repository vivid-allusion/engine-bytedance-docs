---
title: "DeleteRouteTable - Deleting a route table"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DeleteRouteTable"
---

Call the DeleteRouteTable API to delete the specified route table.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* System route tables cannot be deleted using this API. When deleting a VPC, its VPCs are automatically deleted along with it.

* The custom route table is not associated with any subnets. If associated, disassociate. Once disassociated, any affected subnets will be automatically reassociated with the system route table.

* The gateway route table is not associated with any IPv4 gateways. If associated, call [DisassociateRouteTable](https://docs.byteplus.com/en/docs/vpc/DisassociateRouteTable) API to disassociate.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteRouteTable&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String </span><span data-api-tag="require|swu86W">必选</span> `Example value: DeleteRouteTable`

The interface name. The current API name is `DeleteRouteTable`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|EcfHUS">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**RouteTableId ** <span data-label="purple"> String </span><span data-api-tag="require|t69Ecn">必选</span> `Example value: vtb-2fdzao4h726f45******`

Route table ID pending deletion.

You can call the [DescribeRouteTableList](https://docs.byteplus.com/en/docs/vpc/DescribeRouteTableList) API to query the route table ID.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple"> String </span>`optional` `Example value: 2021062415303301022514515207C4****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DeleteRouteTable&Version=2020-04-01&RouteTableId=vtb-2fdzao4h726f45**** HTTP/1.1
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
        "Action": "DeleteRouteTable",
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
|400 |InvalidGatewayRouteTable.InUse |The specified route table has dependent resource of a gateway. |The specified route table is associated with a gateway and cannot be deleted. |
|400 |InvalidRouteTable.InUse |The specified route table has dependent resource of a route entry. |The specified route table contains route entries and cannot be deleted. |
|400 |InvalidRouteTable.InUse |The specified route table has dependent resource of a subnet. |The specified route table is associated with subnets and cannot be deleted. |
|400 |InvalidVpc.InvalidStatus |The specified VPC is not in the correct status for the request. |The specified VPC is in a state that cannot respond to this request. |
|403 |Forbidden |You are not authorized to perform operations on the specified route table. The specified route table is a system route table. |No sufficient permissions to perform this operation on the specified route table. The specified route table is the system route table. |
|404 |InvalidRouteTable.NotFound |The specified route table does not exist. |The specified route table does not exist. |
