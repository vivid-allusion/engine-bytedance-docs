---
title: "Request monitor"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/request_monitor"
---

The request monitor feature consists of two parts: request overview and request list. By using features such as trend charts, distributions, list data, request heatmaps, and data explore to view details, users are assisted in quickly identifying issues related to request errors and slow queries.

<span id=".5YWo6YOo6K-35rGC"></span>
## All requests

<span id=".6K-35rGC6LaL5Yq_5Zu-"></span>
### Request trends


* The request trend chart displays metrics such as request count, number of users sending requests, number of slow queries, and slow query rate within the currently selected time range, providing overall information for site request monitoring.

* If Release information has been set. You will display the Release version information in the chart.


<span id=".5oWi6K-35rGC5YiX6KGo"></span>
### Slow request list


* All requests page, primarily used to diagnose the overall status and duration of page requests.

* Aggregate the request list by the request's domain name and path.

* Supports viewing sorting information related to request count and request time. Displays response time and slow query rate for different request URLs.


<span id=".6ZSZ6K-v6K-35rGC"></span>
## Error request

<span id=".6K-35rGC6LaL5Yq_5Zu-"></span>
### Request trend chart


* Error request page for troubleshooting HTTP 4XX, 5XX, and other error requests.

* The trend chart shows the overall error situation, including error count and error rate under the selected filter conditions, and so on.


<span id=".6ZSZ6K-v6K-35rGC5YiX6KGo"></span>
### Error request list


* The request list uses the domain name and path of the request as the aggregation dimension, and provides the distribution of status codes.

* Click the relevant URL to navigate to data explore and further view details.


<span id=".6K-35rGC5YiX6KGo"></span>
## request list


* Request list, using the domain name and path of the request as the aggregation dimension.

* Support sorting by different metrics. When you select the corresponding path, detailed information about the current path is displayed on the right, including summary information such as request count, SLA (the proportion of correct requests), the proportion of slow requests, and more.

* Trend and distribution provide request time information and its distribution for the current path.

    &nbsp;

* The request heatmap feature is only related to the number of reported requests. According to the time distribution, the periods when requests are most frequently invoked are highlighted as hotspots.

   As shown in the figure below, the request count was higher on the afternoons of March 31 and April 1.

* The blank screen list displays the request URL, DOM score, screenshot, PID, and report time that caused the blank screen to occur. Click **Go to Data Explore** to view detailed reported data.


<span id=".5L2_55So5Zy65pmv"></span>
## Application scenarios

<span id=".5Zy65pmvMe-8miDmjqXlj6Ppl67popjvvIzor7fmsYLnm5HmjqfmiqXorabmjpLmn6U="></span>
### Scenario 1: Interface issues, request monitor alert troubleshooting

Configure the corresponding request error count alert

<span id=".5Zy65pmvMjog5oWi5p-l6K-i5pel5bi45rK755CG"></span>
### Scenario 2: Routine slow query management


* Go to the request list page, set your own slow request threshold, and sort by slow request count. You can view the interface with the highest current slow query count. Click the corresponding interface. The SLA, slow query ratio, and other metrics on the left all reflect the status of that interface. In the diagram below, for the field_values interface, 19.12% of responses take more than 0.5 seconds to return.

* Click the request path to navigate to data explore. and include the corresponding filter conditions. Click a data item to further view Timing information and clarify situations such as network or backend slowness.

    &nbsp;

   You can also view the original report information by clicking **JSON**.
