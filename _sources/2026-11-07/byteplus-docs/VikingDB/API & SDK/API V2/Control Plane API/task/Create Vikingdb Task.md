---
title: "Create Vikingdb Task"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Create_Task_V2"
---

<span id="overview"></span>
# Overview

This interface is used to create offline tasks for the vector database.

<span id="interface-upgrade-notes"></span>
# Interface Upgrade Notes


* The corresponding V1 interface is:

* Usage differences:



| |V2 Interface |V1 Interface |
|---|---|---|
|Parameter Naming Style |Camel Case (TaskType) |Underscore (task_type) |
|Parameter Name Changes |TaskConfig |task_params |


<span id="request-api"></span>
# Request API

When requesting the OpenAPI interface of the vector database VikingDB, you can use AK, SK to construct a signature. Please refer to the [Control Plane API Calling Process](https://docs.byteplus.com/en/docs/VikingDB/Control_Plane_API_V2?_gl=1*p3vdpe*_gcl_au*OTEzMzcwNjk4LjE3NzA2NDEzNjA.*_ga*MTA3NjI3NjM4LjE3NzA2NDEzNTc.*_ga_2377LE7GQM*czE3NzMyMTAxODQkbzgkZzEkdDE3NzMyMTM0MjkkajU5JGwwJGg2MDM3MjE3MjE.*_ga_3H57BBC3B9*czE3NzMyMTAxODQkbzEwJGcxJHQxNzczMjEzNDI5JGo1OSRsMCRoMTU1MDkyOTM5NA..), copy the calling example and fill in the necessary information.

<span id="request-parameters"></span>
## Request Parameters

Request parameter Action value: CreateVikingdbTask

The table below lists only the specific request parameters for this interface and some common parameters. For more information, please see [Control Plane API Calling Process](https://docs.byteplus.com/en/docs/VikingDB/Control_Plane_API_V2?_gl=1*p3vdpe*_gcl_au*OTEzMzcwNjk4LjE3NzA2NDEzNjA.*_ga*MTA3NjI3NjM4LjE3NzA2NDEzNTc.*_ga_2377LE7GQM*czE3NzMyMTAxODQkbzgkZzEkdDE3NzMyMTM0MjkkajU5JGwwJGg2MDM3MjE3MjE.*_ga_3H57BBC3B9*czE3NzMyMTAxODQkbzEwJGcxJHQxNzczMjEzNDI5JGo1OSRsMCRoMTU1MDkyOTM5NA..).


|Parameter |Sub\-parameter |Type |Required |Description |
|---|---|---|---|---|
|ProjectName | |String |No |Project name |
|CollectionName | |String |Conditional |Collection name |
|ResourceId | |String | |The ID of the collection resource. The request must specify either ResourceId or CollectionName. |
|TaskType | |String |Yes |Task type. Different TaskTypes have different TaskConfigs. See **TaskConfig Configuration for Different TaskTypes** for details. |
|TaskConfig | |Map |Yes |Specific task configuration |
| |FileType |String |No |Format of import/export files, supports parquet/json |
| |NeedConfirm |Boolean |No |Whether to skip the manual confirmation step, default is true |
| |FilterConds |Map |No |Filter conditions. Usage reference: https://docs.byteplus.com/en/docs/VikingDB/Scalar_filter |
| |TosPath |String |No |The path in your TOS bucket for the data files, formatted as {bucket_name}/{path}. Note that this is not a domain name. This parameter is required for import and export tasks. |
| |ExportAll |Boolean |No |Specifies whether to export all data. If set to true, the FilterConds parameter is ignored. The default value is false. |
| |UpdateFields |Map |No |Field values to be updated, must be scalar fields. Updating vector, sparse_vector, and text type fields is not supported. |
| |IgnoreError |Boolean |No |Used for data import. When set to true, the system will continue parsing the file when encountering data errors. Default is false. |
| |UsePublic |Boolean |No |Specifies whether to use a public TOS endpoint. |


<span id="taskconfig-configuration-for-different-tasktypes"></span>
## **TaskConfig Configuration for Different TaskTypes**


* When the **TaskType** is **data_import**, the **TaskConfig** parameter configuration is as follows:



|Parameter |Type |Required |Description |
|---|---|---|---|
|FileType |string |Yes |The file type. Supported formats are json and parquet. |
|TosPath |string |Yes |The TOS path, formatted as {bucket_name}/{path}. Note that this is not a domain name. |
|IgnoreError |bool |No |When set to true, the system will continue parsing the file when encountering data errors. Default is false. |



* When the **TaskType** is **filter_update**, the **TaskConfig** parameter configuration is as follows:



|Parameter |Type |Required |Description |
|---|---|---|---|
|FilterConds |Map |Yes |Filter conditions. Usage reference: https://docs.byteplus.com/en/docs/VikingDB/Scalar_filter |
|UpdateFields |Map |Yes |Field values to be updated, must be scalar fields. Updating vector, sparse_vector, and text type fields is not supported. |



* When the **TaskType** is **filter_delete**, the **TaskConfig** parameter configuration is as follows:



|Parameter |Type |Required |Description |
|---|---|---|---|
|FilterConds |Map |Yes |Filter conditions. Usage reference:<br><br>https://docs.byteplus.com/en/docs/VikingDB/Scalar_filter |
|UpdateFields |Map |Yes |Field values to be updated, must be scalar fields. Updating vector, sparse_vector, and text type fields is not supported. |
|NeedConfirm |Boolean |No |Whether to skip the manual confirmation step, default is true |
|TosPath |string |Yes |The TOS path, formatted as {bucket_name}/{path}. Note that this is not a domain name. |
|FileType |string |Yes |The file type. Supported formats are json and parquet. |



* When the **TaskType** is **data_export**, the **TaskConfig** parameter configuration is as follows:



|Parameter |Type |Required |Description |
|---|---|---|---|
|FilterConds |Map |No |Filter conditions. Usage reference: https://docs.byteplus.com/en/docs/VikingDB/Scalar_filter<br><br><br>* If FilterConds is not provided, all data will be exported regardless of ExportAll.<br><br>* If FilterConds is provided:<br><br>* If ExportAll is omitted or ExportAll=false, only data that matches the conditions is exported.<br><br>* If ExportAll=true, all data is exported and FilterConds does not take effect. |
|ExportAll |Boolean |No |Specifies whether to export all data. If set to true, the FilterConds parameter is ignored. The default value is false. |
|TosPath |string |Yes |The TOS path, formatted as {bucket_name}/{path}. Note that this is not a domain name. |
|FileType |string |Yes |The file type. Supported formats are json and parquet. |


<span id="response-parameters"></span>
## Response Parameters

The table below lists only the specific response parameters for this interface. For more information, please see [Control Plane API Calling Process](https://docs.byteplus.com/en/docs/VikingDB/Control_Plane_API_V2).


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|TaskId |String | |Task ID |
|Message |String |success |A message that indicates the result of the operation, such as "success". |


<span id="request-example"></span>
## Request Example

```Plain
action = "CreateVikingdbTask",
body = {
    "TaskType": "data_import",
    "TaskConfig": {
        "FileType": "json",
        "NeedConfirm": True,
        "TosPath": "test-doc1-tos/pic_search_1000_images.json",
        "ExportAll": False
    },
    "ProjectName": "default",
    "CollectionName": "test_doc1_image"
}
```


<span id="response-example"></span>
## Response Example

```Plain
{
  "ResponseMetadata": {
    "RequestId": "202506091026120661022170451FDB08",
    "Action": "CreateVikingdbTask",
    "Version": "2025-06-09",
    "Service": "vikingdb",
    "Region": "cn-beijing"
  },
  "Result": {
    "TaskId": "rtB0u",
    "Message": "success"
  }
}
```


<span id="error-codes"></span>
## Error Codes

For common error codes, please refer to the [Common Error Codes](https://docs.byteplus.com/en/docs/VikingDB/FAQ_common) and [API V2 Error Codes and Troubleshooting Guide](https://docs.byteplus.com/en/docs/VikingDB/FAQnew).
