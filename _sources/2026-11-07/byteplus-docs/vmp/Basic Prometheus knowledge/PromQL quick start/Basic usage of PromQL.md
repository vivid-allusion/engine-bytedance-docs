---
title: "Basic usage of PromQL"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Basic-PromQL-methods"
---

This topic describes the basic usage of PromQL, which is the built\-in data query language of Prometheus.

<span id=".UHJvbVFMIOamgui_sA=="></span>
## PromQL overview

In Prometheus, every time series is uniquely identified by its metric name and corresponding key\-value pairs called labels. The metric name reflects the basic characteristics of the monitoring sample, and the labels provide multiple characteristic dimensions for the collected data based on the basic characteristics. You can filter, aggregate, and collect statistics on data based on these characteristic dimensions to generate a new time series after computing. As a built\-in data query language of Prometheus, PromQL can be used to query, aggregate, and perform logical operations on time series data. PromQL is widely used in the daily application scenarios of Prometheus, including data query, visualization, and alert handling.

<span id=".UHJvbVFMIOihqOi-vuW8jw=="></span>
## PromQL expressions

Each PromQL expression must contain at least a metric name (such as http_request_total) or a label filter (such as {code="200"}) that does not match an empty string. A metric name can be viewed as a label with the key `__name__`. Therefore, you can interpret that **valid PromQL expressions must always contain non\-empty filter conditions.**  Sample code:

```Plain Text
node_filesystem_free_bytes # Good!
{__name__="node_filesystem_free_bytes"} # Good!

node_filesystem_free_bytes{mountpoint="/data00"} #Good!
{mountpoint="/data00"} # Good
{mountpoint=".*"} # Bad！ 

{job=~".+"}              # Good!
{job=~".*",method="get"} # Good!
{job=~".*"} # Bad!
```


Precautions


* The metric name must not be one of the following keywords including `bool`, `on`, `ignoring`, `group_left, and group_right`. If the reported metric name is one of the preceding keywords, you need to replace the name with `__name__`.


```Plain Text
on{} # Bad!

{__name__="on"} # Good!
```



* Labels are frequently used for filtering. Sample code:


```Plain Text
node_filesystem_free_bytes{mountpoint="/data00", instance="10.182.16.127:9100"}

node_filesystem_free_bytes{instance!="10.182.16.127:9100"}

node_filesystem_free_bytes{mountpoint=~"/data00|/data01"}

node_filesystem_free_bytes{mountpoint!~"/data00|/data01"}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In PromQL, the key of a label filter can be repeatedly configured. PromQL will finally parse the values as an AND relationship. For example, <code>node_filesystem_free_bytes{mountpoint!="/data00", mountpoint!="/data01"}</code> is equivalent to <code>node_filesystem_free_bytes{mountpoint!~"/data00|/data01"}</code>.</div>


<div data-tips="true" data-tips-type="tip">The PromQL query result will be empty: <code>node_filesystem_free_bytes{mountpoint="/data00", mountpoint="/data02"}</code></div>


<span id=".5a6M5YWo5Yy56YWN"></span>
## Full match

PromQL supports two full match modes: = and !=.


* Equal to. `label=value` is used to select the time series whose labels match the expression definition.

* Not equal to. `label!=value` is used to exclude time series whose labels match the expression definition. For example, if you need to filter out all data whose code label is not 200, you can modify the PromQL expression to `http_requests_total{code!=“200”}`.


<span id=".5q2j5YiZ5Yy56YWN"></span>
## Regular expression matching

PromQL can also use regular expressions as matching conditions. Multiple matching conditions can be used.


* Inclusive matching. `label=~regx` is used to select those time series whose labels match the regular expression definition.

* Exclusive matching. `label!~regx` is used to exclude those time series whose labels match the regular expression definition. For example, if you want to query all handler labels that start with /api/v1 in the metric `http_requests_total`, you can use the expression `http_requests_total{handler=~"/api/v1/.*"}`.


<span id=".6IyD5Zu05p-l6K-i"></span>
## Range query

<span id=".5Z-656GA5p-l6K-i"></span>
### Basic query

When you query time series by using a PromQL expression such as `http_requests_total`, only one data point is returned for the same metric with the same label. This kind of expression is called an **instant\-vector\-typed expression**, and the returned result is called an **instant vector**. If you want to query sample data within a period of time, you need to use a **range vector expression**, whose queried result is called a **range vector**. The time range is defined by the time range selector  **[]** . For example, you can use the following expression to select all sample data in the last 5 minutes:

```Plain Text
http_requests_total[5m]
```


The following table shows the time units supported in the time range selector.


| | | | | | | |
|---|---|---|---|---|---|---|
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |


<span id=".5pe26Ze05L2N56e7"></span>
### Time offset

In instant\-vector\-typed expressions or range\-vector\-typed expressions, the **current time** is used as a benchmark by default. However, if you want to query the instant sample data in the last 5 minutes, or the sample data in the last day, you can perform the **time offset** operation. The keyword of the **time offset** operation is **offset**. Sample code:

```Plain Text
# Query the vectors at the current time vectornode_filesystem_free_bytes{mountpoint="/data00"}node_filesystem_free_bytes{mountpoint="/data00"}[1 h]# Separately shift the query time range backward by 5 minutes.node_filesystem_free_bytes{mountpoint="/data00"} offset 5mnode_filesystem_free_bytes{mountpoint="/data00"}[1h] offset 5m
```


The preceding sample code shows that **offset** can be used to compare vectors at different time points. Sample code:

```Plain Text
# Query the change in 5 minutes of the /data00 mount point of the node node_filesystem_free_bytes{mountpoint="/data00"}  offset 5m  - node_filesystem_free_bytes{mountpoint="/data00"}
```


In some special scenarios, if you want a PromQL query statement to use a specified time point instead of the current time as the benchmark, you need to use the `@` modifier and follow `@` with a standard Unix timestamp. The following sample code provides an example on the timestamp 1660404944 = "2022\-08\-13 23:35:44".

```Plain Text
node_filesystem_free_bytes{mountpoint="/data00"} @ 1660404944
node_filesystem_free_bytes{mountpoint="/data00"} @ 1660404944  offset 5m
```


<span id=".6IGa5ZCI5pON5L2c"></span>
## Aggregation operations

Generally, you can use PromQL to query a large amount of data. The aggregation operations provided by PromQL can be used to process these time series and form a new time series. Common aggregation operations include count and sum. For example:


* Count: `count(http_requests_total)`

* Sum the values of all data: `sum(http_requests_total)`


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more details of aggregation operations, refer to <a href="https://docs.byteplus.com/en/docs/vmp/PromQL-aggregation-operations">PromQL aggregation operations</a>.</div>
