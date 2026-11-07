---
title: "Creating Cloud Monitor alert rules"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Creating_Cloud_Monitor_alert_rules"
---

To monitor the data status of a cloud service resource, you can create a Cloud Monitor alert rule. When the data of the monitored cloud service resources meets the alert trigger conditions, the system will send alert notifications using the specified method, allowing recipients to identify resources with abnormal data in a timely manner. This topic describes how to create a Cloud Monitor alert rule.

<span id="9q3FzTrz"></span>
## Prerequisites

You have selected an appropriate notification method and created a matching notification policy. The notification policy specifies the contacts who receive notification messages, notification templates, and other information. For more details, see [Creating notification policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_notification_policies).

<span id="9igB3OcA"></span>
## Limits


* When "Selection method" is set to **Manually select**, if "Resources" is set to  **"All"** , there is no limit on the number of resources you can add. If "Resources" is set to  **"Partial"** , you can add a maximum of 1,000 resources per resource type and a maximum of 5,000 resources across all resource types.

* When you select resources by **resource name**, **project** and **tag**, up to 1,000 resources can be matched.

* The following services allow you to select alert objects by project or tag.

   
   |**Service name** |**Namespace** |Supports project\-based selection |Supports tag\-based selection |
   |---|---|---|---|
   |NAT Gateway |VCM_NAT |✅ |✅ |
   |Classic Load Balancer (CLB) |VCM_CLB |✅ |✅ |
   |EIP |VCM_EIP |✅ |✅ |
   |Bandwidth Package |VCM_BandwidthPackage |✅ |✅ |
   |Elastic Compute Service (ECS) |VCM_ECS |✅ |✅ |
   |EBS |VCM_EBS |✅ |✅ |
   |Cloud Enterprise Network (CEN) |VCM_CEN |✅ |✅ |
   |Application Load Balancer (ALB) |VCM_ALB |✅ |✅ |
   |Torch Object Storage (TOS) |VCM_TOS |✅ |✅ |
   |RDS for MySQL |VCM_RDS_MySQL |✅ |✅ |
   |Cache for Redis \- Community Edition |VCM_Redis |✅ |✅ |
   |RDS for PostgreSQL |VCM_RDS_PostgreSQL |✅ |✅ |
   |Document Database for MongoDB \- replica set |VCM_MongoDB_Replica |✅ |✅ |
   |Document Database for MongoDB \- sharding cluster |VCM_MongoDB_Sharded_Cluster |✅ |✅ |
   |TR |VCM_TransitRouter |✅ |❌ |
   |Transit Router (TR) Bandwidth Package |VCM_TransitRouterBandwidthPackage |✅ |❌ |
   |Direct Connect (DC) \- DC gateway |VCM_DirectConnectGateway |❌ |✅ |
   |DC \- virtual interface |VCM_DirectConnectVIF |❌ |✅ |
   


<span id="KrKWneQN"></span>
## Procedure


<Tabs>
<Tab zoneid="TX7vmhq2Vh" title="Method 1: Create a custom alert rule">
<TabTitle>Method 1: Create a custom alert rule</TabTitle>

Create an alert rule from scratch via the console. Configure information such as the resource type, alert object, trigger condition, and notification policy in order. This method applies to on\-demand customization or scenarios with a small number of alert rules.


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard).

2. In the left navigation pane, click **Alert Center \> Alert Configuration** to go to the "Alert Configuration" page.

3. In the left "Alert settings" section, select **Cloud Monitor**, click **Create alert rule**, and configure the relevant parameters for the Cloud Monitor alert rule based on your actual needs.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Available regions and subnamespaces vary based on the cloud service type. The options displayed in the console shall prevail.   </div>
   

   
   |Category |Parameter |Description |
   |---|---|---|
   |Basic information |Name |Specify a name for the Cloud Monitor alert rule as a unique identifier. Duplicate names are not allowed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Alert notifications sent through SMS messages may fail to be delivered if certain characters are used in the name.</div><br> |
   |Alert object |Resource type |Specify the type of cloud products under monitoring. Supported cloud service types displayed in the console shall prevail. |
   ||Subnamespace |Specify the resource subnamespace of the monitored cloud service. |
   ||Selection method |* **Manually select**: Manually select resources.<br><br>* **Resource name**: Match resources by resource name.<br><br>* **Object Group**: Select resources based on object groups. For details, see [Creating object groups](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-a-resource-group).<br><br>* **Project**: selects resources based on projects. <br><br>* **Label**: selects resources based on labels.  |
   ||Region |If you set the **Selection method** parameter to **Manually select**, **Resource name**, **Project**, or **Tag**, you can select one or more regions to which the monitored resources are deployed. |
   ||Resource group |When **Selection method** is set to **Object Group**, you can select a created object group. |
   ||Resource |When **Selection method** is set to **Manually select**, you can set the resource scope for the alert rule. Only resources within the scope will be monitored.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If you select <strong>all resources</strong>, the number of resources is not limited.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you select <strong>part of</strong> resources, the number of resources is limited by the following rules:</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">You can add up to 1,000 resources per resource type as alert objects in an alert rule.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">You can add up to 5,000 resources across all resource types as alert objects in an alert rule.</div><br><br><br>* **All**: The alert rule is configured for all resources matching the specified resource type, region, and dimension under the current account.<br><br>   After you select this option, the alert rule automatically applies to newly created resources that meet the conditions.<br><br>* **Part**: You need to manually select one or more resources.<br><br>   After you select this option, the alert rule is configured only for the resources you specify. |
   ||Resource name |When **Selection method** is set to **Resource name**, you can set the resource scope for the alert rule. Only resources within the scope will be monitored.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">You can add multiple matching rules. Up to 10 matching rules can be added.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The resource name can be up to 100 characters in length.</div><br><br><br>* You can select the relationship between matching rules, which include **arbitrary satisfaction** and **All satisfied**.<br><br>* If you select Specific resources, you can match resources by resource name. The matching rules include **Prefix match**, **Suffix match**, **Contain**, **Not contain**, **Equal to**, and **Not equal to**.<br><br>   * If you set the **matching rule** to **Contain**, **Not contain**, **Prefix match**, or **Suffix match**, you can enter one resource name.<br><br>   * If you set the **matching rule** to **Equal to** or **Not equal to**, you can select multiple resources and must specify the **Region** parameter. |
   ||Project |When **Selection method** is set to **Project**, you can set the resource scope for the alert rule. Only resources within the scope will be monitored. |
   ||Tags |When **Selection method** is set to **Tag**, you can set the resource scope for the alert rule. Only resources within the scope will be monitored.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">You can add multiple matching rules. Up to 10 matching rules can be added.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The tag value can be up to 50 characters in length.</div><br><br><br>* You can select the relationship between matching rules, which include **arbitrary satisfaction** and **All satisfied**.<br><br>* You can select a tag key and filter resources with the tag key by the following rules, including **Exists and the prefix matches**, **Exists and the suffix matches**, **Exists and contains**, **Exists and does not contain**, **Exists and is equal to**, **Exists, but not equal to**, **Exist**, and Does not exist.<br><br>   * If you set the **matching rule** to **Exist**, all tag values of the corresponding tag keys are included, and you cannot enter a tag value.<br><br>   * If you set the **matching rule** to **Exists and is equal to** or **Exists, but not equal to**, you can select multiple tag values.<br><br>   * If you set the **matching rule** to **Exists and contains**, **Exists and does not contain**, **Exists and the prefix matches**, or **Exists and the suffix matches**, you can enter one tag value. |
   |Alert rules |Preset trigger condition<br><br> |The preset alert trigger conditions. Click **Use preset trigger conditions** and the system will automatically populate the metric type and trigger condition. You can modify, delete, and add automatically generated trigger conditions.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If a certain <strong>dimension</strong> of a cloud product does not have preset trigger conditions, this button will be grayed out and trigger conditions cannot be generated automatically.</div><br> |
   ||Metric type |Select the metric type. Available options: **Single\-metric** and **Multi\-metric**. If you need to monitor multiple metrics of a resource, you can select Multiple\-metrics. |
   ||Trigger condition<br><br> |The trigger condition. When the monitored resource metric reaches the trigger condition, the system will send an alert notification. The following items are included:<br><br><br>* **Condition operator**: When **Metric type** is set to **Multi\-metric**, you can configure the relationship between multiple alert trigger conditions. Values:<br><br>   * **All**: Multiple alert trigger conditions have a logical **AND** relationship. This means that all conditions must be met simultaneously to trigger an alert.<br><br>   * **Any**: Multiple alert trigger conditions have logical **OR** relationship. This means that meeting any one condition will trigger an alert.<br><br>* **Cycles**: Specify the number of cycles that must meet the alert trigger condition to trigger an alert. For example, you can configure **In 1 cycles (1 cycle = 1 minute)** . You can also specify that N of M cycles meet the condition. For example: **In 3 periods (1 cycle = 1 minute), there are 2 cycles**.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If the <strong>Metric type</strong> parameter is set to <strong>Single metric</strong>, only one trigger condition can be set. When <strong>Metric type</strong> is set to <strong>Multi\-metric</strong>, you can configure one or more trigger conditions, with a minimum of 1 and a maximum of 10.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can use the same metric to configure multiple trigger conditions. However, within an alert rule, no two trigger conditions can have the same combination of <strong>metric name, statistical cycle, aggregation method, and comparison operator</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If a rule triggers both a threshold alert and a NoData alert at the same time, two notifications will be sent.</div><br><br><br>* **Metric name**: The alert metric for a cloud service. Supported metrics vary by cloud service. For example, when monitoring an ECS instance, you can select metrics such as CPU usage and CPU idle rate.<br><br>* **Statistical cycle**: The statistical cycle of the alert metric. Valid values: Recent 1 cycles, Recent 2 cycles, Recent 3 cycles, Recent 4 cycles, Recent 5 cycles, etc.<br><br>* **Aggregation method**: The method used to aggregate the alert metric within a statistical cycle. Valid values:<br><br>   * **Average**: The value calculated by averaging the raw values within the statistical cycles.<br><br>   * **Maximum**: The highest value among the raw values within the statistical cycles.<br><br>   * **Minimum**: The lowest value among the raw values within the statistical cycles.<br><br>* **Comparison operator**: The comparison operator between the alert metric value and the threshold. Available options include \>, \>=, <, <=, !=, =, Compare to Last Period Increase, Compare to Last Period Decrease, Compare to Last Period Increase or Decrease, Compare to The Same Period of Yesterday Increase, Compare to The Same Period of Yesterday Decrease, Compare to The Same Period of Yesterday Increase or Decrease, Compare to The Same Period of Last Week Increase, Compare to The Same Period of Last Week Decrease, and Compare to The Same Period of Last Week Increase or Decrease.<br><br>* **Alert level**: The alert severity level and its corresponding threshold. Different thresholds can be configured for different severity levels. Alert level options include **Critical**, **Warning**, and **Notification**.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">For example, when the trigger condition is configured as "Average disk usage \> 60%, 120 cycles (1 cycle = 1 minute)", the system checks the resource metric every 1 minute. An alert is triggered if the average disk usage of a resource exceeds 60% for 120 consecutive minutes.</div><br><br><br>* <div data-tips="true" data-tips-type="default">After you configure trigger conditions, you can click <strong>Preview</strong> or <strong>Alert test</strong> to preview and test alerts based on the trigger conditions.</div><br> |
   ||Mute For<br><br> |After an alert rule is triggered, if the monitored resource continues to trigger alerts, the system will send alert notifications at regular intervals to prevent excessive notifications.<br><br><br>* You can set the alert sending cycle to 5 minutes, 10 minutes, 15 minutes, 30 minutes, 60 minutes, 3 hours, 6 hours, 12 hours, or 24 hours.<br><br>* The default value is 5 minutes. |
   ||Notify mode<br><br> |* **Rule**: If any resource in an alert rule continuously exceeds the alert threshold within a notification cycle, only one alert notification is sent during that cycle.<br><br>* **Rule and Resource**: If different resources in an alert rule continuously exceed the alert thresholds within a notification cycle, an alert notification is sent separately for each resource during that cycle. If the monitored metrics are not recovered after the notification cycle ends, Cloud Monitor sends another alert notification for each resource. |
   ||Alert recovery notification<br><br> |A recovery notification is sent to users after the alert is cleared. The feature is enabled by default.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">For threshold alerts, if the resource generates no alert for consecutive 5 minutes, the alert is cleared.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">For NoData alerts, if the resource reports data for consecutive 5 minutes, the alert is cleared.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you set "Notification aggregation policy" to <strong>"Rule"</strong>, one alert recovery notification is sent after the alerts for all resources are recovered.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you set "Notification aggregation policy" to <strong>"Rule and Resource"</strong>, one alert recovery notification is sent each time the alerts for a resource are recovered.</div><br> |
   ||NoData alert<br><br> |Configure the NoData alert.<br><br><br>* Configure a trigger condition. If no data is reported for the specified resource for consecutive n cycles, a NoData alert will be triggered.<br><br>* Configure the level of the NoData alert. Valid values: **Critical**, **Warning**, and **Notification**.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">You can configure 3 to 20 cycles. The default value is 10 cycles.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Not all cloud service metrics support NoData alerts. "NoData alert" can be configured only when the following two conditions are met: <strong>"Dimension"</strong> in the "Alert object" section is set to <strong>"Instance"</strong> and the resource involves only one level of cloud service metrics. The actual console display shall prevail.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If a rule triggers both a threshold alert and a NoData alert at the same time, two notifications will be sent.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">NoData alert notifications will not be sent if the corresponding resource is deleted.</div><br><br><br>   <div data-tips="true" data-tips-type="warning">For example, the Resources parameter is set to All in the Alert object section. If Resource A is deleted and no data is reported for consecutive n cycles, no NoData alert will be sent.   </div><br>    |
   |Advanced Settings |Project |Set the project of the alert rule. The default project is "default".  |
   ||Tags |Click **Add tag** to add tags to the alert rule. |
   |Alert way |Notification policy |Select an appropriate notification policy based on actual circumstances. A notification policy defines the recipients, delivery channels, and content display format for alert notifications when alerts of different levels are triggered or recovered. |
   





</Tab>
<Tab zoneid="sVhQ4cj7PU" title="Method 2: Import or export alert rules via JSON">
<TabTitle>Method 2: Import or export alert rules via JSON</TabTitle>

Export Cloud Monitor alert rules from another project as a JSON file and then import them into the Cloud Monitor alert rules of the current project. This applies to batch copying of alert rules across accounts, regions, or projects.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The import and export features enable quick synchronization of alert configurations across accounts, regions, projects, or workspaces for efficient reuse. The synchronization granularity for Cloud Monitor alert rules is at the project level.</div>



1. Log in to the [Observability Platform console](https://console.byteplus.com/observe).

2. In the left navigation pane, click **Alert Center \> Alert Configuration** to go to the "Alert Configuration" page.

3. In the alert configuration section on the left, select **Cloud Monitor** and click the **Alert Rule** tab.

4. In the upper\-right corner, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c35cb0c323edd4d26fc0ea35f521975b.png) </span>icon and select an operation to perform it. Use the import and export features to import Cloud Monitor alert rules from another project into the Cloud Monitor alert rules in the current project.

   
   |Actions |Description |
   |---|---|
   |Export the selected Cloud Monitor rules |Export the selected rules from the Cloud Monitor alert rule list to a local JSON file.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Only items on the current page can be selected. Cross‑page selection is not supported.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Do not arbitrarily modify the structure of the JSON file, because it may cause import failures. If you lack professional expertise, we recommend not directly editing the JSON file.</div><br> |
   |Export all Cloud Monitor rules matching search criteria |Export all Cloud Monitor rules that match the current filter criteria to a local JSON file. The export is not affected by pagination. You can filter data by region, project, resource type, and keyword. |
   |Import JSON file to generate Cloud Monitor rules |Use a JSON file to import Cloud Monitor alert rules exported from another account, region, or project into the current Cloud Monitor alert rules. You can configure the project and name suffix during the import.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Only rules of the same type can be imported. For example, you can export Cloud Monitor alert rules from the Beijing region and import them into Cloud Monitor alert rules in the Shanghai region. However, Cloud Monitor alert rules cannot be imported into VMP alert rules.</div><br><br><br> |
   





</Tab>
<Tab zoneid="Y7jDVnXtFe" title="Method 3: Create an alert rule using a template">
<TabTitle>Method 3: Create an alert rule using a template</TabTitle>

Quickly create alert rules based on the alert configurations built into platform\-preset alert templates or custom alert templates. This method facilitates quick deployment in standardized scenarios, reduces repetitive configurations, and ensures consistent rule definitions.

Cloud Monitor not only provides the custom alert template feature but also offers preset alert templates for various cloud services. The usage restrictions and methods vary across different types of templates, as described below.


* Apply alert templates to object groups, and use custom alert templates to automatically generate alert rules for resource monitoring. For more details, see [Applying alert templates to object groups](https://docs.byteplus.com/en/docs/Observability_Platform/Applying_alert_templates_to_object_groups).

* Enable preset alert templates to apply the preset alert rules of specified cloud services to all resources in all regions with a few clicks. For more details, see [Enabling Cloud Monitor preset alert templates](https://docs.byteplus.com/en/docs/Observability_Platform/Enabling_Cloud_Monitor_preset_alert_templates).


</Tab>
</Tabs>
