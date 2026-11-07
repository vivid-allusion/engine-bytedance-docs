---
title: "List Vikingdb Task"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/List_Task_V2"
---

<span id="a3e36902"></span>
# Overview

This interface is used to view the list of specified offline tasks.

<span id="ad54114a"></span>
# Interface Upgrade Notes


* The corresponding V1 interface is: [Task List](https://docs.byteplus.com/docs/undefined/68a6825f0c199a02cfbeaf25)

* Usage differences:



| |V2 Interface |V1 Interface |
|---|---|---|
|Parameter Naming Style |Camel Case (TaskStatus) |Underscore (task_status) |


<span id="824013cb"></span>
# Request API

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you can use AK, SK to construct a signature. Please refer to the . Copy the calling example and fill in the necessary information.</div>


<span id="07893b5b"></span>
## Request Parameters

Request parameter Action value: ListVikingdbTask

The table below lists only the specific request parameters for this interface and some common parameters. For more information, please see the [Control Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2).


|Parameter |Type |Required |Description |
|---|---|---|---|
|ProjectName |String |No |Project name |
|CollectionName |String |Conditionally |Dataset name |
|ResourceId |String ||Dataset resource ID. The request must specify either ResourceId or CollectionName. |
|TaskStatus |String |Yes |Task status |
|TaskType |String |Yes |Task type |
|PageNumber |Integer |No |Page number for pagination. Starting from 1. |
|PageSize |Integer |No |Page size for pagination. |


<span id="d434ea93"></span>
## Response Parameters

The table below lists only the specific response parameters for this interface. For more information, please see [Control Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2).


|Parameter |Level 1 Sub\-parameter |Level 2 Sub\-parameter |Type |Description |
|---|---|---|---|---|
|Tasks | | |Array of Map |Task information list |
||TaskId | |String |Task ID |
||TaskType | |String |Task type |
||TaskStatus | |String |Task status |
||UpdatePerson | |String |Updater |
||UpdateTime | |String |Update time |
||CreateTime | |String |Creation time |
||TaskProcessInfo | |Map |Task processing information |
|||TaskProgress |String |Task progress. For example, 50% |
|||ErrorMessage |String |Task error message |
|||SampleData |Array of Map |Sample 5 data entries for display |
|||SampleTimestamp |String |Sample timestamp |
|||ScanDataCount |Long |The number of data entries scanned so far |
|||TotalDataCount |Long |Total number of dataset entries (estimated) |
|||TotalFilterCount |Long |The number of filtered data entries |
||TaskConfig | |Map |Task configuration |
|||ProjectName |String |Project name |
|||ResourceId |String |Resource ID |
|||CollectionName |String |Vector database dataset name |
|||FileType |String |Format of import/export files, supports parquet/json |
|||NeedConfirm |Boolean |Specifies whether to skip the manual confirmation step. The default is true. |
|||FilterConds |Array of map |Filter conditions. Usage reference: https://www.volcengine.com/docs/84313/1419289 |
|||TosPath |String |The path in TOS for the data files to be imported or exported, format: {bucket_name}/{path}, note that this is not a domain name. Required for import/export. |
|||ExportAll |Boolean |Specifies whether to export all data. If set to true, filters are not applied. The default is false. |
|||UpdateFields |Map |Field values to be updated, must be scalar fields. Updating vector, sparse_vector, and text type fields is not supported. |
|||IgnoreError |Boolean |Used for data import. When set to true, the system will continue parsing the file when encountering data errors. Default is false. |
|||UsePublic |Boolean |Specifies whether to use a public TOS endpoint. |
|TotalCount | | |Integer |Total number of tasks |
|PageSize | | |Integer |The page size specified in the request. If not specified, the default value is used. |
|PageNumber | | |Integer |The page number specified in the request. If not specified, the default value is used. |


<span id="d1df0993"></span>
## Request Example

```Plain
action = "ListVikingdbTask",
body = {
  "TaskStatus": "success",
  "TaskType": "data_import",
  "PageNumber": 1,
  "PageSize": 10,
  "CollectionName": "test_coll",
}
```


<span id="d539c752"></span>
## Response Example

```Plain
{
  "ResponseMetadata": {
    "RequestId": "20250609102203036054054146B36A88",
    "Action": "ListVikingdbTask",
    "Version": "2025-06-09",
    "Service": "vikingdb",
    "Region": "cn-beijing"
  },
  "Result": {
    "Tasks": [
      {
        "TaskId": "mLVZS",
        "TaskType": "data_import",
        "TaskStatus": "success",
        "UpdatePerson": "Bob",
        "UpdateTime": "2025-05-13T03:48:52Z",
        "CreateTime": "2025-05-13T03:46:52Z",
        "TaskProcessInfo": {
          "TaskProgress": "100%",
          "ErrorMessage": "z",
          "ScanDataCount": 220,
          "TotalDataCount": 220
        },
        "TaskConfig": {
          "ProjectName": "default",
          "ResourceId": "lTrxBgA",
          "CollectionName": "test_coll",
          "FileType": "json",
          "NeedConfirm": true,
          "TosPath": "a/b.json",
          "ExportAll": false,
          "IgnoreError": false
        }
      }
    ],
    "TotalCount": 1,
    "PageSize": 1,
    "PageNumber": 10
  }
}
```


<span id="b1e83c93"></span>
## Error Codes

For common error codes, please refer to the [Common Error Codes](https://docs.byteplus.com/docs/VikingDB/FAQ_common) and [API V2 Error Codes and Troubleshooting Guide](https://docs.byteplus.com/docs/VikingDB/FAQnew)documents.
