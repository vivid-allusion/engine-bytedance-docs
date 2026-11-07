---
title: "CreateDownloadTask"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-createdownloadtask"
---

Call the CreateDownloadTask API to create a log download task.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

This API creates a log download task, supporting downloads of raw logs within a specified time period or downloads of query and analysis results. After the download task is successfully created, you can view the task status via DescribeDownloadTasks and obtain the download link using the DescribeDownloadUrl API.

The call frequency limit for this API is 20 times per second. Exceeding the limit will result in an ExceedQPSLimit error.

When downloading logs, the data volume for download tasks is subject to the following restrictions:

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For large data volumes, it is recommended to reduce the time range and download in multiple sessions.</div>



|Actions |Description |
|---|---|
|Only query or preview logs |* You can download up to 20 million rows of log data that meet the query criteria in a single batch, with a data limit of 20 GiB. If the limit is exceeded, only the earliest 20 million lines or the first 20 GiB of log data will be downloaded<br><br>* If more than 20 GiB, the **Export History** page displays **File Generation Interrupted** |
|Query and analyze logs |You can download up to 1 million rows of query and analysis results at a time, with a data volume not exceeding 2 GiB. If the limit is exceeded, only the first 1 million rows or 2 GiB of data are downloaded. |


<span id=".6K-35rGC6K-05piO"></span>
## Request instructions


* Request method: POST

* Request URL: https://{tls\-endpoint}/CreateDownloadTask


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only request parameters specific to this API and some common parameters. For more information, see [Public parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="Body"></span>
### Body


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|TaskName |String |Yes |`test-download-task` |Download task name. Length must be between 1 and 63 characters. |
|TopicId |String |Yes |`3***********` |The ID of the TLS topic where the log is located. |
|Query |String |No |\* |Analyze query statement, up to 4 KiB in length.<br><br><br>* Supports specifying only the query statement. For example, setting it as `*` downloads all raw logs within the selected time range.<br><br>* For TLS\-supported query syntax, see [Query Syntax](https://docs.byteplus.com/docs/tls/Log-query-syntax-2). For SQL analysis syntax and list of functions, see [Analysis Syntax](https://docs.byteplus.com/docs/tls/Analysis-overview). |
|StartTime |Integer |Yes |`1658332800000` |The query start time, accurate to milliseconds. Unix timestamp format, representing the number of milliseconds since 1970\-01\-01 00:00:00 UTC. |
|EndTime |Integer |Yes |`1658332800000` |Query end time, accurate to milliseconds. Unix timestamp format, representing the number of milliseconds since 1970\-01\-01 00:00:00 UTC. |
|DataFormat |String |Yes |`csv` |Export file format, supported settings:<br><br><br>* csv: CSV format<br><br>* json: JSON format<br><br>* jsonl: JSONL format |
|Sort |String |No |`asc` |Sort order of logs when only querying without analysis.<br><br><br>* asc: Ascending order<br><br>* desc: Descending order |
|Limit |Integer |No |`100` |Number of original log entries downloaded or number of rows in the analysis result Data volume must comply with download task limits For details, see [User Guide](https://docs.byteplus.com/docs/tls/api-createdownloadtask#.5L2_55So6K-05piO) |
|Compression |String |Yes |`gzip` |Compression format of the exported file<br><br><br>* none: No compression.<br><br>   We recommend using the no\-compression option only for smaller data volumes<br><br>* gzip: Compress using gzip format<br><br>* zip: Compress using zip format |
|AllowIncomplete |Boolean |No |`false` |Allow downloading logs with imprecise query results.<br><br><br>* true: Allowed.<br><br>* false: Not allowed. |
|TaskType |Integer |Yes |`0` |Type of log to download.<br><br><br>* 0: Download logs of the query type.<br><br>* 1: Download logs of the analysis type.<br><br>* 2: Download logs of the context type. |
|LogContextInfos |Object of [LogContextInfos](https://docs.byteplus.com/en/docs/38/17336#logcontextinfos) |No |/ |Download the log information required for query context, including the source host, the LogGroup ID, and the Serial number in the LogGroup.<br><br>This parameter is required when TaskType is 2. |


<span id="logcontextinfos"></span>
### LogContextInfos


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|Source |String |No |127.10.10.\*\* |The host where the logs originate.<br><br>You can obtain this value in the Logs field of the response from the [SearchLogs](https://docs.byteplus.com/docs/tls/api-searchlogs) API. |
|ContextFlow |String |No |e61050c\-f7b3a4bf\-2 |Specify the LogGroup ID where the log is located.<br><br>This value can be found in Logs in the response from the [SearchLogs](https://docs.byteplus.com/docs/tls/api-searchlogs) API. |
|PackageOffset |Long |No |66 |Specifies the Serial number of the log in the LogGroup.<br><br>You can get this value from the Logs section in the response of the [SearchLogs](https://docs.byteplus.com/docs/tls/api-searchlogs) API. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The table below lists only response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/tls/response-message).


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|TaskId |String |`3***********` |Log topic ID. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://{tls-endpoint}/CreateDownloadTask HTTP/1.1
Content-Type: application/json
{
    "TaskName": "test-download-task",
    "TopicId": "3***********",
    "Query": "*",
    "StartTime": 1658332800000,
    "EndTime": 1658332800000,
    "DataFormat": "csv",
    "Sort": "asc",
    "Limit": 100,
    "Compression": "gzip",
    "AllowIncomplete": false,
    "TaskType": 0
    }
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 0
{
    "TaskId": "989b1f8d-13e6-4b14-819d-1a436377****"
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Code

The table below lists error codes related to this interface and its business logic. For public error codes, see the [Public Error Code](https://docs.byteplus.com/en/docs/tls/common-error-codes) documentation.


|**HTTP status code** |**Error Code** |**Error message** |**Description** |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |Invalid parameter. |
|409 |ErrDownloadTaskAlreadyExists |Download task already exist |The download task already exists. A download task with the same name already exists in this region. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |
