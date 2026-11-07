---
title: "UntagResources - Deleting a custom tag from a resource"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/UntagResources"
---

Call the UntagResources API to delete custom tags from a resource

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=UntagResources&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|6WUtR7">必选</span> `Example value: UntagResources`

The interface name. The current API name is `UntagResources`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|Djw11Z">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**Resource type ** <span data-label="purple">String </span><span data-api-tag="require|ypfq6f">必选</span> `Example value: transitrouter`

The resource type. Values:


* transitrouter: TR instance.

* transitrouterroutetable: TR route table.

* transitrouterattachment: Attachment, including network instance attachments (VPC, VPN, or DC Gateway) and inter\-region attachments.

* transitrouterbandwidthpackage: TR bandwidth package.



**ResourceIds.N** <span data-label="purple">String</span> <span data-api-tag="require|eTWxgC">必选</span>`Example value: tr-273sdsdsxxxxxp8u2j****`

The resource ID.


* N represents the serial number of the resource ID, with a maximum of 50 per call.

* Separate multiple resource IDs with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters">DescribeTransitRouters</a> API to get the ID of the “transitrouter” resource.</div>


* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteTables">DescribeTransitRouterRouteTables</a> API to get the ID of the “transitrouterroutetable” resource.</div>


* <div data-tips="true" data-tips-type="tip">Based on the type of the resource to be tagged, you can call <a href="https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpcAttachments">DescribeTransitRouterVpcAttachments</a>, <a href="https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpnAttachments">DescribeTransitRouterVpnAttachments</a>, <a href="https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterDirectConnectGatewayAttachments">DescribeTransitRouterDirectConnectGatewayAttachments</a>, or <a href="https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterPeerAttachments">DescribeTransitRouterPeerAttachments</a> to get the ID of the “transitrouterattachment” resource.</div>


* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterBandwidthPackages">DescribeTransitRouterBandwidthPackages</a> API to get the ID of the “transitrouterbandwidthpackage” resource.</div>




**TagKeys.N ** <span data-label="purple">String </span><span data-api-tag="require|DQywnm">必选</span> `Example: k1`

The tag key of the custom tag to be deleted. Must not start or end with a space.


* N represents the serial number of the tag key, ranging from 1 to 20.

* Separate multiple tag keys with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the specified Tags.N.Key does not exist or has been disassociated, a success response is returned by default without an error.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=UntagResources&Version=2020-04-01&ResourceType=transitrouter&ResourceIds.1=tr-273sdsdsxxxxxp8u2j****&TagKeys.1=k1 HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250815T040737Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250815/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20250815120741074189044074189428",
        "Action": "UntagResources",
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
|400 |InvalidResourceType.Malformed |The specified parameter resource type is invalid. |The resource type is invalid. |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |LimitExceeded.Resource |You've reached the limit on the number of resources that you can operate at a time. |You have reached the maximum number of tags that you can manage in a single request. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at a time. |You have reached the maximum number of tags that you can manage in a single request. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
