---
title: "CreateTransitRouterPeerAttachment - Creating an inter-region attachment"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterPeerAttachment"
---

Call CreateTransitRouterPeerAttachment to create an inter\-region attachment.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateTransitRouterPeerAttachment&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|O0V2x8">必选</span> `Example: CreateTransitRouterPeerAttachment`

The interface name. The current API name is `CreateTransitRouterPeerAttachment`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|CYFwFH">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**Bandwidth ** <span data-label="purple">Integer </span>`optional` `Example: 10`

The bandwidth of the inter\-region attachment, measured in Mbps.

The maximum bandwidth must not exceed the remaining unallocated bandwidth of the specified TR bandwidth package.



**Tags.N.Key ** <span data-label="purple">String </span>`optional` `Example: k1`

The custom tag key of the inter\-region attachment.


* Must be 1 to 128 characters.

* Case\-sensitive. Must not start with `volc:` or `sys:` in any case combination.

* Must not start or end with a space.

* May include letters, digits, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), and at signs (@).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Duplicate tag keys are not allowed for the same resource.</div>


* <div data-tips="true" data-tips-type="tip">If you do not provide this parameter or leave it unset, it defaults to empty.</div>




**Tags.N.Value ** <span data-label="purple">String </span>`optional` `Example: v1`

The custom tag value of the inter\-region attachment.


* Must be 0 to 255 characters.

* Case\-sensitive. Must not start or end with a space.

* May include letters, digits, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), and at signs (@).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To provide this parameter, provide Tags.N.Key first.</div>




**TransitRouterAttachmentName ** <span data-label="purple">String </span>`optional` `Example: tr-attachment`

The name of the inter\-region attachment.


* Must start with a letter, digit, or Chinese character. May include letters, digits, Chinese characters, and the following symbols: periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters in length.

* If you do not provide this parameter or leave it unset, it defaults to the TR instance ID.



**Description ** <span data-label="purple">String </span>`optional` `Example: This peer attachment is used for test.`

The description of the inter\-region attachment.


* Must start with a letter, digit, or Chinese character. May include letters, digits, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), Chinese commas ( ， ), and Chinese periods ( 。 ).

* Must be 0 to 255 characters.

* If you do not provide this parameter or leave it unset, it defaults to an empty string.



**TransitRouterId ** <span data-label="purple">String </span><span data-api-tag="require|xa3JUO">必选</span> `Example: tr-7qthudw0ll6jmc****`

The ID of the local TR instance.



**PeerTransitRouterId ** <span data-label="purple">String </span><span data-api-tag="require|YorkEb">必选</span> `Example: tr-q3wuhuumlho9r****`

The ID of the peer TR instance. You can call [DescribeTransitRouters](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters) to obtain the ID of the TR instance.



**PeerTransitRouterRegionId ** <span data-label="purple">String </span><span data-api-tag="require|8Qgm0P">必选</span> `Example: cn-beijing`

The ID of the region where the peer TR instance belongs. You can review [Regions](https://docs.byteplus.com/en/docs/transitrouter/Product-Overview-05) to get the region ID.



**TransitRouterBandwidthPackageId ** <span data-label="purple">String </span>`optional` `Example: tr-bp-qw2u6ur8lhe2t****`

The ID of the TR bandwidth package. You can call the [DescribeTransitRouters](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters) API to obtain the ID of the TR instance.

When providing this parameter, you must provide `Bandwidth`. If you do not provide this parameter, `Bandwidth` should be omitted.



**ClientToken ** <span data-label="purple">String </span>`optional` `Example: test-client-token`

The Client Token that is used to ensure the request idempotency.


* This parameter value is auto\-generated by the client. Ensure uniqueness across requests, preventing duplicate actions caused by multiple client retries during API timeouts or server internal errors.

* Must not exceed 64 ASCII characters.

* If you do not set this parameter, idempotency check is not performed.



**PeerTransitRouterOwnerId ** <span data-label="purple">String </span>`optional` `Example: 2100****63`

The ID of the account that owns the peer TR instance.



**BandwidthType ** <span data-label="purple">String </span>`optional` `Example: BandwidthPackage`

The bandwidth allocation method for the inter\-region peering attachment.


* BandwidthPackage (default): Bandwidth is allocated from a bandwidth package.

* CloudDataTransfer: Bill by traffic via Cloud Data Transfer.



**LineOperator ** <span data-label="purple">String </span>`optional` `Example: ChinaUnicom`

The provider of the cross\-border bandwidth package. This parameter is required for cross\-border interconnection.


* ChinaUnicom: China Unicom.

* ChinaTelecom: China Telecom.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TransitRouterAttachmentId ** <span data-label="purple">String </span>`Example: tr-attach-12w7hruhlhlrd****`

The ID of the network instance attachment.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=CreateTransitRouterPeerAttachment&Version=2020-04-01&TransitRouterId=tr-7qthudw0ll6jmc****&PeerTransitRouterId=tr-q3wuhuumlho9r****&PeerTransitRouterRegionId=cn-beijing HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T034632Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "202508041146350532261280917BD6E8",
        "Action": "CreateTransitRouterPeerAttachment",
        "Version": "2020-04-01",
        "Service": "transitrouter",
        "Region": "cn-beijing"
    },
    "Result": {
        "TransitRouterAttachmentId": "tr-attach-12w7hruhlhlrd****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InstanceCreateOrderError |Failed to create cdt instance order. |The order placement failed. |
|400 |InvalidBandwidthType.NotSupported |The specified bandwidth type is not supported. |The specified bandwidth allocation method is not supported. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format specified for the description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format specified for the description is invalid. A description must not exceed 255 characters. |
|400 |InvalidInterRegionBandwidth.Existed |The specified inter region bandwidth existed. |The specified cross\-region bandwidth already exists. |
|400 |InvalidLineOperator.MissMatchBandwidthType |The specified line operator does not match the bandwidth type. |The specified line operator does not match the bandwidth allocation method. |
|400 |InvalidLocalRegionId.Conflict |The specified LocalRegionId and PeerRegionId are the same. |The specified local region is same as the peer region. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format specified for the name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format specified for the name is invalid. A name must not exceed 128 characters in length. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format specified for CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidPeerTransitRouter.InvalidBusinessStatus |The request is denied because the specified peer Transit Router is shut down due to arrears. |The specified peer TR is suspended due to overdue payments. The action is not supported. |
|400 |InvalidRegionId.Conflict |The LocalRegionId or PeerRegionId of peer attachment are different from bandwidth package. |The interconnected regions of the specified bandwidth package does not match those of the inter\-region attachment. |
|400 |InvalidTag.Disorder |The specified index order of tag is malformed. |The index order format specified for the tag is invalid |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The tag value is invalid. |
|400 |InvalidTransitRouter.InvalidBusinessStatus |The request is denied because the specified Transit Router is shut down due to arrears. |The specified TR is suspended due to arrears. The current action is not supported. |
|400 |InvalidTransitRouter.InvalidStatus |The specified Transit Router is not in the correct status for the request. |The specified TR cannot respond to the request due to its status. |
|400 |InvalidTransitRouterBandwidthPackage.InvalidStatus |The specified TransitRouter bandwidth package is being operated now. |The specified bandwidth package is in a status that cannot respond to this request. Retry later. |
|400 |InvalidTransitRouterBandwidthPackageId.MissMatchBandwidthType |The specified bandwidth package ID does not match the bandwidth type. |The specified bandwidth package ID does not match the bandwidth allocation method. |
|400 |InvalidTransitRouterPeer.InvalidAccount |The specified granted account is equal to the login account, please change the account to grant. |The specified account for authorization is the same as the current account. Change another account to authorize. |
|400 |InvalidTransitRouterPeerAttachment.PeerRegionIdConfict |The peer region id of the specified attachment conflicts with current region. |The peer region for the specified attachment must differ from the current region. |
|400 |InvalidTransitRouterPeerAttachment.PeerRegionNotSupported |The specified peer region does not support to create peer attachment. |The specified peer region does not support creating inter\-region attachments. |
|400 |InvalidTransitRouterPeerAttachment.PeerRegionTypeConflicts |The region type of specified peer region conflicts with the local region type. |The specified peer region conflicts with the current region in types. |
|400 |InvalidTransitRouterPeerAttachment.PeerTransitRouterInvalidStatus |The specified peer Transit Router is not in the correct status for the request. |The specified peer TR cannot respond to the request due to its status. |
|400 |InvalidTransitRouterPeerAttachment.SharedTransitRouter |The specified peer Transit Router is shared instance, and does not support to create peer attachment. |The specified peer TR is a shared instance, which does not support creating inter\-region attachments. |
|400 |InvalidTransitRouterRouteTableAssociation.TransitRouterMismatch |The specified route table and attachment do not belong to one same Transit Router. |The TR of the specified route table does not match the TR attached to the attachment. |
|400 |InvalidTransitRouterRouteTablePropagation.ASNConflict |Peer Transit Router ASN conflicts with local Transit Router ASN. |The peer TR has the same ASN as the current instance and cannot create route learning. |
|400 |LimitExceeded.CDTBandwidth |You've reached the maximum bandwidth limit. |You have reached the maximum number of CDT bandwidth that can be created per account. |
|400 |LimitExceeded.InterRegionBandwidth |The specified inter region bandwidth exceeds the available bandwidth of the bandwidth package. |The specified inter\-region bandwidth size exceeds the allocatable bandwidth of the bandwidth package. |
|400 |LimitExceeded.InterRegionBandwidth |The specified peer attachment bandwidth exceeds the lower limit. |The specified bandwidth size exceeds the minimum limit for the inter\-region bandwidth. |
|400 |LimitExceeded.PhysicalLineBandwidth |You’ve reached the bandwidth limit on the number of physical line. |You have reached the maximum bandwidth allocable to the DC Connection. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at a time. |You have reached the maximum of tags that can be processed in a single request. |
|400 |MainAccountNotSupportPaypalErr |You are requested to contact the main account to provide an alternative payment method other than Paypal before enabling the pay\-as\-you\-go products in BytePlus. |PayPal is not supported for postpaid products in this order. Contact your root account to add other payment methods. |
|400 |MissingParameter |The specified peer attachment with a bandwidth type assigned to it, needs to allocate an inter region bandwidth parameter. |The specified inter\-region attachment is billed by bandwidth package or traffic. Allocate cross\-region bandwidth. |
|400 |NotSupportPaypalErr |You are requested to provide an alternative payment method other than Paypal before enabling the pay\-as\-you\-go products in BytePlus. |PayPal is not supported for postpaid products in this order. Add other payment methods. |
|400 |QuotaExceeded.InterRegionPeerAttachment |You've reached the maximum number of inter region attachments that one transit router can have. |You have reached the maximum number of inter\-region attachments that can be created per TR. |
|400 |QuotaExceeded.PeerTransitRouterAttachment |You've reached the maximum number of attachments that one Transit Router can have in the peer region. |You have reached the maximum number of network instance ttachments for the specified peer TR. |
|400 |QuotaExceeded.TransitRouterAttachment |You've reached the maximum number of attachments that one Transit Router can have. |You have reached the maximum of network instances that you can create in a single TR. |
|400 |UnsupportedOperation.ExpiredStatus |The request on the specified bandwidth package is denied because the bandwidth package is expired. |The specified bandwidth package is expired. The action is not supported. |
|400 |UnsupportedOperation.OverdueStatus |The request on the specified bandwidth package is denied because the bandwidth package is shut down due to arrears. |The specified bandwidth package is suspended due to overdue payments. The action is not supported. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|403 |Forbidden.CreateTransitRouterPeerAttachment |You are not authorized to create peer attachment on Transit Router. |No permission to create inter\-region attachments. Enable the allowlist for inter\-region attachments. |
|403 |Forbidden.CrossBorderApprovalNotApplied |You cannot create cross\-border resources because you have not applied for cross\-border audit yet. |You did not submit a cross\-border qualification for review and cannot create cross\-border resources. |
|403 |Forbidden.CrossBorderApprovalPending |The specified request is denied because your cross\-border audit application is pending approval. |Your cross\-border application is still under review. Please wait for the business qualification to be approved before creating cross\-border resources. |
|403 |Forbidden.CrossBorderApprovalRejected |You cannot create cross\-border resources because your cross\-border audit application has been rejected. |You fail the cross\-border qualification review and cannot create cross\-border resources. |
|403 |Forbidden.CrossBorderUserFrozen |The specified request is denied because your account has been frozen for cross\-border. Please wait for the Service Provider to unfreeze it. |The cross\-border service under your account is suspended. Proceed after the line operator reactivates your service. |
|403 |Forbidden.EnablePeerTransitRouterRouteTablePropagation |You are not authorized to enable peer attachment route table propagation. |No permission to enable route learning for inter\-region attachment. Enable the allowlist. |
|403 |Forbidden.NoPermissionToOperate |You are not authorized to operate the specified resource. |No permission to manage the specified resource. |
|403 |Forbidden.TransitRouterIPv6 |You are not authorized to use ipv6 on Transit Router. |The IPv6 feature is not enabled for the TR. The action is not supported. |
|404 |InvalidPeerTransitRouter.NotFound |The specified peer Transit Router does not exist. |The specified peer TR does not exist. |
|404 |InvalidPeerTransitRouterRouteTable.NotFound |The specified route table of peer Transit Router does not exist. |The specified peer TR route table does not exist. |
|404 |InvalidRegionId.NotFound |The specified RegionId does not exist. |The specified region does not exist. |
|404 |InvalidTransitRouter.NotFound |The specified Transit Router does not exist. |The specified TR does not exist. |
|404 |InvalidTransitRouterBandwidthPackage.NotFound |The specified bandwidth package id does not exist. |The specified bandwidth package does not exist. |
|404 |InvalidTransitRouterRouteTable.NotFound |The specified route table does not exist. |The specified Transit Router (TR) route table does not exist. |
|409 |InvalidParameter.ParameterConflict |Cannot set the bandwidth when peer attachment has not associated bandwidth package or bandwidth type. |The inter\-region attachment does not support setting cross\-region bandwidth because it is not added to the bandwidth package. |
|409 |InvalidTransitRouterAttachment.Conflict |The specified instance has already been attached to the Transit Router. |The specified network instance has been added to the specified TR. Duplicate action is not supported. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
