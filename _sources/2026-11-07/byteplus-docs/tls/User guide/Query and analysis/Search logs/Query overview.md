---
title: "Query overview"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Query-overview-2"
---

Torch Log Service (TLS) offers a real\-time query capability that allows you to query massive log data collected to the server within seconds. To quickly filter and query information, you can execute a query statement for log field matching.

TLS supports the log query and analysis features. If you want to query log data without statistical analysis, specify the topic, time range, and search condition. For more information, refer to [Query logs](https://docs.byteplus.com/docs/tls/Query-logs-2). TLS can query and return the logs that match the specified search condition. For example, you can specify `status:500` for querying access logs whose HTTP status code is 500.

<span id="04eee9d4"></span>
## Search condition syntax

TLS can query data based on the specified topic, time range, and search condition.

Topic: After you specify a topic, TLS searches for log data in the topic.

Log time: TLS can filter logs by log time, which allows you to view log data that is within the specified time period and meets the search condition. If the search box contains spaces or nothing, all logs in the specified time period are displayed.

Search condition: A search condition is a filter condition for querying logs. Only logs that meet the filter condition are returned. Search conditions support multiple operators such as logical operators and mathematical operators. For information on the syntax, refer to [Log query syntax](https://docs.byteplus.com/docs/tls/Log-query-syntax-2).

<span id="Limits"></span>
## Limits


|Item |Description |Remarks |
|---|---|---|
|Number of characters for a single field |After a log is separated by delimiters, the length of a single field cannot exceed 255 characters. |If the length exceeds the limit, the log cannot be queried by keyword, but the log data remains complete on the server. |
|Query statement length |The maximum length of a single query statement is 4,096 characters. |/ |
|Phrase search |Phrase search selects a maximum of 10,000 logs for phrase matching. |/ |
|Number of concurrent operations |* Standard Storage:<br><br>   * Each project supports up to 100 concurrent query operations.<br><br>   * Each topic supports up to 15 concurrent query operations.<br><br>* Infrequent Access Storage:<br><br>   * Each topic supports up to 10 concurrent query operations.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Infrequent Access Storage is a beta feature, and if there are business needs, you can contact your account manager to apply for the whitelist.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the search range of logs includes both Standard Storage and Infrequent Access Storage, the number of concurrent operations is based on the limit for Infrequent Access Storage.</div><br> |/ |
|Timeout period |The query timeout period is 55 seconds. |/ |
|Fuzzy search |In a fuzzy search, TLS can retrieve up to 100 words that meet the search condition and return all logs that contain these 100 words and meet the search condition. |/ |
|Keyword search |In a keyword search, you can specify up to 30 search conditions excluding Boolean logical operators. |/ |
|Responses |After a query, up to 100 query results are returned by default. |Turn pages to get up to 100,000 log entries. |
|Query result sorting |By default, the latest logs are displayed. The log time is accurate to seconds or milliseconds. |/ |
|Display of a single log entry |TLS performs the Document Object Model (DOM) operation only on the first 10,000 characters of a log due to browser performance limits. |/ |


<span id="Log query methods"></span>
## Log query methods

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you query logs, make sure that you have collected log data using LogCollector or other methods and configured indexes correctly. For information on how to configure indexes, refer to <a href="https://docs.byteplus.com/docs/tls/Configure-indexes-2">Configure indexes</a>.</div>



* Console: In the TLS console, find the target project and topic, then query logs on the corresponding **Query and Analysis** page. For the detailed procedure and precautions, refer to Querying logs.

* API action: TLS offers query\-related API actions for your use.

   * [SearchLogs](https://docs.byteplus.com/docs/tls/api-searchlogs): queries logs.

   * [DescribeHistogram](https://docs.byteplus.com/docs/tls/api-describehistogram): queries logs and displays the distribution of the matched logs by time.

   * [DescribeLogContext](https://docs.byteplus.com/docs/tls/api-describelogcontext): displays context information on a specific log.
