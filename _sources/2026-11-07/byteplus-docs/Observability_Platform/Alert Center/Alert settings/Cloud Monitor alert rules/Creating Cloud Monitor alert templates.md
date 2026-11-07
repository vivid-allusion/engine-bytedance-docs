---
title: "Creating Cloud Monitor alert templates"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Creating_Cloud_Monitor_alert_templates"
---

An alert template is a collection of alert rules and resource types for various cloud services. This helps you quickly create alert rules. This topic describes how to create a Cloud Monitor alert template.

<span id="g1fGIgIZ"></span>
## Limits


* Each root user can have up to 1,000 alert templates at the same time.

* Each alert template can contain up to 100 alert object groups.


<span id="Q5qDicF7"></span>
## Procedure


<Tabs>
<Tab zoneid="IhOycP8h7G" title="Method 1: Create a Cloud Monitor alert template">
<TabTitle>Method 1: Create a Cloud Monitor alert template</TabTitle>

Create an alert template from scratch in the console. Configure the resource type, trigger condition, and other information for the alert object. After you save the template, you can reuse it to quickly generate alert rules. This method applies to scenarios that involve custom configuration requirements or require standardized, reusable templates.


2. Log in to the [Observability Platform console](https://console.byteplus.com/observe).

3. In the left navigation pane, click **Alert Center \> Alert Configuration** to go to the Alert Configuration page.

4. In the alert configuration section on the left, select **Cloud Monitor** and click the **Alert template** tab.

5. Click **Create alert template** and configure the relevant parameters for the Cloud Monitor alert template as needed. After you complete the configuration, click **Create**.

   
   |Category |Parameter |Description |
   |---|---|---|
   |Basic information |Name |Specify a custom name for the alert template. |
   |Alert object |Resource type |Specify the type of cloud products under monitoring. Supported cloud service types displayed in the console shall prevail. |
   ||Subnamespace |Specify the resource subnamespace of the monitored cloud service. |
   |Alert rules |Preset trigger condition<br><br> |The preset alert trigger conditions. Click **Use preset trigger conditions** and the system will automatically populate the metric type and trigger condition. You can modify, delete, and add automatically generated trigger conditions.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If a certain <strong>dimension</strong> of a cloud product does not have preset trigger conditions, this button will be grayed out and trigger conditions cannot be generated automatically.</div><br> |
   ||Rule name |Provide a custom rule name. |
   ||Metric type |Select the metric type. Available options: **Single\-metric** and **Multi\-metric**. If you need to monitor multiple metrics of a resource, you can select Multiple\-metrics. |
   ||Trigger condition<br><br> |The trigger condition. When the monitored resource metric reaches the trigger condition, the system will send an alert notification. The following items are included:<br><br><br>* **Condition operator**: When **Metric type** is set to **Multi\-metric**, you can configure the relationship between multiple alert trigger conditions. Values:<br><br>   * **All**: Multiple alert trigger conditions have a logical **AND** relationship. This means that all conditions must be met simultaneously to trigger an alert.<br><br>   * **Any**: Multiple alert trigger conditions have logical **OR** relationship. This means that meeting any one condition will trigger an alert.<br><br>* **Cycles**: Specify the number of cycles that must meet the alert trigger condition to trigger an alert. For example, you can configure **In 1 cycles (1 cycle = 1 minute)** . You can also specify that N of M cycles meet the condition. For example: **In 3 periods (1 cycle = 1 minute), there are 2 cycles**.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If the <strong>Metric type</strong> parameter is set to <strong>Single metric</strong>, only one trigger condition can be set. When <strong>Metric type</strong> is set to <strong>Multi\-metric</strong>, you can configure one or more trigger conditions, with a minimum of 1 and a maximum of 10.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can use the same metric to configure multiple trigger conditions. However, within an alert rule, no two trigger conditions can have the same combination of <strong>metric name, statistical cycle, aggregation method, and comparison operator</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If a rule triggers both a threshold alert and a NoData alert at the same time, two notifications will be sent.</div><br><br><br>* **Metric name**: The alert metric for a cloud service. Supported metrics vary by cloud service. For example, when monitoring an ECS instance, you can select metrics such as CPU usage and CPU idle rate.<br><br>* **Statistical cycle**: The statistical cycle of the alert metric. Valid values: Recent 1 cycles, Recent 2 cycles, Recent 3 cycles, Recent 4 cycles, Recent 5 cycles, etc.<br><br>* **Aggregation method**: The method used to aggregate the alert metric within a statistical cycle. Valid values:<br><br>   * **Average**: The value calculated by averaging the raw values within the statistical cycles.<br><br>   * **Maximum**: The highest value among the raw values within the statistical cycles.<br><br>   * **Minimum**: The lowest value among the raw values within the statistical cycles.<br><br>* **Comparison operator**: The comparison operator between the alert metric value and the threshold. Available options include \>, \>=, <, <=, !=, =, Compare to Last Period Increase, Compare to Last Period Decrease, Compare to Last Period Increase or Decrease, Compare to The Same Period of Yesterday Increase, Compare to The Same Period of Yesterday Decrease, Compare to The Same Period of Yesterday Increase or Decrease, Compare to The Same Period of Last Week Increase, Compare to The Same Period of Last Week Decrease, and Compare to The Same Period of Last Week Increase or Decrease.<br><br>* **Alert level**: The alert severity level and its corresponding threshold. Different thresholds can be configured for different severity levels. Alert level options include **Critical**, **Warning**, and **Notification**.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">For example, when the trigger condition is configured as "Average disk usage \> 60%, 120 cycles (1 cycle = 1 minute)", the system checks the resource metric every 1 minute. An alert is triggered if the average disk usage of a resource exceeds 60% for 120 consecutive minutes.</div><br><br><br>* <div data-tips="true" data-tips-type="default">After you configure trigger conditions, you can click <strong>Preview</strong> or <strong>Alert test</strong> to preview and test alerts based on the trigger conditions.</div><br> |
   ||NoData alert<br><br> |Configure the NoData alert.<br><br><br>* Configure a trigger condition. If no data is reported for the specified resource for consecutive n cycles, a NoData alert will be triggered.<br><br>* Configure the level of the NoData alert. Valid values: **Critical**, **Warning**, and **Notification**.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">You can configure 3 to 20 cycles. The default value is 10 cycles.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Not all cloud service metrics support NoData alerts. "NoData alert" can be configured only when the following two conditions are met: <strong>"Dimension"</strong> in the "Alert object" section is set to <strong>"Instance"</strong> and the resource involves only one level of cloud service metrics. The actual console display shall prevail.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If a rule triggers both a threshold alert and a NoData alert at the same time, two notifications will be sent.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">NoData alert notifications will not be sent if the corresponding resource is deleted.</div><br><br><br>   <div data-tips="true" data-tips-type="warning">For example, the Resources parameter is set to All in the Alert object section. If Resource A is deleted and no data is reported for consecutive n cycles, no NoData alert will be sent.   </div><br>    |
   |Other operations |Mute For<br><br> |After an alert rule is triggered, if the monitored resource continues to trigger alerts, the system will send alert notifications at regular intervals to prevent excessive notifications.<br><br><br>* You can set the alert sending cycle to 5 minutes, 10 minutes, 15 minutes, 30 minutes, 60 minutes, 3 hours, 6 hours, 12 hours, or 24 hours.<br><br>* The default value is 5 minutes. |
   ||Notify mode<br><br> |* **Rule**: If any resource in an alert rule continuously exceeds the alert threshold within a notification cycle, only one alert notification is sent during that cycle.<br><br>* **Rule and Resource**: If different resources in an alert rule continuously exceed the alert thresholds within a notification cycle, an alert notification is sent separately for each resource during that cycle. If the monitored metrics are not recovered after the notification cycle ends, Cloud Monitor sends another alert notification for each resource. |
   ||Alert recovery notification<br><br> |A recovery notification is sent to users after the alert is cleared. The feature is enabled by default.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">For threshold alerts, if the resource generates no alert for consecutive 5 minutes, the alert is cleared.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">For NoData alerts, if the resource reports data for consecutive 5 minutes, the alert is cleared.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you set "Notification aggregation policy" to <strong>"Rule"</strong>, one alert recovery notification is sent after the alerts for all resources are recovered.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you set "Notification aggregation policy" to <strong>"Rule and Resource"</strong>, one alert recovery notification is sent each time the alerts for a resource are recovered.</div><br> |
   





</Tab>
<Tab zoneid="xaJIZTBshX" title="Method 2: Copy a preset Cloud Monitor alert template">
<TabTitle>Method 2: Copy a preset Cloud Monitor alert template</TabTitle>

You can copy the preset alert templates provided by the platform and adjust the configurations to generate new alert templates. This is suitable for getting started quickly or for customization based on official best practices.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The preset alert template applies to all resources of the specified resource type by default. When you copy this preset template, this configuration is cleared, and you need to reconfigure the new template.</div>



1. Log in to the [Observability Platform console](https://console.byteplus.com/observe).

2. In the left navigation pane, click **Alert Center \> Alert Configuration** to go to the Alert Configuration page.

3. In the alert configuration section on the left, select **Cloud Monitor** and click the **Preset alert template** tab.

4. Click **Copy to alert template** in the Actions column that corresponds to the target preset alert template. Specify a template name and then click **Confirm**.

5. Go to the **Alert Template** tab. Click **Edit** in the Actions column that corresponds to the copied template, adjust the configuration based on your business scenario, and then click **Save**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For detailed descriptions of parameters, see <code>Method 1: Create a Cloud Monitor alert template</code>.   </div>
   




</Tab>
<Tab zoneid="UZ2yiy8Jaa" title="Method 3: Import/export alert templates via JSON">
<TabTitle>Method 3: Import/export alert templates via JSON</TabTitle>

Export Cloud Monitor alert templates from another account as a JSON file and then import them into the Cloud Monitor alert templates of the current account. This method is suitable for copying multiple alert templates across accounts.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The import and export features enable quick synchronization of alert configurations across accounts, regions, projects, or workspaces for efficient reuse. Cloud Monitor alert templates are synchronized at the account level.</div>



1. Log in to the [Observability Platform console](https://console.byteplus.com/observe).

2. In the left navigation pane, click **Alert Center \> Alert Configuration** to go to the Alert Configuration page.

3. In the alert configuration section on the left, select **Cloud Monitor** and click the **Alert template** tab.

4. In the upper\-right corner, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c35cb0c323edd4d26fc0ea35f521975b.png) </span>icon and select an operation to perform it. Use the import and export features to import Cloud Monitor alert templates from another account into the Cloud Monitor alert templates within the current account.

   
   |Actions |Description |
   |---|---|
   |Export selected Cloud Monitor alert templates |Export the selected templates from the Cloud Monitor alert template list to a local JSON file.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can select only the entries on the current page of the list. You cannot select entries across pages.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Do not arbitrarily modify the structure of the JSON file. Otherwise, the import fails. If you lack professional expertise, we recommend not directly editing the JSON file.</div><br> |
   |Export all Cloud Monitor templates that match the search criteria |Export all Cloud Monitor alert templates that meet the filter criteria to a local JSON file. The export is not affected by pagination. You can filter data by resource type and name. |
   |Import a JSON file to generate Cloud Monitor templates |Use a JSON file to import Cloud Monitor alert templates from another account into the Cloud Monitor alert templates within the current account. During the import, you can specify a name suffix to avoid duplicate names.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Only alert templates of the same type can be imported. For example, you can export a Cloud Monitor alert template from Account A and import it into Cloud Monitor alert templates in Account B for use. However, Cloud Monitor templates cannot be imported into VMP alert templates.</div><br><br><br> |
   





</Tab>
</Tabs>


<span id="s3WbL7C8"></span>
## What to do next

Apply the alert template to an object group. Alert rules will be automatically generated based on this template for resource monitoring. For application steps, see [Applying alert templates to object groups](https://docs.byteplus.com/en/docs/Observability_Platform/Applying_alert_templates_to_object_groups).


&nbsp;

&nbsp;
