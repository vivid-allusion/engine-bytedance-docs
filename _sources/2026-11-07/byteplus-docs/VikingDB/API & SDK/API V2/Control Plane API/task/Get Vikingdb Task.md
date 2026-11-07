---
title: "Get Vikingdb Task"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Get_Task_V2"
---

<span id="2ff51be2"></span>
# Overview

This interface is used to view the details of a specified offline task.

<span id="1b42ea9c"></span>
# Interface Upgrade Notes


* The corresponding V1 interface is:

* Usage differences:



| |V2 Interface |V1 Interface |
|---|---|---|
|Parameter Naming Style |Camel Case (TaskId) |Underscore (task_id) |


<span id="7c833db5"></span>
# Request API

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you can use AK, SK to construct a signature. Please refer to the <a href="https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2">Control Plane API Calling Process</a>, copy the calling example and fill in the necessary information.</div>


<span id="c2be34ef"></span>
## Request Parameters

Request parameter Action value: GetVikingdbTask

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see[Control Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2).


|Parameter |Type |Required |Description |
|---|---|---|---|
|TaskId |String |Yes |Task ID |


<span id="a6340c0b"></span>
## Response Parameters

The table below lists only the specific response parameters for this interface. For more information, please see [Control Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2).


|Parameter |Sub\-parameter |Type |Description |
|---|---|---|---|
|TaskProcessInfo | |Map |Task processing information |
||TaskProgress |String |Task progress. For example:<br><br>50% |
||ErrorMessage |String |Task error message |
||SampleData |Array of Map |Sample 5 data entries for display |
||SampleTimestamp |String |Sample timestamp |
||ScanDataCount |Long |Currently scanned data volume |
||TotalDataCount |Long |Total number of dataset entries (estimated) |
||TotalFilterCount |Long |Already filtered data volume |
|TaskConfig | |Map |Task configuration information |
||ProjectName |String |Project name |
||ResourceId |String |Resource ID |
||CollectionName |String |Collection name |
||FileType |String |Format of import/export files, supports parquet/json |
||NeedConfirm |Boolean |Whether to skip the manual confirmation step. The default is true. |
||FilterConds |Array of String |Filter conditions. For usage details, see: https://www.volcengine.com/docs/84313/1419289 |
||TosPath |String |The TOS path for the data files. This parameter is required for import and export operations. Format: `{bucket_name}/{path}`. Note: This is a path, not a domain name. |
||ExportAll |Boolean |Whether to export all data. If true, filter conditions are ignored. The default is false. |
||UpdateFields |Map |Field values to be updated, must be scalar fields. Updating vector, sparse_vector, and text type fields is not supported. |
||IgnoreError |Boolean |For data import, specifies whether the system continues to parse the file when it encounters data errors. The default is false. |
||UsePublic |Boolean |Whether to use a public TOS endpoint. |
|TaskId | |String |Task ID |
|UpdatePerson | |String |Updater |
|TaskStatus | |String |Task status |
|TaskType | |String |Task type |
|CreateTime | |String |Creation time |
|UpdateTime | |String |Update time |


<span id="7dbaa1d6"></span>
## Request Example

```Plain
action = "GetVikingdbTask",
body = {
  "TaskId": "0ae385ed-47ec-5661-a82c-965dab9d3b99"
}
```


<span id="0b87d609"></span>
## Response Example

```Plain
{
  "ResponseMetadata": {
    "RequestId": "20250609102352190158161083FBD6BB",
    "Action": "GetVikingdbTask",
    "Version": "2025-06-09",
    "Service": "vikingdb",
    "Region": "cn-beijing"
  },
  "Result": {
    "TaskId": "abcabc",
    "TaskType": "data_export",
    "TaskStatus": "running",
    "UpdatePerson": "Bob",
    "CreateTime": "2025-05-13T03:46:52Z",
    "UpdateTime": "2025-05-13T04:47:52Z",
    "TaskConfig": {
      "ProjectName": "default",
      "ResourceId": "vdb-aaaa",
      "CollectionName": "test_coll",
      "FileType": "json",
      "TosPath": "a/b.json",
      "ExportAll": true,
      "IgnoreError": true
    }
  }
}
```


<span id="99123ca2"></span>
## Error Codes

For common error codes, please refer to the [Common Error Codes](https://docs.byteplus.com/docs/VikingDB/FAQ_common) and [API V2 Error Codes and Troubleshooting Guide](https://docs.byteplus.com/docs/VikingDB/FAQnew)Guide] documentation.
