---
title: "Monitoring metrics"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Monitoring_metrics"
---

This article introduces the monitoring metrics supported by the API gateway.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Due to native Prometheus issues with the P99/P90 algorithm’s statistical methods, there is some error in the P99/P90 response times.</div>



|Metric name |Meaning of metric |Measurement object |Method of statistics |Unit |
|---|---|---|---|---|
|Average response time |Statistics on the average response time made by the API gateway to requests. |Instances, Service |Average over the statistical period. |ms |
|Request count |Statistically count the number of requests made to the API Gateway. |Instance, Service |Sum by statistical time period. |Times |
|HTTP\-4XX error count |Statistics on the API gateway returning HTTP\-4XX errors. |Instances, Services |Sum for the statistical period |occasions |
|Number of HTTP\-5XX errors |Statistics on the number of HTTP\-5XX errors returned by the API gateway. |Instances, Service |Sum over the statistical period. |times |
|QPS |Count the number of times the API gateway is requested per second. |Instances, Service |Statistically based on seconds. |req/s |
|Response time |Statistical analysis of P99, P90, AVG response times that the API gateway makes to requests. |Instances, Service |* P99: Calculates the response time for the request at the 99th percentile in an ascending order.<br><br>* P90: Calculates the response time for the request at the 90th percentile in an ascending order.<br><br>* AVG: Average response time metric. |ms |
|HTTP response code distribution |Count the occurrences per minute of HTTP\-2XX, HTTP\-4XX, HTTP\-5XX. |Instances, Services |Statistically based on minutes. |Times/minute |
|HTTP response message size |Statistics on the size of HTTP response messages. |Instance, Service |Average over the statistical period. |Byte |
|HTTP request message size |Measure the size of HTTP request messages. |Instance, Service |Average over the statistical period. |Byte |
|Entry public network bandwidth |Statistics on the public network data packet traffic received by the API gateway per second. |Instance |Statistics are gathered in seconds. |bit/s |
|Public network bandwidth |Calculate the traffic of public network data packets per second sent by the API gateway. |Instance |Statistics per second granularity. |bit/s |
|Create connection count |Statistically creates new connections per second (CPS, Connection Per Second). Currently, it only supports the creation of new connections on the public network. |Instance |Statistics are calculated in seconds. |Count/s |
