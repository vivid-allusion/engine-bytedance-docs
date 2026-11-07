---
title: "UntagResources"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/UntagResources"
---

Call the UntagResources interface to unbind tags from resources in bulk.

<span id="request-syntax"></span>
## Request syntax


* Request Method: **POST**

* Request URL: **https://tls\-{Region}.bytepluses.com/UntagResources**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|ResourceType |String |True |`project` |The resource types, can be set to:<br><br><br>* project: Project<br><br>* topic: Topic |
|ResourcesIds |Array of String |True |`["c7e0e442-19bf-4fb3-b547-5992fb8b****","2d838e08-a5d2-4d12-a1c1-5dc2b9bf****"]` |The resource list, that is, the ID list of projects or topics.<br><br>Support the input of multiple resource IDs at once, up to 50 resource IDs can be input at the same time. |
|TagKeys |Array of String |True |`["owner","city"]` |The list of resource tag keys to be unbound.<br><br>Supports passing in multiple tag keys at once, with each key separated by an English comma (,). Up to 20 tag keys can be passed in simultaneously. |


<span id="responses"></span>
## Responses

There are no unique return parameters for this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).

<span id="sample-request"></span>
## Sample Request

```json
POST https://tls-{Region}.bytepluses.com/UntagResources HTTP/1.1
Content-Type: application/json
{
    "ResourceType": "project",
    "ResourcesIds": [
        "c7e0e442-19bf-4fb3-b547-5992fb8b****",
        "2d838e08-a5d2-4d12-a1c1-5dc2b9bf****"
    ],
    "TagKeys": ["owner","city"]
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
