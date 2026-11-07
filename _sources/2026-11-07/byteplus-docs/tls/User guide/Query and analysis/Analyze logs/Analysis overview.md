---
title: "Analysis overview"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Analysis-overview"
---

Torch Log Service (TLS) allows you to query and analyze massive log data in real time. It can perform SQL analysis and calculations based on query results and display the results in charts.

<span id="Limits"></span>
## Limits


|Item |Description |
|---|---|
|Data volume |A single shard supports analyzing up to 1 GiB of data at a time. |
|Length of a single query and analysis statement |The maximum length of a single query and analysis statement is 50,000 characters, with the query statement portion having a maximum length of 4,096 characters. |
|Size of field values |The maximum value of a single field is 16 KB, that is, 16384 bytes, and the part exceeding this limit will not be involved in the analysis.<br><br>The maximum length of the field values supported by TLS by default is 2048 bytes, that is, 2 KB. When you need to adjust the maximum length of the field values, you can set the maximum length of the statistical fields. For specific operations, please refer to [Set the maximum length of the field](https://docs.byteplus.com/docs/tls/Configure-indexes-2#3233079a).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After the maximum length of the field is updated, it is only valid for incremental data.</div><br> |
|Number of concurrent operations |* Standard Storage:<br><br>   * Each project supports up to 100 concurrent analysis operations.<br><br>   * Each topic supports up to 15 concurrent analysis operations.<br><br>* Infrequent Access Storage:<br><br>   * Each topic supports up to 2 concurrent analysis operations.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Infrequent Access Storage is a beta feature, and if there are business needs, you can contact your account manager to apply for the whitelist.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the search range of logs includes both Standard Storage and Infrequent Access Storage, the number of concurrent operations is based on the limit for Infrequent Access Storage.</div><br> |
|Applicable data scope |The analysis feature only takes effect for data written to TLS after the statistics feature is enabled. For fields where the statistics feature is not enabled, SQL analysis results are empty. |
||SQL analysis only takes effect for data corresponding to the latest version of the index. Data before index modification can only be queried. |
|Timeout period |The query timeout period is 55 seconds. |
|Number of results |After analysis, up to 100 results are returned by default.<br><br>To view more data, use the [LIMIT syntax](https://docs.byteplus.com/docs/tls/LIMIT-syntax-2) to get up to 100,000 results. |


<span id="15fde56f"></span>
## Log analysis

On the query and analysis page of TLS, type a query and analysis statement and specify the topic and time range to query and analyze logs in real time. For more information, refer to [Analyze logs](https://docs.byteplus.com/docs/tls/Analyze-logs-2).

A query and analysis statement consists of a query condition and an SQL analysis statement, separated by a pipe symbol `( | )`, which indicates that statistical analysis is performed based on the query results.

Structure of a query and analysis statement:

```SQL
&{Query condition} | &{SQL analysis statement}
```


where:


* Query condition: specifies the filter rule, indicating that statistical analysis is performed based on the query results. Log queries must conform to the query syntax. Full\-text search and key\-value search are supported. The search can be an exact search or a fuzzy search. If you specify a space or an asterisk ( \* ), full data is queried. For more information, refer to [Query overview](https://docs.byteplus.com/docs/tls/Query-overview-2)and [Log query syntax](https://docs.byteplus.com/docs/tls/Log-query-syntax-2).

   If log analysis is not required, specify the query condition only.

* SQL analysis statement: specifies the way the query results are analyzed and calculated. Multiple types of SQL functions and syntax are supported. For more information, refer to the function and syntax topics.


To analyze log data, you must specify the query condition and SQL analysis statement at the same time.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Generally, you do not need to specify a <code>FROM</code> clause in an SQL analysis statement. By default, log data in the specified topic is analyzed. In a subquery, you must specify a FROM clause in the SELECT statement.</div>


* <div data-tips="true" data-tips-type="tip">SQL analysis statements are case\-insensitive. A semicolon ( ; ) is not required at the end of an SQL analysis statement to indicate the end.</div>


* <div data-tips="true" data-tips-type="tip">To use strings in SQL analysis statements, enclose the strings in single quotation marks ( ' ' ). Strings that are not enclosed or enclosed in double quotation marks ( " " ) indicate field names or column names. For example, <code>'time'</code> indicates a string, while <code>time</code> or <code>"time"</code> indicates a field or column name.</div>



Example of a query and analysis statement:


|Analysis Scope |Sample Statement |Description |
|---|---|---|
|Analysis of full data |`* \| SELECT status, count(*) AS PV GROUP BY status` |Counts the number of access requests by status code. |
|Analysis of query results |`status:200 \| SELECT COUNT(*) AS PV` |Counts the number of access requests for status code 200. |


<span id="e88849cb"></span>
##
