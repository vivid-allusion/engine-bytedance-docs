---
title: "TagResources"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/TagResources"
---

Call the TagResources interface to batch bind tags to resources.

<span id="usage-notes"></span>
## Usage notes


* When setting tags, the tag key and tag value must meet certain rules. For detailed information, please refer to [Bind tags](https://docs.byteplus.com/docs/tls/Add_tags).

* The tag keys of multiple tags under the same instance cannot be repeated, and each tag key can only have one tag value.

* If the newly bound tag key overlaps with the tag key already bound to the instance, the new tag value will overwrite the original tag value, please operate with caution.


<span id="request-syntax"></span>
## Request syntax


* Request Method: **POST**

* Request URL: **https://tls\-{Region}.bytepluses.com/TagResources**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|ResourceType |String |True |`project` |The resource types, can be set to:<br><br><br>* project: Project<br><br>* topic: Topic |
|ResourcesIds |Array of String |True |`["c7e0e442-19bf-4fb3-b547-5992fb8b****","2d838e08-a5d2-4d12-a1c1-5dc2b9bf****"]` |The resource list, that is, the ID list of projects or topics.<br><br>Support the input of multiple resource IDs at once, up to 50 resource IDs can be input at the same time. |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/38/36073#tag) |True |`[{"Key":"owner", "Value":"zhangsan"}]` |The array object of the tag key and tag value that needs to be bound.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Supports passing in multiple sets of tag key\-value pairs at once, separated by English commas (,). Up to 20 sets of tag key\-value pairs can be passed in at the same time.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The tag key value needs to meet the setting rules. please refer to <a href="https://docs.byteplus.com/docs/tls/Add_tags">Bind tags</a>.</div><br> |


<span id="tag"></span>
### Tag


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Key |String |False |`owner` |The key of the tag. For setting rules, please refer to [Tag Setting Rules](https://docs.byteplus.com/docs/tls/Add_tags#rules-for-setting-tags). |
|Value |String |False |`zhangsan` |The value of the tag. For setting rules, please refer to [Tag Setting Rules](https://docs.byteplus.com/docs/tls/Add_tags#rules-for-setting-tags). |


<span id="responses"></span>
## Responses

There are no unique return parameters for this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).

<span id="sample-request"></span>
## Sample Request

```json
POST https://tls-{Region}.bytepluses.com/TagResources HTTP/1.1
Content-Type: application/json
{
    "ResourceType": "project",
    "ResourcesIds": ["c7e0e442-19bf-4fb3-b547-5992fb8b****","2d838e08-a5d2-4d12-a1c1-5dc2b9bf****"],
    "Tags": [
        {
            "Key": "owner",
            "Value":"zhangsan"
        },
        {
            "Key":"",city
            "Value":"beijing"
        }
    ]
}
```


<span id="sample-response"></span>
## Sample Response

```json
Content-Type: application/json; charset=utf-8
{}
```


<span id="error-code"></span>
## Error code

For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).

&nbsp;
