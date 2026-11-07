---
title: "DMUpdateWorkflow"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/DMUpdateWorkflow"
---

Call DMUpdateWorkflow to update the workflow.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DMUpdateWorkflow&groupName=%E5%B7%A5%E4%BD%9C%E6%B5%81%E7%AE%A1%E7%90%86&serviceCode=milvus&version=2023-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [Public parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string</span><span data-api-tag="require|F5xj1W">必选</span>`  Example value: DMUpdateWorkflow`

The action to execute, values: DMUpdateWorkflow.



**Version ** <span data-label="purple">string</span><span data-api-tag="require|WMaDRr">必选</span> ` Example value: 2023-01-01`

API version, value: 2023\-01\-01.



**InstanceId ** <span data-label="purple">string </span><span data-api-tag="require|YBEDkj">必选</span>` example value: m-8uhja72****`

Workflow instance ID.



**Name ** <span data-label="purple">string </span>`Optional` `Example value: workflow-mq2es`

Workflow name.



**Remark ** <span data-label="purple">string </span>`optional` `Example: consume mq write es workflow`

Workflow description.



**ResourcePoolId ** <span data-label="purple">string </span><span data-api-tag="require|AxlgdT">必选</span> `Example: o-00g0k****dke`

Flink resource pool ID used by the workflow.



**ResourcePoolName**<span data-label="purple"> string</span><span data-api-tag="require|ACvTt4">必选</span>`  Example value: flink-resource-pool`

Name of the Flink resource pool used by the workflow.



**settings ** <span data-label="purple">object[] </span>`optional` `Example value: -`

Flink task parameter configuration used by the workflow.


**Key ** <span data-label="purple">string </span>`optional` `Example value: -`

Workflow setting key.



**Value ** <span data-label="purple">string </span>`optional` `Example: -`

Set workflow configuration value.




**Source ** <span data-label="purple">object </span><span data-api-tag="require|aLD91W">必选</span> `example value: -`

Workflow data transformation.


**Config ** <span data-label="purple">object </span>`Optional` `Example value: -`

Workflow node configuration.



**Operator**<span data-label="purple"> string </span><span data-api-tag="require|UU508t">必选</span>` Example value: -`

Workflow node operator name.



**Options**<span data-label="purple"> object</span><span data-api-tag="require|oF7ymT">必选</span> ` Example value: -`

Workflow node operator options.




**Configs ** <span data-label="purple">object[] </span><span data-api-tag="require|atwdxm">必选</span>` Example value: -`

Workflow environment configuration.


**Key ** <span data-label="purple">string </span>`optional` `Example value: -`

Workflow configuration key.



**Value ** <span data-label="purple">object </span>`optional` `Example: -`

Workflow configuration value.




**Sink**<span data-label="purple"> object</span><span data-api-tag="require|qRlvM6">必选</span>`  Example value: -`

Workflow data transformation.


**Config ** <span data-label="purple">object </span>`Optional` `Example value: -`

Workflow node configuration.



**Operator ** <span data-label="purple">string </span><span data-api-tag="require|O0lNUH">必选</span> `Example: -`

Workflow node operator name.



**Options**<span data-label="purple"> object </span><span data-api-tag="require|TtT2PH">必选</span>` Example value: -`

Workflow node operator options.




**Transforms ** <span data-label="purple">object[] </span>`optional` `Example: -`

Workflow data transformations.


**Config ** <span data-label="purple">object </span>`optional` `Example value: -`

Workflow node configuration.



**Operator**<span data-label="purple"> string</span><span data-api-tag="require|15rTuO">必选</span> ` example: -`

Workflow node operator name.



**Options**<span data-label="purple"> object</span><span data-api-tag="require|gpa05G">必选</span> ` Example value: -`

Workflow node operator options.




**StartAfterUpdate ** <span data-label="purple">boolean </span>`optional` `example: false`

Whether to start the workflow.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters unique to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Status ** <span data-label="purple">string </span>`example: SUCCESSFUL/FAILED`

Operation result.



**Message ** <span data-label="purple">string </span>`Example: -`

Returned note information.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
POST /?Action=DMUpdateWorkflow&Version=2023-01-01 HTTP/1.1
Host: /
Content-Type: application/json; charset=UTF-8
X-Date: 20260427T121004Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260427/cn-beijing/milvus/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "InstanceId": "m-8uhja72****",
  "ResourcePoolId": "o-00g0k****dke",
  "ResourcePoolName": "flink-resource-pool",
  "Source": {
    "Operator": "O2k",
    "Options": {}
  },
  "Configs": [],
  "Sink": {
    "Operator": "c9v",
    "Options": {}
  }
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20260427201006030071020015F26148",
    "Action": "DMUpdateWorkflow",
    "Version": "2023-01-01",
    "Service": "milvus",
    "Region": "cn-beijing"
  },
  "Result": {
    "Status": "SUCCESSFUL/FAILED",
    "Message": "-"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists error codes related to this API and business logic. For more information, see [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|200 |InternalServerError |InternalServerError |Internal server exception. |
