---
title: "Log query examples"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/log-query-examples_en-us"
---

To effectively analyze your CDN logs and gain insights into service performance, you can use the query examples provided in this document. These examples cover common scenarios such as monitoring request errors, tracking key service metrics like hit ratio and response time, and identifying popular access patterns.

When querying logs, you need to understand the query syntax. A query statement consists of two parts: the query statement and the analysis statement, formatted as `<query statement>|<analysis statement>`. The analysis statement is optional. This document will not elaborate on the query syntax, but will demonstrate common query syntax through examples. For more information about log query syntax and functions you can use in query statements, see [Log Analysis Overview](https://docs.byteplus.com/en/docs/tls/Analysis-overview).

If you have configured to display query results as charts, you can add the charts to a dashboard for easy viewing. See [Adding Charts to a Dashboard](https://docs.byteplus.com/en/docs/tls/Adding_charts_to_a_dashboard).

For descriptions of the log fields used in the examples, see [Log Field Descriptions](https://docs.byteplus.com/en/docs/byteplus-cdn/log-streaming-overview_en-us#log-fields).

<span id="prerequisites"></span>
## Prerequisites

To use the examples in this document, you must complete the following operations:


* [Specify a time range](https://docs.byteplus.com/en/docs/18/49619#specify-a-time-range).

* [Update index configuration](https://docs.byteplus.com/en/docs/18/49619#update-index-configuration).


<span id="specify-a-time-range"></span>
### Specify a time range

On the **Query and analysis** page, click the calendar icon to specify a time range.

<span id="update-index-configuration"></span>
### Update index configuration

You need to make the following updates to the index configuration of the log topic:


* Enable indexing for `ds_http_ua`. This field records the User\-Agent header value.

* Set the field type of `ds_http_status` to `double`.

   After you update the index configuration, new logs delivered to the log topic will use the updated index configuration.


To modify the index configuration, follow these steps:


1. On the **Log Streaming** tab, find the corresponding task. This is the task that delivers the logs for which you are configuring the index.

2. In the **Actions** column, click **Query Logs**.

3. On the **Query and analysis** page, click **Index configuration**.

4. Set the field type of ds_http_status to double, and then enable indexing for ds\-http_ua.

5. Click **OK** to save the changes.


For detailed information about indexes in log services, see [Configure Indexes](https://docs.byteplus.com/en/docs/tls/Configure-indexes-2).

<span id="query-logs-that-meet-specified-conditions"></span>
## Query logs that meet specified conditions

<span id="find-user-requests-with-specific-status-codes"></span>
### Find user requests with specific status codes

Requirement:


* Get user requests with a CDN response status code of 404.


Query syntax:

```sql
ds_http_status:404
```


<span id="get-slow-responding-user-requests"></span>
### Get slow\-responding user requests

Requirement:


* Query user requests with a response time greater than 1 second.


Query syntax:

```sql
ds_req_time:>=1
```


<span id="get-user-requests-for-a-specific-url"></span>
### Get user requests for a specific URL

Requirement:


* Get user requests for a specific URL.


Query syntax:

```sql
ds_http_uri: "/smoke.jpg"
```


<span id="monitor-cdn-request-errors"></span>
## Monitor CDN request errors

<span id="top-domains-by-request-errors"></span>
### Top domains by request errors

Requirement:


* Get the top 10 domains with the most request errors.


Query syntax:

```sql
ds_http_status:>=400 | select domain,count(*) AS PV group by domain order by PV  DESC limit 10 
```


Chart format: Table

<span id="statistics-of-top-urls"></span>
### Statistics of TOP URLs

Requirement:


* Get the top 10 URLs with the most request errors.


Query syntax:

```sql
ds_http_status:>=400 | select ds_http_uri,count(*) AS PV group by ds_http_uri order by PV  DESC limit 10 
```


Chart format: Pie chart

<span id="statistics-of-top-uas"></span>
### Statistics of TOP UAs

Requirement:


* Get the top 10 User\-Agents with the most request errors.


Query syntax:

```sql
ds_http_status:>=400 | select ds_http_ua,count(*) AS PV  group by ds_http_ua order by PV DESC limit 10
```


Chart format: Pie chart

<span id="statistics-of-cdn-response-size"></span>
### Statistics of CDN response size

Requirement:


* With a time granularity of 5 minutes, calculate the following data for each time period:

   * The average size of CDN responses that resulted in errors.


5 minutes is 300000 milliseconds.

Query syntax:

```sql
ds_http_status:>=400 |select __time__ - __time__ % 300000 as time,AVG(ds_http_resp_size) as SIZE group by time 
```


Chart format: Time series chart

<span id="statistics-of-request-error-proportion"></span>
### Statistics of request error proportion

Requirement:


* With a time granularity of 5 minutes, calculate the proportion of request errors for each time period.


5 minutes is 300000 milliseconds.

Query syntax:

```sql
* | select __time__ - __time__ % 300000 as time , sum(case when ds_http_status BETWEEN 400 AND 599  then 1 else 0 end) / count(*) as percent group by time
```


Chart format: Time series chart

<span id="get-request-error-codes"></span>
### Get request error codes

Requirement:


* Calculate the number of request errors based on error codes.


Query syntax:

```sql
ds_http_status:>=400 | select ds_http_status,count(*) As errors group by ds_http_status
```


Chart format: Pie chart

<span id="monitor-cdn-service-metrics"></span>
## Monitor CDN service metrics

<span id="statistics-of-total-response-bytes-ranking-and-average-response-time"></span>
### Statistics of total response bytes ranking and average response time

Requirement:


* Calculate the total response bytes and average response time for each URL. Then, sort the results in descending order by total response bytes.


The unit of response time is seconds.

Query syntax:

```sql
* | select domain,ds_http_uri,ds_http_resp_content_type,sum(ds_http_resp_size) AS total_size,avg(ds_http_resp_size)  AS resource_size,avg(ds_req_time) as avg_resp_time, count(*) as PV group by domain,ds_http_uri,ds_http_resp_content_type  order by total_size DESC
```


Chart format: Table

<span id="statistics-of-slow-response-request-proportion"></span>
### Statistics of slow response request proportion

Requirement:


* Calculate the following data based on client IP. Data is sorted in descending order.

   * The proportion of requests with a response time exceeding 10 seconds.


Query syntax:

```sql
* | select client_ip, pv/c as rate from (select client_ip, sum(case when ds_req_time > 10 then 1 else 0 end) as pv, count(*) * 1.0000 as c group by client_ip ) order by rate DESC
```


Chart format: Table

<span id="statistics-of-cdn-data-transfer-rate-to-users"></span>
### Statistics of CDN data transfer rate to users

The rate is measured in Mbps.

Requirement:


* Calculate the data transfer rate for each time period based on a 5\-minute time granularity.

   * The unit of data transfer rate is Mbps. 5 minutes is 300000 milliseconds.


Query syntax:

```sql
* |select __time__ - __time__ % 300000 as time,avg(ds_http_resp_size)*8/1000/1000/avg(ds_req_time) as download_speed group by time
```


Chart format: Time series chart

<span id="statistics-of-cdn-response-time"></span>
### Statistics of CDN response time

Requirement:


* In 5\-minute intervals, calculate the average response time.

   * The unit of response time is seconds. 5 minutes is 300000 milliseconds.


Query syntax:

```sql
* |select __time__ - __time__ % 300000 as time,AVG(ds_req_time) as req_time group by time
```


Chart format: Time series chart

<span id="statistics-of-hit-ratio"></span>
### Statistics of hit ratio

Requirement:


* Calculate the cache hit ratio and traffic hit ratio for each time period based on a 5\-minute time granularity.


5 minutes is 300000 milliseconds.

Query syntax:

```sql
* | select __time__ - __time__ % 300000 as Time , sum(case when ds_http_bd_status_hit='hit'  then 1 else 0 end) / count(*) as count_percent , sum(case when ds_http_bd_status_hit='hit'  then ds_http_resp_size else 0.0 end) / sum(ds_http_resp_size) as size_percent group by Time
```


Chart format: Time series chart

<span id="statistics-of-cdn-service-availability"></span>
### Statistics of CDN service availability

Requirement:


* Calculate the number of request failures due to internal CDN errors.


Query syntax:

```sql
* | select  sum(case when ds_http_status<500 then 1  else 0 end ) / count(*) as count
```


Chart format: Single value chart

<span id="statistics-of-cdn-miss-ratio"></span>
### Statistics of CDN miss ratio

Requirement:


* Calculate the CDN miss ratio.


Query syntax:

```sql
* | select  sum(case when ds_http_bd_status_hit='miss' then 1  else 0 end) / count(*) as miss_rate 
```


Chart format: Single value chart

<span id="analyze-popular-requests"></span>
## Analyze popular requests

<span id="top-referers-by-user-request-count"></span>
### Top referers by user request count

Requirement:


* Calculate the top 10 Referers among all client requests.


Query syntax:

```sql
* | select ds_http_referer,count(*) as PV group by ds_http_referer order by PV desc limit 10 
```


Chart format: Table

<span id="statistics-of-top-referers-based-on-origin-request-count"></span>
### Statistics of TOP Referers (based on origin request count)

Requirement:


* Calculate the top 10 Referers among user requests that trigger origin requests.


Query syntax:

```sql
ds_http_bd_status_hit:MISS |select ds_http_referer,count(*) as PV group by ds_http_referer order by PV desc limit 10
```


Chart format: Table

<span id="statistics-of-top-client-ips-based-on-user-request-count"></span>
### Statistics of TOP client IPs (based on user request count)

Requirement:


* Calculate the top 10 client IP addresses that send the most requests among all user requests.


Query syntax:

```sql
* |select client_ip,count(*) as PV group by client_ip order by PV desc limit 10
```


Chart format: Table

<span id="statistics-of-top-client-ips-based-on-origin-request-count"></span>
### Statistics of TOP client IPs (based on origin request count)

Requirement:


* Calculate the top 10 client IP addresses that send the most requests among user requests that trigger origin requests.


Query syntax:

```sql
ds_http_bd_status_hit:MISS |select client_ip,count(*) as PV group by client_ip order by PV desc limit 10
```


Chart format: Table

<span id="statistics-of-top-urls-based-on-user-request-count"></span>
### Statistics of TOP URLs (based on user request count)

Requirement:


* Calculate the top 10 URLs with the most requests.


Query syntax:

```sql
* |select ds_http_uri,count(*) as PV group by ds_http_uri order by PV desc limit 10
```


Chart format: Table

<span id="statistics-of-top-urls-based-on-origin-request-count"></span>
### Statistics of TOP URLs (based on origin request count)

Requirement:


* Calculate the top 10 URLs with the most requests among user requests that trigger origin requests.


Query syntax:

```sql
ds_http_bd_status_hit:MISS |select ds_http_uri,count(*) as PV group by ds_http_uri order by PV desc limit 10
```


Chart format: Table

<span id="statistics-of-top-uas-based-on-user-request-count"></span>
### Statistics of TOP UAs (based on user request count)

Requirement:


* Calculate the top 10 User\-Agents.


Query syntax:

```sql
* |select ds_http_ua,count(*) as PV group by ds_http_ua order by PV desc limit 10
```


Chart format: Table

<span id="statistics-of-top-uas-based-on-origin-request-count"></span>
### Statistics of TOP UAs (based on origin request count)

Requirement:


* Calculate the top 10 User\-Agents among user requests that trigger origin requests.


Query syntax:

```sql
ds_http_bd_status_hit:MISS |select ds_http_ua,count(*) as PV group by ds_http_ua order by PV desc limit 10
```


Chart format: Table

<span id="statistics-of-unique-client-ip-address-count-trend"></span>
### Statistics of unique client IP address count trend

Requirement:


* Within the specified time range, calculate the number of unique client IP addresses with a granularity of 5 minutes.


5 minutes is 300000 milliseconds.

Query syntax:

```sql
* |select __time__ - __time__ % 300000 as time,COUNT(DISTINCT(client_ip)) as PV group by time
```


Chart format: Time series chart
