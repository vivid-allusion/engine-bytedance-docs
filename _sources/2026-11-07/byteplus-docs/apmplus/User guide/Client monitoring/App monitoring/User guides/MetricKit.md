---
title: "MetricKit"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/MetricKit"
---

In iOS 13, Apple provided the MetricKit framework. This framework analyzes and summarizes certain performance and power metrics for the app from the past 24 hours. In iOS 14, Apple further expanded exception monitoring capabilities, providing diagnostic reports on exceptions and crashes from the past 24 hours.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Only the iOS platform supports MetricKit.</div>


<span id="b89e2d91"></span>
## stability

The feature provides statistics and analysis related to stability in MetricKit (iOS), including crashes, CPU anomalies, disk issues, and lags.

<span id="7c9bea28"></span>
### Filter dimensions

You can filter data using the following filter criteria:

time, exception type, exception detail, Device ID, User ID, issue new status, Mach code, Signal code, system policy crash, jailbreak status, OS version, device model, app version, app minor version, APM SDK Version, download channel, app name, parsing status, issue status, assignee, tag, PV custom dimension.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Exception types include crash, CPU anomaly, lag, and disk monitor.</div>


<span id=".5byC5bi46LaL5Yq_"></span>
### Exception trends

The exception trend displays a trend chart of exception metrics under filter conditions, allowing users to see how two metrics for the issue change over time: exception count and affected user count. On the right side of the metric data, you can view changes in exception data compared to the previous period.

Metric description:


|Metric |DescriptionS |
|---|---|
|exception count |Exception count under filter conditions |
|Exception rate |Exception count under filter conditions / total launch count under filter conditions |
|Exception Impacted User count |Deduplicated UV count where exceptions occurred under filter conditions |
|Exception Impacted Users rate |Number of deduplicated unique visitors for which exceptions occurred under filter conditions / total number of deduplicated unique visitors under filter conditions |
|user count |Active user count under filter conditions |


<span id="689be1af"></span>
### Anomaly distribution

Supports multidimensional analysis to understand how exceptions are distributed across dimensions and to locate issues. You can also switch to other additional dimensions for querying.

<span id="ac9cc2de"></span>
### Exception crash list

The exception crash list displays the exception description, exception type, number of affected users, occurrence count, exception rate, most recent occurrence time, log report time, status, and assignee.

<span id=".6K-m57uG5L-h5oGv"></span>
### Detailed information

In the detailed information, you can view the properties of each field for a single exception. Click **Trace** next to the device ID or UserID to jump to [single point tracing](https://docs.byteplus.com/en/docs/apmplus/log_query) and view the complete context log stream. Use the upper right corner to switch exception.

<span id="1673a148"></span>
#### Exception summary

The exception summary provides the exception title, key stack trace information, latest report time, latest occurrence time, first occurrence time, exception count, exception impacted user count, exception rate, and exception impacted users rate.

<span id=".5Y6f5aeL5aCG5qCIJlJldHJhY2U="></span>
#### Raw stack trace and Retrace


* The symbol table has not been uploaded; the raw stack trace is displayed, that is, the stack trace information from the original log uploaded by the client.

* The symbol table has been uploaded. The displayed result is the parsed stack trace, shown as Retrace, which is the stack trace after symbolization. If the symbol table or parsing is incorrect, you can re\-upload the symbol table or click **Retry Retrace** in the Retrace interface.


<span id=".56ym5Y-36KGo"></span>
#### symbol table

You can manually upload the symbol table here.

<span id=".5byC5bi45L-h5oGv"></span>
#### Exception information

Key\-value information reported during a crash.

<span id="392feaf3"></span>
## Performance

This feature provides performance\-related statistics and analysis in MetricKit (iOS), including metrics such as CPU, GPU, location, network, and other metrics.

<span id="29951de5"></span>
### Filter dimensions

You can filter data using the following filter criteria:

time, Device ID, User ID, jailbreak status, OS version, device model, app version, app minor version number, APM SDK Version, download channel.

<span id="0271013d"></span>
### Performance trends

The Performance Trends section displays trend charts of performance metrics under filter conditions. By default, it shows the distribution trends of sample size, average value, and other metrics for dimensions such as running time, cellular network, CPU, GPU, positioning, and network transmission.

Click **metric details** to view metric trend charts, multidimensional analysis, and raw logs.

Metric description:


|Metric category |Metric |DescriptionS |Calculation formulas |
|---|---|---|---|
|Running time |Foreground duration |The total time the application runs in the foreground. |\- |
||Background runtime duration |Total time the application is active in the background. |\- |
||Background audio playback duration |Total time the application runs in the background and plays audio. |\- |
||Background location duration |The total time the application runs in the background and uses location services. |\- |
|Cellular network |Cellular network status |The overall status of the cellular network while the application is running. Signal strength is represented by the number of bars; unit: bars. |\- |
|CPU |CPU utilization |CPU usage while the application is running. |CPU usage duration / total running time \* 100% |
||Total CPU instructions per unit time |The number of CPU instructions executed by the application per unit of time during runtime. |Total number of CPUs / sum of running time \* 100% |
|GPU |GPU utilization |GPU usage rate during application runtime. |GPU usage duration / total runtime \* 100% |
|Positioning |High\-precision navigation usage rate |The usage rate of high\-precision navigation during application runtime. |high\-precision navigation usage duration / total operating time \* 100% |
||High\-precision positioning usage rate |High\-precision positioning usage rate during application operation |High\-precision positioning usage duration / total runtime \* 100% |
||Usage rate of 10\-meter accuracy positioning |Usage rate of ten\-meter accuracy positioning while the application is running. |10\-meter accuracy positioning usage duration / total operating time \* 100% |
||Usage rate of hundred\-meter accuracy positioning |Usage rate of 100\-meter\-accuracy positioning while the application is running |Usage duration of 100\-meter accuracy positioning / total running time \* 100% |
||Kilometer\-level positioning usage rate |Kilometer\-level positioning usage rate during application runtime. |usage duration of kilometer\-level positioning / total operating time \* 100% |
||Usage rate of 3,000\-meter accuracy positioning |Usage rate of positioning with three\-kilometer accuracy while the application is running. |Usage duration of positioning with 3,000\-meter accuracy / total running time \* 100% |
|network transmission |Cellular network download data volume per unit time |The amount of data downloaded via cellular network by the application per unit time during its runtime. |download data volume over cellular network / total runtime \* 100% |
||Amount of data uploaded to the cellular network per unit time |The amount of data uploaded over the cellular network per unit time while the application is running. |Amount of data uploaded via cellular network / total running time \* 100% |
||The amount of Wi\-Fi download data per unit time |The amount of data downloaded via WIFI per unit time during application runtime. |Wi\-Fi amount of data downloaded / total runtime \* 100% |
||Wi\-Fi data uploaded per unit time |Amount of data uploaded via Wi\-Fi per unit time during application runtime. |WIFI uploaded data volume / total operating time \* 100% |
