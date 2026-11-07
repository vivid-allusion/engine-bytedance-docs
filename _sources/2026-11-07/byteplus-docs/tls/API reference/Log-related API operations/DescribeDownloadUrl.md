---
title: "DescribeDownloadUrl"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-describedownloadurl"
---

Call the DescribeDownloadUrl interface to get the download link for the log corresponding to the specified task.

<span id="usage-notes"></span>
## Usage notes

This interface is used to obtain the download link corresponding to the specified log download task. Through this download link, the corresponding log data can be directly downloaded without authentication.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Before calling this interface, it is recommended to check the status of the download task through the DescribeDownloadTasks. Only tasks with success (file generated) and partially created_cut (file generation interrupted) status can download the corresponding files.</div>


* <div data-tips="true" data-tips-type="tip">The valid period of the link is 5 minutes. Please download it in time after getting the download link. If the link is invalid, you need to call this interface again to get a new download link.</div>


* <div data-tips="true" data-tips-type="tip">The calling frequency of this interface is limited to 20 times/s, and an error ExceedQPSLimit will be reported if the frequency limit is exceeded.</div>



<span id="request-syntax"></span>
## Request syntax


* Request Method：**GET**

* Request URL：**https://tls\-{Region}.bytepluses.com/DescribeDownloadUrl**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="query"></span>
### Query


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|TaskId |String |True |`4a9bd4bd-53f1-43ff-b88a-64ee1be5****` |The task ID of the download task. |


<span id="responses"></span>
## Responses

The table below only lists the return parameters specific to this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).


|Name |Type |Example |Description |
|---|---|---|---|
|DownloadUrl |String |`https://www.******` |Designate the download link corresponding to the download task.<br><br>The link is valid for 5 minutes. Please download it in time after getting the download link. If the link is invalid, you need to call this interface again to get a new download link. |


<span id="sample-request"></span>
## Sample Request

```json
GET /DescribeDownloadUrl?TaskId=9f* HTTP/1.1
Content-Type: application/json
...
{
}
```


<span id="sample-response"></span>
## Sample Response

```json
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 0 
{
    "DownloadUrl": "https://www.******"
}
```


<span id="error-code"></span>
## Error code

The following table lists the error codes related to the interface and business logic. For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|404 |ErrDownloadTaskNotExists |Task does not exist |The download task does not exist |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |


&nbsp;
