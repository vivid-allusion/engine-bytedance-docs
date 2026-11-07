---
title: "DissociateTransitRouterMulticastDomain - Detaching multicast domain from subnet"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DissociateTransitRouterMulticastDomain"
---

Call the DissociateTransitRouterMulticastDomain API to disassociate the multicast domain from the specified subnet.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DissociateTransitRouterMulticastDomain&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|tA0V7d">必选</span> `Example: DissociateTransitRouterMulticastDomain`

The interface name. The current API name is `DissociateTransitRouterMulticastDomain`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|yrqXdy">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterMulticastDomainId ** <span data-label="purple">String </span><span data-api-tag="require|RbTKg6">必选</span> `Example value: tr-md-hy13n2l4c6c0v****`

The ID of the multicast domain. You can call [DescribeTransitRouterMulticastDomains](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterMulticastDomains) to obtain the ID of the multicast domain.



**TransitRouterAttachmentId ** <span data-label="purple">String </span><span data-api-tag="require|O4WZ4u">必选</span> `Example value: tr-attach-12w7hruhlhlrd****`

The ID of the network instance attachment. You can call the [DescribeTransitRouterVpcAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpcAttachments) API to obtain the ID of the Virtual Private Cloud (VPC) attachment.



**SubnetId** <span data-label="purple">String</span> <span data-api-tag="require|zxVCNj">必选</span> `Example value: subnet-p0w9alkte4w2htrqe****`

ID of the subnet.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DissociateTransitRouterMulticastDomain&Version=2020-04-01&TransitRouterMulticastDomainId=tr-md-hy13n2l4c6c0v****&TransitRouterAttachmentId=tr-attach-12w7hruhlhlrd****&SubnetId=subnet-p0w9alkte4w2htrqe**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250721T122256Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250721/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "202504012153111790280050711B****",
        "Action": "DissociateTransitRouterMulticastDomain",
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
|400 |InvalidTransitRouterMulticastDomain.InvalidStatus |The specified Transit Router multicast domain is not in the correct status for the request. |The specified multicast domain cannot respond to this request due to its status. |
|400 |InvalidTransitRouterMulticastDomainAssociation.WithMulticastGroup |There are multicast members or sources within the specified subnet, which cannot be dissociated from the multicast domain. |The specified subnet cannot be disassociated with the multicast domain because it contains multicast members or multicast sources. |
|403 |Forbidden.NoPermissionToOperate |You are not authorized to operate the specified resource. |No permission to manage the specified resource. |
|404 |InvalidSubnet.MulticastDomainNotAssociated |The specified subnet has not been associated to the multicast domain, and the dissociating operation is invalid. |This multicast domain is not associated with the specified subnet. Therefore, disassociation is invalid. |
|404 |InvalidTransitRouterAttachment.NotFound |The specified Transit Router attachment does not exist. |The specified network instance attachment does not exist. |
|404 |InvalidTransitRouterMulticastDomain.NotFound |The specified Transit Router multicast domain does not exist. |The specified multicast domain does not exist. |
