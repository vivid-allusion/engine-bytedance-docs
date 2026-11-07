---
title: "Alarm tasks"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Alert_tasks"
---

The alarm feature detects metric values or watchdog events and sends alarm messages when the configured conditions are met. With alarm tasks, you can monitor abnormalities in the metrics for configuration parameters of the target service and receive notifications in a timely manner, helping you keep track of the service's health status.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Basic metrics: Integrate APMPlus Server Agent to complete monitoring of hosts, containers, and processes.

* Service metrics: The service integrates with APMPlus, Skywalking, OpenTelemetry, Jaeger, Zipkin, runtime, AI, and other application monitoring capabilities.

* Custom metrics: Integrate APMPlus, OpenTelemetry, Prometheus, and other custom instrumentation capabilities.


<span id=".5oql6K2m5Y-R6YCB562W55Wl"></span>
## Alarm sending policy

When alarms are generated frequently, so that each execution of the alarm rule triggers an alarm, to reduce unnecessary alarms and avoid an alarm storm, you can control the frequency of alarm notification delivery and filter possible data spikes by configuring the alarm sending policy.


* Rule execution frequency: once per minute; sending policy: a sending cycle is 3 minutes.

   The alarm notification times are: 1 minute, 4 (1+3) minutes, 7 (1+3+3) minutes, 10 (1+3+3+3) minutes, and so on.

* Rule execution frequency: once per minute; sending policy: a sending cycle is 3 minutes. If triggered twice within one sending cycle, the alarm is sent on the second trigger (spike filtering).

   The alarm notification times are: 2 minutes, 5 (2+3) minutes, 8 (2+3+3) minutes, 11 (2+3+3) minutes, and so on.

* Rule execution frequency: once per minute; sending policy: a sending cycle is 3 minutes. If triggered twice within one sending cycle, the alarm is sent on the second trigger (spike filtering). Enable notification throttling. Alarm batch aggregation interval: 5 minutes.

   The alarm notification times are: 2 minutes, 5 (2+3) minutes, 11 (2+3+6) minutes, 23 (2+3+6+12) minutes, and so on.

   The aggregation is as follows: alarms sent at 2 minutes and 5 minutes are aggregated into one alarm group, alarms sent at 11 minutes form another alarm group, and alarms sent at 23 minutes form another alarm group.


In summary, by setting the sending cycle as d and the spike as k, the general calculation method for alarm notifications is as follows:

The alarm notification times are: k, k+20d, k+21d, k+22d, and so on.

The notification interval cannot exceed 60 minutes. If the threshold is exceeded, notifications are sent at 60\-minute intervals.

<span id=".5Yib5bu65oql6K2m5Lu75Yqh"></span>
## Create alert tasks


1. Log in to the [Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server). 

2. Select the region.

3. In the upper left corner of the console, select **Alert Management \> Alert Task**.

4. On the **Alert Task** page, click **Create Alert Task**.

7. On the **Create Alert Task** page, complete the configuration, then click **Save**.

   The parameter descriptions are as follows:

   
   |**Sections** |**Parameter** |**Descriptions** |
   |---|---|---|
   |Basic information |Alarm task name |Custom name, used to identify the alert task. |
   |Alert policy |workspace |Select a workspace to filter services.<br><br>A workspace is a data management and data isolation method provided by application performance monitoring. Each workspace has an independent data reporting credential. According to the feature of application ownership, the corresponding trace, log, and metric data can be managed in a unified manner. |
   ||Alarm Type |Supported alert types: service, custom metric, host, process, container, Watchdog, runtime, and AI.<br><br>WatchDog requires configuration of the monitoring type and event name. WatchDog events can be queried in the Event Center. |
   ||Alert level |Alert level supports multiple selections and allows setting different alert levels for different metric values.<br><br><br>* Notice: Note<br><br>* Warning: Warning<br><br>* Fatal: Severe |
   ||Alert engine |Threshold engine. |
   ||Relationship between multiple policies |When configuring multiple policy relationships, you can configure the relationships between policies.<br><br><br>* All conditions met: Default configuration. An alert is triggered only when all policies are satisfied.<br><br>* Any condition met: An alert is triggered when any one of the policies is satisfied. |
   ||Alert trigger policy |* Metric query: Different alert types have different metrics.<br><br>* Filter conditions: On the basis of metrics, add filter conditions to locate more precise data.<br><br>   Filter conditions include: service type, service name, interface name, downstream service type, downstream service name, downstream interface name, status code, host, and process ID.<br><br>* Grouping: Multi\-dimensional grouping is supported.<br><br>   After turning on group alerts, an alert is triggered if any group meets the alert condition. For example, if there are multiple services and service grouping is enabled, an alert is triggered if any service meets the alert threshold. This feature allows you to use a single alert rule to implement alerts and monitoring for all groups.<br><br>* Trigger condition: Define the alert trigger rule. By configuring the time window, aggregation method, and judgment condition, automatic detection of metric anomalies is achieved.<br><br>   * Time window: Specifies the statistical time range. For example, "within the last 5 minutes" means only the metric data generated within this period is analyzed.<br><br>   * Time interval: Defines the time granularity for data aggregation. For example, "5 minutes" means that metric data is aggregated every 5 minutes.<br><br>   * Aggregation method: Performs statistical calculations on metric data within the time interval. For example: AVG (the average value of the metric within N minutes), MAX (the maximum value of the metric within N minutes), MIN (the minimum value of the metric within N minutes), SUM (the sum of the metric within N minutes), and more, to generate an aggregate value that can be evaluated.<br><br>   * Evaluation criteria: By selecting the evaluation type (for example, threshold or ratio), comparison operators (for example, \>, <, =), and evaluation values, you define the logic for the trigger condition. When the result of the aggregation calculation meets the threshold condition, an alert of the corresponding level is triggered.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>   * <div data-tips="true" data-tips-type="default">Threshold: When the number of exceptions within a single time window reaches a certain amount, an alert is triggered.</div><br><br><br>   * <div data-tips="true" data-tips-type="default">Ratio: Refers to whether the increase or decrease in the value within a single time window, compared to the value in the same time window n time units ago, exceeds the configured value.</div><br> |
   ||Associated service |Select the service to which it belongs.<br><br>Sometimes, issues with data in Service A may actually be caused by Service B. |
   ||Project |The project to which the alert task belongs. Project management is a resource management mechanism that  provides to enable grouping of cloud resources by project. Project\-based authorization with Identity and Access Management (IAM) facilitates resource isolation and data security, while streamlining expense allocation and auditing for diverse cloud resources.  |
   ||Tags |A label is a key\-value pair that allows you to classify and aggregate cloud resources from different dimensions. You can use labels for resource authorization and bill splitting. <br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">A maximum of 20 tags can be added to the same alarm task.</div><br> |
   ||Custom label |Customize label and value. You can filter by tag in the alert list. |
   ||Alert verification |Select the time point to trigger the alert and verify whether the alert event is generated as expected. |
   |Alert sending policy |Rule execution frequency |Set the rule's running frequency in minutes/times. The default is once per minute. |
   ||Sending policy |* Set the sending period. The default is one minute per sending period.<br><br>* Set which occurrence of the alert within a sending period triggers the notification. By default, the alert is triggered on the first occurrence within a sending period. |
   ||Notification throttling |When enabled, if alarms are triggered continuously, the sending interval will gradually increase.<br><br>The attenuation policy is: next sending interval = current sending interval \* 2. For example, the first sending interval is 1 minute, the second is 2 minutes, the third is 4 minutes, the fourth is 8 minutes, and so on. |
   ||Alert batch aggregation interval |Set aggregation for alerts that occur within n minutes of each other.<br><br><br>* When an alert is generated, if there is an alert within the previous n minutes, it is merged with the alert from the previous n minutes into one alert group.<br><br>* When an alert is generated, if there is no alert within the previous n minutes, a new alert group is created and it is not merged with the alert from the previous n minutes. |
   |Notification method |Alert way |Alerts are supported via Feishu, email, and webhook. For details on webhook configuration, see [How to configure webhook?](https://docs.byteplus.com/en/docs/apmplus/How_to_configure_a_webhook). |
   |Alert description |Alarm description |Enter the alert description. |
   


<span id=".57yW6L6R5oql6K2m5Lu75Yqh"></span>
## Edit alert tasks


1. Log in to the [Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server). 

2. Select the region.

3. In the upper left corner of the console, select **Alert Management \> Alert Task**.

4. On the **Alert Task** page, find the target alert task. In the **Actions** column on the right, click **Edit**.

7. On the **Edit Alert Task** page, modify the configuration, then click **Save**.

   For parameter descriptions, see [Create Alert Task](https://docs.byteplus.com/en/docs/apmplus/Alert_tasks?lang=en&TagIDs=2,238#.5Yib5bu65oql6K2m5Lu75Yqh).


<span id=".5aSN5Yi25oql6K2m5Lu75Yqh"></span>
## Copy alert tasks


1. Log in to the [Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server). 

2. Select the region.

3. In the upper left corner of the console, select **Alert Management \> Alert Task**.

4. On the **Alert Task** page, find the target alert task. In the **Actions** column on the right, click **Copy**.

7. On the **Create Alert Task** page, modify the configuration, then click **Save**.

   For parameter descriptions, see [Create Alert Task](https://docs.byteplus.com/en/docs/apmplus/Alert_tasks?lang=en&TagIDs=2,238#.5Yib5bu65oql6K2m5Lu75Yqh).


<span id=".5Yig6Zmk5oql6K2m5Lu75Yqh"></span>
## Delete alert tasks


1. Log in to the [Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server). 

2. Select the region.

3. In the upper left corner of the console, select **Alert Management \> Alert Task**.

4. On the **Alert Task** page, find the target alert task. In the **Actions** column on the right, click **Delete**.

7. In the confirmation dialog, click **Confirm**.


<span id=".5p-l55yL5oql6K2m5Lu75Yqh5YiX6KGo"></span>
## **View alert task list**


1. Log in to the [Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server). 

2. Select the region.

3. In the upper left corner of the console, select **Alert Management \> Alert Task**.

4. On the **Alert Task** page, view alert tasks.

   The alert tasks page centrally displays all alert configurations. All alert tasks can be viewed and managed on this page, with support for filtering by status and type.

   The list includes the task name, alert type, alert rule summary, alert method, the number of alerts in the past month, status, and the actions column. The actions column supports toggling, editing, copying, and deleting alert tasks.


<span id=".5p-l55yL5oql6K2m6K-m5oOF"></span>
## **View alert details**


1. Log in to the [Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server). 

2. Select the deployment region.

3. In the upper left corner of the console, select **Alert Management \> Alert Tasks**.

4. On the **alert tasks** page, click the alert task name to go to the alert details page.

   The details page consists of three sections: **alert rule summary**, **alert trend chart**, and **alert history**.

   * Alert rule summary: Displays the alert rule and its running status. You can toggle, edit, and ACK the alert task.

      * ACK will suppress alert messages for three hours. Suppressed messages do not send alert notifications. Alerts generated during the suppression period can still be viewed in alert history.

   * Alert trend chart: Displays the metric trend chart monitored by the alert task. If an alert is triggered, a red dot appears in the chart.

   * Alert history: Displays the send time of triggered alerts, rule snapshot, alert metric value, and notification method for each alert occurrence.


&nbsp;
