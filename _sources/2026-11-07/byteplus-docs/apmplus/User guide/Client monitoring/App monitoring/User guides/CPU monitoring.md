---
title: "CPU monitoring"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/CPU_monitoring"
---

A CPU anomaly occurs when an application in the foreground or background continuously consumes a large amount of CPU resources. Prolonged high CPU utilization can result in rapid battery drain, cause the device to overheat, and lead to other issues, making it essential to prioritize monitoring and optimization. CPU monitor provides online CPU metrics and offers a certain degree of CPU anomaly attribution analysis capabilities, enabling the identification of CPU anomaly issues using flame graphs.

<span id="a325e0e2"></span>
## Prerequisites


* CPU monitor has been integrated. For details, refer to [Application integration with Android SDK](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_Android_SDK_into_the_application) and [Application integration with iOS SDK](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_iOS_SDK_app).

* CPU monitor has been configured. For details, refer to [SDK setting](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration).


<span id=".Q1BV5oyH5qCH"></span>
## CPU metric

The CPU metric confirms the overall CPU usage status.

<span id="5707ddfc"></span>
### Filter conditions

You can filter data using the following filter criteria.


* Filter dimensions supported by the Android operating system:

   Time, Device ID, User ID, Foreground/Background State, OS version, app version, minor app version number, device model, APM SDK Version, download channel, collection scenario/page, network type, process name, whether it is the main process, remaining battery capacity, CPU model, charging status, whether power saving mode is turned on, device temperature status, battery temperature, device normal status, custom dimension.

* Filter dimensions supported by the iOS operating system:

   time, Device ID, User ID, Foreground/Background State, jailbreak status, OS version, app version, app minor version, device model, APM SDK Version, download channel, collection scenario/page, network type, and custom dimension.


<span id="1c309be6"></span>
### Metric trend chart

The CPU trend displays a chart of CPU metrics based on the selected filter conditions, and by default shows distribution trends such as sample size, average value, and other related data.

Click **Metric details** to view the metric trend chart and multidimensional distribution.

CPU monitoring provides two core metrics: **CPU utilization** (referred to as rate) and **CPU usage rate** (referred to as speed):

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The only CPU information that can be obtained from thread information in iOS is CPU utilization.</div>



|Metric |Method/description |
|---|---|
|CPU utilization |Within the sampling window, process CPU time divided by operating system CPU time |
|CPU Usage Rate |Within the sampling window: process CPU time / natural time |


Other descriptions:


* Each sampling corresponds to a 360 ms time window.

* CPU time, also known as CPU time, refers to the actual time the CPU spends running. It can be understood as the sum of all time slices. The CPU time of a process is the sum of the time slices allocated to the target process. The operating system CPU time is the sum of the time slices allocated to all processes. Therefore, 0 < rate < 1.

* For a single core in a multicore CPU, cpu time is the actual working time of that core. Here, for the entire CPU, cpu time is the sum of the cpu time of all cores. Therefore, 0 < speed < number of cores.


<span id="8ed81e62"></span>
### Metric details

On the CPU metric details page, you can view the usage trend chart and multidimensional analysis for a specific thread.

<span id=".Q1BV5byC5bi4"></span>
## CPU anomaly

A CPU anomaly occurs when an application in the Foreground or Background **continuously** **heavily** consumes CPU resources, resulting in serious power consumption and overheating issues. Locate exception classes and functions using stack trace trees and flame graphs.

After completing [prerequisites](https://docs.byteplus.com/en/docs/apmplus/CPU_monitoring#a325e0e2), the platform uses the metrics **Foreground process CPU Usage Rate exception threshold** and **Background process CPU Usage Rate exception threshold** under the CPU monitor module in the configuration reported by the SDK to determine whether the CPU Usage Rate exceeds the threshold.

If the CPU utilization continuously exceeds the threshold, the platform will, based on the metric **Thread CPU Usage exception threshold** under the CPU monitor module in the SDK configuration, identify threads whose CPU utilization exceeds the threshold and capture their stack trace.

<span id="e504f646"></span>
### Filter dimensions

You can filter data using the following filter criteria.


* Android operating system supported filter dimensions:

   time, stack trace details, Device ID, User ID, issue new status, Foreground/Background State, OS version, device model, app version, app minor version, APM SDK Version, download channel, ROM Information, province, usage duration, process name, manufacturer, collection scenario/page, issue status, assignee, tag, custom dimension, PV custom dimension.

* iOS\-supported filter dimensions:

   time, stack trace details, Device ID, User ID, issue new status, Foreground/Background State, jailbreak status, OS version, device model, app version, app minor version, APM SDK Version, download channel, province, usage duration, collection scenario/page, issue status, assignee, tag, custom dimension, PV custom dimension.


<span id=".Q1BV5byC5bi46LaL5Yq_"></span>
### CPU anomaly trends

The CPU anomaly trend chart displays the changes in CPU anomaly reporting under the specified filter conditions. On the right side of the metric data, you can view changes in crash data compared to the previous period.

Metric description


|Metric |DescriptionS |
|---|---|
|exception count |Total number of errors that occurred under filter conditions |
|Exception rate |Total number of errors under filter conditions / total number of times all users started under filter conditions |
|impacted user |Total number of users affected after global deduplication of filtered results |
|Overall user impact comparison |Total number of affected users after overall deduplication under filter conditions / total number of active users after overall deduplication under filter conditions |
|The average ratio of affected users |The sum of the overall affected user ratio at each time point divided by the number of time points with values |
|Average report count per start |The average number of logs reported by each user during an exception period can be used to estimate the duration of the exception. |


<span id=".Q1BV5byC5bi45YiX6KGo"></span>
### CPU anomalies list

The CPU anomaly list is aggregated and displayed based on exception threads and the function names in high\-frequency exception stack traces.

<span id=".Q1BV5byC5bi46K-m5oOF"></span>
### CPU anomaly details

The issue collected by the CPU anomaly feature consists of the information and stack traces of all CPU anomaly threads within a time window. Therefore, the collected information and stack traces can be converted into a flame graph.

<span id="0b353e5d"></span>
#### Overall call tree

The overall call tree flattens the stack traces of all CPU anomaly threads and aggregates them into a single tree, while also allowing direct viewing of the flame graph.

The number to the left of each function represents its "weight." A higher weight indicates that the function consumes more CPU resources. Therefore, in the flame graph, a wider function block corresponds to a greater weight.

<span id="d4dc9561"></span>
#### Thread call tree

The difference between the thread call tree and the overall call tree is that information and stack trace are separated at the thread level.

You can also view the information and stack trace of a specific CPU anomaly thread within this time window.

<span id="fe51d767"></span>
#### Issue summary call trees

The issue summary call tree no longer represents just a single issue; instead, it represents the aggregation of stack traces for all issues within the issue group.
