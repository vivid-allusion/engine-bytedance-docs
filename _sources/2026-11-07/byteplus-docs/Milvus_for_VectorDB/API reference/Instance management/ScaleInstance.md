---
title: "ScaleInstance"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/ScaleInstance"
---

Call ScaleInstance to change the instance specification.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [Public parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action**<span data-label="purple"> string</span><span data-api-tag="require|0nU4X4">必选</span> ` Example: ScaleInstance`

The action to execute, values: ScaleInstance.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|haOqpI">必选</span> `Example value: 2023-01-01`

API version, value: 2023\-01\-01.



**InstanceId ** <span data-label="purple">string</span><span data-api-tag="require|ezQsEm">必选</span>`  Example: milvus-xxx`

Instance ID.



**ComponentSpecList ** <span data-label="purple">object[]</span><span data-api-tag="require|Qvs20k">必选</span> ` Example value: []`

Component specification.


**NodeType ** <span data-label="purple">string </span><span data-api-tag="require|Osl7EA">必选</span> `Example value: -`

Node type.



**ResourceSpecName ** <span data-label="purple">string </span><span data-api-tag="require|482DYX">必选</span> `Example value: specification code`

Resource specification name.



**NodeNum ** <span data-label="purple">integer </span><span data-api-tag="require|egab0S">必选</span> `Example value: -`

Number of nodes.



**CpuNum ** <span data-label="purple">integer </span>`optional` `Example value: -`

CPU core count.



**MemSize ** <span data-label="purple">integer </span>`optional` `Example value: -`

Memory size.



**NodeCUType ** <span data-label="purple">string </span>`optional` `Example value: -`

Node CU type. This field is available only when NodeType is QUERY_NODE.


* CAPACITY: capacity.

* PERFORMANCE: performance.




**HaEnabled ** <span data-label="purple">boolean </span>`optional` `example: false`

Whether to enable high availability



**OneStep ** <span data-label="purple">boolean </span>`optional` `Example: false`

Whether to pay directly.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters unique to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**InstanceId ** <span data-label="purple">string </span>`Example: milvus-xxx`

Instance ID.



**OrderNO ** <span data-label="purple">string </span>`Example value: B00`

Order number.



**TradeConfigId ** <span data-label="purple">string </span>`Example value: B00`

Trade configuration ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
POST /?Action=ScaleInstance&Version=2023-01-01 HTTP/1.1
Host: milvus.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20251027T125453Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251027/cn-beijing/milvus/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "InstanceId": "PX8zgkDF",
  "ComponentSpecList": [
    {
      "NodeType": "W",
      "CpuNum": 935,
      "MemSize": 977,
      "NodeNum": 656,
      "NodeCUType": "R3F"
    }
  ],
  "HaEnabled": true,
  "OneStep": true
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20251027205456003180254231425405",
    "Action": "ScaleInstance",
    "Version": "2023-01-01",
    "Service": "milvus",
    "Region": "cn-beijing"
  },
  "Result": {
    "InstanceId": "xNmoXmL0L",
    "OrderNO": "2wbSo6oOAsG",
    "TradeConfigId": "mL7NU5VA"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists error codes related to this API and business logic. For more information, see [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|200 |BadRequestParameterEmpty |Parameter can not be empty. |The parameter cannot be empty. |
|200 |ComponentSpecMissing |Component spec missing |Specification missing. |
|200 |NodeNumTooSmall |Node number too small |Insufficient number of nodes. |
|200 |NodeCpuNotValid |Node cpu not valid |CPU specifications are incorrect. |
|200 |NodeMemNotValid |Node mem not valid |Memory specification error. |
|200 |ComponentSpecNotSupported |Component spec not supported |Not supported to input specifications. |
|200 |NodeNumTooBig |Node number too big |Number of nodes too large. |
|200 |CreateOrderFailed |CreateOrderFailed |Failed to create order. |
|200 |InternalServerError |InternalServerError |Internal server exception. |
|200 |InstanceOperationForbidden |Instance with current can not scale/upgrade |The current instance status cannot be changed. |
|200 |ComponentSpecDuplicate |Component spec duplicate |Duplicate node specification. |
|200 |CUTypeOfQueryNodeCanNotChange |cu type of query node can not change |Modification of the Query node CU type is not allowed. |
|200 |ComponentSpecUnchanged |Instance node specification unchanged |The instance node specification has not changed. |
