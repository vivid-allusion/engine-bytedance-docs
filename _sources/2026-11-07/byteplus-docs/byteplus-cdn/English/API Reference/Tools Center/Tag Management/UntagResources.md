---
title: "UntagResources"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/UntagResources_En"
---

Removes specified tags from one or more domain names.

<span id="usage-limits"></span>
## Usage Limits

Throttle limit: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=UntagResources&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `UntagResources`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|ResourceIds |String[] |Yes |Represents a list of domain names from which specified tags need to be removed. The list can contain up to 50 domain names. |`["www.example.com","img.example.com"]` |
|ResourceType |String |Yes |The parameter value must be `domain`. |`domain` |
|TagKeys |String[] |Yes |For the tags that need to be removed, this parameter represents their Keys. The list can contain up to 50 Keys. |`["key1","key2"]` |


<span id="response-parameters"></span>
## Response Parameters

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=UntagResources&Version=2021-03-01
{
        "ResourceType": "domain",
        "ResourceIds": ["www.example.com","img.example.com"],
    "TagKeys": [
        {
            "myKey1",
            "myKey2"
        }
    ]
}
```


&nbsp;
