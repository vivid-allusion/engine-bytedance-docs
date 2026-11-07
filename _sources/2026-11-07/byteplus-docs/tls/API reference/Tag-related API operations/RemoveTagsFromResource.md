---
title: "RemoveTagsFromResource"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-removetagsfromresource"
---

Call RemoveTagsFromResource interface to batch unbind tags for the specified project or topic.

<span id="usage-notes"></span>
## Usage notes

This interface is used to unbind tags for the specified projects or topics, and supports batch operations.

<span id="request-syntax"></span>
## Request syntax


* Request Method: **POST**

* Request URL: **https://tls\-{Region}.bytepluses.com/RemoveTagsFromResource**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|ResourceType |String |True |`project` |The resource types, can be set to:<br><br><br>* project: Project<br><br>* topic: Topic |
|ResourcesList |Array of String |True |`["0fdaa6b6-3c9f-424c-8664-fc0d222c****", "c7e0e442-19bf-4fb3-b547-5992fb8b****"]` |The resource list, that is, the ID list of projects or topics.<br><br>&nbsp;<br><br>Supports the input of multiple resource IDs at once, up to 50 resource IDs can be input at the same time. |
|TagKeyList |Array of String |True |`["Key1", "Key2"]` |The list of resource tag keys to be unbound.<br><br>Supports multiple tag keys to be entered at once, separated by English commas (,). Up to 20 tag keys can be entered at the same time. |


<span id="responses"></span>
## Responses

There are no unique return parameters for this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).

<span id="sample-request"></span>
## Sample Request

```json
POST https://tls-{Region}.bytepluses.com/RemoveTagsFromResource HTTP/1.1
Content-Type: application/json
{
    "ResourceType": "project",
    "ResourcesList": ["0fdaa6b6-3c9f-424c-8664-fc0d222c****","c7e0e442-19bf-4fb3-b547-5992fb8b****"],
    "TagKeyList": ["key1","key2"]
}
```


<span id="sample-response"></span>
## Sample Response

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{}
```


<span id="error-code"></span>
## Error code

The following table lists the error codes related to the interface and business logic. For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |The parameters are invalid, or the number of tags exceeds the threshold, or some of the resources do not exist. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |


&nbsp;
