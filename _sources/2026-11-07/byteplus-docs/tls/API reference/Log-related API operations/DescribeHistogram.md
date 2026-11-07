---
title: "DescribeHistogram"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-describehistogram"
---

Call the DescribeHistogram interface to query the logs and view the distribution of logs that meet the conditions over time.

<span id="usage-notes"></span>
## Usage notes

This interface is used to query the logs and construct a histogram of log query results.

The related interfaces (SearchLogs, DescribeLogContext, and DescribeHistogram) share a quota for call frequency and concurrent limits, with specific restrictions as follows:


* For a single BytePlus account or IAM user, the request frequency limit for log query is 100 times/second, otherwise, the error ExceedQPSLimit will be received.

* For a single topic, the concurrent limit for log query is 15, otherwise, the error ExceedCountLimit will be received.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Before querying logs, please make sure the index has been enabled.</div>


* <div data-tips="true" data-tips-type="tip">When the number of logs involved in the query changes dramatically, this interface may return <code>ResultStatus: incomplete</code>, indicating that Torch Log Service cannot scan all data within the specified period in a single query. To ensure short query time, it first returns part of the query results, which may be incomplete. In this case, it is recommended to narrow down the query time range and call this interface multiple times to execute the query.</div>



<span id="request-syntax"></span>
## Request syntax


* Request Method：**POST**

* Request URL：**https://tls\-{Region}.bytepluses.com/DescribeHistogram**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|TopicId |String |True |`4a********` |The ID of the topic. |
|Query |String |True |`error` |The query statements. The maximum length of the statement is 4 KiB. |
|StartTime |Long |True |`1346457600000` |The start time of the query, accurate to the millisecond. It is in Unix timestamp format, representing the number of milliseconds calculated from January 1, 1970, 00:00:00 UTC. If specified at the second level, the server will automatically convert the precision to milliseconds. |
|EndTime |Long |True |`1630454400000` |The end time of the query, accurate to the millisecond. It's in Unix timestamp format, representing the number of milliseconds calculated from January 1, 1970, 00:00:00 UTC. If specified at the second level, the server will automatically convert the precision to milliseconds. |
|Interval |Long |False |`4733280000` |The length of the sub\-interval in the histogram. The unit is milliseconds. This value must be greater than 1.<br><br>After specifying the time range of the query, you can also specify the duration represented by each sub\-interval in the histogram through Interval. By default, the histogram is displayed through 60 sub\-intervals, that is, by default, `Interval = (EndTime-StartTime)/60`, and it is rounded up.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Up to 60 sub\-intervals can be specified in the histogram, please plan the time range of the query and the size of the sub\-interval reasonably.</div><br> |


<span id="responses"></span>
## Responses

The table below only lists the return parameters specific to this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).


|Name |Type |Example |Description |
|---|---|---|---|
|ResultStatus |String |`complete` |The status of the query.<br><br><br>* complete: The query is complete, returning full results.<br><br>* incomplete: The query is complete, returning partial results.<br><br>* error: The query is incomplete, returning an error.<br><br>* time_out: The query has timed out, the returned results may be incomplete. |
|Interval |Long |`9527` |The length of the sub\-interval in the histogram. |
|TotalCount |Long |`10000` |The total number of histogram data for this request, that is, the number of logs that meet the conditions within the corresponding time. |
|Histogram |Array of [HistogramInfo](https://docs.byteplus.com/en/docs/38/16763#histograminfo) | |The result set of all sub\-intervals. |


<span id="histograminfo"></span>
### HistogramInfo


|Name |Type |Example |Description |
|---|---|---|---|
|Time |Integer |`1346457600000` |The start time of the subinterval, in milliseconds. This is in UNIX timestamp format, representing the number of milliseconds calculated from January 1, 1970, 00:00:00 UTC. |
|Count |Integer |`1000` |The number of corresponding search results in the sub\-interval, that is, the number of log entries that meet the conditions during this period. |


<span id="sample-request"></span>
## Sample Request

```json
POST https://tls-{Region}.bytepluses.com/DescribeHistogram HTTP/1.1 Content-Type: application/json
{
    "TopicId": "c1***********",
    "Query": "error",
    "StartTime": 1662364780730,
    "EndTime": 1662452983818,
    "Interval": 1470051
}
```


<span id="sample-response"></span>
## Sample Response

```json
{
    "Histogram": [
        {
            "Count": 0,
            "Time": 1662364780730
        },
        {
            "Count": 4,
            "Time": 1662366011922
        }
    ],
    "Interval": 1470051,
    "TotalCount": 4,
    "ResultStatus": "complete"
}
```


<span id="error-code"></span>
## Error code

The following table lists the error codes related to the interface and business logic. For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |The parameter is invalid. |
|400 |SqlSyntaxError |Sql syntax Error |SQL format or syntax error. |
|404 |TopicNotExist |Topic does not exist. |The topic does not exist. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |


&nbsp;
