---
title: "DisableTransitRouterRouteTablePropagation - Deleting route learning"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DisableTransitRouterRouteTablePropagation"
---

Call the DisableTransitRouterRouteTablePropagation API to delete the specified route learning rule.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DisableTransitRouterRouteTablePropagation&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|Lw10H9">必选</span> `Example value: DisableTransitRouterRouteTablePropagation`

The interface name. The current API name is `DisableTransitRouterRouteTablePropagation`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|4GYvx8">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterRouteTableId ** <span data-label="purple">String </span><span data-api-tag="require|UoFDrZ">必选</span>`Example: tr-rtb-hy13n2l4c6c0v****`

The ID of the route table associated with the Transit Router (TR) instance. You can call the [DescribeTransitRouterRouteTables](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteTables) API to obtain the TR route table ID.



**TransitRouterAttachmentId ** <span data-label="purple">String </span><span data-api-tag="require|7BAqBe">必选</span> `Example: tr-attach-a*******`

The ID of the network instance attachment.


* You can call the [DescribeTransitRouterVpcAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpcAttachments) API to obtain the ID of the Virtual Private Cloud (VPC) attachment.

* You can call the [DescribeTransitRouterDirectConnectGatewayAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterDirectConnectGatewayAttachments) API to obtain the ID of the Direct Connect (DC) Gateway attachment.

* You can call the [DescribeTransitRouterPeerAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterPeerAttachments) API to obtain the ID of the inter\-region attachment.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DisableTransitRouterRouteTablePropagation&Version=2020-04-01&TransitRouterRouteTableId=tr-rtb-hy13n2l4c6c0v****&TransitRouterAttachmentId=tr-attach-a******* HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250815T031049Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250815/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20250815111053010154206181C61DA3",
        "Action": "DisableTransitRouterRouteTablePropagation",
        "Version": "2020-04-01",
        "Service": "transitrouter",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|Status code |Error codes |Error message |Explanation |
|---|---|---|---|
|400 |InvalidTransitRouter.InvalidStatus |The specified Transit Router is not in the correct status for the request. |The specified Transit Router (TR) is in a status that cannot respond to the request. |
|403 |Forbidden.NoPermissionToOperate |You are not authorized to operate the specified resource. |No permission to manage the specified resource. |
|404 |InvalidTransitRouterAttachment.NotFound |The specified Transit Router attachment does not exist. |The specified network instance attachment does not exist. |
|404 |InvalidTransitRouterRouteTable.NotFound |The specified route table does not exist. |The specified Transit Router (TR) route table does not exist. |
|404 |InvalidTransitRouterRouteTablePropagation.NotFound |The specified Transit Router route table propagation does not exist. |The specified TR does not have route learning configuration. |
