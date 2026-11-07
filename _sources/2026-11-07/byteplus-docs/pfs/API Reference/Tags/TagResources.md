---
title: "TagResources"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/TagResources"
---

Call the TagResources interface to bind tags for PFS\-related resources.

<span id="requirements"></span>
## Requirements

For detailed label setting rules, see [Label Setting Rules](https://docs.byteplus.com/en/docs/pfs/Binding-or-adding-tags).

<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|ResourceType |String |Yes |filesystem |The resource type that needs to bind the tag, the value selection description is as follows:<br><br><br>* `Filesystem`: Represents a PFS instance. |
|ResourceIds |Array of String |Yes |["vepfs\-apse1dfff3e96\*\*\*\*","vepfs\-apse17cf88bf7\*\*\*\*"] |The list of resources that need to be bound supports up to 20 file system IDs at a time, separated by a comma (,) between each ID. |
|Tags |Array of [TagInfo](https://docs.byteplus.com/en/docs/92/25031#taginfo) |Yes |See the request example for details |The list of labels that the resource needs to bind, and up to 20 groups of label key\-value pairs can be added at a time. Please refer to the following table for detailed value selection descriptions. |


<span id="taginfo"></span>
### TagInfo


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Key |String |No |key |Label key, detailed setting rules, see [Label Setting Rules](https://docs.byteplus.com/en/docs/pfs/Binding-or-adding-tags). |
|Value |String |No |value |For detailed setting rules, see [Label Setting Rules](https://docs.byteplus.com/en/docs/pfs/Binding-or-adding-tags). |


<span id="response-parameters"></span>
## Response parameters

Empty.

<span id="sample-request"></span>
## Sample request

```json
POST /?Action=TagResources&Version=2022-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/vepfs/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "ResourceType": "filesystem",
    "ResourceIds": [
        "vepfs-apse1dfff3e96****",
        "vepfs-apse17cf88bf7****"
    ],
    "Tags": [
        {
            "Value": "value",
            "Key": "key"
        },
         {
            "Value": "value1",
            "Key": "key1"
        }
    ]
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "TagResources",
        "Region": "ap-southeast-1",
        "Service": "vepfs",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {}
}
```
