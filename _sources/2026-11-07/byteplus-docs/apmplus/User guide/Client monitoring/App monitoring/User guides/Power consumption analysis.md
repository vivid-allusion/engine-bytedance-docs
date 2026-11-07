---
title: "Power consumption analysis"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Power_consumption_analysis"
---

Power consumption monitoring enables you to understand device power consumption metrics and the causes of power consumption, and also provides the capability to analyze abnormal power consumption. The power consumption analysis feature consists of three parts: power consumption metrics, power consumption factors, and abnormal trends.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Only Android supports battery analysis.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**


* Power analysis has been integrated. For details, refer to [Integrating with the Android SDK](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_Android_SDK_into_the_application).

* Power analysis has been configured. For details, refer to [SDK reporting configuration](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration).


<span id=".55S16YeP5oyH5qCH"></span>
## Battery metrics

<span id="62eb70c0"></span>
### Filter criteria

You can filter data using the following filter criteria.


* Filter dimensions supported by the Android system:

   Time, Device ID, User ID, Statistical value, System version, App version, App minor version number, Device model, APM SDK version, Download channel, Custom dimension.

* Battery analysis is not currently supported on iOS.


<span id=".6ICX55S15oyH5qCH6LaL5Yq_"></span>
### Trend chart

The power consumption metrics trend chart displays the trend of power consumption metrics under the filter conditions. You can also display the trend chart by grouping dimensions. To the right of the metric data, you can view changes in crash data compared to the previous period.

After completing the [prerequisites](https://docs.byteplus.com/en/docs/apmplus/Power_consumption_analysis#.5YmN5o-Q5p2h5Lu2), the platform will use the value of the **data collection interval** indicator under the power Monitoring module in the SDK\-reported configuration, which by default collects data every 5 minutes and then aggregates and reports it.

Indicator description:


|**Metric** |**DescriptionS** |
|---|---|
|The frontend current value |Power is the core metric for device power consumption, and it is determined by voltage and current.<br><br>In real\-world scenarios, voltage rarely changes, so current is a very good indicator for measuring power consumption. When the app is in the foreground, most of the power consumption is attributable to the app itself. When the sample size is sufficiently large, bad cases can also be eliminated, and the App is running in the foreground, the current can be used to measure the App's power consumption. |
|Battery temperature |Battery temperature indirectly reflects the power consumption of the device. In general, the higher the power consumption of a device, the higher its battery temperature. |


<span id="f2340e22"></span>
### Power consumption list

The power consumption list displays the current consumption and battery temperature values at each stage for the foreground of every page.

<span id=".6ICX55S16aG16Z2i5YiX6KGo"></span>
### Page details

The page details display the battery temperature distribution, battery temperature trends, and the ability to query individual devices.

<span id=".6ICX55S15Zug57Sg"></span>
## Power consumption factors

<span id="b914facd"></span>
### Filter criteria

You can filter data using the following filter criteria.


* Filter dimensions supported by the Android system:

   Time, foreground and background, process name, app version, statistical value, calculation method, app minor version number, download channel, system version, device model, APM SDK version, app page, custom dimension.

* Battery analysis is not currently supported on iOS.


<span id="ab94aacc"></span>
### Trend charts

The power consumption factor module conducted a preliminary analysis of the application's power consumption, using six attribution\-type indicators. You can view the trends of each type based on the selected filters. To the right of the attribution data, you can see the changes in the data compared to the previous period.

Indicator description:


|**Metric** |**DescriptionS** |
|---|---|
|Traffic |Usage statistics, including data usage and Wi\-Fi usage |
|Obtain Location duration |Locate the usage duration detected by monitoring |
|AlarmManager set count |Number of times the WakeUp type Alarm was triggered |
|WakeLock active duration |Duration for which WakeLock is held, and the time interval between PowerManager's releaseWakeLock() and acquireWakeLock(). |
|Process uptime |The time period from when a process starts until just before it is killed |
|User session duration |The duration a user remains in the foreground activity, the time the user enters the background minus the time the user enters the foreground. |


<span id="5cb5c658"></span>
### List of power\-consuming devices

You can also query the details of power metrics for individual points by using the DeviceID list.

<span id=".55S16YeP5byC5bi4"></span>
## Power anomaly

<span id="e0ba13f6"></span>
### Filter criteria

You can filter data using the following filter criteria.


* Filter dimensions supported by the Android system:

   Time, issue creation status, APP version, exception type, Device ID, User ID, APP minor version number, download channel, system version, device model, parsing status, APM SDK version, APP page, exception details, issue status, assignee, tag, custom dimension, PV custom dimension.

* iOS does not currently support battery analysis.


<span id="97162fea"></span>
### Trend chart

Abnormal power consumption trends are monitored using three metrics: the duration to obtain Location, the number of times AlarmManager is set, and the duration of WakeLock activation. If any of these exceed the threshold, it is considered abnormal power consumption. The threshold can be customized. To adjust the threshold, refer to [SDK reporting configuration](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration).

After completing [prerequisites](https://docs.byteplus.com/en/docs/apmplus/Power_consumption_analysis#.5YmN5o-Q5p2h5Lu2), the platform will determine whether power consumption is abnormal based on the values of the following metrics under the power monitoring module in the SDK\-reported configuration: **maximum duration of a single location session**, **number of location requests within 10 minutes**, **total location usage duration within 10 minutes**, **duration of a single wake lock hold**, **number of wake lock acquisitions within 10 minutes**, **total wake lock hold duration within 10 minutes**, **number of Alarm (wake_up type) wake\-ups within 10 minutes**, and **number of Alarm wake\-ups within 10 minutes**.

The indicator description:


|**Metric** |**DescriptionS** |
|---|---|
|Exception count |Number of reports of power anomalies under the filter criteria |
|Abnormal rate |Number of reported power anomalies under filter conditions / total number of launches (PV) under filter conditions |
|Abnormal number of people |Number of unique devices reporting power anomalies under filter conditions |
|Abnormal user ratio |Number of unique devices reporting abnormal power under filter conditions / total number of launches (UV) under filter conditions |


<span id="e6336e31"></span>
### Exception lists

For abnormal power consumption, similar problems are grouped into issues based on stack information. Click the issue title to analyze and locate the problem on the details page using dimensions, trends, and abnormal details.
