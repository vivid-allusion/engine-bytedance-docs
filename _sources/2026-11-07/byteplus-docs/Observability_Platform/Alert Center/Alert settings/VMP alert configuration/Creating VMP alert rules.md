---
title: "Creating VMP alert rules"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Creating_VMP_alert_rules"
---

You can configure alert rules by using PromQL statements, use Alert Center to monitor specific metrics in a specified workspace, and configure alerts based on metric thresholds. This topic describes how to manually configure an alerting rule by using a PromQL statement.

<span id="ncsMOPM1"></span>
## Prerequisites


* An alert notification policy has been created to specify the recipients, notification templates, and other information for receiving notification messages. For details, see [Creating notification policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_notification_policies).

* An alert aggregation policy has been created to aggregate alert notifications and prevent alert storms. For details, see [Creating aggregation policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_aggregation_policies).


<span id="I9mPo9fB"></span>
## Limits


* Each account can create up to 500 alert rules.

* You can configure up to 100 labels and 100 annotations for an alert rule.


<span id="hpzx33DX"></span>
## Procedure


<Tabs>
<Tab zoneid="G4R41y5N6M" title="Method 1: Create an alert rule">
<TabTitle>Method 1: Create an alert rule</TabTitle>

You can create an alert rule from scratch in the console and configure key parameters such as the query statement and the trigger policy in sequence. This method applies to scenarios that require customization or that involve a small number of alert rules.


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard).

2. In the left navigation pane, click **Alert Center \> Alert Configuration** to go to the Alert Configuration management page.

3. In the Alert Configuration section on the left, select **VMP ** and click the ** Alert Rule** tab.

4. Click **Create alert rule** and configure the relevant parameters for the VMP alert rule as needed. After completion, click **Confirm**.

   
   |Category |Parameter |Description |
   |---|---|---|
   |Basic information |Name |Specify a name for the alert rule as a unique identifier. Duplicate names are not allowed. |
   ||Project |Projects are a platform\-provided resource management mechanism that allows you to group resources for different business applications or projects.<br><br>Project\-based authorization with Identity and Access Management (IAM) facilitates resource isolation and data security, as well as cost calculation across cloud resources. <br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">By default, VMP alert rules are added to the default project, and the project cannot be changed.</div><br> |
   ||Tags |A tag is a key\-value pair that allows you to classify and aggregate cloud resources from different dimensions. You can use tags for resource authorization and bill splitting. <br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can add up to 50 tags to a single alert rule.</div><br> |
   |Alert trigger configuration |workspace |The workspace that you want to monitor and trigger alerts.<br><br>The workspace of Vital Managed Service for Prometheus (VMP) is an abstract integration of data and collection rules, which provides users with standard cloud Prometheus capabilities. For more details, see[ Workspace overview](https://docs.byteplus.com/en/docs/vmp/Workspace-overview). |
   ||Query statement |Use standard PromQL statements to configure monitoring objects or metrics. |
   ||Metric preview |Visually preview the metrics that match the query statement. By default, data from the last hour is queried. |
   ||Trigger policy |Configure an alert trigger policy. You can specify the alert level, condition, threshold, and condition duration.<br><br><br>* **Alert level**: Select P0, P1, or P2 to set different alert levels. If you do not select an option, alerts at this level are not configured.<br><br>* **Comparison condition**: Specify the comparison condition between the PromQL statement and the threshold. You can configure multiple comparison conditions. Valid values: Greater than, Greater than or equal to, Less than, Less than or equal to, Equal to, and Not equal to.<br><br>* **Threshold**: Set the threshold of the metric.<br><br>* **Condition duration**: Configures the duration for which the metric meets the condition. Valid values:<br><br>   * **Trigger immediately**: An alert is triggered immediately when the alert condition is met.<br><br>   * **Custom duration**: Select an alert trigger time. For example, 1 minute means that the alert will be triggered after the alert condition has been met for 1 minute. |
   |Alert notification |Notification policy |Select an alert notification policy. The system sends alerts to the specified contacts based on the alert levels and contact groups configured in the notification policy. For notification policy details, see [Creating notification policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_notification_policies). |
   ||Aggregation policies |Select an alert aggregation policy. An aggregation policy is primarily used to configure the aggregation cycle for alerts. It groups a batch of alerts for notification, preventing a large number of alert messages from being generated in a short period when alerts are triggered frequently. For details, see [Creating aggregation policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_aggregation_policies). |
   |Advanced configuration |Label |Configure the labels of the alert rule. Labels are primarily used for alert identification, grouping, deduplication, and route matching. A label consists of a key and a value.  <br><br><br>* **Key**: The key is a string. It can start with a letter or an underscore (`_`), but cannot start with a double underscore (`__`). Allows 1–256 characters, which can contain letters, digits, and underscores (`_`).<br><br>* **Value**: The value is a string. It can contain Chinese characters, letters, digits, and special characters and must be 1 to 512 characters in length.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When you configure multiple types of labels, the priorities of the labels are sorted in the following descending order: rule label \> global label \> PromQL label.</div><br><br><br>Common configuration example:<br><br>```YAML```<br>```labels:```<br>```  severity: critical   # Alert level```<br>```  business: pay        # Business line```<br>```  alert_type: resource # Alert type```<br><br><br> |
   ||Annotation |Configure the annotations for the alert rule. Annotations are primarily used to display key information. An annotation consists of a key and a value. Valid values:<br><br><br>* **Key**: The key is a string. It can start with a letter or an underscore (`_`), but cannot start with a double underscore (`__`). Allows 1–256 characters, which can contain letters, digits, and underscores (`_`).<br><br>* **Value**: The value is a string. It can contain Chinese characters, letters, digits, and special characters and must be 1 to 512 characters in length.<br><br><br>Common configuration example:<br><br>```YAML```<br>```annotations:```<br>```  summary: "High CPU usage on instance {{ $labels.instance }}"```<br>```  description: "Current CPU usage is {{ $value \| humanizePercentage }}, threshold is 80%"```<br>```  runbook_url: "https://xxx/docs/cpu-alert"```<br>```  dashboard_url: "https://grafana/xxx"```<br><br><br> |
   





</Tab>
<Tab zoneid="Si0qD8ZejW" title="Method 2: Import or export alert rules via JSON">
<TabTitle>Method 2: Import or export alert rules via JSON</TabTitle>

Export VMP alert rules from another workspace as a JSON file, and then import them into the VMP alert rules in the current workspace. This method applies when you need to copy alert rules in batches across accounts, regions, projects, or workspaces.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The import and export features enable quick synchronization of alert configurations across accounts, regions, projects, or workspaces for efficient reuse. For VMP alert rules, the synchronization granularity is at the workspace level.</div>



1. Log in to the [Observability Platform console](https://console.byteplus.com/observe).

2. In the left navigation pane, click ** Alert Center \> Alert Configuration** to go to the Alert Configuration management page.

3. In the Alert Configuration section on the left, select **VMP** and click the ** Alert Rule** tab.

4. In the upper\-right corner, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c35cb0c323edd4d26fc0ea35f521975b.png) </span>button, select Actions, and perform the corresponding operation. Use the import/export feature to import VMP alert rules that are exported from another workspace into the current workspace.

   
   |Actions |Description |
   |---|---|
   |Export selected VMP rules |Export the rules that are selected in the VMP alert rule list to a local JSON file.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Only items on the current page can be selected. Cross‑page selection is not supported.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Do not arbitrarily modify the structure of the JSON file, because it may cause import failures. If you do not have the required technical knowledge, we recommend that you do not edit the JSON file directly.</div><br> |
   |Export all VMP alert rules that meet search criteria |Export all VMP alert rules that meet the filter criteria to a local JSON file. The export is not affected by pagination. You can filter data by region, project, workspace, alert rule group, or search function. |
   |Import a JSON file to generate VMP alert rules |Use JSON files to import VMP alert rules exported from other accounts, regions, projects, or workspaces into the current VMP alert rule module. During the import, you can configure the target region, project, workspace, and name suffix.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Only rules of the same type can be imported. For example, you can export VMP alert rules from the Beijing region and import them into the Shanghai region for use. However, VMP alert rules cannot be imported into the alert rule module for Cloud Monitor.</div><br><br><br> |
   





</Tab>
</Tabs>
