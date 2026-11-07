---
title: "Request monitoring"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Request_monitoring"
---

The request monitoring feature consists of two parts: request overview and request list. By using features such as trend charts, distributions, list data, request heatmaps, and the data exploration feature for viewing details, you can more quickly identify issues related to request errors and slow queries.

<span id=".5YWo6YOo6K-35rGC"></span>
## All requests

The All Requests page is mainly for troubleshooting the overall status and duration of page requests, and displays comprehensive site request monitoring information.

<span id=".6K-35rGC6LaL5Yq_5Zu-"></span>
### Request trend charts

Indicator description:


|**Metric** |**DescriptionS** |
|---|---|
|Number of requests |Number of requests |
|User count |Number of users who have made requests |
|Slow request count |Number of requests exceeding the configured slow request threshold |
|Rate of slow requests |Number of slow requests/number of requests |
|Number of users affected by slow requests |Number of users affected by slow requests |
|Impact of slow requests on user retention rate |Number of slow requests per user |
|Callback duration |Total execution time of the success, fail, and complete callbacks |


<span id=".5oWi6K-35rGC5YiX6KGo"></span>
### List of slow requests

The request list is aggregated by domain name and path. You can view sorting options based on request count and request duration. For each request URL, the system displays the request duration and the status of the slow query rate.

<span id=".6ZSZ6K-v6K-35rGC"></span>
## Bad request

Error request page for troubleshooting error requests, for example HTTP errors, 4XX errors, 5XX errors, and more.

<span id=".6K-35rGC6LaL5Yq_5Zu-"></span>
### Request trend charts

The trend chart displays overall error statistics, including the number of errors, error rate, and other metrics under the selected filter conditions.


|**Metric** |**DescriptionS** |
|---|---|
|Request error count |Number of requests with status codes \>= 400 |
|Number of users affected by request errors |Deduplicate user IDs for the request error count |
|Request error rate |Number of request errors / total number of requests |
|Impact of request errors on user engagement rate |Request errors per user |


<span id=".6ZSZ6K-v6K-35rGC5YiX6KGo"></span>
### List of error requests

The request list is aggregated by domain name and path, displaying the distribution of abnormal status codes. Click the request path to navigate to **Data Exploration** to view more details, with the relevant time range and filter conditions retained.

<span id=".6K-35rGC5YiX6KGo"></span>
## Request lists

The request list is aggregated by the domain name and path of the request, and supports sorting by different metrics. When you select the corresponding path, the right side displays detailed information about the current path, including summary metrics such as request count, SLA (percentage of correct requests), and proportion of slow requests.

Click the request path to navigate to **Data Exploration** to view in more detail, with the corresponding filter conditions applied.

Trends and distribution provide information about request durations and the distribution of request durations for the current path.

The request heatmap feature is only related to the volume of request reporting. The time distribution shows the hot zones for request invocation times.
