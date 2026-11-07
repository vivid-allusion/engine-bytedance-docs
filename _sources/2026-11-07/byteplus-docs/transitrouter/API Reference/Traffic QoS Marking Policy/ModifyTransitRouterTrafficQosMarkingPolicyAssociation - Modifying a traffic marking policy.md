---
title: "ModifyTransitRouterTrafficQosMarkingPolicyAssociation - Modifying a traffic marking policy associated with an attachment"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterTrafficQosMarkingPolicyAssociation"
---

Call the ModifyTransitRouterTrafficQosMarkingPolicyAssociation API to modify the traffic marking policy associated with a Transit Router (TR) attachment.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Traffic marking may be impacted by modifying a traffic marking policy associated with an attachment. If the bandwidth allocated to the scheduling queue matched by the traffic marking is insufficient for actual business requirements, normal service forwarding may be impacted.​

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyTransitRouterTrafficQosMarkingPolicyAssociation&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|8FsCOa">必选</span> `Example value: ModifyTransitRouterTrafficQosMarkingPolicyAssociation`

The interface name. The current API name is `ModifyTransitRouterTrafficQosMarkingPolicyAssociation`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|ToXq3g">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterAttachmentId ** <span data-label="purple">String </span><span data-api-tag="require|oIrPHi">必选</span> `Example: tr-attach-13n2l4c****`

The attachment ID.

Currently, only inter\-region attachments are supported. You can call [DescribeTransitRouterPeerAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterPeerAttachments) to obtain the ID of the inter\-region attachment.



**TransitRouterTrafficQosMarkingPolicyId ** <span data-label="purple">String </span><span data-api-tag="require|h1BRQQ">必选</span> `Example value: tr-tmp-hy13n2l4c6c0v****`

ID of the traffic marking policy. You can call the [DescribeTransitRouterTrafficQosMarkingPolicies](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterTrafficQosMarkingPolicies) API to obtain the ID of the traffic marking policy.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ModifyTransitRouterTrafficQosMarkingPolicyAssociation&Version=2020-04-01&TransitRouterAttachmentId=tr-attach-13n2l4c****&TransitRouterTrafficQosMarkingPolicyId=tr-tmp-hy13n2l4c6c0v**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250731T090601Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250731/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20250731170608217076195158235217",
        "Action": "ModifyTransitRouterTrafficQosMarkingPolicyAssociation",
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
|400 |InvalidTransitRouterTrafficQosMarkingPolicyAssociation.TransitRouterMismatch |The specified attachment and traffic qos marking policy do not belong to the same Transit Router. |The specified network instance attachment and the traffic marking policy are not associated with the same TR. |
|403 |Forbidden.NoPermissionToOperate |You are not authorized to operate the specified resource. |No permission to manage the specified resource. |
|404 |InvalidTransitRouterAttachment.NotFound |The specified Transit Router attachment does not exist. |The specified network instance attachment does not exist. |
|404 |InvalidTransitRouterAttachment.TrafficQosMarkingPolicyNotAssociated |The specified Transit Router attachment has not been associated with any traffic qos marking policy, and the update operation is invalid. |The specified network instance attachment has no traffic marking policy configured. Therefore, update is invalid. |
|404 |InvalidTransitRouterTrafficQosMarkingPolicy.NotFound |The specified Transit Router traffic qos marking policy does not exist. |The specified traffic marking policy does not exist. |
