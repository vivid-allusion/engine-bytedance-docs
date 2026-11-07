---
title: "AssociateTransitRouterForwardPolicyTableToAttachment - Associating a forwarding policy with an attachment"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/AssociateTransitRouterForwardPolicyTableToAttachment"
---

Call the AssociateTransitRouterForwardPolicyTableToAttachment API to associate the specified forwarding policy with a network instance attachment or an inter\-region attachment.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=AssociateTransitRouterForwardPolicyTableToAttachment&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|YJhjoS">必选</span> `Example: AssociateTransitRouterForwardPolicyTableToAttachment`

The interface name. The current API name is `AssociateTransitRouterForwardPolicyTableToAttachment`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|lPJMG6">必选</span> `example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterAttachmentId ** <span data-label="purple">String </span><span data-api-tag="require|CJOEaI">必选</span> `Example: tr-attach-13n2l4c****`

The ID of the network instance attachment.


* You can call the [DescribeTransitRouterVpcAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpcAttachments) API to obtain the ID of the Virtual Private Cloud (VPC) attachment.

* You can call the [DescribeTransitRouterVpnAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpnAttachments) API to obtain the ID of the Virtual Private Network (VPN) attachment.

* You can call the [DescribeTransitRouterDirectConnectGatewayAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterDirectConnectGatewayAttachments) API to obtain the ID of the Direct Connect (DC) Gateway attachment.



**TransitRouterForwardPolicyTableId ** <span data-label="purple">String </span><span data-api-tag="require|9teNkL">必选</span> `Example: tr-fpt-1i5i8khf9m58gae5kcx6****`

ID of the forwarding policy. You can call the [DescribeTransitRouterForwardPolicyTables](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterForwardPolicyTables) API to get the ID of the forwarding policy.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=AssociateTransitRouterForwardPolicyTableToAttachment&Version=2020-04-01&TransitRouterAttachmentId=tr-attach-13n2l4c****&TransitRouterForwardPolicyTableId=tr-fpt-1i5i8khf9m58gae5kcx6**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250815T034525Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250815/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "2025081511452814100607922028DC57",
        "Action": "AssociateTransitRouterForwardPolicyTableToAttachment",
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
|400 |InvalidTransitRouterAttachment.InvalidBusinessStatus |The request is denied because the specified Transit Router attachment is shut down due to arrears. |The specified attachment is suspended due to overdue payments. Action unsupported. |
|400 |InvalidTransitRouterAttachment.InvalidStatus |The specified Transit Router Attachment is not in the correct status for the request. |The specified network instance attachment is in a status that cannot respond to the request. |
|400 |InvalidTransitRouterForwardPolicyTableAssociation.TransitRouterMismatch |The specified attachment and forward policy table do not belong to the same Transit Router. |The specified network instance attachment and the forwarding policy do not belong to the same Transit Router (TR). |
|403 |Forbidden.NoPermissionToOperate |You are not authorized to operate the specified resource. |No permission to manage the specified resource. |
|404 |InvalidTransitRouterAttachment.NotFound |The specified Transit Router attachment does not exist. |The specified network instance attachment does not exist. |
|404 |InvalidTransitRouterForwardPolicyTable.NotFound |The specified Transit Router forward policy table does not exist. |The specified forwarding policy does not exist. |
|409 |InvalidTransitRouterForwardPolicyTableAssociation.Conflict |The specified Transit Router attachment has already been associated to a forward policy table. |The specified network instance attachment has a configured forwarding policy. Duplicate configuration is not permitted. |
