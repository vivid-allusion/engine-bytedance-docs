---
title: "AssociateTransitRouterTrafficQosMarkingPolicyToAttachment - Associating a traffic marking policy with an attachment"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/AssociateTransitRouterTrafficQosMarkingPolicyToAttachment"
---

Call the AssociateTransitRouterTrafficQosMarkingPolicyToAttachment API to associate a traffic marking policy with a Transit Router (TR) attachment.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Traffic marking may be impacted by enabling a traffic marking policy. If the bandwidth allocated to the scheduling queue matched by the traffic marking is insufficient for actual business requirements, normal service forwarding may be impacted.​

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=AssociateTransitRouterTrafficQosMarkingPolicyToAttachment&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String</span> <span data-api-tag="require|HGH4pk">必选</span>`Example value: AssociateTransitRouterTrafficQosMarkingPolicyToAttachment`

The interface name. The current API name is `AssociateTransitRouterTrafficQosMarkingPolicyToAttachment`.



**Version ** <span data-label="purple"> String </span><span data-api-tag="require|bfjFaS">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterAttachmentId ** <span data-label="purple"> String </span><span data-api-tag="require|sQf520">必选</span> `Example: tr-attach-13n2l4c****`

The attachment ID. Currently, only inter\-region attachments are supported. You can call [DescribeTransitRouterPeerAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterPeerAttachments) to obtain the ID of the inter\-region attachment.



**TransitRouterTrafficQosMarkingPolicyId ** <span data-label="purple"> String </span><span data-api-tag="require|w1sBRi">必选</span> `Example value: tr-tmp-hy13n2l4c6c0v****`

ID of the traffic marking policy. You can call the [DescribeTransitRouterTrafficQosMarkingPolicies](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterTrafficQosMarkingPolicies) API to obtain the ID of the traffic marking policy.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=AssociateTransitRouterTrafficQosMarkingPolicyToAttachment&Version=2020-04-01&TransitRouterAttachmentId=tr-attach-13n2l4c****&TransitRouterTrafficQosMarkingPolicyId=tr-tmp-hy13n2l4c6c0v**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250731T090108Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250731/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
  "ResponseMetadata": {
    "RequestId": "202507311701120060441162019A0618",
    "Action": "AssociateTransitRouterTrafficQosMarkingPolicyToAttachment",
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


|**Status code** |**Error codes** |**Error message** |**Explanation** |
|---|---|---|---|
|400 |InvalidTransitRouter.InvalidBusinessStatus |The request is denied because the specified Transit Router is shut down due to arrears. |The specified Transit Router (TR) is suspended due to overdue payments. Action unsupported. |
|400 |InvalidTransitRouter.InvalidStatus |The specified Transit Router is not in the correct status for the request. |The specified Transit Router (TR) is in a status that cannot respond to the request. |
|400 |InvalidTransitRouterAttachment.InvalidStatus |The specified Transit Router Attachment is not in the correct status for the request. |The specified network instance attachment is in a status that cannot respond to the request. |
|400 |InvalidTransitRouterTrafficQosMarkingPolicyAssociation.AttachmentTypeNotSupport |The specified Transit Router attachment type does not support to associate traffic qos marking policy. |The type of the specified network instance attachment does not support configuring traffic marking policies. |
|400 |InvalidTransitRouterTrafficQosMarkingPolicyAssociation.TransitRouterMismatch |The specified attachment and traffic qos marking policy do not belong to the same Transit Router. |The specified network instance attachment and the traffic marking policy are not associated with the same TR. |
|403 |Forbidden.NoPermissionToOperate |You are not authorized to operate the specified resource. |No permission to manage the specified resource. |
|404 |InvalidTransitRouterAttachment.NotFound |The specified Transit Router attachment does not exist. |The specified network instance attachment does not exist. |
|404 |InvalidTransitRouterTrafficQosMarkingPolicy.NotFound |The specified Transit Router traffic qos marking policy does not exist. |The specified traffic marking policy does not exist. |
|409 |InvalidTransitRouterTrafficQosMarkingPolicyAssociation.Conflict |The specified Transit Router attachment has already been associated with a traffic qos marking policy. |The specified network instance attachment has a configured traffic marking policy. Duplicate configuration is not permitted. |
