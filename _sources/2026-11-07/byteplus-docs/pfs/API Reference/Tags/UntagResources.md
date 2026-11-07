---
title: "UntagResources"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/UntagResources"
---

Call the UntagResources interface to unbind tags for PFS\-related resources.

<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|ResourceType |String |Yes |filesystem |The resource type that needs to be untied, the value selection description is as follows:<br><br>`Filesystem`: Represents the PFS file system. |
|ResourceIds |Array of String |Yes |[<br><br>"vepfs\-apse1dfff3e96\*\*\*\*",<br><br>"vepfs\-apse17cf88bf7\*\*\*\*"<br><br>] |The list of resource IDs that need to be unlabeled supports up to 20 file system IDs at a time, separated by English commas (,) between each ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/pfs/DescribeFileSystems">DescribeFileSystems</a> interface to query the basic information of all file systems in the target region, including the file system ID.</div><br> |
|TagKeys |Array of String |Yes |See the request example for details |For label keys that need to be untied, a maximum of 20 label key\-value pairs can be passed in each time, and multiple label keys are separated by English commas (,). |


<span id="response-parameters"></span>
## Response parameters

Empty.

<span id="sample-request"></span>
## Sample request

```json
POST /?Action=UntagResources&Version=2022-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/vepfs/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "ResourceType": "filesystem",
    "ResourceIds":[
        "vepfs-apse1dfff3e96****",
        "vepfs-apse17cf88bf7****"
    ],
    "TagKeys": [
        "key",
        "key1"
    ]
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "UntagResources",
        "Region": "ap-southeast-1",
        "Service": "vepfs",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {}
}
```
