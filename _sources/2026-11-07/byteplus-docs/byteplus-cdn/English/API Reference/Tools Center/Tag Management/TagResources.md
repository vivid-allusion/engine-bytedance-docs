---
title: "TagResources"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/TagResources_En"
---

Adds tags to one or more domain names.

<span id="usage-limits"></span>
## Usage Limits

Throttle limit: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=TagResources&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `TagResources`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|ResourceIds |String[] |Yes |Represents a list of domain names to which tags need to be added. The list can contain up to 50 domain names. |`["www.example.com","img.example.com"]` |
|ResourceType |String |Yes |The parameter value must be `domain`. |`domain` |
|Tags |Object[] |Yes |Represents a list of tags. The list can contain up to 50 tags. Each tag is a key\-value pair. | |
|Key |String |No |Represents the Key of a tag in the list. The length ranges from 1 to 128 characters.<br><br>Keys are case\-sensitive and can contain letters, numbers, spaces, and the following characters:<br><br><br>* _./=+\-@ |`myKey` |
|Value |String |No |Represents the Value of the tag. The length ranges from 1 to 256 characters. Other input requirements are the same as for `Key`. |`myValue` |


<span id="response-parameters"></span>
## Response Parameters

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=TagResources&Version=2021-03-01
{
    "ResourceType": "domain",
    "ResourceIds": [
        "www.example.com",
        "img.example.com"
    ],
    "Tags": [
        {
            "Key": "myKey1",
            "Value": "myValue1"
        },
        {
            "Key": "myKey2",
            "Value": "myValue2"
        }
    ]
}
```


&nbsp;
