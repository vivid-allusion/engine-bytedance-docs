---
title: "TagResources - Adding a custom tag to a resource"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/TagResources"
---

Call the TagResources API to add custom tags to a resource.

<span id=".5L2_55So6K-05piO"></span>
## Notes


* ​​If multiple tags with the same key are applied to a resource, the most recent value overwrites any previous ones.​

* Each resource supports up to 50 custom tags, while a single API call can add a maximum of 20 tags.​​

* In a request parameter such as Tags.N.a, the "N" represents the serial number of the tag entry. It must be assigned a value in strict numerical order, starting from 1 up to 50. Separate multiple tags with ampersands (&). Each tag key pairs one tag value.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=TagResources&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> string </span><span data-api-tag="require|LEtzlt">必选</span> `Example value: TagResources`

The interface name. The current API name is `TagResources`.



**Version ** <span data-label="purple"> String </span><span data-api-tag="require|oYwdhA">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**ResourceType ** <span data-label="purple"> String  </span><span data-api-tag="require|MD_BB2">必选</span> `Example value: transitrouter`

The resource type. Values:


* transitrouter: TR instance.

* transitrouterroutetable: TR route table.

* transitrouterattachment: Attachment, including network instance attachments (VPC, VPN, or DC Gateway) and inter\-region attachments.

* transitroutermulticastdomain: TR multicast domain.

* transitrouterbandwidthpackage: TR bandwidth package.



**ResourceIds.N ** <span data-label="purple"> String </span><span data-api-tag="require|9ZOnxb">必选</span> `Example value: tr-2fe6fszjgeznk5oxruv0u****`

The resource ID.


* N represents the serial number of the resource ID, ranging from 1 to 50.

* Separate multiple resource IDs with ampersands (&).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters">DescribeTransitRouters</a> API to get the ID of the “transitrouter” resource.</div>


* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteTables">DescribeTransitRouterRouteTables</a> API to get the ID of the “transitrouterroutetable” resource.</div>


* <div data-tips="true" data-tips-type="default">Based on the type of the resource to be tagged, you can call <a href="https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpcAttachments">DescribeTransitRouterVpcAttachments</a>, <a href="https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpnAttachments">DescribeTransitRouterVpnAttachments</a>, <a href="https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterDirectConnectGatewayAttachments">DescribeTransitRouterDirectConnectGatewayAttachments</a>, or <a href="https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterPeerAttachments">DescribeTransitRouterPeerAttachments</a> to get the ID of the “transitrouterattachment” resource.</div>


* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterMulticastDomains">DescribeTransitRouterMulticastDomains</a> API to obtain the ID of the "transitroutermulticastdomain" resource.</div>


* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterBandwidthPackages">DescribeTransitRouterBandwidthPackages</a> API to get the ID of the “transitrouterbandwidthpackage” resource.</div>




**Tags.N.Key ** <span data-label="purple"> String  </span><span data-api-tag="require|0d0fXS">必选</span> `Example: k1`

The tag key of the custom tag.


* Must be 1 to 128 characters.

* Case\-sensitive. Must not start with `volc:` or `sys:` in any case form.

* Must not start or end with a space.

* May include characters (any language), numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), minus signs (\-) and at signs (@).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Tag keys of the same resource must be unique. If the applied Tags.N.Key duplicates an existing tag key, the most recent tag overwrites any previous ones.​</div>


* <div data-tips="true" data-tips-type="default">If you do not provide this parameter or leave it unset, it defaults to empty.</div>




**Tags.N.Value ** <span data-label="purple"> String  </span>`optional` `example: v1`

The tag value of the custom tag.


* Must be 1 to 256 characters.

* Case\-sensitive. Must not start or end with a space.

* May include characters (any language), numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), minus signs (\-) and at signs (@).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To provide this parameter, provide Tags.N.Key first.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=TagResources&Version=2020-04-01&ResourceType=transitrouter&ResourceIds.1=tr-273sdsdsxxxxxp8u2j**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250717T094408Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250717/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
  "ResponseMetadata": {
    "RequestId": "202507171744120171792131840FA5C8",
    "Action": "TagResources",
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
|400 |InvalidResourceType.Malformed |The specified parameter resource type is invalid. |The resource type is invalid. |
|400 |InvalidTag.Disorder |The specified index order of tag is malformed. |The index order format of the specified tag is invalid |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The tag value is invalid. |
|400 |LimitExceeded.Resource |You've reached the limit on the number of resources that you can operate at a time. |You have reached the maximum number of tags that you can manage in a single request. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at a time. |You have reached the maximum number of tags that you can manage in a single request. |
|400 |QuotaExceeded.ResourceSystemTags |You've reached the limit on the number of system tags that you can create. |You have reached the maximum number of system tags that you can add to a single resource. |
|400 |QuotaExceeded.ResourceTags |You've reached the limit on the number of resource tags that you can create. |You have reached the maximum number of custom tags that you can add to a single resource. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
