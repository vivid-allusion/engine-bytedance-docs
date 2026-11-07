---
title: "Creating VMP alert templates"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Creating_VMP_alert_templates"
---

In addition to the preset alerting rule templates provided by the system, you can also create custom alerting rule templates based on your business requirements to quickly configure alerting rules for cloud services. This topic describes how to create a custom alerting rule template.

<span id="EESAxQK3"></span>
## Procedure


<Tabs>
<Tab zoneid="tWBU3pCRfh" title="Method 1: Create an alert template">
<TabTitle>Method 1: Create an alert template</TabTitle>

You can create an alert template from scratch in the console by configuring information such as the query statement, match expression, and PromQL in sequence. After you save the template, you can reuse it to quickly create alert rules. Applicable to scenarios that require personalized configurations or the establishment of standard templates.


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe).

2. In the left navigation pane, click **Alert Center \> Alert Configuration** to go to the Alert Configuration management page.

3. In the Alert Configuration section on the left, select **VMP** and click the **Alert Template** tab.

4. Click **Create alert template** and configure the relevant parameters for the VMP alert template as needed. After completion, click **Submit**.

   
   |Category |Parameter |Description |
   |---|---|---|
   |Basic information |Name |Specify a custom name for the alert template. The name must be unique. |
   ||Label |The global labels of the alert rule. They are mainly used for alert identification, grouping, deduplication, and route matching. A label consists of a key and a value.  <br><br><br>* **Key**: The key is a string. It can start with a letter or an underscore (`_`), but cannot start with a double underscore (`__`). Allows 1–256 characters, which can contain letters, digits, and underscores (`_`).<br><br>* **Value**: The value is a string. It can contain Chinese characters, letters, digits, and special characters and must be 1 to 512 characters in length.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When you configure multiple types of labels, the priorities of the labels are sorted in the following descending order: rule label \> global label \> PromQL label.</div><br> |
   |Variable configuration |Variable types |Select the variable type. Valid values:<br><br><br>* **Query**: the dynamic PromQL variable. You can only define the name, not the value, for this type of variable. For example, cluster metrics such as cluster IDs and namespaces always have values generated dynamically. The values of dynamic variables can be obtained by specifying PromQL statements and regular expressions.<br><br>* **Custom**: a type of variables that have predefined values. For example, in cluster metrics, the workload type is fixed (such as Deployment, StatefulSet, DaemonSet) and can be directly specified. |
   ||Variable name |Configure the name and PromQL label for the variable.<br><br><br>* **Variable name**: Match the specific label in the PromQL statement. The variable name can contain uppercase and lowercase letters and digits and must be 1 to 32 characters in length.<br><br>* **Label**: Describe the meaning and purpose of the variable, which is displayed in the console for users to understand. The label can contain Chinese characters, uppercase and lowercase letters, digits, and special characters and must be 1 to 20 characters in length.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Variables are used for more fine\-grained filtering of cloud service resources in monitoring data. For example, in Vital Kubernetes Engine (VKE), you can select a VKE cluster or namespace by using variables.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A variable name needs to start with an uppercase letter and use CamelCase convention. For example, <code>ClusterNode</code>.</div><br> |
   ||Query statement |When you set the **Variable type** parameter to **Query**, you need to configure a PromQL query statement to obtain the variable value. Example: `kube_node_info`. |
   ||Match expression |When you set the **Variable type** parameter to **Query**, you need to configure a regular expression to obtain variable values. The system then obtains the variable values based on the **Query statement ** and **Match expression** parameters.<br><br>For example, you can use the `/.*cluster="(.*?)".*/` expression to match any string in the PromQL statement that contains the `cluster="any text"` format, and capture the text between `cluster="` and the closing `"` as a variable group. |
   ||Variable |When you set the **Variable type** parameter to **Custom**, enter the fixed values of the variable in the text box. The values can be separated by spaces. |
   ||Can select multiple variable values |Disabled by default. After you switch on this option, you can select multiple variable values when you select variables. |
   ||Add all selections |Disabled by default. After you switch on the "Add all selections" option, the variables include the ** All ** option, which allows you to select all variable values. |
   |Rule configuration |Rule name |Specify a name for the alert rule as a unique identifier. Duplicate names are not allowed. |
   ||PromQL |Use standard PromQL statements to configure monitoring objects or metrics.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can use <code>$variable name</code> in a PromQL statement to reference global variables. For example, if you have defined the cluster variable as <code>Cluster</code>, you can reference it by using <code>node_cpu_seconds_total{cluster="$Cluster"}</code>.</div><br> |
   ||Trigger policy |Configure an alert trigger policy. You can specify the alert level, condition, threshold, and condition duration.<br><br><br>* **Alert level**: Select P0, P1, or P2 to set different alert levels. If you do not select an option, alerts at this level are not configured.<br><br>* **Comparison condition**: Specify the comparison condition between the PromQL statement and the threshold. You can configure multiple comparison conditions. Valid values: Greater than, Greater than or equal to, Less than, Less than or equal to, Equal to, and Not equal to.<br><br>* **Threshold**: Set the threshold of the metric.<br><br>* **Condition duration**: Configures the duration for which the metric meets the condition. Valid values:<br><br>   * **Trigger immediately**: An alert is triggered immediately when the alert condition is met.<br><br>   * **Custom duration**: Select an alert trigger time. Available options include 1 minute, 2 minutes, 5 minutes, 10 minutes, 20 minutes, 30 minutes, 1 hour, 3 hours, 6 hours, and 12 hours. For example, 1 minute means that the alert will be triggered after the condition has been met for 1 minute. |
   ||Label |Configure the labels of the alert rule. Labels are primarily used for alert identification, grouping, deduplication, and route matching. A label consists of a key and a value.  <br><br><br>* **Key**: The key is a string. It can start with a letter or an underscore (`_`), but cannot start with a double underscore (`__`). Allows 1–256 characters, which can contain letters, digits, and underscores (`_`).<br><br>* **Value**: The value is a string. It can contain Chinese characters, letters, digits, and special characters and must be 1 to 512 characters in length.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When you configure multiple types of labels, the priorities of the labels are sorted in the following descending order: rule label \> global label \> PromQL label.</div><br><br><br>Common configuration example:<br><br>```YAML```<br>```labels:```<br>```  severity: critical   # Alert level```<br>```  business: pay        # Business line```<br>```  alert_type: resource # Alert type```<br><br><br> |
   ||Annotation |Configure the annotations for the alert rule. Annotations are primarily used to display key information. An annotation consists of a key and a value. Valid values:<br><br><br>* **Key**: The key is a string. It can start with a letter or an underscore (`_`), but cannot start with a double underscore (`__`). Allows 1–256 characters, which can contain letters, digits, and underscores (`_`).<br><br>* **Value**: The value is a string. It can contain Chinese characters, letters, digits, and special characters and must be 1 to 512 characters in length.<br><br><br>Common configuration example:<br><br>```YAML```<br>```annotations:```<br>```  summary: "High CPU usage on instance {{ $labels.instance }}"```<br>```  description: "Current CPU usage is {{ $value \| humanizePercentage }}, threshold is 80%"```<br>```  runbook_url: "https://xxx/docs/cpu-alert"```<br>```  dashboard_url: "https://grafana/xxx"```<br><br><br> |
   





</Tab>
<Tab zoneid="bshBnx2ftg" title="Method 2: Import or export alert templates via JSON">
<TabTitle>Method 2: Import or export alert templates via JSON</TabTitle>

You can export VMP alert templates from other regions as JSON files and then import them into the current region. This is useful for batch replicating alert templates across accounts or regions.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The import and export features enable quick synchronization of alert configurations across accounts, regions, projects, or workspaces for efficient reuse. For VMP alert templates, the synchronization granularity is at the region level.</div>



1. Log in to the [Observability Platform console](https://console.byteplus.com/observe).

2. In the left navigation pane, click **Alert Center \> Alert Configuration** to go to the Alert Configuration management page.

3. In the Alert Configuration section on the left, select **VMP** and click the **Alert Template** tab.

4. In the upper\-right corner, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c35cb0c323edd4d26fc0ea35f521975b.png) </span>button, select Actions, and perform the corresponding operation. Use the import/export feature to import VMP alert templates exported from other regions into the current region for use.

   
   |Actions |Description |
   |---|---|
   |Export selected VMP templates |Exports the templates selected in the VMP alert template list to a local JSON file.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can select only the entries on the current page of the list. You cannot select entries across pages.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Do not arbitrarily modify the structure of the JSON file. Otherwise, the import fails. If you do not have the required technical knowledge, we recommend that you do not edit the JSON file directly.</div><br> |
   |Export all VMP templates that meet search criteria |Export all VMP alert templates that meet the filter criteria to a local JSON file. The export is not affected by pagination. You can filter data by name. |
   |Import a JSON file to generate a VMP template |By using JSON files, you can import VMP alert templates exported from another account into the VMP alert template module of the current account for use. The import process allows you to configure the region and a name suffix.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Only alert templates of the same type can be imported. For example, you can export a VMP alert template from account A and import it into account B for use. However, VMP alert templates cannot be imported into the Cloud Monitor template module.</div><br><br><br> |
   





</Tab>
</Tabs>


<span id="RWaQMoRf"></span>
## What to do next

Configure the workspace, notification policy, and aggregation policy, and then apply the alert template. Based on the template, alert rules and one alert rule group are automatically generated to monitor resources. For detailed descriptions, see [Creating VMP alert rule groups](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_VMP_alert_rule_groups).
