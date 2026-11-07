---
title: "AcceptTransitRouterPeerAttachment - Accepting a cross-account inter-region attachment"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/AcceptTransitRouterPeerAttachment_-_Accepting_a_cross-account_inter-region_attachment"
---

Call AcceptTransitRouterPeerAttachment to accept an inter\-region attachment spanning multiple accounts.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=AcceptTransitRouterPeerAttachment&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|bLlHzd">必选</span> `Example: AcceptTransitRouterPeerAttachment`

The interface name. The current API name is `AcceptTransitRouterPeerAttachment`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|uLKbNi">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterAttachmentId ** <span data-label="purple">String </span><span data-api-tag="require|IpvPOu">必选</span> `Example: tr-attach-abb******`

The ID of the inter\-region attachment.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=AcceptTransitRouterPeerAttachment&Version=2020-04-01&TransitRouterAttachmentId=tr-attach-abb****** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "AcceptTransitRouterPeerAttachment",
        "Version": "2020-04-01",
        "Service": "transitrouter",
        "Region": "cn-beijing"
    }
  "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InstanceCreateOrderError |Failed to create cdt instance order. |The order placement failed. |
|400 |InvalidTransitRouter.InvalidStatus |The specified Transit Router is not in the correct status for the request. |The specified TR cannot respond to the request due to its status. |
|400 |InvalidTransitRouterAttachment.InvalidStatus |The specified Transit Router Attachment is not in the correct status for the request. |The specified network instance attachment cannot respond to the request due to its status. |
|400 |LimitExceeded.CDTBandwidth |You've reached the maximum bandwidth limit. |You have reached the maximum number of CDT bandwidth that can be created per account. |
|400 |MainAccountNotSupportPaypalErr |You are requested to contact the main account to provide an alternative payment method other than Paypal before enabling the pay\-as\-you\-go products in BytePlus. |PayPal is not supported for postpaid products in this order. Contact your root account to add other payment methods. |
|400 |NotSupportPaypalErr |You are requested to provide an alternative payment method other than Paypal before enabling the pay\-as\-you\-go products in BytePlus. |PayPal is not supported for postpaid products in this order. Add other payment methods. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|403 |Forbidden.CrossBorderApprovalNotApplied |You cannot create cross\-border resources because you have not applied for cross\-border audit yet. |You did not submit a cross\-border qualification for review and cannot create cross\-border resources. |
|403 |Forbidden.CrossBorderApprovalPending |The specified request is denied because your cross\-border audit application is pending approval. |Your cross\-border application is still under review. Please wait for the business qualification to be approved before creating cross\-border resources. |
|403 |Forbidden.CrossBorderApprovalRejected |You cannot create cross\-border resources because your cross\-border audit application has been rejected. |You fail the cross\-border qualification review and cannot create cross\-border resources. |
|403 |Forbidden.CrossBorderUserFrozen |The specified request is denied because your account has been frozen for cross\-border. Please wait for the Service Provider to unfreeze it. |The cross\-border service under your account is suspended. Proceed after the line operator reactivates your service. |
|403 |Forbidden.NoPermissionToOperate |You are not authorized to operate the specified resource. |No permission to manage the specified resource. |
|404 |InvalidTransitRouter.NotFound |The specified Transit Router does not exist. |The specified TR does not exist. |
|404 |InvalidTransitRouterAttachment.NotFound |The specified Transit Router attachment does not exist. |The specified network instance attachment does not exist. |
|404 |InvalidTransitRouterRouteTable.NotFound |The specified route table does not exist. |The specified TR route table does not exist. |
