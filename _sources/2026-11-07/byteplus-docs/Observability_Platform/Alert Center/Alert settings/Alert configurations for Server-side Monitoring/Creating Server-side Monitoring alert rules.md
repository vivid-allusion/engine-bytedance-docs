---
title: "Creating Server-side Monitoring alert rules"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Creating_Server-side_Monitoring_alert_rules"
---

Alert tasks can detect anomalies in target services or metrics. When the configured conditions are met, notification messages are sent to help you monitor the health status of your services. This topic describes how to create Server\-side Monitoring alert rules.

## Background

When the alert frequency is set to 1, meaning every rule evaluation triggers an alert, you can reduce unnecessary interruptions and avoid alert storms by configuring the alert delivery policy. This allows you to control the notification frequency and filter out potential data spikes.

When the delivery cycle is set to d, and the spike filter threshold is set to k, the alert notification times will be: k, k+20d, k+21d, k+22d, ... The notification interval must not exceed 60 minutes. If the calculated interval exceeds 60 minutes, notifications will be sent at 60\-minute intervals instead. Example:

* Rule evaluation frequency: Once per minute. Delivery policy: 3\-minute delivery cycle.

   Alert notification times: 1 minute, 4 (1+3) minutes, 7 (1+3+3) minutes, 10 (1+3+3+3) minutes, ...

* Rule evaluation frequency: Once per minute. Delivery policy: 3\-minute delivery cycle. An alert is sent on the second trigger within a delivery cycle (glitch filtering).

   Alert notification times: 2 minutes, 5 (2+3) minutes, 8 (2+3+3) minutes, 11 (2+3+3+3) minutes, ...

* Rule evaluation frequency: Once per minute. Delivery policy: 3\-minute delivery cycle. An alert is sent on the second trigger within a delivery cycle (glitch filtering). Delivery policy is enabled. Alert batch aggregation interval: 5 minutes.

   Alert notification times: 2 minutes, 5 (2+3) minutes, 11 (2+3+6) minutes, 23 (2+3+6+12) minutes, ...

   The aggregation results are as follows: Alerts sent at 2 minutes and 5 minutes are aggregated into one alert group; alerts sent at 11 minutes form one alert group; alerts sent at 23 minutes form one alert group.

## Prerequisites

* You have created an alert notification policy that specifies the contacts who receive notification messages, the notification template, and other information. For detailed instructions, see [Creating notification policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_notification_policies).

* Basic metrics: Integrate with the APMPlus Server Agent to monitor hosts, containers, and processes.

* Service metrics: Integrate services with application monitoring capabilities such as APMPlus, Skywalking, OpenTelemetry, Jaeger, Zipkin, runtime, and AI.

* Custom metrics: Integrate with custom instrumentation capabilities such as APMPlus, OpenTelemetry, and Prometheus.

## Procedure

**Method 1: Create an alert rule**

You can create an alert rule from scratch via the console by configuring key information such as alert type, alert severity, trigger policy, and delivery policy in sequence. This is suitable for on\-demand customization or scenarios with a small number of alert rules.

1. Log in to the [Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard).

2. In the left navigation pane, click **Alert Center \> Alert Configuration** to go to the Alert Configuration management page.

3. In the alert configuration section on the left, select **Server\-side Monitoring** and go to the **Alert rule** tab.

4. Click **Create alert rule**, configure the relevant parameters for the Server\-side Monitoring alert rule based on your actual needs, and then click **Save**.

   |Category |Parameter |Description |
   |---|---|---|
   |Basic information |Alert task name |Specify a custom name for the alert task. |
   |Alert policy |Project |The project to which the alert task belongs. Projects are a platform\-provided resource management mechanism that allows you to group resources for different business applications or projects.<br><br>Project\-based authorization with Identity and Access Management (IAM) facilitates resource isolation and data security, as well as cost calculation across cloud resources.  |
   ||workspace |Workspaces are a data management and isolation method provided by Server\-side Monitoring. Each workspace has independent data reporting credentials and can centrally manage traces, logs, and metrics for different application ownership scenarios. |
   ||Alert type |Configure the alert types and service scope to be monitored. Currently supported alert types include: service, runtime, custom metrics, host, process, container, AI, and Claw.<br><br><br>* When the alert type is set to runtime or service, you can filter target services by service language, monitoring system, or service name, or you can directly select all services.<br><br>* When the alert type is set to AI or Claw, you can filter target services by platform or service name, or you can directly select all services. |
   ||Detect Type |Specifies the type of alert trigger mechanism. The following types are supported: static threshold and dynamic threshold.<br><br><br>* **Static threshold**: The alert trigger condition is set to a fixed threshold. The system sends an alert message when the metric value meets the trigger condition. This type suits stable workloads with clear metric baselines.<br><br>* **Dynamic threshold**: The system automatically pulls historical metric data to learn trends. It dynamically calculates thresholds and identifies abnormal fluctuations. An AI model then determines whether to trigger an alert. No manual maintenance of threshold rules is required.<br><br>   > **tip**<br>   <br><br>   > Dynamic threshold is currently in public beta.<br>    |
   ||Alert level |The alert severity level when metrics trigger an alert. When the detection type is set to "Static threshold", you can select multiple levels. This allows different alert levels to be set for different metric values. When the detection type is set to "Dynamic threshold", you can select only one level.<br><br><br>* Notice: Info<br><br>* Warn: Warning<br><br>* Fatal: Critical |
   ||Alert engine |The threshold engine for alerts. Currently, static thresholds are supported, where a fixed constant is pre\-defined as the judgment criterion, and real\-time metrics are compared directly against this fixed value.<br><br>For example, in the alert rule "memory usage \> 90%", the 90% is the static threshold used as the evaluation condition. |
   ||Multiple\-policy logic |This is the logic for triggering alerts when multiple alert trigger policies are configured.<br><br><br>* **All met**: The default configuration. Alerts are triggered only when all policies are met simultaneously.<br><br>* **Any met**: Alerts are triggered when any one of the policies is met. |
   ||Alert trigger policy |The specific policy for triggering alerts requires the following parameters to be configured:<br><br><br>* **Alert metric**: Select the metric for which you want to set up alerts. The available metrics vary by alert type. The actual metrics are subject to the exact options displayed on the console.<br><br>* **Filter criteria**: Apply filters on top of the selected metric to narrow down and pinpoint more precise data. Filter conditions include: service type, service name, interface name, downstream service type, downstream service name, downstream interface name, status code, host, process ID, and more.<br><br>* **Grouped alert**: Provides multi\-dimensional grouping, enabling a single alert rule to be effective for all groups. When no group is configured, an alert is triggered if the single aggregated metric across all dimensions meets the condition. When a group is configured, an alert is triggered if any group's aggregated metric meets the condition.<br><br>* **Trigger conditions (static threshold)** : Defines the alert trigger rule. This policy takes effect when **Detect type** is set to **Static threshold**. Use the time window, aggregation method, and evaluation condition to detect metric anomalies automatically.<br><br>   * **Time window**: Specifies the statistical time range. For example, "within the last 5 minutes" means that only metric data generated during this period is analyzed.<br><br>   * **Time interval**: Defines the time granularity for data aggregation. For example, "5 minutes" means that aggregation calculations are performed on metric data every 5 minutes.<br><br>   * **Aggregation method**: Performs statistical calculations on metric data within the time interval. Examples include AVG (average value over N minutes), MAX (maximum value over N minutes), MIN (minimum value over N minutes), and SUM (sum over N minutes). These are used to generate evaluable aggregated values.<br><br>   * **Evaluation condition**: Defines trigger logic by selecting the condition type (threshold or ratio), an operator (\>, <, =), and a value. An alert at the corresponding severity level is triggered when the aggregated result meets the threshold condition.<br><br>      > **tip**<br>      <br><br>      * > Threshold: An alert is triggered when the number of anomalies within a single time window reaches a certain threshold.<br>      <br><br>      * > Ratio: Indicates whether the increase or decrease value (change range) within a single time window, compared to the value from the same time window n time units ago, exceeds the configured threshold.<br>      <br><br>* **Trigger conditions (dynamic threshold)** : Defines the alert trigger rule. This policy takes effect when **Detect type** is set to **Dynamic threshold**.<br><br>   > **tip**<br>   <br><br>   > After you configure parameters, click "**Detection preview**" to view how the dynamic threshold bounds map to the real\-time metric value. The gray shading indicates the pre\-detection interval. The yellow shading indicates suppressed spike data. The red circles indicate the actual anomaly points that triggered alerts.<br>   <br><br>   * **Time window**: Specifies the statistical time range. For example, "within the last 5 minutes" means that only metric data generated during this period is analyzed.<br><br>   * **Time interval**: Defines the time granularity for data aggregation. For example, "5 minutes" means that aggregation calculations are performed on metric data every 5 minutes.<br><br>   * **Anomaly trend**: Defines the scope of anomaly trends. For example, "Increase or decrease" means upward or downward trends that reach the anomaly range calculated by the AI model are detected.<br><br>   * **Model sensitivity**: The core configuration that controls the sensitivity of anomaly detection. It determines how strongly the model responds to metric fluctuations. Higher sensitivity makes detection more sensitive and more likely to classify fluctuations as anomalies.<br><br>   * **Spike suppression**: Controls whether jitter anomalies are included in anomaly detection. Use it to handle spike data. This option is enabled by default. When this option is enabled, spike data is automatically suppressed and flagged, reducing false positives and improving alert accuracy.<br><br>   * **Zero or missing data detection**: Detects scenarios where metrics stay at 0 or are missing. This option is disabled by default. When this option is enabled, the system detects an anomaly when data drops to zero or goes missing and the anomaly step threshold is reached.<br><br>      > **tip**<br>      <br><br>      > The anomaly step is the step count threshold for anomaly detection. One step equals one data point. For metrics with 1\-minute granularity, a maximum of 30 steps can be configured. For metrics with other granularities, a maximum of 24 steps can be configured.<br>      <br><br>   * **Baseline threshold**: The detection range for metric values. This option is disabled by default. When this option is enabled, an alert is generated only when the metric value meets the baseline threshold and the detection result meets the alert trigger condition. This prevents false positives caused by metric fluctuations within the normal range. |
   ||No\-data policy |Notification policy for when no metric data is reported.<br><br><br>* Ignore: Ignore it and do not send a notification.<br><br>* No\-data notification: If no data is reported after the specified time, send a notification message. |
   ||Tags |A tag is a key\-value pair that allows you to classify and aggregate cloud resources from different dimensions. You can use tags for resource authorization and bill splitting.  |
   ||Custom label |Custom labels and values You can filter alerts in the alert list by label. |
   ||Alert verification |Select the time point at which the alert is triggered to verify whether the alert task is generated as expected. |
   |Alert send policy |Rule evaluation frequency |The rule evaluation frequency defaults to once per minute. Combined with other alert send policy configurations, this reduces invalid alert noise and prevents alert storms. |
   ||Send policy |The policy for sending the first alert within a sending interval. It is mainly used for spike filtering to avoid multiple alerts due to the threshold being exceeded frequently. The default send cycle is 3 minutes. If an alert is triggered once within a cycle, it is sent on the first occurrence. |
   ||Send frequency reduction |The de\-escalation policy for alert notifications during continuous alert triggering. If enabled, during continuous alert triggering, the send interval will gradually increase to avoid alert storms.<br><br>The specific policy is as follows:<br><br><br>* When the send period is \>= 1 hour, the de\-escalation logic is not triggered.<br><br>* When the send period is < 1 hour, after each send, the send period = min(send period \* 2, 1h). For example, the first send period is 1 minute, the second is 2 minutes, the third is 4 minutes, the fourth is 8 minutes, and so on. |
   ||Alert batch aggregation interval |Aggregate alerts with an interval not longer than N minutes.<br><br><br>* When an alert is generated, if an alert exists within the previous N minutes, then the alerts from the previous N minutes are aggregated into one alert group.<br><br>* When an alert is generated, if no alert exists within the previous N minutes, then a new alert group is generated. |
   |Notification methods |Notification methods |The alert notification method supports either selecting an existing notification policy or manual selection. Server\-side Monitoring supports the following notification methods: Phone, SMS, email, Feishu, WeCom, DingTalk, Slack, alert callback, and Feishu app.<br><br><br>* **Notification policy**: Select an alert notification policy. The system will use the alert severity and contact groups configured in the policy to send alerts to the specified contacts. For notification policy details, see [Creating notification policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_notification_policies).<br><br>* **Manual selection**: Manually select email, Feishu webhook, or alert callback to receive alert notification messages. |
   |Alert description |Alert description |Fill in the notes or description for the alert task. |

**Method 2: Apply a preset alert template**

Quickly create alert rules based on the pre\-configured settings encapsulated in preset alert templates. This method facilitates quick deployment in standardized scenarios, reduces repetitive configurations, and ensures consistent rule definitions.

> **tip**

> This scenario uses the AgentKit service as an example.

1. Log in to the [Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard).

2. In the left navigation pane, click **Alert Center \> Alert Configuration** to go to the Alert Configuration management page.

3. In the alert configuration section on the left, select **Server\-side Monitoring**, and go to the **Preset alert template** tab.

4. Click **Application** in the Actions column on the right side of the target template to go to the **Alert rule** tab on the Template details page. Then, you can view the detailed configuration of the alert rules.

5. Go to the **Application scope** tab, click **Add application scope**, configure the application scope, workspaces, and notification method for the alert, and then click **Confirm**.

   Using AgentKit as an example, you can quickly filter AgentKit\-related services by platform and service name.

6. Return to the preset alert template details page, and click **Submit** in the alert change notification. The system will automatically create an alert task based on the configuration and monitor metric status in real time.

**Method 3: Apply a custom alert template**

Quickly create alert rules based on the pre\-configured settings encapsulated in custom alert templates. This method facilitates quick deployment in standardized scenarios, reduces repetitive configurations, and ensures consistent rule definitions.

> **tip**

> This scenario uses the AgentKit service as an example.

1. Log in to the [Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard).

2. In the left navigation pane, click **Alert Center \> Alert Configuration** to go to the Alert Configuration management page.

3. In the alert configuration section on the left, select **Server\-side Monitoring** and go to the **Alert template** tab.

4. Click **Create alert template**, then configure the basic information.

5. Return to the alert template management page, and click **Edit** in the Actions column to the right of the target alert template.

6. Click the **Alert rule** tab and the **Add alert rule** button in sequence. Configure the alert rule name, alert policy, notification policy, and other details as needed. All AI\-related alert metrics are listed in the alert query section. For detailed descriptions of configuration items, see [Creating Server-side Monitoring alert templates](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_an_alert_template_for_Server-side_Monitoring).

7. Click **Add application scope** in the **Application scope** tab, then configure the detailed application scope for the alert.

8. Return to the alert template details page, and click **Submit** in the alert change notification. The system will automatically create an alert task based on the configuration and monitor metric health status in real time.

**Method 4: Import/export alert rules via JSON**

You can export Server\-side Monitoring alert rules from other projects as JSON files and then import them into the current project for use. This is suitable for batch replication of alert rules across accounts, regions, or projects.

> **tip**

> The import and export features enable quick synchronization of alert configurations across accounts, regions, projects, or workspaces for efficient reuse. The synchronization granularity for Server\-side Monitoring alert rules is at the project level.

1. Log in to the [Observability Platform console](https://console.byteplus.com/observe).

2. In the left navigation pane, click **Alert Center \> Alert Configuration** to go to the Alert Configuration management page.

3. In the alert configuration section on the left, select **Server\-side Monitoring** and go to the **Alert rule** tab.

4. In the upper\-right corner, click the ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c35cb0c323edd4d26fc0ea35f521975b.png)button, select Actions, and perform the corresponding operation. Use the import/export feature to import Server\-side Monitoring alert rules exported from other projects into the current project for use.

   |Actions |Description |
   |---|---|
   |Export selected Server\-side Monitoring rules |Export the selected rules from the Server\-side Monitoring alert rule list to a local JSON file.<br><br>> **tip**<br><br><br><br>* > You can select only the entries on the current page of the list. You cannot select entries across pages.<br><br><br>* > Do not arbitrarily modify the structure of the JSON file. Otherwise, the import fails. If you do not have the required technical knowledge, we recommend that you do not edit the JSON file directly.<br> |
   |Export all Server\-side Monitoring alert rules that match the search criteria |Export all Server\-side Monitoring alert rules that meet the filter criteria to a local JSON file. The export is not affected by pagination. You can filter data by region, project, or search function. |
   |Import a JSON file to generate Server\-side Monitoring alert rules |Use JSON files to import Server\-side Monitoring alert rules exported from other accounts, regions, or projects into the current Server\-side Monitoring alert rules for use. The import process supports configuring the target region, project, and name suffix.<br><br>> **warning**<br><br><br>> Only rules of the same type can be imported. For example, you can export Server\-side Monitoring alert rules from the Beijing region and import them into the Shanghai region for use. However, Server\-side Monitoring alert rules cannot be imported into Cloud Monitoring alert rules.<br><br><br> |

## What to do next

After the alert rule takes effect, click the name of the target alert rule to go to the alert details page, where you can view detailed information about the alert task, including the alert rule summary, alert trend chart, and alert history.

* **Alert rule summary**: Displays the alert rule, its running status, and quick\-action buttons. Quick actions include the enable/disable toggle, edit alert, and ACK alert rule.

   > **tip**

   * > By default, only the assignees or group members specified in the rule can configure the ACK switch.

   * > ACK only silences alert notifications. Alert events are still generated as normal, and the rule remains in the "active" state. The initial state is "ACK". By default, an ACK silences alerts for 3 hours. After the user clicks "ACK", the expiration time is set, and the button state changes to "Reset ACK". Within 3 hours after the user confirms ACK, authorized users can reset the ACK at any time, and the countdown will refresh. After 3 hours, the button state reverts to "ACK".

* **Alert trend chart**: Displays the metric trend chart monitored by the alert task. If an alert is triggered, a red dot will be shown.

* **Alert history**: Displays the send time, rule snapshot, alert metric values, and notification method for triggered alerts.
