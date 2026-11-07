---
title: "ListTagsForResources"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/ListTagsForResources"
---

Call the ListTagsForResources interface to query all the tags bound to a resource.

<span id="request-syntax"></span>
## Request syntax


* Request Method: **POST**

* Request URL: **https://tls\-{Region}.bytepluses.com/ListTagsForResources**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|MaxResults |Integer |False |`10` |The page size. The default value is 20, and the maximum is 100. |
|NextToken |String |False |`caeba0bbb2be03f84b699f0a****` |The paging query token, used to mark the position of pagination.<br><br><br>* If not filled, the query will start from the beginning.<br><br>* If the `NextToken` value from a previous API call is passed, the query will start from the position marked by that API call and continue onwards. |
|ResourceType |String |True |`project` |The resource types, can be set to:<br><br><br>* project: Project<br><br>* topic: Topic |
|ResourcesIds |Array of String |False |`["c7e0e442-19bf-4fb3-b547-5992fb8b****","2d838e08-a5d2-4d12-a1c1-5dc2b9bfc63e"]` |The resource list, that is, the ID list of projects or topics.<br><br>Support the input of multiple resource IDs at once, up to 50 resource IDs can be input at the same time. |
|TagFilters |Array of [FilterTag](https://docs.byteplus.com/en/docs/38/36074#filtertag) |False |`[{"Key": "owner", "Values": ["zhangsan"]}]` |The resource tag filter. |


<span id="filtertag"></span>
### FilterTag


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Key |String |False |`owner` |The key of the tag. For setting rules, please refer to [Tag Setting Rules](https://docs.byteplus.com/docs/tls/Add_tags#rules-for-setting-tags). |
|Values |Array of String |False |`["zhangsan"]` |The value of the tag. For setting rules, please refer to [Tag Setting Rules](https://docs.byteplus.com/docs/tls/Add_tags#rules-for-setting-tags). |


<span id="responses"></span>
## Responses

The table below only lists the return parameters specific to this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).


|Name |Type |Example |Description |
|---|---|---|---|
|ResourceTags |Array of [ResourceTag](https://docs.byteplus.com/en/docs/38/36074#resourcetag) |`/` |The list of tags bound to the resources. |
|nextToken |String |`caeba02be03f84b699f0b****` |The paging query credentials. |


<span id="resourcetag"></span>
### ResourceTag


|Name |Type |Example |Description |
|---|---|---|---|
|TagKey |String |`owner` |The value of the tag key. |
|TagValue |String |`zhangsan` |The value of the tag value. |
|ResourceId |String |`0fdaa6b6-3c9f-424c-8664-fc0d222c****` |The resource list, that is, the ID list of projects or topics. |
|ResourceType |String |`project` |The resource type. |


<span id="sample-request"></span>
## Sample Request

```json
POST https://tls-{Region}.bytepluses.com/ListTagsForResources HTTP/1.1
Content-Type: application/json
{
    "MaxResults": 10,
    "NextToken": "caeba0bbb2be03f84b699f0a****",
    "ResourceType": "project",
    "ResourcesIds": [
        "c7e0e442-19bf-4fb3-b547-5992fb8b****",
        "2d838e08-a5d2-4d12-a1c1-5dc2b9bfc63e"
    ],
    "TagFilters": [
        {
            "Key": "owner",
            "Values": [
                "zhangsan"
            ]
        }
    ]
}
```


<span id="sample-response"></span>
## Sample Response

```json
Content-Type: application/json; charset=utf-8
{
    "ResourceTags": [
        {
            "TagKey": "owner",
            "TagValue": "zhangsan",
            "ResourceId": "0fdaa6b6-3c9f-424c-8664-fc0d222c****",
            "ResourceType": "project"
        }
    ],
    "nextToken": "caeba02be03f84b699f0b****"
}
```


<span id="sdk"></span>
## SDK

For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).

&nbsp;
