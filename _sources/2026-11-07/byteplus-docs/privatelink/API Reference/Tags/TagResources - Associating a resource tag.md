---
title: "TagResources - Associating a resource tag"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/TagResources"
---

Call the TagResources API to add custom tags to a resource.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* ​​If multiple tags with the same key are applied to a resource, the most recent value overwrites any previous ones.​

* Each resource can have a maximum of 50 tags. Each call to this API can add up to 20 tags.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=TagResources&serviceCode=privatelink&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|2KhZKV">必选</span> `Example: TagResources`

Action to execute. Set the value to **TagResources**.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|rHfD-j">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**ResourceType ** <span data-label="purple"> String  </span><span data-api-tag="require|uwRPeh">必选</span> `Example: endpointservice`

The resource type. Values:


* endpointservice: Endpoint service

* endpoint: Interface endpoint

* gatewayendpoint: Gateway endpoint



**ResourceIds.N ** <span data-label="purple"> String  </span><span data-api-tag="require|k2q99r">必选</span> `Example: epsvc-2fe630gurkl37k5gfuy33****`

The resource ID.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServices">DescribeVpcEndpointServices</a> API to get resource IDs of the <strong>endpointservice</strong> type.</div>


* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpoints">DescribeVpcEndpoints</a> API to get the resource ID of the <strong>endpoint</strong> type.</div>


* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/privatelink/DescribeVpcGatewayEndpoints">DescribeVpcGatewayEndpoints</a> API to get the resource ID of the <strong>gatewayendpoint</strong> type.</div>


* <div data-tips="true" data-tips-type="default">N represents the serial number of the resource ID, ranging from 1 to 50.</div>


* <div data-tips="true" data-tips-type="default">Separate multiple resource IDs with ampersands (&).</div>




**Tags.N.Key ** <span data-label="purple"> String  </span><span data-api-tag="require|T9KzWZ">必选</span> `Example: k1`

The tag key of the custom tag.


* Must be 1 to 128 characters.

* Case\-sensitive. Must not start with `volc:` or `sys:` in any case form.

* Must not start or end with a space.

* May include letters, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), and at signs (@).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Duplicate tag keys are not allowed for the same resource.</div>




**Tags.N.Value ** <span data-label="purple"> String </span>`optional` `Example value: v1`

The tag value of the custom tag.


* Must be 0 to 255 characters.

* Case\-sensitive. Must not start or end with a space.

* May include letters, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), minus signs (\-) and at signs (@).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To provide this parameter, provide <code>Tags.N.Key</code> first.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple"> String  </span>` optional` `Example: 2021062415303301022514515207C4****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=TagResources&Version=2020-04-01&ResourceType=endpointservice&ResourceIds.1=epsvc-2fe630gurkl37k5gfuy33****&ResourceIds.2=epsvc-2fe630gurkl58k5gfuy26****&Tags.1.Key=k1&Tags.2.Key=k2&Tags.1.Value=v1&Tags.2.Value=v2 HTTP/1.1
Host: privatelink.cn-guangzhou.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-guangzhou/privatelink/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "TagResources",
        "Version": "2020-04-01",
        "Service": "privatelink",
        "Region": "cn-guangzhou"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [common error codes](https://docs.byteplus.com/en/docs/privatelink/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Notes** |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'XXX'. |This request does not contain required parameters. Ensure that your request includes all required parameters, such as XXX.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Here, XXX represents the name of the missing parameter.</div><br> |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidResourceType.Malformed |The specified ResourceType is malformed. |The specified ResourceType parameter format is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey parameter format is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified TagValue parameter format is invalid. |
|400 |LimitExceeded.Resource |You've reached the limit on the number of resources that you can operate at a time. |You have reached the maximum number of tags that can be processed in a single request. |
|400 |LimitExceeded.TagOperation |You've reached the limit on the number of tags that you can operate at a time. |You have reached the maximum number of tag entries that can be operated on in a single request. |
|400 |QuotaExceeded.ResourceCustomTags |You've reached the limit on the number of resource tags that you can create. |You have reached the maximum number of custom tags that you can add to a single resource. |
|400 |QuotaExceeded.ResourceSystemTags |You've reached the limit on the number of system tags that you can create. |You have reached the maximum number of system tags that you can add to a single resource. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
