---
title: "AssociateTransitRouterAttachmentToRouteTable - Associating a TR route table with an  attachment"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/AssociateTransitRouterAttachmentToRouteTable"
---

Call the AssociateTransitRouterAttachmentToRouteTable API to associate the specified route table with a network instance attachment.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=AssociateTransitRouterAttachmentToRouteTable&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|vCilrL">必选</span> `Example value: AssociateTransitRouterAttachmentToRouteTable`

The interface name. The current API name is `AssociateTransitRouterAttachmentToRouteTable`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|t2rBgn">必选</span>`Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterAttachmentId ** <span data-label="purple">String </span><span data-api-tag="require|Lg8H35">必选</span>`Example: tr-attach-13n2l4c****`

The ID of the network instance attachment.


* You can call the [DescribeTransitRouterVpcAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpcAttachments) API to obtain the ID of the Virtual Private Cloud (VPC) attachment.

* You can call the [DescribeTransitRouterVpnAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpnAttachments) API to obtain the ID of the Virtual Private Network (VPN) attachment.

* You can call the [DescribeTransitRouterDirectConnectGatewayAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterDirectConnectGatewayAttachments) API to obtain the ID of the Direct Connect (DC) Gateway attachment.

* You can call the [DescribeTransitRouterPeerAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterPeerAttachments) API to obtain the ID of the inter\-region attachment.



**TransitRouterRouteTableId ** <span data-label="purple">String </span><span data-api-tag="require|zgzKtP">必选</span> `Example: tr-rtb-hy13n2l4c6c0v****`

The ID of the route table associated with the Transit Router (TR) instance. You can call the [DescribeTransitRouterRouteTables](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteTables) API to obtain the TR route table ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=AssociateTransitRouterAttachmentToRouteTable&Version=2020-04-01&TransitRouterAttachmentId=tr-attach-a*******&TransitRouterRouteTableId=tr-rtb-hy13n2l4c6c0v**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250721T114234Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250721/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "202507211940210690630421693CF526",
        "Action": "AssociateTransitRouterAttachmentToRouteTable",
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
|400 |InvalidTransitRouter.InvalidBusinessStatus |The request is denied because the specified Transit Router is shut down due to arrears. |The specified Transit Router (TR) is suspended due to overdue payments. Action unsupported. |
|400 |InvalidTransitRouter.InvalidStatus |The specified Transit Router is not in the correct status for the request. |The specified Transit Router (TR) is in a status that cannot respond to the request. |
|400 |InvalidTransitRouterAttachment.InvalidStatus |The specified Transit Router Attachment is not in the correct status for the request. |The specified network instance attachment is in a status that cannot respond to the request. |
|400 |InvalidTransitRouterRouteTableAssociation.TransitRouterMismatch |The specified route table and attachment do not belong to one same Transit Router. |The TR of the specified route table does not match the TR attached to the network instance attachment. |
|404 |InvalidTransitRouterAttachment.NotFound |The specified Transit Router attachment does not exist. |The specified network instance attachment does not exist. |
|404 |InvalidTransitRouterRouteTable.NotFound |The specified route table does not exist. |The specified Transit Router (TR) route table does not exist. |
|409 |InvalidTransitRouterRouteTableAssociation.Conflict |The specified Transit Router attachment has already associated to a route table. |The specified network instance attachment is configured with an association forwarding route table. Duplicate configuration is not permitted. |
