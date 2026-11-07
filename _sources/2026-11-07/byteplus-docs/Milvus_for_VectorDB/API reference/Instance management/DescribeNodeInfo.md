---
title: "DescribeNodeInfo"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/DescribeNodeInfo"
---

Call DescribeNodeInfo to query node information.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeNodeInfo&groupName=%E5%AE%9E%E4%BE%8B%E7%AE%A1%E7%90%86&serviceCode=milvus&version=2023-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [Public parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action**<span data-label="purple"> string</span><span data-api-tag="require|XgGq5v">必选</span>`  Example value: DescribeNodeInfo`

The action to execute, value: DescribeNodeInfo.



**Version**<span data-label="purple"> string</span><span data-api-tag="require|mmYyaI">必选</span>` Example: 2023-01-01`

API version, value: 2023\-01\-01.



**InstanceId**<span data-label="purple"> string</span><span data-api-tag="require|lQ8pFZ">必选</span> ` Example: milvus-xxx`

Instance ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters unique to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**NodeInfoList ** <span data-label="purple">object[] </span>`Example value: []`

Node information.


**NodeName ** <span data-label="purple">string </span>`Example value: -`

Node name.



**Node type ** <span data-label="purple">string </span>`Example value: -`

Node type.

META_NODE: Meta node.

PROXY_NODE: Proxy node.

INDEX_NODE: Index node.

DATA_NODE: Data node.

QUERY_NODE: Query node.

STREAMING_NODE: Streaming node.



**DisplayName ** <span data-label="purple">string </span>`Example value: -`

Display name.



**Status ** <span data-label="purple">string </span>`Example value: -`

Status.


* Normal: Running

* Exception: Error



**TotalCpu ** <span data-label="purple">string </span>`Example value: -`

Total number of CPUs.



**UsedCpu ** <span data-label="purple">string </span>`Example value: -`

CPU usage count.



**TotalMemInBytes ** <span data-label="purple">string </span>`Example value: -`

Total memory size.



**UsedMemInBytes ** <span data-label="purple">string </span>`Example value: -`

Used memory size.



**CreateTime ** <span data-label="purple">string </span>`Example value: -`

Creation time.



**UpdateTime ** <span data-label="purple">string </span>`Example value: -`

Updated at.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
POST /?Action=DescribeNodeInfo&Version=2023-01-01 HTTP/1.1
Host: milvus.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20251027T125620Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251027/cn-beijing/milvus/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "InstanceId": "a"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20251027205623060245012029FF40FB",
    "Action": "DescribeNodeInfo",
    "Version": "2023-01-01",
    "Service": "milvus",
    "Region": "cn-beijing"
  },
  "Result": {
    "NodeInfoList": [
      {
        "NodeName": "a3NK0BMsp7e",
        "NodeType": "5mw",
        "DisplayName": "yBdCsP",
        "Status": "q85Jf5",
        "TotalCpu": "5",
        "UsedCpu": "MoBhmcOe",
        "TotalMemInBytes": "l8dhk",
        "UsedMemInBytes": "U0mxHtUmL",
        "CreateTime": "dfn",
        "UpdateTime": "h3DUaCELHja"
      }
    ]
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists error codes related to this API and business logic. For more information, see [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|200 |InternalServerError |InternalServerError |Internal service exception |
|200 |InstanceNotFound |InstanceNotFound |The specified instance does not exist. |
|200 |InstanceIsReleased |InstanceIsReleased |The instance has been released. |
|200 |AccountNoPermission |accountId have no permission |This account does not have permission. |
