---
title: "TagResources"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/TagResources"
---

Add tags to resources in batches.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=TagResources&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=TagResources&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |TagResources |The name of the API. The API name is `TagResources`. |
|Version |String |Yes |2018\-01\-01 |The API version. The current API version is `2018-01-01`. |
|ResourceIds |Array of String |No |["188906\*\*\*48"] |A list of resources to which tags are added. Currently, this is a list of alert policy IDs. |
|ResourceType |String |No |rule |The type of resources to which tags will be added. Currently, only `rule` (alert policies) is supported. |
|Tags |Array of [ResourceTag](https://docs.byteplus.com/en/docs/39/45545#resourcetag) |No |\- |Tag details. |


<span id="resourcetag"></span>
### ResourceTag


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Key |String |No |doc |Tag key.<br><br><br>* It can contain Chinese characters, uppercase and lowercase letters, digits, and spaces.<br><br>* The following special characters are supported: `_.:/=+-@`.<br><br>* It cannot start or end with a space.<br><br>* `volc:` and `/sys:` are tag keys reserved by the system. You cannot add a tag key that starts with `volc:` or `/sys:` in any case variation.<br><br>* A tag key must be from 1 to 128 characters in length. |
|Value |String |No |demo |Tag value.<br><br><br>* It can contain Chinese characters, uppercase and lowercase letters, digits, and spaces.<br><br>* The following special characters are supported: `_.:/=+-@`.<br><br>* It cannot start or end with a space.<br><br>* The length of a tag key must be 0 to 255 characters. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=TagResources&Version=2018-01-01
Content-Type: application/json
{
    "ResourceIds": [
        "188906***48"
    ],
    "ResourceType": "rule",
    "Tags": [
        {
            "Key": "doc",
            "Value": "demo"
        }
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Data |Object of [TagResourcesResp](https://docs.byteplus.com/en/docs/39/45545#tagresourcesresp) |\- |Response data. |


<span id="tagresourcesresp"></span>
### TagResourcesResp


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|FailedResources |Array of String |["188906\*\*\*12"] |A list of IDs of resources to which tags failed to be added. This field is not empty only when the request fails. |
|SucceedResources |Array of String |["188906\*\*\*48"] |A list of IDs of resources to which tags were added. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "TagResources",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": {
            "FailedResources": [
                "188906***12"
            ],
            "SucceedResources": [
                "188906***48"
            ]
        }
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).

&nbsp;
