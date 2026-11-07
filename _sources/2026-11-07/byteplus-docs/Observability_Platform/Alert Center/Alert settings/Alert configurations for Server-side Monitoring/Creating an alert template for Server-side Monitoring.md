---
title: "Creating an alert template for Server-side Monitoring"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Creating_an_alert_template_for_Server-side_Monitoring"
---

Alert templates provide the ability to inject alert rules, solving the problem of batch configuration. This topic describes how to create Server\-side Monitoring alert templates.

<span id="VVQECTD0"></span>
## Procedure


<Tabs>
<Tab zoneid="Tq6zPwFRQn" title="Method 1: Create an alert template">
<TabTitle>Method 1: Create an alert template</TabTitle>

You can create an alert template from scratch via the console by configuring the alert type, alert policy, delivery policy, and other settings in sequence. Once saved, the template can be reused to quickly generate alert rules. Applicable to scenarios that require personalized configurations or the establishment of standard templates.


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard).

2. In the left navigation pane, click **Alert Center \> Alert settings** to open the "Alert settings" page.

3. In the alert configuration section on the left, select **Server\-side Monitoring** and go to the **Alert template** tab.

4. Click **Create alert template**, configure the basic template information, and then click **Confirm**.

   
   |Parameter |Description |
   |---|---|
   |Name |Duplicate custom alert template names are not allowed. |
   |Alert type |Select an appropriate alert type. The available options include service alert, AI alert, and Claw Alert.<br><br><br>* **Service alert**: A general alert type that can be selected for services, runtimes, custom metrics, hosts, processes, and containers.<br><br>* **AI alert**: An alert type specifically for AI applications.<br><br>* **Claw alert**: An alert type specifically for ArkClaw applications. |
   

5. After the basic information is configured, you will be redirected to the **Alert rule** tab within the alert template details page. Click **Add alert rule**, configure the detailed rule settings, and then click **Save**.

   
   |Category |Parameter |Description |
   |---|---|---|
   |Basic information |Name of the alert rule |Specify a custom name for the alert rule. |
   |Alert policy |Alert level |The alert severity level when metrics trigger an alert. Supports multiple selections and setting different alert levels for different metric values.<br><br><br>* Notice: Info<br><br>* Warn: Warning<br><br>* Fatal: Critical |
   ||Alert engine |The alert threshold engine currently supports static thresholds. |
   ||Multiple\-policy logic |This is the logic for triggering alerts when multiple alert trigger policies are configured.<br><br><br>* **All met**: The default configuration. Alerts are triggered only when all policies are met simultaneously.<br><br>* **Any met**: Alerts are triggered when any one of the policies is met. |
   ||Alert trigger policy |The specific policy for triggering alerts requires the following parameters to be configured:<br><br><br>* **Alert metric**: Select the metric for which you want to set up alerts. The available metrics vary by alert type. The actual metrics are subject to the exact options displayed on the console.<br><br>* **Filter criteria**: Apply filters on top of the selected metric to narrow down and pinpoint more precise data. Filter conditions include: service type, service name, interface name, downstream service type, downstream service name, downstream interface name, status code, host, process ID, and more.<br><br>* **Grouped alert**: Provides multi\-dimensional grouping, enabling a single alert rule to be effective for all groups. When no group is configured, an alert is triggered if the single aggregated metric across all dimensions meets the condition. When a group is configured, an alert is triggered if any group's aggregated metric meets the condition.<br><br>* **Trigger condition**: Define the rules for triggering alerts. Automatic detection of metric anomalies is achieved through time windows, aggregation methods, and judgment conditions.<br><br>   * Time window: Specifies the statistical time range. For example, "within the last 5 minutes" means that only metric data generated during this period is analyzed.<br><br>   * Time interval: Defines the time granularity for data aggregation. For example, "5 minutes" means that aggregation calculations are performed on metric data every 5 minutes.<br><br>   * Aggregation method: Performs statistical calculations on metric data within the time interval. Examples include AVG (average value over N minutes), MAX (maximum value over N minutes), MIN (minimum value over N minutes), and SUM (sum over N minutes). These are used to generate evaluable aggregated values.<br><br>   * Evaluation condition: Defines the evaluation logic for trigger conditions by selecting the judgment type (e.g., threshold, ratio), comparison operator (e.g., \>, <, =), and threshold value. An alert at the corresponding severity level is triggered when the aggregated result meets the threshold condition.<br><br>      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Threshold: An alert is triggered when the number of anomalies within a single time window reaches a certain threshold.      </div><br>      <br><br>         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Ratio: Indicates whether the increase or decrease value (change range) within a single time window, compared to the value from the same time window n time units ago, exceeds the configured threshold.      </div><br>       |
   ||No\-data policy |Notification policy for when no metric data is reported<br><br><br>* Ignore: Ignore it and do not send a notification.<br><br>* No\-data notification: If no data is reported after the specified time, send a notification message. |
   ||Custom label |Customize labels and values. You can filter by label in the alert list. |
   |Alert send policy |Rule evaluation frequency |The rule evaluation frequency defaults to once per minute. Combined with other alert send policy configurations, this reduces invalid alert noise and prevents alert storms. |
   ||Send policy |The policy for sending the first alert within a sending interval. It is mainly used for spike filtering to avoid multiple alerts due to the threshold being exceeded frequently. The default send cycle is 3 minutes. If an alert is triggered once within a cycle, it is sent on the first occurrence. |
   ||Send frequency reduction |The de\-escalation policy for alert notifications during continuous alert triggering. If enabled, during continuous alert triggering, the send interval will gradually increase to avoid alert storms.<br><br>The specific policy is as follows:<br><br><br>* When the send period is \>= 1 hour, the de\-escalation logic is not triggered.<br><br>* When the send period is < 1 hour, after each send, the send period = min(send period \* 2, 1h). For example, the first send period is 1 minute, the second is 2 minutes, the third is 4 minutes, the fourth is 8 minutes, and so on. |
   ||Alert batch aggregation interval |Aggregate alerts with an interval not longer than N minutes.<br><br><br>* When an alert is generated, if an alert exists within the previous N minutes, then the alerts from the previous N minutes are aggregated into one alert group.<br><br>* When an alert is generated, if no alert exists within the previous N minutes, then a new alert group is generated. |
   |Alert description |Alert description |Fill in the notes or description for the alert rule. |
   





</Tab>
<Tab zoneid="mdGHA2roRU" title="Method 2: Copy an existing alert template">
<TabTitle>Method 2: Copy an existing alert template</TabTitle>

Copy a custom alert template and adjust its configuration to generate a new alert template. This is suitable for getting started quickly or for customizing based on existing best practices.


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard).

2. In the left navigation pane, select **Alert Center \-\> Alert settings** to open the "Alert settings" page.

3. In the alert configuration section on the left, select **Server\-side Monitoring** and go to the **Alert template** tab.

4. Click **Copy** in the operation column on the right side of an existing alert template to quickly create a new alert template based on the existing one.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When an alert template is copied, its alert rules and application scope are copied too.   </div>
   


</Tab>
<Tab zoneid="iMVOCVQcQh" title="Method 3: Copy a preset alert template">
<TabTitle>Method 3: Copy a preset alert template</TabTitle>

You can copy the preset alert templates provided by the platform and adjust the configurations to generate new alert templates. This is suitable for getting started quickly or for customization based on official best practices.


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard).

2. In the left navigation pane, select **Alert Center \-\> Alert settings** to open the "Alert settings" page.

3. In the alert configuration section on the left, select **Server\-side Monitoring**, and go to the **Preset alert template** tab.

4. Click **Copy** in the Actions column of the target preset alert template to quickly create a new alert template based on it.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When an alert template is copied, its alert rules and application scope are copied too.   </div>
   


</Tab>
<Tab zoneid="gc2Txtoybr" title="Method 4: Import/export alert templates via JSON">
<TabTitle>Method 4: Import/export alert templates via JSON</TabTitle>

You can export Server\-side Monitoring alert templates from other regions as JSON files and then import them into the current region. This is particularly useful for batch replicating alert templates across accounts or regions.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The import and export features enable quick synchronization of alert configurations across accounts, regions, projects, or workspaces for efficient reuse. The synchronization granularity of Server\-side Monitoring alert templates is down to the "region" level.</div>



1. Log in to the [Observability Platform console](https://console.byteplus.com/observe).

2. In the left navigation pane, click **Alert Center \> Alert settings** to open the "Alert settings" page.

3. In the alert configuration section on the left, select **Server\-side Monitoring** and go to the **Alert template** tab.

4. In the upper\-right corner, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c35cb0c323edd4d26fc0ea35f521975b.png) </span>button, select Actions, and perform the corresponding operation. Use the import/export feature to import Server\-side Monitoring alert rules exported from other regions into the current region for use.

   
   |Actions |Description |
   |---|---|
   |Export selected Server\-side Monitoring alert templates |Export the selected templates from the Server\-side Monitoring alert template list to a local JSON file.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Only items on the current page can be selected. Cross‑page selection is not supported.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Do not arbitrarily modify the structure of the JSON file, because it may cause import failures. If you lack professional expertise, we recommend not directly editing the JSON file.</div><br> |
   |Export all Server\-side Monitoring templates that match the search criteria |Export all Server\-side Monitoring alert templates that meet the filter criteria to a local JSON file. The export is not affected by pagination. You can filter data by region or name. |
   |Import a JSON file to generate a Server\-side Monitoring template |Use a JSON file to import a Server\-side Monitoring alert template exported from another account into the current account. The import process allows you to configure the region and a name suffix.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Only alert templates of the same type can be imported. For example, you can export a Server\-side Monitoring alert template from account A and import it into account B for use. However, Server\-side Monitoring templates cannot be imported into Cloud Monitoring templates.</div><br><br><br> |
   





</Tab>
</Tabs>


<span id="3KSR3VfS"></span>
## What to do next

Use alert templates to create alert tasks quickly. For more details, see Method 3 in [Creating Server-side Monitoring alert rules](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_Server-side_Monitoring_alert_rules).
