---
title: "DescribeDownloadTasks"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-describedownloadtasks"
---

Call the DescribeDownloadTasks API to retrieve the list of log download tasks for a specified log topic.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

This API is limited to 20 calls per second. If exceeded, an ExceedQPSLimit error will be returned.

<span id=".6K-35rGC6K-05piO"></span>
## Request instructions


* Request method: GET

* Request URL: https://{tls\-endpoint}/DescribeDownloadTasks


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists request parameters unique to this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="Query"></span>
### Query


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|PageNumber |Integer |No |`10` |Page number for paginated queries. Defaults to 1, which returns data starting from the first page. |
|PageSize |Integer |No |`20` |Page size. Default is 20; maximum is 100. |
|TopicId |String |Yes |`4a9bd4bd-53f1-43ff-b88a-64ee1be5****` |Log topic ID. |
|TaskName |String |No |`task1` |Filter by task name; supports fuzzy search. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Return parameters

The following table lists only the unique return parameters of this API. For more information, see [Return Structure](https://docs.byteplus.com/en/docs/tls/response-message).


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Tasks |Array of [DownloadTaskResp](https://docs.byteplus.com/en/docs/38/17338#downloadtaskresp) |`Refer to the returned example.` |Download task details. |
|Total |Integer |`1` |Number of log download tasks. TLS only supports saving download task information for up to one day. |


<span id="downloadtaskresp"></span>
### DownloadTaskResp


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Query |String |\* |Log query and analysis statement. |
|TaskId |String |`4a************` |ID of the download task. |
|EndTime |String |`2022-08-25 15:00:02` |You must specify a log time range when performing query and analysis. Use this parameter to specify the end time. The format is `yyyy-MM-dd HH:mm:ss`. |
|LogSize |Integer |`1024` |The original log size; the unit is byte. |
|TopicId |String |`4a************` |Name of the log topic. |
|LogCount |Integer |`20` |Number of downloaded log entries. |
|TaskName |String |`test-task` |Name of the download task. |
|StartTime |String |`2022-08-25 15:00:01` |When performing query and analysis, you must specify the log time range. This parameter defines the start time. The format is `yyyy-MM-dd HH:mm:ss`. |
|CreateTime |String |`2022-08-25 15:00:03` |The creation time of the download task, formatted as `yyyy-MM-dd HH:mm:ss`. |
|DataFormat |String |`json` |Supported export formats: CSV, JSON, JSONL. |
|TaskStatus |String |`creating` |Download task status, indicating the generation status of the log compressed file. including:<br><br><br>* Creating: Generating file<br><br>* Created_cut: File generation interrupted<br><br>* Success: File has been generated<br><br>* Wait: Waiting<br><br>* Fail: Failed<br><br><br>For more details on status, see [the download log](https://docs.byteplus.com/docs/6470/141497). |
|Compression |String |`gzip` |Export file compression format.<br><br><br>* none: No compression.<br><br>* gzip: Compress using gzip format.<br><br>* zip: Compress using zip format. |
|TaskType |Integer |0 |Type of log to download.<br><br><br>* 0: Download query log type.<br><br>* 1: Download analysis log type.<br><br>* 2: download logs for the context type. |
|AllowIncomplete |Boolean |`false` |Allow downloading logs for imprecise query results.<br><br><br>* true: Allowed.<br><br>* false: Not allowed. |
|LogContextInfos |Object of [LogContextInfos](https://docs.byteplus.com/en/docs/38/17338#logcontextinfos) |/ |Download the log information required for context query, including the source host, LogGroup ID, and the Serial number of the log within the LogGroup.<br><br>This parameter will be returned when TaskType is 2. |


<span id="logcontextinfos"></span>
### LogContextInfos


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Source |String |127.10.10.\*\* |Hostname of the log source.<br><br>You can get this value from the Logs in the response of the [SearchLogs](https://docs.byteplus.com/docs/tls/api-searchlogs) API. |
|ContextFlow |String |e61050c\-f7b3a4bf\-2 |Specify the LogGroup ID where the log is located.<br><br>You can obtain this value from the Logs in the response of the [SearchLogs](https://docs.byteplus.com/docs/tls/api-searchlogs) API. |
|PackageOffset |Long |66 |Specify the log's serial number in the LogGroup.<br><br>You can get this value from Logs in the [SearchLogs](https://docs.byteplus.com/docs/tls/api-searchlogs) API response. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
GET https://{tls-endpoint}/DescribeDownloadTasks?&PageNumber=10&PageSize=20&TopicId=4a9bd4bd-53f1-43ff-b88a-64ee1be5****&TaskName=task1 HTTP/1.1
Content-Type: application/json
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
Content-Type: application/json; charset=utf-8
{
    "Tasks": [
        {
            "Query": "*",
            "TaskId": "4a************",
            "EndTime": "2022-08-25 15:00:02",
            "LogSize": 1024,
            "TopicId": "4a9bd4bd-53f1-43ff-b88a-64ee1be5****",
            "LogCount": 1000,
            "TaskName": "ProjectName-TopicName-timestamp",
            "TaskType": 0,
            "StartTime": "2022-08-25 15:00:01",
            "CreateTime": "2022-08-25 15:00:03",
            "DataFormat": "json",
            "TaskStatus": "creating",
            "Compression": "gzip",
            "AllowIncomplete": false
            }
        }
    ],
    "Total": 1
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Code

The table below lists error codes related to the business logic of this API. For public error codes, see the [Public Error Codes](https://docs.byteplus.com/en/docs/tls/common-error-codes) documentation.


|**HTTP status code** |**Error Code** |**Error message** |**Description** |
|---|---|---|---|
|404 |ErrIndexNotExists |Index does not exist |The index does not exist. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |
