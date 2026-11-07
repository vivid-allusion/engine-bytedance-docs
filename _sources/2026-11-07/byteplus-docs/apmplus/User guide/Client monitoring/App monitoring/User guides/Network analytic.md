---
title: "Network analytic"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Network_analytic"
---

In terms of functionality, network monitoring provides several features, including network overview, network error, log search, network alert, and many other features.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**


* Network analytic has been connected. For details, refer to [Android SDK integration](https://docs.byteplus.com/en/docs/apmplus/Android_SDK_integration) and [iOS SDK integration](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_iOS_SDK).

* The network analytic has been configured. For details, refer to [SDK setting](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration#60fb4f24).


<span id=".572R57uc5qaC6KeI"></span>
## Network overview

The network overview allows you to view the overall status of app network requests, including success rate, overall duration, stage duration, and other data.

<span id="7e5890b8"></span>
### Filter conditions

You can filter data using the following filter criteria.


* Filter dimensions supported by the Android operating system:

   Time, Device ID, User ID, OS Version, App Version, App Minor Version, Device Model, APM SDK Version, Download Channel, Custom Dimension.

* Filter dimensions supported by the iOS operating system:

   time, Device ID, User ID, jailbreak status, OS version, app version, app minor version, device model, APM SDK Version, download channel, custom dimension.

* General filter conditions include network\-related filter conditions:

   Domain name, interface, network type, country, province, Internet Service Provider, return code, HTTPMethod, network error code, network log type, Host (header), network library name, server IP, server country, server province, server Internet Service Provider, Cache.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Only the Android version supports filtering data based on Cache.   </div>
   

<span id="b9f0357c"></span>
### Trend charts

The network overview trend chart displays the trends of network metrics based on filter conditions. You can view metrics such as the overall duration and success rate of network requests, and you can also display the trend chart grouped by dimensions.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">On the iOS operating system, when both the SDK version is 3.3.2 or higher and the OS version is 13 or higher, data on the server side can be reported successfully.</div>



* Network leaderboard: The left side displays network data that has been filtered by the filter conditions and sorted in ascending or descending order according to the specified metric. By default, items are sorted in ascending order by the success rate for each **domain** and **interface**.

* Metric trends: On the right are the network data under the filter conditions, including **report volume**, **user count**, **success rate**, **link reuse rate**, **error volume**, **total request time**, **DNS time**, **TCP time**, **SSL time**, **send time**, **wait time**, **receive time**, **request bytes**, **receive bytes**, and **scheduling analysis**.

   
   |**Metric** |**DescriptionS** |
   |---|---|
   |report volume |The number of network requests initiated is affected by the network analytic sampling rate. |
   |user count |The number of users initiating network requests is affected by the sampling rate of network analytics. |
   |success rate |Successful request count / total request count in network requests, where a returned status code from 0 to 399 is considered successful. |
   |Link reuse rate |link reuse request count / total request count |
   |Error count |The number of network requests with errors is affected by the sampling rate of network analytics. |
   |Total request time |The time from when a network request is initiated (preparing to establish the link) to when the network request is completed (when the response has been fully received).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Click the setting button on the right side of the request total time tab to navigate to the <strong>platform setting</strong> page, where you can configure the <strong>network request time upper limit</strong>.</div><br> |
   |DNS time |DNS resolution time for network requests. |
   |TCP time |Tcp connection time for network requests. |
   |SSL time |SSL Handshake Time for the network request. |
   |Send time |The time from when request data begins to be sent until sending is complete. |
   |Waiting time |The time from the completion of sending request data to the start of receiving response data. |
   |Received time |Time from when response data begins to be received to when reception is complete. |
   |Request byte count |Total amount of data sent or uploaded by network requests, unit: bytes. |
   |Received bytes |Total amount of data received or downloaded by network requests, unit: bytes. |
   |Scheduling analysis |By analyzing the client\-side IP and server\-side IP, cross\-region scheduling and cross\-Internet Service Provider scheduling can be determined. |
   

* Network details: Click **Network details** to enter the **Log search** page and view single\-point network log details.


<span id=".5pel5b-X5qOA57Si"></span>
### log search

Log search allows you to view network reporting trends and single\-point details data under specified filter conditions, and analyze detailed network timing and failure causes.


* You can navigate to the log filter from the network overview and network error screens.

* Log filter allows you to view the time taken for detailed data analysis and the specific reasons for failure for each network point.


<span id=".572R57uc6ZSZ6K-v"></span>
## network error

You can view network error metrics for app network requests and perform attribution, including the type of failure, proportion, and failure details.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Due to a network error, only part of the sampled data is displayed.</div>


<div data-tips="true" data-tips-type="tip">Whether all data is reported depends on whether you have configured full reporting for network errors. You can view all reported data in the log query. Configuration path: <strong>SDK reporting configuration \> sampling rate configuration for each module \> network analytic</strong>.</div>


<span id="d5a7aa05"></span>
### Filter conditions

You can filter data using the following filter criteria.


* Filter dimensions supported by the Android operating system:

   Time, Device ID, User ID, OS Version, APP Version, APP Minor Version Number, Device Model, APM SDK Version, Download Channel, Custom Dimension.

* Filter dimensions supported by the iOS operating system:

   Time, Device ID, User ID, Jailbreak Status, OS Version, App Version, App Minor Version Number, Device Model, APM SDK Version, Download Channel, Custom Dimension.

* General filter conditions include network\-related filter conditions:

   Domain name, interface, network type, country, province, Internet Service Provider, return code, HTTP method, network error code, network log type, Host (header), network library name, server IP, server country, server province, server Internet Service Provider, cache.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Only the Android client supports filtering data based on cache.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Filter no network status. On Android, in <strong>network type</strong>, select <code>no network</code>; on iOS, in <strong>network error code</strong>, select <code>-1009</code>.   </div>
   


<span id="52632368"></span>
### Error dashboard

The network error dashboard displays a trend chart of network error metrics under filter conditions, enabling assessment of the overall network quality status. On the right side of the metric data, you can view the changes in network error data compared to the previous period.

The error code trend chart for all network errors, based on the selected filters, helps you understand error reporting trends and report volume.


* iOS: Network errors reported on iOS are provided by the operating system. For the specific corresponding codes (API introduction), refer to [URLError.Code](https://developer.apple.com/documentation/foundation/urlerror/code/).

* Android: The backend parses the following error categories. Any reported error codes of these types will be parsed and displayed. If other error codes are reported, they will be displayed in the list as "Unknown error [error code]".


```JSON
{
"1": "Unknown error",
"2": "Connection timed out",
"3": "SOCKET timed out",
"4": "IO error",
"5": "SOCKET error",
"6": "The other side closed the connection",
"7": "Error binding port",
"8": "An exception occurred in the connection",
"9": "no route to host",
"10": "Port is unavailable",
"11": "Unknown host, domain name resolution failed",
"12": "Connection reset",
"13": "Connection refused",
"14": "Server is unreachable, no routing node to the server was found",
"15": "Network is unreachable",
"16": "Address is unavailable",
"17": "Address is already in use",
"18": "No HTTP response",
"19": "Client protocol error",
"20": "File is too large",
"21": "Too many redirects (usually occurs in circular redirects)",
"31": "Unknown client error",
"32": "Insufficient disk space",
"33": "File or directory does not exist",
"34": "Insufficient disk quota",
"35": "EROFS:",
"36": "Permission denied",
"37": "IO error",
"38": "json_exception",
"39": "security_exception",
"40": "No network",
"41": "Network cancelled"
}
```


<span id=".6ZSZ6K-v56CB"></span>
### Error distribution list

The error distribution list displays the quantity and proportion of all network errors for the selected filter conditions.

Clicking the list takes you to the log search page.

<span id="4b3bd9d6"></span>
#### Android error code descriptions


|Error code |DescriptionS |
|---|---|
|Unknown error [1] |Exceptions thrown by the client network library that are not individually grouped.<br><br>Click the network error code in the error distribution list to enter the details page, where you can view specific exception classes and exception information. |
|unKnown\-Android[0] |Typically, the setting is configured to use the local cache, and no network request is sent.<br><br>It can be determined by the Cache status in the distribution details.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Two necessary conditions for Cache monitoring:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Use OkHttp 4.7+</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The minimum supported version of apm_insight <code>1.5.1.cn-rc.5</code></div><br><br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e7db0761944c45209dcf55f1740a27f9~tplv-goo7wpa0wc-image.image) </span><br><br><br>* If the necessary conditions for Cache Monitoring are not met, the Cache distribution defaults to No Cache, which serves no purpose.<br><br>* If the necessary conditions for Cache Monitoring are met, No Cache indicates that Cache usage has not been configured. |


<span id="ed0f190f"></span>
### error alert

You can configure network error alert tasks on the **error alert** page and monitor network success rate and response time. For network anomalies, alerts can be received immediately to facilitate troubleshooting.


* Network error types can be filtered using domain name and path as filter criteria.

* Configure alert tasks based on metrics such as failure rate. If a network exception occurs, such as the success rate or response time exceeding the threshold, an alert will be triggered and an alert email message will be sent.


<span id="DNS"></span>
## DNS

<span id="7957264f"></span>
### Filter criteria

You can filter data using the following filter criteria:

time, operating system, OS version, APM SDK Version, app version, device model.

<span id="fcfd970a"></span>
### Trend charts


* Provides the capability to analyze the distribution ranking and to perform trend chart analysis of DNS average time.

* The left side displays the rankings for regions, Internet Service Providers, and DNS Resolution Time, while the right side shows the trend chart for the top five regions by DNS Resolution Time.

* A list of time metrics for each location and time period is provided below the trend chart.
