---
title: "DescribeMountServiceNodeTypes"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/DescribeMountServiceNodeTypes"
---

Call DescribeMountServiceNodeTypes interface to query the node information that can be created under an Availability Zone.

<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|ZoneId |String |No |ap\-southeast\-1a |The availability zone ID to query.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/pfs/DescribeZones">DescribeZones</a> interface to query the availability zone ID.</div><br> |


<span id="response-parameters"></span>
## Response parameters


|Name |Type |Example |Description |
|---|---|---|---|
|NodeTypeInfos |Array of [NodeTypeInfo](https://docs.byteplus.com/en/docs/pfs/DescribeMountServiceNodeTypes#nodetypeinfo) |See the return example for details |Selectable client side management node type. |


<span id="nodetypeinfo"></span>
### NodeTypeInfo


|Name |Type |Example |Description |
|---|---|---|---|
|NodeType |String |ecs.g1ie.large |Please refer to the actual return for the supported ECS specifications. |
|Description |String |It is recommended to use this specification when adding the number range of client sides 1\-10. |ECS instance type description information. |


<span id="sample-request"></span>
## Sample request

```json
POST /?Action=DescribeMountServiceNodeTypes&Version=2022-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/vepfs/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "ZoneId": "ap-southeast-1a"
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "DescribeMountServiceNodeTypes",
        "Region": "ap-southeast-1",
        "Service": "vepfs",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "NodeTypeInfos": [
            {
                "NodeType": "ecs.g1ie.large",
                "Description": "It is recommended to use this specification when adding the number range of client sides 1-10."
            }
        ]
    }
}
```
