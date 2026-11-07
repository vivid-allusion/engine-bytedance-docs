---
title: "DMDescribeWorkflows"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/DMDescribeWorkflows"
---

Call DMDescribeWorkflows to view the workflow list.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DMDescribeWorkflows&groupName=%E5%B7%A5%E4%BD%9C%E6%B5%81%E7%AE%A1%E7%90%86&serviceCode=milvus&version=2023-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [Public parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action**<span data-label="purple"> string</span><span data-api-tag="require|FdKfhI">必选</span> ` Example value: DMDescribeWorkflows`

The action to execute, value: DMDescribeWorkflows.



**Version ** <span data-label="purple">string</span><span data-api-tag="require|JnswHx">必选</span>`  Example value: 2023-01-01`

API version, value: 2023\-01\-01.



**PageNumber ** <span data-label="purple">Integer </span>`Optional` `Example value: 1`

Page number, default is 1.



**PageSize ** <span data-label="purple">Integer </span>`Optional` `Example: 10`

Number of items displayed per page, default is 10.



**Filters ** <span data-label="purple">object[] </span>`Optional` `Example: -`

Query filter list.


**Key ** <span data-label="purple">string </span>`optional` `Example: xxx`

Filter key.



**Values ** <span data-label="purple">string[] </span>`Optional` `Example value: yyy`

Filter values.




**Orders ** <span data-label="purple">object[] </span>`Optional` `Example value: -`

Query the sorter list.


**Key ** <span data-label="purple">string </span>`optional` `Example: xxx`

Filter key.



**Asc ** <span data-label="purple">boolean </span>`optional` `example value: true`

Whether ascending order.




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters unique to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Items ** <span data-label="purple">object[] </span>`Example: -`

Data entries.


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

Workflow node list.


**Config ** <span data-label="purple">object </span>`Example: -`

Config。



**InstanceId ** <span data-label="purple">string </span>`Example: -`

Workflow instance ID.



**Sequence ** <span data-label="purple">integer </span>`Example value: -`

Workflow node sequence number.



**Type ** <span data-label="purple">string </span>`example value: -`

Workflow node operator type.



**Operator ** <span data-label="purple">string </span>`Example value: -`

workflow node operator name.



**Options ** <span data-label="purple">object </span>`Example value: -`

Workflow node operator options.




**Configs ** <span data-label="purple">object[] </span>`Example value: -`

Workflow environment configuration.


**Key ** <span data-label="purple">string </span>`Example: -`

Workflow project configuration key.



**Value ** <span data-label="purple">object </span>`Example value: -`

Workflow project configuration value.




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


**Key ** <span data-label="purple">string </span>`Example value: -`

Workflow project setting key.



**Value ** <span data-label="purple">string </span>`Example: -`

Set workflow project values.





**CurrentPage ** <span data-label="purple">long </span>`Example: -`

Current page number.



**TotalPages ** <span data-label="purple">long </span>`example value: -`

Total pages.



**PageSize ** <span data-label="purple">long </span>`example value: -`

Number of items per page.



**TotalSize ** <span data-label="purple">long </span>`example value: -`

Total count.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
POST /?Action=DMDescribeWorkflows&Version=2023-01-01 HTTP/1.1
Host: /
Content-Type: application/json; charset=UTF-8
X-Date: 20260427T121039Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260427/cn-beijing/milvus/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20260427201042166162208076362505",
    "Action": "DMDescribeWorkflows",
    "Version": "2023-01-01",
    "Service": "milvus",
    "Region": "cn-beijing"
  },
  "Result": {
    "Items": [
      {
        "AccountId": "P",
        "RegionId": "RITCvOJ31C0",
        "VipId": "zHfIm",
        "InstanceId": "KNrAX",
        "Name": "gA",
        "Remark": "fPwZABYmBs",
        "Status": "iYEpo",
        "StartTime": "DjXZGS",
        "EndTime": "Cg9OfDlnv4",
        "CreateTime": "QXhIz",
        "UpdateTime": "gTcPw",
        "WorkNodes": [
          {
            "Config": {},
            "InstanceId": "gidnv6KJeQ1",
            "Sequence": 508,
            "Type": "3Oo",
            "Operator": "5q345",
            "Options": {}
          }
        ],
        "Configs": [
          {
            "Key": "O",
            "Value": {}
          }
        ],
        "ProjectId": "fy568",
        "ProjectName": "A0l",
        "GtsJobUuid": "ayf6F",
        "ResourcePoolId": "F86jIm42qf",
        "ResourcePoolName": "1rO5g",
        "Settings": [
          {
            "Key": "Mu",
            "Value": "H"
          }
        ]
      }
    ],
    "CurrentPage": 125,
    "TotalPages": 481,
    "PageSize": 682,
    "TotalSize": 30
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists error codes related to this API and business logic. For more information, see [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|200 |InternalServerError |InternalServerError |Internal server exception. |
