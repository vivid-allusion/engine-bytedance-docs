---
title: "SearchLogs"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-searchlogs"
---

Call the SearchLogs interface to query the logs of a topic.

<span id="usage-notes"></span>
## Usage notes

The related interfaces (SearchLogs, DescribeLogContext, and DescribeHistogram) share a quota for call frequency and concurrent limits, with specific restrictions as follows:


* For a single BytePlus account or IAM user, the request frequency limit for log query is 100 times/second, otherwise, the error ExceedQPSLimit will be received.

* For a single topic, the concurrent limit for log query is 15, otherwise, the error ExceedCountLimit will be received.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Before calling this interface, it is recommended to read <a href="https://docs.byteplus.com/docs/tls/query_overview">Query overview</a> and <a href="https://docs.byteplus.com/docs/tls/analysis_overview">Analysis overview</a> to understand the capabilities and limitations of log query and analysis functions, as well as the supported query syntax and SQL analysis syntax.</div>


* <div data-tips="true" data-tips-type="tip">Before querying logs, please make sure that the index has been enabled. If you need to count the logs, the field index and statistics should have been enabled for the log fields involved in the statistics.</div>


* <div data-tips="true" data-tips-type="tip">The storage time of log data in Torch Log service is determined by the <strong>Log storage period</strong> of the topic. Logs that have expired and been deleted cannot be queried.</div>



<span id="request-syntax"></span>
## Request syntax


* Request Method: **POST**

* Request URL: **https://tls\-{Region}.bytepluses.com/SearchLogs**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|TopicId |String |True |`4a********` |The ID of the topic. |
|Query |String |True |`error` |The query and analysis statements. The maximum length of the statement is 4 KiB.<br><br>Please refer to [Analysis overview](https://docs.byteplus.com/docs/tls/analysis_overview) for the structure of the query and analysis statement. For the syntax of the query statement, please refer to [Log query syntax](https://docs.byteplus.com/docs/tls/search_syntax), and for the list of supported SQL analysis syntax and functions, please refer to [Analysis overview](https://docs.byteplus.com/docs/tls/analysis_overview). |
|StartTime |Integer |True |`1346457600000` |The start time of the query, accurate to the millisecond. It is in unix timestamp format, representing the number of milliseconds calculated from January 1, 1970, 00:00:00 UTC. If specified at the second level, the server will automatically convert the precision to milliseconds. |
|EndTime |Integer |True |`1630454400000` |The end time of the query, accurate to the millisecond. It's in unix timestamp format, representing the number of milliseconds calculated from January 1, 1970, 00:00:00 UTC. If specified at the second level, the server will automatically convert the precision to milliseconds. |
|Limit |Integer |False |`30` |This parameter is used to indicate the amount of data per page when displaying the query results in pages. The maximum value is 1000, and it can return up to 20MiB of the logs at a time, and up to 100,000 entries through pagination.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">This parameter is required when only query the logs, there are only query statements in the <code>Query</code> parameter, and no analysis statements. When query and analyze at the same time, the number of log entries to be returned should be specified through the <code>LIMIT</code> syntax in the <code>Query</code> parameter.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The usage of this parameter is equivalent to the traditional pagination parameter <code>PageSize</code>, which is different from the <code>LIMIT</code> syntax of Torch Log Service.</div><br> |
|Context |String |False |`[1650349469000, 130,9, null]` |This is used to specify the position for a secondary query during a follow\-up search, typically used in context search scenarios. Each time the SearchLogs interface is called, it will also return the data end point. If you need to view subsequent log information, you can call the SearchLogs interface again, and pass in the `Context` obtained from the last response in the request.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter takes effect when only query the logs, there are only query statements in the <code>Query</code> parameter, and no analysis statements. Pagination is not supported during simultaneous query and analysis.</div><br> |
|Sort |String |False |`desc` |Return logs in order of log timestamps, accurate to the millisecond.<br><br><br>* desc: (default value) Return logs in reverse chronological order, with the newest logs first.<br><br>* asc: Return logs in chronological order, with the oldest logs first.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter takes effect when only query the logs, there are only query statements in the <code>Query</code> parameter, and no analysis statements.</div><br> |
|HighLight |Boolean |False |`false` |Whether the search keywords are highlighted in the query results. |
|AccurateQuery |Boolean |False |`true` |Whether to query logs with nanosecond precision.<br><br><br>* true: Query logs with nanosecond precision.<br><br>* false: Query logs with millisecond precision. |


<span id="responses"></span>
## Responses

The table below only lists the return parameters specific to this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).


|Name |Type |Example |Description |
|---|---|---|---|
|ResultStatus |String |`complete` |The status of the query.<br><br><br>* complete: The query is complete, and the full results are returned.<br><br>* incomplete: The query is complete, and the partial results are returned.<br><br>* error: The query is incomplete, and an error is returned.<br><br>* time_out: The query has timed out, the returned results may be incomplete. |
|HitCount |Integer |`9527` |HitCount represents the total number of search matches. When the total number of matches is less than 10,000, an accurate number is returned. When it is greater than or equal to 10,000, the return value is 10,000. |
|ListOver |Boolean |`true` |Whether all results have been returned.<br><br><br>* true: All results have been returned.<br><br>* false: Not all results returned, you can pass in the context to continue the query.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is valid if there are only query statements in the <code>Query</code> parameter, and no analysis statements.</div><br> |
|Analysis |Boolean |`false` |The type of the returned result.<br><br><br>* true: The result of the analysis is returned.<br><br>* false: The result of the query is returned. |
|Count |Integer |`0` |Analyze the number of entries hit by the request. |
|Limit |Integer |`0` |the limit number of log entries to return is specified in the request. Default is 100.<br><br><br>* Only when query logs, return the value specified in the request parameter `limit`.<br><br>* When query and analyze logs, return the number of log entries specified by the `LIMIT` syntax in the SQL analysis statements. |
|Context |String |`[1650349469000, 130,9, null]` |This is used to specify the continuation point for a secondary query, typically used in scenarios such as context queries. Each time the SearchLogs interface is called, it will also return the end point of the data. If you need to view subsequent log information, you can call the SearchLogs interface again and pass in the `Context` obtained from the last response in the request. |
|Logs |Array of JSON Map |`/` |The returned list of log entries, where:<br><br><br>* `__path__`: The path and filename of the log.<br><br>* `__source__`: The source IP address of the log.<br><br>* `__time__`: The time of the log was generated.<br><br>* `__content__`: The full text of the log.<br><br>* `__context_flow__`: The ID of the log group where the initial log is located.<br><br>* `__package_offset__`: The sequence number of the initial log in the log group. |
|AnalysisResult |Object of [AnalysisResult](https://docs.byteplus.com/en/docs/38/16761#analysisresult) |`/` |Analysis results. |
|HighLight |Array of JSON Map |`/` |The highlighted keywords. |
|ElapsedMillisecond |Integer |`100` |The time used for this query, with the unit of milliseconds. |


<span id="analysisresult"></span>
### AnalysisResult


|Name |Type |Example |Description |
|---|---|---|---|
|Data |Array of JSON Map |`[{ "KeyInfo": "key:000000000940", "KeyType": "string", "ValueLen": "1", }]` |The returned key\-value pairs from the analysis results. |
|Type |JSON Map |`{ "KeyInfo": "text", "KeyType": "text", "ValueLen": "long", }` |The attributes corresponding to the log analysis column. |
|Schema |Array of String |`["KeyType","ValueLen","KeyInfo"]` |The names of the columns for log analysis. |


<span id="sample-request-1"></span>
## Sample Request 1

```json
{
    "TopicId":"c1***********",
    "Query":"error",
    "StartTime":1346457600000,
    "EndTime":1630454400000,
    "Limit":30,
    "Sort":"desc"
}
```


<span id="sample-response-1"></span>
## Sample Response 1

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Content-Length:  0
{
    "ResultStatus": "complete",
    "HitCount": 20,  
    "Count": 0,      
    "Limit": 0,      
    "ListOver":false,
    "Analysis":false,
    "Context":"[1650349469000,130,9,null]",
    "Logs": [
        {
            "__path__": "/root/my_script/tls-conf-master/input_logs/log/hashkey.log",    
            "__source__": "10.17.0.2",  
            "__time__": "1655788239654",    
            "__content__": "", 
            "__context_flow__":"e61050c909dcccc3-f7b3a4bfaf6af941-2",
            "__package_offset__":"3"
        },
        ...
    ],
    "AnalysisResult": {
        "Schema": [],
        "Type": {},
        "Data": []
    }
}
```


<span id="sample-request-2"></span>
## Sample Request 2

```json
POST https://tls-{Region}.bytepluses.com/SearchLogs HTTP/1.1
Content-Type: application/json
{
    "TopicId":"c1**********",
    "Query":"name:xiaoming",
    "StartTime":1346457600000,
    "EndTime":1630454400000,
    "Limit":30,
    "Sort":"desc"
}
```


<span id="sample-response-2"></span>
## Sample Response 2

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Content-Length:  0
{
    "ResultStatus": "complete",
    "HitCount": 20, 
    "Count": 0, 
    "Limit": 0,
    "ListOver": false,
    "Analysis": false,
    "Context": "[1650349469000,130,9,null]",
    "Logs": [
        [
            {
                "__path__": "/root/my_script/tls-conf-master/input_logs/log/hashkey.log",
                "__source__": "10.17.0.2",
                "__time__": "1655788239654",
                "__context_flow__": "e61050c909dcccc3-f7b3a4bfaf6af941-2",
                "__package_offset__": "3",
                "age": "xxx",
                "class": "xxx"
            },
        ],
        "AnalysisResult": {
            "Schema": [],
            "Type": {},
            "Data": []
        }
    }
```


<span id="sample-request-3"></span>
## Sample Request 3

```json
POST https://tls-{Region}.bytepluses.com/SearchLogs HTTP/1.1
Content-Type: application/json
{
    "TopicId":"c1***********",
    "Query":"* | select name, age, address",
    "StartTime":1346457600000,
    "EndTime":1630454400000,
    "Limit":30,
    "Sort":"desc"
}
```


<span id="sample-response-3"></span>
## Sample Response 3

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Content-Length:  0
{
    "ResultStatus": "complete",
    "Analysis": true,
    "ListOver": true,
    "HitCount": 5924,
    "Count": 1, 
    "Limit": 1, 
    "Logs": [],
    "AnalysisResult": {
        "Schema": [
            "name",
            "age",
            "address"
        ],
        "Type": {
            "name": "text",
            "age": "long",
            "address": "text"
        },
        "Data": [
            {
                "name": "zhangsan",
                "age": "23",
                "address": "zhejiang"
            }
        ]
    },
    "Context": ""
}
```


<span id="error-code"></span>
## Error code

The following table lists the error codes related to the interface and business logic. For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |The parameter is invalid. |
|400 |SqlSyntaxError |Sql syntax Error,details: Function [%s] cannot work with [%s]. Usage: SUM(NUMBER T) \-\u003e T |SQL format or syntax error. |
|404 |TopicNotExist |Topic does not exist. |The topic does not exist. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |
|400 |SearchSyntaxError |The key\-value index for field (%s) is not configured. |The key\-value index has not been configured for the query field. |


&nbsp;
