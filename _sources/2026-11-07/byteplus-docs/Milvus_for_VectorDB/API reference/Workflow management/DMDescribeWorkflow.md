---
title: "DMDescribeWorkflow"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/DMDescribeWorkflow"
---

Call DMDescribeWorkflow to query workflow details.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DMDescribeWorkflow&groupName=%E5%B7%A5%E4%BD%9C%E6%B5%81%E7%AE%A1%E7%90%86&serviceCode=milvus&version=2023-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [Public parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action**<span data-label="purple"> string </span><span data-api-tag="require|nZeakD">必选</span>` Example value: DMDescribeWorkflow`

The action to execute, value: DMDescribeWorkflow.



**Version**<span data-label="purple"> string </span><span data-api-tag="require|pF5mO3">必选</span> `Example value: 2023-01-01`

API version, value: 2023\-01\-01.



**InstanceId**<span data-label="purple"> string</span><span data-api-tag="require|WGvkFw">必选</span>  `example value: m-8uhja72****`

Workflow instance ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters unique to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**AccountId ** <span data-label="purple">string </span>`Example value: -`

Account ID.



**RegionId ** <span data-label="purple">string </span>`Example value: -`

Region ID.



**VipId ** <span data-label="purple">string </span>`Example value: -`

Private network ID.



**InstanceId ** <span data-label="purple">string </span>`Example value: -`

Workflow instance ID.



**Name ** <span data-label="purple">string </span>`Example: -`

Workflow name.



**Remark ** <span data-label="purple">string </span>`Example value: -`

Workflow remarks.



**Status ** <span data-label="purple">string </span>`Example value: -`

Workflow status.



**StartTime ** <span data-label="purple">string </span>`Example value: -`

Workflow startup time.



**End time ** <span data-label="purple">string </span>`Example value: -`

Workflow end time.



**CreateTime ** <span data-label="purple">string </span>`Example value: -`

Workflow creation time.



**UpdateTime ** <span data-label="purple">string </span>`Example value: -`

Workflow update time.



**WorkNodes ** <span data-label="purple">object[] </span>`Example value: -`

workflow node list.


**InstanceId ** <span data-label="purple">string</span>

Workflow ID.



**Sequence ** <span data-label="purple">integer</span>

Workflow node sequence number.



**Type ** <span data-label="purple">string</span>

Workflow node operator type.



**Operator ** <span data-label="purple">string</span>

workflow node operator name.



**Config ** <span data-label="purple">object</span>

Node configuration for the workflow.



**Options ** <span data-label="purple">object</span>

Workflow node operator options.




**Configs ** <span data-label="purple">object[] </span>`Example value: -`

Workflow environment configuration.


**Key ** <span data-label="purple">string</span>

Workflow configuration key.



**Value ** <span data-label="purple">object</span>

workflow configuration value.




**ProjectId ** <span data-label="purple">string </span>`Example value: -`

Flink project ID.



**ProjectName ** <span data-label="purple">string </span>`example value: -`

Flink project name.



**GtsJobUuid ** <span data-label="purple">string </span>`Example value: -`

Flink GTS job ID.



**ResourcePoolId ** <span data-label="purple">string </span>`example value: -`

Flink resource pool ID.



**ResourcePoolName ** <span data-label="purple">string </span>`Example value: -`

Flink project name.



**Settings ** <span data-label="purple">object[] </span>`example value: -`

Configure Flink task parameters.


**Key ** <span data-label="purple">string</span>

Workflow settings key.



**Value ** <span data-label="purple">string</span>

workflow setting value.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
POST /?Action=DMDescribeWorkflow&Version=2023-01-01 HTTP/1.1
Host: /
Content-Type: application/json; charset=UTF-8
X-Date: 20260427T120935Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260427/cn-beijing/milvus/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "InstanceId": "m-8uhja72****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20260427200938007203020250AAB723",
    "Action": "DMDescribeWorkflow",
    "Version": "2023-01-01",
    "Service": "milvus",
    "Region": "cn-beijing"
  },
  "Result": {
    "AccountId": "5894dD",
    "RegionId": "r",
    "VipId": "kttvcL",
    "InstanceId": "b",
    "Name": "tulYq",
    "Remark": "Sb",
    "Status": "GIJ",
    "StartTime": "G00Li",
    "EndTime": "M",
    "CreateTime": "5NQlX0Gw",
    "UpdateTime": "k0",
    "WorkNodes": [
      {
        "InstanceId": "tvKol",
        "Sequence": 886,
        "Type": "8CoKZpBw",
        "Operator": "bHp",
        "Config": {},
        "Options": {}
      }
    ],
    "Configs": [
      {
        "Key": "MaIBJQgZl",
        "Value": {}
      }
    ],
    "ProjectId": "poF0QeLAG",
    "ProjectName": "W53qJkOJxuf",
    "GtsJobUuid": "G3RtF9ckZ",
    "ResourcePoolId": "9zTGyvTQov",
    "ResourcePoolName": "oJke6X",
    "Settings": [
      {
        "Key": "P5CUuN",
        "Value": "YAVWddp"
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
