---
title: "ModifyTransitRouterPeerAttachmentAttributes - Modifying basic information for a specified inter-region attachment"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterPeerAttachmentAttributes"
---

Call the ModifyTransitRouterPeerAttachmentAttributes API to modify the basic information of a specified inter\-region attachment.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyTransitRouterPeerAttachmentAttributes&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|Vy3Tck">必选</span> `Example: ModifyTransitRouterPeerAttachmentAttributes`

The interface name. The current API name is `ModifyTransitRouterPeerAttachmentAttributes`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|GvfHP5">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterAttachmentId ** <span data-label="purple">String </span><span data-api-tag="require|0JkOnJ">必选</span> `Example: tr-attach-7qthudw0ll6jmc****`

The ID of the inter\-region attachment. You can call [DescribeTransitRouterPeerAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterPeerAttachments) to obtain the inter\-region attachment ID.



**TransitRouterAttachmentName ** <span data-label="purple">String </span>`optional` `Example: tr-attachment`

The name of the inter\-region attachment.


* Must start with a letter, digit, or Chinese character. May include letters, digits, Chinese characters, and the following symbols: periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters in length.

* If you do not provide this parameter or leave it unset, the original name is retained.



**Description ** <span data-label="purple">String </span>`optional` `Example: This peer attachment is used for test.`

The description of the inter\-region attachment.


* Must start with a letter, digit, or Chinese character. May include letters, digits, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), Chinese commas ( ， ), and Chinese periods ( 。 ).

* Must be 0 to 255 characters.

* If you do not provide this parameter or leave it unset, the original description is retained.



**TransitRouterBandwidthPackageId ** <span data-label="purple">String </span>`optional` `Example: tr-bp-qw2u6ur8lhe2t****`

The ID of the TR bandwidth package. You can call [DescribeTransitRouterBandwidthPackages](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterBandwidthPackages) to obtain the ID of the TR bandwidth package.

When providing this parameter, you must provide "Bandwidth". If you do not provide this parameter, "Bandwidth" should be omitted.



**Bandwidth ** <span data-label="purple">Integer </span>`optional` `Example: 10`

The bandwidth of the inter\-region attachment, measured in Mbps.

The maximum bandwidth must not exceed the remaining unallocated bandwidth of the specified TR bandwidth package.



**BandwidthType ** <span data-label="purple">String </span>`optional` `Example: BandwidthPackage`

The bandwidth allocation method for the inter\-region peering attachment.


* BandwidthPackage: Bandwidth is allocated from a bandwidth package.

* CloudDataTransfer: Bill by traffic via Cloud Data Transfer.



**LineOperator ** <span data-label="purple">String </span>`optional` `Example: ChinaUnicom`

The provider of the cross\-border bandwidth package. This parameter is required for cross\-border interconnection.


* ChinaUnicom: China Unicom.

* ChinaTelecom: China Telecom.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=ModifyTransitRouterPeerAttachmentAttributes&Version=2020-04-01&TransitRouterAttachmentId=tr-attach-7qthudw0ll6jmc**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T034759Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20250804114802076189175083AF2848",
        "Action": "ModifyTransitRouterPeerAttachmentAttributes",
        "Version": "2020-04-01",
        "Service": "transitrouter",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InstanceCreateOrderError |Failed to create cdt instance order. |The order placement failed. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format specified for the description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format specified for the description is invalid. A description must not exceed 255 characters. |
|400 |InvalidLineOperator.MissMatchBandwidthType |The specified line operator does not match the bandwidth type. |The specified line operator does not match the bandwidth allocation method. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format specified for the name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format specified for the name is invalid. A name must not exceed 128 characters in length. |
|400 |InvalidRegionId.Conflict |The LocalRegionId or PeerRegionId of peer attachment are different from bandwidth package. |The interconnected regions of the specified bandwidth package does not match those of the inter\-region attachment. |
|400 |InvalidTransitRouter.InvalidStatus |The specified Transit Router is not in the correct status for the request. |The specified TR cannot respond to the request due to its status. |
|400 |InvalidTransitRouterAttachment.InvalidStatus |The specified Transit Router Attachment is not in the correct status for the request. |The specified network instance attachment cannot respond to the request due to its status. |
|400 |InvalidTransitRouterBandwidthPackage.InvalidStatus |The specified TransitRouter bandwidth package is being operated now. |The specified bandwidth package cannot respond to this request due to its status. Retry later. |
|400 |InvalidTransitRouterPeerAttachment.PeerTransitRouterInvalidStatus |The specified peer Transit Router is not in the correct status for the request. |The specified peer TR cannot respond to the request due to its status. |
|400 |LimitExceeded.CDTBandwidth |You've reached the maximum bandwidth limit. |You have reached the maximum number of CDT bandwidth that can be created per account. |
|400 |LimitExceeded.InterRegionBandwidth |The specified inter region bandwidth exceeds the available bandwidth of the bandwidth package. |The specified inter\-region bandwidth size exceeds the allocatable bandwidth of the bandwidth package. |
|400 |LimitExceeded.InterRegionBandwidth |The specified peer attachment bandwidth exceeds the lower limit. |The specified bandwidth size exceeds the minimum limit for the inter\-region bandwidth. |
|400 |LimitExceeded.PhysicalLineBandwidth |You’ve reached the bandwidth limit on the number of physical line. |You have reached the maximum bandwidth allocable to the DC Connection. |
|400 |MainAccountNotSupportPaypalErr |You are requested to contact the main account to provide an alternative payment method other than Paypal before enabling the pay\-as\-you\-go products in BytePlus. |PayPal is not supported for postpaid products in this order. Contact your root account to add other payment methods. |
|400 |MissingParameter |The specified peer attachment with a bandwidth type assigned to it, needs to allocate an inter region bandwidth parameter. |The specified inter\-region attachment is billed by bandwidth package or traffic. Allocate cross\-region bandwidth. |
|400 |NotSupportPaypalErr |You are requested to provide an alternative payment method other than Paypal before enabling the pay\-as\-you\-go products in BytePlus. |PayPal is not supported for postpaid products in this order. Add other payment methods. |
|400 |UnsupportedOperation.ExpiredStatus |The request on the specified bandwidth package is denied because the bandwidth package is expired. |The specified bandwidth package is expired. The action is not supported. |
|400 |UnsupportedOperation.OverdueStatus |The request on the specified bandwidth package is denied because the bandwidth package is shut down due to arrears. |The specified bandwidth package is suspended due to overdue payments. The action is not supported. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|403 |Forbidden.CrossBorderApprovalNotApplied |You cannot create cross\-border resources because you have not applied for cross\-border audit yet. |You did not submit a cross\-border qualification for review and cannot create cross\-border resources. |
|403 |Forbidden.CrossBorderApprovalPending |The specified request is denied because your cross\-border audit application is pending approval. |Your cross\-border application is still under review. Please wait for the business qualification to be approved before creating cross\-border resources. |
|403 |Forbidden.CrossBorderApprovalRejected |You cannot create cross\-border resources because your cross\-border audit application has been rejected. |You fail the cross\-border qualification review and cannot create cross\-border resources. |
|403 |Forbidden.CrossBorderUserFrozen |The specified request is denied because your account has been frozen for cross\-border. Please wait for the Service Provider to unfreeze it. |The cross\-border service under your account is suspended. Proceed after the line operator reactivates your service. |
|403 |Forbidden.NoPermissionToOperate |You are not authorized to operate the specified resource. |No permission to manage the specified resource. |
|404 |InvalidInterRegionBandwidth.NotFound |The specified inter region bandwidth does not exist. |The specified cross\-region bandwidth does not exist. |
|404 |InvalidTransitRouterAttachment.NotFound |The specified Transit Router attachment does not exist. |The specified network instance attachment does not exist. |
|404 |InvalidTransitRouterBandwidthPackage.NotFound |The specified bandwidth package id does not exist. |The specified bandwidth package does not exist. |
|409 |InvalidParameter.ParameterConflict |Cannot set the bandwidth when peer attachment has not associated bandwidth package or bandwidth type. |The inter\-region attachment cannot set cross\-region bandwidth because neither a bandwidth allocation method nor a bandwidth package has been specified. |
