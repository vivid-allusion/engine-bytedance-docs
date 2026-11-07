---
title: "DeleteTransitRouterVpcAttachment - Deleting a VPC attachment"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterVpcAttachment"
---

Call DeleteTransitRouterVpcAttachment to delete the specified Virtual Private Cloud (VPC) attachment.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteTransitRouterVpcAttachment&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|Km5NT2">必选</span> `Example value: DeleteTransitRouterVpcAttachment`

The interface name. The current API name is `DeleteTransitRouterVpcAttachment`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|fiAvVB">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterAttachmentId ** <span data-label="purple">String </span><span data-api-tag="require|LYaBRc">必选</span> `Example value: tr-attach-7qthudw0ll6jmc****`

The ID of the network instance attachment. You can call the [DescribeTransitRouterVpcAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpcAttachments) API to obtain the ID of the Virtual Private Cloud (VPC) attachment.



**Force ** <span data-label="purple">Boolean </span><span data-api-tag="require|4SNJKC">必选</span> `Example value: false`

Describe whether to force delete the VPC attachment.


* true: Force delete.

* false: Not force delete.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DeleteTransitRouterVpcAttachment&Version=2020-04-01&TransitRouterAttachmentId=tr-attach-7qthudw0ll6jmc**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033735Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20250804113737249144220240A84298",
        "Action": "DeleteTransitRouterVpcAttachment",
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
|400 |InvalidTransitRouterAttachment.VpcWithRouteEntryToTransitRouter |The VPC of the specified attachment has customized route entries to the Transit Router. |The route table of the VPC associated with the specified attachment contains route entries pointing to the TR. |
|400 |InvalidTransitRouterAttachment.WithAssociation |The specified Transit Router has route table associations depending on the attachment. |Cannot delete the specified attachment because it contains an association forwarding route table. |
|400 |InvalidTransitRouterAttachment.WithMulticastDomainAssociation |The specified attachment has subnets associated to multicast domain, and can not be deleted. |Cannot delete the specified network instance attachment because it contains a subnet associated with a multicast domain. |
|400 |InvalidTransitRouterAttachment.WithMulticastGroup |The specified attachment has multicast sources or members within it, and can not be deleted. |Cannot delete the specified network instance attachment because its subnet contains elastic network interfaces that are configured as static sources or members of a multicast group.​ |
|400 |InvalidTransitRouterAttachment.WithRouteTablePropagation |The specified Transit Router has route table propagations depending on the attachment. |The specified network instance attachment has route learning configured and cannot be deleted. |
|400 |InvalidTransitRouterAttachment.WithStaticRouteEntry |The specified Transit Router has static route entries depending on the attachment. |The specified network instance attachment has static routes configured and cannot be deleted. |
|404 |InvalidTransitRouterAttachment.NotFound |The specified Transit Router attachment does not exist. |The specified network instance attachment does not exist. |
