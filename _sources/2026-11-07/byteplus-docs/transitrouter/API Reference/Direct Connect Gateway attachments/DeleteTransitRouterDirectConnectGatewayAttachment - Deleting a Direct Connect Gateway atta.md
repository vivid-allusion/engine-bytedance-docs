---
title: "DeleteTransitRouterDirectConnectGatewayAttachment - Deleting a Direct Connect Gateway attachment"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterDirectConnectGatewayAttachment"
---

Call DeleteTransitRouterDirectConnectGatewayAttachment to delete the specified Direct Connect (DC) Gateway attachment.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Deleting a network instance attachment will remove the association between the network instance and the Transit Router (TR) instance, causing communication failure between network instances. Proceed with caution.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteTransitRouterDirectConnectGatewayAttachment&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|eRqe5n">必选</span> `Example value: DeleteTransitRouterDirectConnectGatewayAttachment`

The interface name. The current API name is `DeleteTransitRouterDirectConnectGatewayAttachment`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|r2viRM">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**Force ** <span data-label="purple">Boolean </span><span data-api-tag="require|pGbs2C">必选</span> `Example value: false`

Describe whether to force delete the DC Gateway attachment.


* true: Force delete.

* false: Not force delete.



**TransitRouterAttachmentId ** <span data-label="purple">String </span><span data-api-tag="require|vXrvHd">必选</span> `Example value: tr-attach-13n2l4c****`

The ID of the network instance attachment. You can call the [DescribeTransitRouterDirectConnectGatewayAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterDirectConnectGatewayAttachments) API to obtain the ID of the Direct Connect (DC) Gateway attachment.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DeleteTransitRouterDirectConnectGatewayAttachment&Version=2020-04-01&TransitRouterAttachmentId=tr-attach-13n2l4c**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T034452Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20250804114456052025032201B117B5",
        "Action": "DeleteTransitRouterDirectConnectGatewayAttachment",
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
|400 |InvalidTransitRouterAttachment.InvalidStatus |The specified Transit Router Attachment is not in the correct status for the request. |The specified network instance attachment is in a status that cannot respond to the request. |
|400 |InvalidTransitRouterAttachment.WithAssociation |The specified Transit Router has route table associations depending on the attachment. |Cannot delete the specified attachment because it contains an association forwarding route table. |
|400 |InvalidTransitRouterAttachment.WithIPv4StaticRouteEntry |The specified TR attachment can not be modified as IPv6 only, since there are IPv4 static routes in TR route tables depending on the attachment. |The TR route table contains an IPv4 static route pointing to this network instance. Therefore, disabling IPv4 for this attachment is not permitted. |
|400 |InvalidTransitRouterAttachment.WithRouteTablePropagation |The specified Transit Router has route table propagations depending on the attachment. |The specified network instance attachment has route learning configured and cannot be deleted. |
|400 |InvalidTransitRouterAttachment.WithStaticRouteEntry |The specified Transit Router has static route entries depending on the attachment. |The specified network instance attachment has static routes configured and cannot be deleted. |
|403 |Forbidden.NoPermissionToOperate |You are not authorized to operate the specified resource. |No permission to manage the specified resource. |
|404 |InvalidTransitRouterAttachment.NotFound |The specified Transit Router attachment does not exist. |The specified network instance attachment does not exist. |
