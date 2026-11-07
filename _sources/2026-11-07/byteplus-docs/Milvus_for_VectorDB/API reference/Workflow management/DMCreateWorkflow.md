---
title: "DMCreateWorkflow"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/DMCreateWorkflow"
---

Call DMCreateWorkflow to create a workflow.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DMCreateWorkflow&groupName=%E5%B7%A5%E4%BD%9C%E6%B5%81%E7%AE%A1%E7%90%86&serviceCode=milvus&version=2023-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [Public parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action**<span data-label="purple"> string </span><span data-api-tag="require|ucTucZ">必选</span> `Example: DMCreateWorkflow`

The action to execute, value: DMCreateWorkflow.



**Version**<span data-label="purple"> string </span><span data-api-tag="require|OGrZKu">必选</span>` Example value: 2023-01-01`

API version, value: 2023\-01\-01.



**Name**<span data-label="purple"> string</span><span data-api-tag="require|C2Qm4Z">必选</span> ` example: workflow-mq2es`

Workflow name.



**Remark ** <span data-label="purple">string </span>`optional` `Example: consume mq write es workflow`

Workflow description.



**VpcId ** <span data-label="purple">string</span><span data-api-tag="require|tmVJeR">必选</span>`  Example: vpc-274uhjap8u72****`

Private network ID used by the workflow.



**ProjectId ** <span data-label="purple">string </span><span data-api-tag="require|Lmru0n">必选</span> `Example: rxwza****cd3`

Flink project ID used by the workflow.



**ProjectName**<span data-label="purple"> string</span><span data-api-tag="require|SJPgq2">必选</span> ` Example: default`

Name of the Flink project used by the workflow.



**ResourcePoolId**<span data-label="purple"> string</span><span data-api-tag="require|MYr7uh">必选</span> ` Example: o-00g0k****dke`

Flink resource pool ID used by the workflow.



**ResourcePoolName**<span data-label="purple"> string</span><span data-api-tag="require|F3TafM">必选</span>  `Example value: flink-resource-pool`

Name of the Flink resource pool used by the workflow.



**Configs ** <span data-label="purple">object[]</span><span data-api-tag="require|mpejAs">必选</span>  `Example: -`

Workflow environment configuration.


**Key ** <span data-label="purple">string </span>`optional`

Workflow configuration key.



**Value ** <span data-label="purple">object </span>`optional`

workflow configuration value.




**settings ** <span data-label="purple">object[] </span>`optional` `Example value: -`

Flink task parameter configuration used by the workflow.


**Key ** <span data-label="purple">string </span>`optional`

Workflow settings key.



**Value ** <span data-label="purple">string </span>`optional`

Set workflow values.




**Source ** <span data-label="purple">object</span><span data-api-tag="require|oWQDcd">必选</span>  `example value: -`

Workflow data transformation.


**Config ** <span data-label="purple">object </span>`optional`

Node configuration for the workflow.



**Operator ** <span data-label="purple">string</span><span data-api-tag="require|WgIIAC">必选</span>

workflow node operator name.



**Options ** <span data-label="purple">object</span><span data-api-tag="require|pquRx1">必选</span>

Workflow node operator options.




**Sink**<span data-label="purple"> object</span><span data-api-tag="require|Ii5hnB">必选</span> ` example value: -`

Workflow data transformation.


**Config ** <span data-label="purple">object </span>`optional`

Node configuration for the workflow.



**Operator ** <span data-label="purple">string</span><span data-api-tag="require|gTmvxf">必选</span>

workflow node operator name.



**Options ** <span data-label="purple">object</span><span data-api-tag="require|czGL1y">必选</span>

Workflow node operator options.




**Transforms ** <span data-label="purple">object[] </span>`optional` `Example: -`

Workflow data transformations.


**Config ** <span data-label="purple">object </span>`optional`

Node configuration for the workflow.



**Operator ** <span data-label="purple">string</span><span data-api-tag="require|bILipR">必选</span>

workflow node operator name.



**Options ** <span data-label="purple">object</span><span data-api-tag="require|SPJZ9G">必选</span>

Workflow node operator options.




**StartAfterCreate** <span data-label="purple">boolean</span> `optional` `example: false`

Whether to start the workflow.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters unique to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**InstanceId ** <span data-label="purple">string </span>`example: m-8uhja72****`

Workflow instance ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
POST /?Action=DMCreateWorkflow&Version=2023-01-01 HTTP/1.1
Host: /
Content-Type: application/json; charset=UTF-8
X-Date: 20260427T121056Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260427/cn-beijing/milvus/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "Name": "workflow-mq2es",
  "VpcId": "vpc-274uhjap8u72****",
  "ProjectId": "rxwza****cd3",
  "ProjectName": "default",
  "ResourcePoolId": "o-00g0k****dke",
  "ResourcePoolName": "flink-resource-pool",
  "Configs": [],
  "Source": {
    "Operator": "ohP8o",
    "Options": {}
  },
  "Sink": {
    "Operator": "pEHyUJub",
    "Options": {}
  }
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20260427201100104074066133E1C2E6",
    "Action": "DMCreateWorkflow",
    "Version": "2023-01-01",
    "Service": "milvus",
    "Region": "cn-beijing"
  },
  "Result": {
    "InstanceId": "6XISgYY1H"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists error codes related to this API and business logic. For more information, see [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|200 |InternalServerError |InternalServerError |Internal server exception. |
