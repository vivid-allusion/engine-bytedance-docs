---
title: "Log streaming overview"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/log-streaming-overview_en-us"
---

<span id="log-streaming"></span>
# Log Streaming

Log Streaming is a BytePlus CDN service that delivers access logs to your specified destination in near real\-time, typically within 5 minutes. You can use these logs for timely analysis to monitor service metrics, detect security risks, and gain business insights. This document provides an overview of the service, its use cases, billing details, and log fields. For differences between this service and the other two CDN log retrieval methods, see [Logs Overview](https://docs.byteplus.com/en/docs/byteplus-cdn/logs-overview_en-us).

<span id="what-is-log-streaming"></span>
## What is Log Streaming

You can configure Log Streaming to deliver real\-time logs for user requests received by CDN nodes to a specified destination.

Logs are delivered within 5 minutes of being collected. Real\-time logs can be used for monitoring metrics, detecting security risks, gaining insights into business trends, and more. For fields included in real\-time logs, see [Log Fields](https://docs.byteplus.com/en/docs/18/48598#log-fields).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">CDN integrates the log query functionality from TLS. If you deliver real\-time logs to TLS, you can query logs without leaving the CDN console. See <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/log-query-examples_en-us">Log Query Examples</a>.</div>


<span id="use-cases"></span>
## Use Cases

[Logs Overview](https://docs.byteplus.com/en/docs/byteplus-cdn/logs-overview_en-us) briefly describes the use cases for Log Streaming. This section describes more specific use cases.

Log Streaming can help you analyze issues encountered by your domain and understand how users access your domain. In addition to filtering real\-time logs, you can also process log data to meet log analysis needs in different scenarios.


|**Log Analysis Scenario** |**Description** |
|---|---|
|Filter logs with specific conditions |Specify one or more conditions to filter logs. For example, you can filter logs by URL, IP address, and time range. This allows you to analyze requests from a specific IP address to a particular URL within a specified time range and quickly identify issues. |
|Monitor CDN service metrics |Metric data can help you understand the quality of CDN service and user access efficiency, allowing you to detect anomalies promptly. Access efficiency includes hit ratio, CDN response time, data transfer rate, etc. |
|Monitor CDN access errors |If users encounter problems when accessing your domain, this data can help you identify the cause of the problem. For example, URL issues, origin server failures, errors when accessing files on the origin server, etc. |
|Analyze popular content |This data can help you identify the most frequently requested content. For example, popular domains, popular URIs, popular visitor IPs, popular Referers, etc. |


<span id="log-streaming-billing"></span>
## Log Streaming Billing

The Log Streaming feature is a paid service. The fees consist of the following parts:


* Log delivery fees: CDN charges for delivered logs. The billing unit is 10,000 entries. For detailed information about log delivery billing, see [CDN Pricing](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-pricing).

* TLS fees. TLS charges for log storage, log read/write traffic, etc. For detailed information about TLS billing, see [TLS Pricing](https://docs.byteplus.com/en/docs/tls/billable_items).


<span id="log-fields"></span>
## Log Fields

The request logs delivered by CDN include the following fields:


|**Field** |**Description** |**Example** |
|---|---|---|
|time |Indicates the time when CDN completed the response to the request, that is, the time when CDN transmitted the last byte of the file. |`23/Oct/2022:17:48:59 +0800` |
|client_ip |Indicates the IP address of the client sending the request. |`192.0.2.1` |
|client_ip_country |The country associated with the client's IP address. |`Indonesia` |
|client_ip_isp |Indicates the network operator to which the client IP address belongs. |`Tencent Cloud` |
|client_ip_province |Indicates the province to which the client IP address belongs. |`Jakarta` |
|client_port |Indicates the client port used for the request. |`37030` |
|domain |Indicates the domain in the request URL, which is your domain. |`cdn.example.com` |
|ds_http_bd_status_hit |Indicates whether the request hit the CDN cache. The possible values are:<br><br><br>* `HIT`: Indicates that the request hit the CDN cache.<br><br>* `MISS`: Indicates that the request did not hit the CDN cache. |`HIT` |
|ds_http_method |Indicates the method used in the request. |`GET` |
|ds_http_protocol |Indicates the HTTP protocol version used in the request. |`HTTP/3` |
|ds_http_range |Indicates the value of the Range header in the request. If the request does not contain this header, the field value is `-`. |`bytes=200-1000` |
|ds_http_referer |Indicates the value of the Referer header in the request. If the request does not contain this header, the field value is `-`. |`https://example.com/index?version=123` |
|ds_http_resp_content_length |Indicates the size of the requested file. The unit is bytes. |`500` |
|ds_http_resp_content_type |Indicates the value of the Content\-Type header in the CDN response. If the response does not contain this header, the field value is `-`. |`image/jpeg` |
|ds_http_resp_size |Indicates the amount of data transmitted from CDN to the user, in bytes. |`573` |
|ds_http_scheme |Indicates the scheme in the request URL. |`HTTPS` |
|ds_http_status |Indicates the response status code from CDN. |`200` |
|ds_http_ua |Indicates the value of the User\-Agent header in the request. If the request does not contain this header, the field value is `-`. |`curl/7.85.0` |
|ds_http_uri |Indicates the path and query string in the request URL, starting with a slash (/). |`/chickadee.png?version=1` |
|ds_http_uri_path |Indicates the path in the request URL, starting with a slash (/). |`/img/chickadee.png` |
|ds_http_uri_query |Indicates the query parameters in the request URL. |`version=1&colar=red` |
|ds_req_time |Indicates the average time spent by CDN to respond to user requests, in seconds. CDN response time is the duration between the following two points:<br><br><br>* CDN completes receiving the last byte of the user request.<br><br>* CDN completes transmitting the last byte of the requested file. |`0.104` |


<span id="steps"></span>
## Steps

See [Task Configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/log-streaming-task-config_en-us).
