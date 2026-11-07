---
title: "GetWorkflowExecution"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-getworkflowexecution"
---

This interface is used to retrieve the status of the workflow run using the specified workflow task ID `RunId`.

<span id="requirements"></span>
## Requirements

Time Range: The current supported time range for querying tasks is **30 days**.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=GetWorkflowExecution&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetWorkflowExecution` |The API action. For the current API, the value is `GetWorkflowExecution`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|RunId |String |Yes |`fershg899***` |The workflow task ID. It is used to uniquely indicate the current transcoding event. It can be obtained through the [StartWorkflow](https://docs.byteplus.com/en/docs/byteplus-vod/reference-startworkflow) interface. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|RunId |String |`2ce437f301a9***cf80b5369fe4` |The workflow task ID. |
|Vid |String |`v0c931g7007ac***833096m05os10` |The video ID. |
|DirectUrl |Object of [DirectUrl](https://docs.byteplus.com/en/docs/25/8042#directurl) |`-` |The file storage path in DirectUrl mode. |
|TemplateId |String |`3447e8db6***6271401b132a455` |The workflow ID. |
|SpaceName |String |`test` |The VOD space name. |
|TemplateName |String |`HLS` |The workflow name. |
|Status |String |`0` |The execution status.<br><br><br>* After the workflow task is completed, the values are as follows:<br><br>   * `0`: Successful.<br><br>   * `[1000,1999]`: Failure due to user error.<br><br>   * `[2000,2999]`: Failure due to system error.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more details, see <a href="https://docs.byteplus.com/en/docs/byteplus-vod/workflow-status-codes">Workflow status codes</a>.   </div><br>   <br><br>* During the execution of the workflow task, the values are as follows:<br><br>   * `PendingStart`: Queued.<br><br>   * `Running`: In progress.<br><br>* When the user terminates the task, and the workflow execution ends, the values are as follows:<br><br>   * `Terminated`: Terminated. |
|JobSource |String |`API` |The task source. The values are as follows:<br><br><br>* `API`: Actively triggered.<br><br>* `AutoTrigger`: Automatically triggered.<br><br>* `TranscodeStrategy`: Strategy triggered.<br><br>* `SystemTrigger`: System triggered. |
|CreateTime |String |`2024-08-29T03:30:04Z` |The creation time. Follows the RFC3339 format for UTC time with second precision, formatted as `yyyy-MM-ddTHH:mm:ssZ`. |
|StartTime |String |`2024-08-29T04:46:22Z` |The start time. Follows the RFC3339 format for UTC time with second precision, formatted as `yyyy-MM-ddTHH:mm:ssZ`. |
|EndTime |String |`2024-08-29T04:46:22Z` |The end time. Follows the RFC3339 format for UTC time with second precision, formatted as `yyyy-MM-ddTHH:mm:ssZ`. |


#{.custom\-md\-table\-4}#

<span id="directurl"></span>
### DirectUrl


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|FileName |String |`example.mp4` |The file path. After audio and video are uploaded to the VOD service, you can obtain the `FileName` through the [FileUploadComplete](https://docs.byteplus.com/en/docs/byteplus-vod/docs-fileuploadcomplete) event. |
|BucketName |String |`tos-cn-v-cd3a11` |The bucket name. You can call [ListSpace](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listspace) to get the bucket name bound to the space. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=GetWorkflowExecution&Version=2023-01-01&RunId=fershg899***
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "GetWorkflowExecution",
        "Region": "ap-southeast-1",
        "Service": "vod",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "RunId": "2ce437f301a9***cf80b5369fe4",
        "Vid": "v0c931g7007ac***833096m05os10",
        "TemplateId": "3447e8db6***6271401b132a455",
        "TemplateName": "HLS",
        "SpaceName": "000000",
        "Status": "0",
        "TaskListId": "87f133ea9b***d3058335f673",
        "JobSource": "API",
        "CreateTime": "2022-08-29T03:30:04Z",
        "StartTime": "2022-08-29T04:46:22Z",
        "EndTime": "2022-08-29T04:46:22Z"
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see the [shared errors of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParameter |\- |Invalid parameter. |
|403 |RequestForbidden |\- |The request is forbidden. |
|404 |ResourceNotFound |\- |The ID cannot be found. |
|409 |ResourceInUse |\- |The ID is in use (during deletion). |
|429 |RequestLimitExceeded |\- |The request exceeds the limit. |
|500 |InternalError |\- |Internal error. |
|503 |ServiceUnavailable |\- |The service is unavailable. |


#{.custom\-md\-table\-4}#

&nbsp;
