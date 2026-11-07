---
title: "TagResources - Adding custom tags"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/TagResources"
---

Call the TagResources API to add custom tags to resources.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=TagResources&groupName=%E6%A0%87%E7%AD%BE&serviceCode=natgateway&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|16MAQH">必选</span> `Example: TagResources`

The action that you want to perform. Value: TagResources.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|uvMlZP">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**ResourceType ** <span data-label="purple">string </span><span data-api-tag="require|9H8afJ">必选</span> `Example: ngw`

The type of the resource to be tagged. Currently only "ngw" (NAT gateway instance) is supported.



**ResourceIds.N ** <span data-label="purple">string[] </span><span data-api-tag="require|9A0NqF">必选</span> `Example: ngw-273w3e33y2y9s7fap8u2j****`

ID of the NAT gateway.


* N represents the sequence number of a NAT gateway. You can specify a maximum of 50 IDs per call.

* Separate multiple IDs with ampersands (&).



**Tags.N.Value ** <span data-label="purple">string[] </span>`optional` `Example: v1`

The tag key of the resource.


* N represents the sequence number of a tag key. Valid range: 1 to 20.

* Separate multiple tag keys with ampersands (&).

* Must not start with volc: or sys: in any case form.

* Must be 1 to 128 characters. May include characters (any language), numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* If a tag key contains leading or trailing spaces, the system will automatically delete them.

> Duplicate tag keys are not allowed for the same resource.



**Tags.N.Key ** <span data-label="purple">string[] </span><span data-api-tag="require|PVKRap">必选</span> `Example: k1`

The tag value of the resource.


* N represents the serial number of the tag value. Valid range: 1–20.

* Separate multiple tag values with ampersands (&).

* Must be 0 to 256 characters. If left blank, this parameter defaults to an empty string.

* The following characters are allowed: characters from all languages, numbers, spaces ( ), underscores (_), periods (.), colons (:), forward slashes (/), equal signs (=), plus signs (+), hyphens (\-), and the at symbol (@).

* Case\-sensitive.

* If a tag value starts or ends with a space, the system will automatically delete it.

> To pass in this parameter, pass in Tags.N.Key first.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 2021062415303301022514515207C4****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=TagResources&Version=2020-04-01&ResourceType=ngw&ResourceIds.1=ResourceIds.1%3Dngw-273w3e33y2y9s7fap8u2j****%26ResourceIds.2%3Dngw-bp15zckdt37pq72zv**** HTTP/1.1
Host: natgateway.cn-beijing.byteplusapi.com.cn
X-Date: 20251113T124710Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251113/cn-beijing/natgateway/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "TagResources",
        "Version": "2020-04-01",
        "Service": "natgateway",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****"
    }
}

```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/natgateway/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The tag value is invalid. |
|400 |LimitExceeded.Resource |You've reached the limit on the number of resources that you can operate at one time. |You have reached the maximum number of tags that you can manage in a single request. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at one time. |You have reached the maximum of tags that can be processed in a single request. |
|400 |InvalidTag.Disorder |The specified index order of tag is malformed. |The index order format of the specified tag is invalid. |
|400 |QuotaExceeded.ResourceSystemTags |You've reached the limit on the number of system tags that you can create. |You have reached the maximum number of system tags that can be created per resource. |
|400 |QuotaExceeded.ResourceTags |You've reached the limit on the number of resource tags that you can create. |You have reached the maximum number of custom tags that you can add to a single resource. |
|400 |InvalidResourceType.Malformed |The specified parameter resource type is invalid. |The resource type is invalid. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
