---
title: "Traffic monitor"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/traffic_monitor"
---

Traffic monitor helps you understand overall app traffic usage by establishing traffic metrics, and enables attribution of traffic consumption to specific URLs. You can also use the single\-point query to view high\-traffic issues reported by users.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Traffic monitor is supported only on Android.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The traffic monitor has been integrated. For details, refer to [Integrate Android SDK into your application](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_Android_SDK_into_the_application).

* The traffic monitor has been configured. For details, refer to [SDK setting](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration).


<span id=".5rWB6YeP5oyH5qCH"></span>
## traffic metric

<span id="f319cf84"></span>
### Filter criteria

You can filter data using the following filter criteria:

Time, System, Device ID, User ID, OS Version, App Version, App Minor Version Number, Device Model, APM SDK Version, Download Channel, Process Name, Custom Dimension.

<span id="63f791be"></span>
### Trend charts

Traffic metrics can be used to evaluate the overall usage of app traffic. Devices selected by sampling report traffic usage for the current time period every 10 minutes.

Metric description:


|**Metric** |**DescriptionS** |
|---|---|
|Traffic per process |After the app starts, it reports the total traffic consumed during the previous app start. |
|10\-minute traffic |Traffic usage within 10 minutes for devices selected by sampling |
|Foreground WiFi traffic from 10 minutes ago |Foreground Wi\-Fi traffic usage of sampled devices over a 10\-minute period. |
|The foreground mobile traffic from 10 minutes ago |Foreground mobile traffic usage on sampled devices over a 10\-minute period. |
|Background Wi\-Fi traffic over 10 minutes |Background Wi\-Fi traffic usage status on sampled devices within a 10\-minute period |
|10\-minute background mobile traffic |Background mobile traffic usage details within 10 minutes for sampled devices. |


<span id=".5rWB6YeP5byC5bi4"></span>
## traffic anomaly

The client collects traffic metrics every 10 minutes. If a traffic metric exceeds the configured traffic anomaly threshold and traffic anomaly sampling is triggered, the client reports the traffic anomaly data to the platform. View aggregated traffic consumption when a traffic anomaly occurs.

Traffic anomalies include the following scenarios:


* Excessive total traffic: Traffic consumed within 10 minutes exceeds the configured traffic anomaly threshold.

* Background traffic overload: Traffic consumed in the background scenario within 10 minutes exceeds the configured background exception traffic threshold.

* Excessive traffic with no page launched: When the app is launched without any page being started, the traffic consumed exceeds the configured background exception traffic threshold.


<span id="a4a1c2b7"></span>
### Filter criteria

You can filter data using the following filter criteria:

time, operating system, Device ID, User ID, exception type, OS version, APP version, APP minor version, device model, APM SDK Version, download channel, process name, custom dimension, PV custom dimension.

<span id=".5byC5bi46LaL5Yq_"></span>
### Exception trends

The traffic anomaly trend displays a trend chart of traffic anomaly metrics based on the filter conditions. On the right side of the metric data, you can view the changes in traffic anomaly data compared to the previous period.

Metric description:


|**Metric** |**DescriptionS** |
|---|---|
|exception count |Traffic anomaly count under filter conditions |
|Exception rate |traffic anomaly count under filter conditions / count of all exceptions under filter conditions |
|impacted user |User count impacted by traffic anomaly under filter conditions |
|impacted users rate |Number of impacted users due to traffic anomaly under filter condition / number of impacted users due to all exceptions under filter condition |


<span id=".5byC5bi45YiG5biD"></span>
### Exception distribution

The anomaly distribution page displays the distribution of traffic anomaly data across various dimensions.


* The platform displays the following four dimensions by default: OS version, app version, app minor version number, and device model. You can click the setting button in the upper right corner to customize the distribution dimensions. A maximum of four dimensions can be selected.

* By default, the platform displays the distribution based on data about reported quantities. You can switch to viewing by user volume to see how traffic anomalies are distributed.


<span id=".5Lia5Yqh5byC5bi45YiX6KGo"></span>
### Business exception list

A traffic anomaly is caused by excessive traffic consumption. Traffic is consumed by the URLs requested by the network library. You can view exception details and locate anomalies based on the total traffic consumed by the network library and the average traffic consumption.


* The business exception list displays the business category, the start and end versions, the average size of traffic consumed by the network library, the total size of traffic consumed by the network library, and the sample size.

* Click the business type to view the exception trend, exception distribution, and exception list for that type on the details page.


<span id=".5rWB6YeP5byC5bi45Y2V54K5"></span>
## traffic anomaly point

The client collects traffic metrics every 10 minutes. If a traffic metric exceeds the configured traffic anomaly threshold and traffic anomaly sampling is triggered, the traffic anomaly data is reported to the platform. At the traffic anomaly point, view the specific traffic consumption for an individual device by selecting its DID.

<span id="b9f4afbd"></span>
### Filter dimensions

You can filter data using the following filter criteria:

time, operating system, Device ID, User ID, exception type, OS version, device model, APP version, APP minor version, APM SDK Version, download channel, ROM Information, province, process name, manufacturer, custom dimension.

<span id="fe37b9f9"></span>
### Exception list


* The exception list displays information about traffic anomaly data, including Device ID, collection time, total traffic, exception type, minor version number, OS version, and more.

* Device ID: Click to view detailed information about the device when a traffic anomaly occurs, including Device ID, UserID, client occurrence time, data report time, whether it was running in the background, as well as which network library and which URL requests specifically consumed the traffic.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the chart above, there is a significant difference in traffic between the two metrics, <strong>total traffic consumed in 10 minutes</strong> and <strong>okhttp (10\-minute traffic)</strong>, which is in line with product expectations. This is because the current SDK can only track the traffic from okhttp, and other traffic cannot be tracked.</div>



* <div data-tips="true" data-tips-type="tip">If you want to view the specific reason and have turned on the APMPlus log during integration, you can <strong>recover logs</strong> to check specific data such as page openings and other related information to assist with troubleshooting.</div>


* <div data-tips="true" data-tips-type="tip">If you confirm that there are no special operations in the business that consume traffic, but some devices still have issues where the system reports abnormal traffic usage.</div>


   <div data-tips="true" data-tips-type="tip">For Android 9 and later operating systems, traffic data is obtained through <code>NetworkStatsManager</code>, while for Android 8 and earlier operating systems, it is obtained through <code>/proc/net/xt_qtaguid/stats</code>. If a small number of devices experience inaccurate data returned by the operating system, you can go to the platform's <strong>SDK reporting configuration \> traffic monitor \> traffic anomaly monitoring sampling rate</strong> and set the sampling rate for the specified device did to 0 to prevent abnormal traffic data reporting from the current device.   </div>
