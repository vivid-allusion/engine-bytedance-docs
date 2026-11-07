---
title: "Check and self-healing observability"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Check_Self-healing_Observation"
---

Check and self\-healing observability allows you to monitor node pool check and self\-healing in the cluster. This observability enables you to monitor nodes for kubelet, runtime, and GPU failures based on metrics and receive alerts. This topic describes how to configure check and self\-healing observability.

> **tip**

> For details on self\-healing, see [Configuring node check and self\-healing](https://docs.byteplus.com/en/docs/vke/NodePool-health-check-and-auto-repair).

## Prerequisites

* Cloud\-native observability has been enabled. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

* The VKE observability feature has been enabled. For details, see [VKE observability](https://docs.byteplus.com/en/docs/vke/VKE-observability).

* (Optional) An alert notification policy has been created in the Observability Platform or VMP. For details, see [Creating notification policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_notification_policies?lang=en) and [Creating alert notification policies](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-notification-rules?lang=en).

* (Optional) An alert aggregation policy has been created in the Observability Platform or VMP. For details, see [Creating aggregation policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_aggregation_policies?lang=en) and [Creating alert aggregation policies](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-aggregation-rules?lang=en).

## Enabling observability

### Step 1: Configure observability items

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Find the target cluster and click its name.

3. In the left navigation pane of the cluster management page, click **Observability settings**, and select the **Basic observability** tab.

4. Find the **AIOps remediation** card and click **Enable observation** to go to the observability item configuration page.

5. The system automatically checks the necessary conditions for enabling observability, such as the workspace configuration and add\-on status.

6. Click **Next** to go to the alert and notification configuration page.

### Step 2: Configure alerts and notifications

1. In the **Alert and notification** step, select the platform to receive alerts. Currently, **Unified Alert Center** and **The original VMP alarm strategy** are supported.

2. For the **Notification strategy name** parameter, select the created alert notification policy and specify the **notification object** and **Notification method** parameters based on different alert levels.

   > **tip**

   * > If you do not need to configure alerts for a certain level, you can unselect the corresponding alert level.

   * > If the existing notification policies do not meet your needs, you can select **vke_default_notify_policy (automatically created)** for the **Notification strategy name** parameter, and specify the **notification object** and **Notification method** parameters for the required alert levels. After you save the configuration, the system will automatically create a custom notification policy named vke_default_notify_policy in the unified Alert Center or VMP.

3. In the **Alerting aggregation policy** section, select the created alert aggregation policy.

4. Configure preset alert rules.

   * Enable or disable the switch next to a preset alert rule. After it is enabled, the system detects metrics based on the configured trigger conditions and generates alerts. When it is disabled, the rule will no longer trigger new alerts.

   * Click **View PromQL** to view the description and corresponding PromQL statement of the current preset alert rule.

   * Click the name of the preset rule to be configured to expand the preset alert rule configuration page, and configure the trigger conditions for different levels (P0, P1, or P2) of alerts in the **Triggering condition** section.

      |Parameter |Description |
      |---|---|
      |Alert level |Select the check box in the **Enable** column that corresponds to each alert level (P0, P1, or P2) to activate its trigger condition. If you do not select an option, alerts at this level are not configured. |
      |Comparison condition |Specify the comparison condition between the PromQL statement and the threshold. You can configure multiple comparison conditions, including **Greater than**, **Greater than or equal to**, **Less than**, **Less than or equal to**, **Equal to**, and **Not equal to**. |
      |Threshold |Configure the threshold of the metric. |
      |The duration of the condition |Configure the duration for which the metric continuously meets the trigger condition. The system triggers the alert at the corresponding level only if the metric continuously meets the comparison condition within this duration. |
      |Label |Configure the label of the alert rule. It is mainly used for alert identification, grouping, deduplication, and routing matching. A label consists of a key and a value. Where:<br><br><br>* **Key**: A string. It can start with a letter or an underscore (`_`), but cannot start with a double underscore (`__`). It can contain letters, digits, and underscores (`_`) and can be 1 to 256 characters in length.<br><br>* **Value**: A string. It can contain Chinese characters, English letters, digits, and special characters, and can be 1 to 512 characters in length.<br><br><br>Common configuration example:<br><br>```YAML```<br>```labels:```<br>```  severity: critical   # The alert level.```<br>```  business: pay        # The business line.```<br>```  alert_type: resource # The alert type.```<br><br><br> |
      |Annotation |Configure the annotation of the alert rule. It is mainly used to display key information. An annotation consists of a key and a value. Where:<br><br><br>* **Key**: A string. It can start with a letter or an underscore (`_`), but cannot start with a double underscore (`__`). It can contain letters, digits, and underscores (`_`) and can be 1 to 256 characters in length.<br><br>* **Value**: A string. It can contain Chinese characters, English letters, digits, and special characters, and can be 1 to 512 characters in length.<br><br><br>Common configuration example:<br><br>```YAML```<br>```annotations:```<br>```  summary: "High CPU usage on instance {{ $labels.instance }}"```<br>```  description: "Current CPU usage is {{ $value \| humanizePercentage }}, threshold is 80%"```<br>```  runbook_url: "https://xxx/docs/cpu-alert"```<br>```  dashboard_url: "https://grafana/xxx"```<br><br><br> |

5. Click **Complete the configuration**.

## Observability dashboards

> **tip**

> The built\-in dashboards provide features such as period\-over\-period comparisons of monitoring data and the ability to copy dashboard queries. For details, see [Usage of dashboards](https://docs.byteplus.com/en/docs/vke/Using_dashboard).

You can view monitoring information related to node check and self\-healing. This includes the number of abnormal nodes, number of nodes with GPU abnormalities, number of self\-healing actions, number of successful self\-healing actions, and more. You can specify a custom time range for querying information and set the information refresh mode to manual refresh or automatic refresh.

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, click **AIOps** \> **Check and self\-healing** to view the monitoring dashboard.

## View metrics

* You can use the Explore feature of VMP to quickly query and display metric data. For details, see [Querying metrics](https://docs.byteplus.com/en/docs/vmp/explore-metrics).
