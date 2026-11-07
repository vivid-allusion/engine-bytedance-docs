---
title: "Event analytics"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Event_analytics"
---

In addition to built\-in metrics, Application Performance Management Plus App Monitoring also supports reporting custom metrics. The event analytic feature helps you view custom events, enabling you to better monitor and analyze application performance issues.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To help you better control your event consumption, only events added through <strong>Event management</strong> can be queried in <strong>Event Trend</strong>.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**

Event reporting has been integrated. For details, refer to [Android SDK integration](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_Android_SDK_into_the_application) or [iOS SDK integration](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_iOS_SDK_app).

<span id="51b9f6fd"></span>
## Event management

Currently, two event creation methods are available: create event and batch import via JSON. You can select the appropriate method based on your specific situation and usage requirements.


<Tabs>
<Tab zoneid="DwV57GSi2F" title="Create an event">
<TabTitle>Create an event</TabTitle>

1. Log in to [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client/console/overview), select **Client Monitoring** in the left navigation bar, and select the target region in the top navigation bar.

2. Click the target application name to go to the application service management page, and select **Use service** under the App Monitoring tab.

3. In the left navigation bar, select **All features \-\> Event management** to go to the event management page.

4. Click **Add Event**, configure the event information and reporting configuration according to the actual scenario, and after completing the configuration, click **Create**.



|Categories |Parameter |DescriptionS |
|---|---|---|
|Event information |Event name |Custom event name, used to identify the current event. Duplicate names are not allowed. |
||Event description |Notes or descriptions related to the event. If the event name does not fully convey the meaning of the event, it is recommended to supplement the description with detailed information to facilitate recording and understanding the details of the current event. |
||System |Select the appropriate App client for the event as needed. Currently supported clients are iOS, Android, and Harmony. |
||Tag |Select tags to associate with the event to quickly search or filter events by tag. |
|Reporting configuration |Rule name |The name of the custom event reporting rule, used to identify the current rule. |
||Sampling rate |It is recommended to reasonably configure the proportion of occurrences that are actually recorded and used for analysis and billing, based on business volume. For example, when 100 document edit events are triggered and the sampling rate is set to 50%, only 50 document edit events will be recorded for analysis and billing. |
||Conditions for rules |Matching rules for event reporting—only events that meet the rule criteria will be reported. Currently, event reporting rules can be configured based on four dimensions: App version, App version code, download channel, and DeviceID. |





</Tab>
<Tab zoneid="qXYhpmAHr6" title="JSON batch import">
<TabTitle>JSON batch import</TabTitle>

1. Log in to the [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client/console/overview), select **Client Monitoring** in the left navigation pane, and select the target region in the top navigation bar.

2. Click the target application name, navigate to the application service management page, and select **Use service** in the App Monitoring tab.

3. In the left navigation bar, select **All features \-\> Event management** to go to the Event management page.

4. Click **Json batch import**, paste the prepared event configuration, and once finished, click **confirm**.



|Parameter |DescriptionS |
|---|---|
|System |Select the applicable App clients for the event as appropriate. Currently supported clients are iOS, Android, and Harmony. |
|Json |Paste the prepared JSON code, then batch import events. JSON\-related field descriptions:<br><br><br>* **event_name**: Required field, event name. Type: String. Naming rules: maximum length is 50 characters; only digits, letters, and underscores are allowed; the first character must not be an underscore; must satisfy the `"^[a-zA-Z]\w*$" ` regular expression.<br><br>* **event_describe**: Optional. Event description. String type, maximum 50 characters.<br><br>* **sample_rate**: Optional; sampling rate. float64 type, if left blank, the default value is 100.<br><br>* **sample_rate_name**: Optional. Name of the sampling configuration. String type. If left blank or not configured, the default is `default_$event_name`. |





</Tab>
</Tabs>


<span id=".5LqL5Lu26LaL5Yq_"></span>
## event trend

Events successfully added through **Event management** can be analyzed using event trend to analyze metric data. It supports setting filter conditions for metric thresholds and filtering by dimension.

<span id="8cbcd2ae"></span>
### Filter criteria

You can filter data using the following filter conditions.


* Filter dimensions supported by the Android operating system:

   time, Device ID, User ID, OS version, APP version, APP minor version number, device model, APM SDK version, download channel.

* Filter dimensions supported by the iOS operating system:

   time, Device ID, User ID, jailbreak status, OS version, APP version, APP minor version, device model, APM SDK Version, download channel.


<span id="9c00d70d"></span>
### Trend charts

Under the filter conditions, the event trend displays three separate trend charts: one showing the top 5 events by report volume, one showing the top 5 events by user volume, and one showing the top 5 events by average reports per user. To the right of the metric data, you can view the changes compared to the previous period.


* The search box on the left supports fuzzy search by event name.

* The search results on the left display matching event items. When you click an event, the trend chart area on the right displays the trends of report volume, user count, and average reports per user for that event under the filter conditions.

* Expand the search results on the left. You can view the metrics and dimensions under that event.

   * Click the corresponding metric to display trend charts for **average**, **pct25**, **pct50**, **pct75**, and **pct90** on the right. The list below displays event metrics. Click a metric name to enter event metric details, where you can view event metric trends, event metric distribution, and metric intervals.

      **pct25**, **pct50**, **pct75**, and **pct90** are statistical data aggregation methods related to percentiles. pct stands for percentile. For example, **pct50** refers to the data at the 50th quantile when the data is sorted in ascending order, that is, the data point located at the 50% position after sorting.

   * Click the corresponding dimension. The right side displays trend charts showing the **report volume** and **proportion** for the TOP 5 dimensions. The list below displays event dimensions. Click a dimension name to enter event dimension details and view event dimension trends, event dimension distribution, and the dimension list.


<span id=".5LqL5Lu25YiX6KGo"></span>
### Event list

The event list displays the event name, most recent report time, report volume, user count, and average reports per user.


* Click **Download Data** to obtain a list of the first 10,000 events in `.xlsx` format.

* Click the event name to go to the event details page and view more detailed information.


<span id=".5LqL5Lu26K-m5oOF"></span>
### Event details

<span id="8e21a1ca"></span>
#### Event trend overview

The event trend displays the trends of report volume, user count, and average reports per user for the event within the filter criteria.

<span id="514b5e22"></span>
#### Event list

The list displays the details of **event metric**, **event dimension**, and **DID query**.


* Under the DID query tab, click the download button in the upper right corner to obtain the DID query list in `.xlsx` format. In addition to the DID, client occurrence time, and data report time displayed on the page, the list also includes metrics and dimensions.

* Under the DID query tab, enter the Device ID in the search box to query the DID.
