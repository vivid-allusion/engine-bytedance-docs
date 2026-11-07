---
title: "EnableTransitRouterRouteTablePropagation - Creating route learning"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/EnableTransitRouterRouteTablePropagation"
---

Call the EnableTransitRouterRouteTablePropagation API to create route learning for the specified network instance attachment.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=EnableTransitRouterRouteTablePropagation&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|L0Vq1m">必选</span> `Example: EnableTransitRouterRouteTablePropagation`

The interface name. The current API name is `EnableTransitRouterRouteTablePropagation`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|BhRyYm">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterRouteTableId ** <span data-label="purple">String </span><span data-api-tag="require|kdqNzJ">必选</span> `Example: tr-rtb-1i5i8khf9m58gae5kcx6****`

The ID of the route table associated with the TR instance. You can call the [DescribeTransitRouterRouteTables](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteTables) API to obtain the TR route table ID.



**TransitRouterAttachmentId ** <span data-label="purple">String </span><span data-api-tag="require|aqTsJD">必选</span> `Example: tr-attach-13n2l4c****`

The ID of the network instance attachment.


* You can call [DescribeTransitRouterVpcAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpcAttachments) to obtain the ID of the VPC attachment.

* You can call the [DescribeTransitRouterDirectConnectGatewayAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterDirectConnectGatewayAttachments) API to obtain the ID of the Direct Connect (DC) Gateway attachment.

* You can call the [DescribeTransitRouterPeerAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterPeerAttachments) API to obtain the ID of the inter\-region attachment.



**PropagationGranularity ** <span data-label="purple">String </span> `Optional` `Example: Subnet`

The route learning granularity.


* Subnet (default): Learn routes per subnet

* VPC: Learn routes per Virtual Private Cloud (VPC).



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=EnableTransitRouterRouteTablePropagation&Version=2020-04-01&TransitRouterRouteTableId=tr-rtb-1i5i8khf9m58gae5kcx6****&TransitRouterAttachmentId=tr-attach-13n2l4c**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250815T030906Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250815/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "202508151109102441861352156DA9A8",
        "Action": "EnableTransitRouterRouteTablePropagation",
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


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidTransitRouter.InvalidBusinessStatus |The request is denied because the specified Transit Router is shut down due to arrears. |The specified TR is suspended due to overdue payments. Action unsupported. |
|400 |InvalidTransitRouter.InvalidStatus |The specified Transit Router is not in the correct status for the request. |The specified TR is in a status that cannot respond to the request. |
|400 |InvalidTransitRouterAttachment.InvalidStatus |The specified Transit Router Attachment is not in the correct status for the request. |The specified network instance attachment is in a status that cannot respond to the request. |
|400 |InvalidTransitRouterRoutePropagation.TransitRouterMismatch |The specified route table and attachment do not belong to one same Transit Router. |The TR of the specified route table does not match the TR attached to the network instance attachment. |
|400 |InvalidTransitRouterRouteTablePropagation.ASNConflict |Peer Transit Router ASN conflicts with local Transit Router ASN. |The peer TR has the same ASN as the current instance and cannot create route learning. |
|400 |InvalidTransitRouterRouteTablePropagation.PropagationGranularityInvalid |The specified Transit Router route table propagation granularity is invalid, only VPC and Subnet are supported. |The specified route learning granularity is invalid. |
|400 |InvalidTransitRouterRouteTablePropagation.UnsupportedAttachment |The specified Transit Router attachment does not support enabling route table propagation. |The specified TR attachment does not support configuring route learning. |
|400 |InvalidTransitRouterRouteTablePropagation.UnsupportedPropagationGranularity |The specified Transit Router attachment does not support enabling route table propagation with granularity. |The specified TR attachment does not support configuring learning granularity. |
|403 |Forbidden.CreateRouteTablePropagationWithVpnAttachment |You are not authorized to create route table propagation with vpn attachment on Transit Router. |No permission to create route learning for VPN attachments. Enable the allowlist for VPN attachments with a routing type of BGP on the TR. |
|403 |Forbidden.CreateTransitRouterBgpVpnAttachment |You are not authorized to create BGP vpn attachment on Transit Router. |No permission to create VPN attachments using BGP. Enable the associated allowlist in the TR. |
|403 |Forbidden.EnablePeerTransitRouterRouteTablePropagation |You are not authorized to enable peer attachment route table propagation. |No permission to enable route learning for inter\-region attachment. Enable the allowlist. |
|404 |InvalidTransitRouter.NotFound |The specified Transit Router does not exist. |The specified TR does not exist. |
|404 |InvalidTransitRouterAttachment.NotFound |The specified Transit Router attachment does not exist. |The specified network instance attachment does not exist. |
|404 |InvalidTransitRouterPeerAttachment.PeerAttachmentNotFound |The specified peer attachment does not exist. |The specified inter\-region network instance attachment does not exist. |
|404 |InvalidTransitRouterRouteTable.NotFound |The specified route table does not exist. |The specified Transit Router (TR) route table does not exist. |
|409 |InvalidTransitRouterRouteTablePropagation.Conflict |The specified Transit Router route table propagation on the specified attachment already exists. |The specified TR has route learning configured. |
