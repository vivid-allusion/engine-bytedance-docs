---
title: "DescribeInstanceConfig"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/DescribeInstanceConfig"
---

Query instance configuration.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeInstanceConfig&groupName=%E5%AE%9E%E4%BE%8B%E9%85%8D%E7%BD%AE&serviceCode=milvus&version=2023-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [Public parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|5hRMof">必选</span>`Example value: DescribeInstanceConfig`

The action to execute, possible value: DescribeInstanceConfig.



**Version**<span data-label="purple"> string</span><span data-api-tag="require|vKma19">必选</span> `Example: 2023-01-01`

API version, value: 2023\-01\-01.



**InstanceId ** <span data-label="purple">string</span><span data-api-tag="require|NjJsHv">必选</span> ` Example: milvus-xxx`

Instance ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters unique to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Configurations ** <span data-label="purple">object[] </span>`Example: []`

configuration list.


**ConfigKey ** <span data-label="purple">string </span>`Example: queryNode.gracefulTime`

Configuration key.



**Module ** <span data-label="purple">string </span>`Example value: queryNode`

Module.



**Unit** <span data-label="purple">string</span> `Example value: milliseconds`

Unit.



**ValueType ** <span data-label="purple">string </span>`Example value: STRING`

Value type.



**Default value ** <span data-label="purple">string </span>`Example value: 5000`

Default value.



**ValueRange ** <span data-label="purple">string </span>`example value: [0, 2147483647]`

Value range



**Description ** <span data-label="purple">string</span>

description



**CurValue ** <span data-label="purple">string </span>`Example value: 6000`

current value



**HotUpdateEnabled ** <span data-label="purple">boolean</span>

Does it support Hot Module Replacement?




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST /?Action=DescribeInstanceConfig&Version=2023-01-01 HTTP/1.1
Host: milvus.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20251027T124952Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251027/cn-beijing/milvus/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "InstanceId": "HiuUIeSajBm"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20251027204955019084098038D93398",
    "Action": "DescribeInstanceConfig",
    "Version": "2023-01-01",
    "Service": "milvus",
    "Region": "cn-beijing"
  },
  "Result": {
    "Configurations": [
      {
        "ConfigKey": "queryNode.gracefulTime",
        "Module": "queryNode",
        "Unit": "milliseconds",
        "ValueType": "STRING",
        "DefaultValue": "5000",
        "ValueRange": "[0, 2147483647]",
        "Description": "lg",
        "CurValue": "6000",
        "HotUpdateEnabled": false
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
|200 |InternalServerError |InternalServerError |Internal server exception. |
|200 |InstanceNotFound |InstanceNotFound |The specified instance does not exist. |
|200 |InstanceIsReleased |InstanceIsReleased |The instance has been released. |
|200 |AccountNoPermission |accountId have no permission |This account does not have permission. |
