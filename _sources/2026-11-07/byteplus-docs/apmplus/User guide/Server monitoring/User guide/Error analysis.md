---
title: "Error analysis"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/error_analytic"
---

The error analysis feature collects exceptions or error information that occur in the service, aggregates and classifies them, and analyzes various errors in the service.

<span id=".5Yqf6IO95YWl5Y-j"></span>
## Feature entry


* Global entry

   1. Log in to the [Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server). 

   2. Select the region where the service is deployed.

   3. Select **Service Monitoring \> Error analysis**.

* Service entry

   1. Log in to the [Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server). 

   2. Select the region where the service is deployed.

   3. Click the service name to enter the service details page.

   4. Click the **Error analysis** tab.


<span id=".6ZSZ6K-v5YiX6KGo"></span>
## Error list

<span id=".5pCc57Si5LiO562b6YCJ"></span>
### Search and filter

Provides filtering features for workspace, time range, tag, attribute, and each dimension of error information. In addition, supports quick search by error information or stack trace; entered strings are case\-insensitive.

<span id=".6ZSZ6K-v6LaL5Yq_"></span>
### Error trend


* The upper right corner displays the total request count, error count, and average error count per request.

* The stacked chart shows the normal request count and error request count, with the scale on the left Y\-axis.

* The line chart shows the "average error count per request", with the scale on the right Y\-axis.

* Click the legend to gray out and hide the corresponding bar or line.

* The tip content includes time, total request count, normal request count, error request count, and average error count per request.

   Here:

   Total request count = normal request count + error request count

   Average error count per request = total error count / total request count


<span id=".SXNzdWXliJfooag="></span>
## Issue list

 &nbsp;

Displays the issue list aggregated from error information, sorted by error count in descending order by default. Errors are categorized into multiple types according to different scenarios, including but not limited to:


* Uncaught Exception

* HTTP Error Code

* External service exception

* Database exception

* NoSQL exception

* MQ exception


Error exceptions refer to exceptions thrown in the service. Some errors do not have an exception, such as errors of the `HTTP Error Code` type.

<span id=".SXNzdWXor6bmg4U="></span>
## Issue details

<span id=".6LaL5Yq_5Zu-"></span>
### Trend chart

The trend chart information is the same as on the list page, and the data content is the metric of the specified issue.

<span id=".6ZSZ6K-v5YiX6KGo"></span>
### Error list

The error list below displays all error information that occurred for this issue.

The detailed information is the error or exception message, and the columns on the right also include the host, service, instance, and Trace ID where the error occurred.

<span id=".6ZSZ6K-v6K-m5oOF"></span>
### Error details

Click Trace ID to go to the details page of this trace link, which by default is positioned at the span where the error occurred. Below, you can select the stack trace to view detailed stack trace information about the exception.
