---
title: "Ingress service observability"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Ingress-observability"
---

VKE provides an NGINX Ingress Controller based on the community edition. The controller converts Ingresses into NGINX configurations and uses NGINX for Layer 7 traffic forwarding. VKE also allows you to monitor the NGINX Ingress Controller. This topic describes how to configure NGINX Ingress monitoring and query monitoring information.

## Prerequisites

* Cloud\-native observability has been enabled. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

* The VKE observability feature has been enabled. For details, see [VKE observability](https://docs.byteplus.com/en/docs/vke/VKE-observability).

* The ingress\-nginx add\-on has been installed. For details, see [ingress-nginx](https://docs.byteplus.com/en/docs/vke/ingress-nginx-add-on).

* (Optional) An alert notification policy has been created in the Observability Platform or VMP. For details, see [Creating notification policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_notification_policies?lang=en) and [Creating alert notification policies](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-notification-rules?lang=en).

* (Optional) An alert aggregation policy has been created in the Observability Platform or VMP. For details, see [Creating aggregation policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_aggregation_policies?lang=en) and [Creating alert aggregation policies](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-aggregation-rules?lang=en).

## Enabling observability

### Step 1: Configure observability items

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Find the target cluster and click its name.

3. In the left navigation pane of the cluster management page, click **Observability settings**, and select the **Basic observability** tab.

4. Find the **Ingress service** card and click **Enable observation** to go to the observability item configuration page.

5. The system automatically checks the necessary conditions for enabling observability, such as the workspace configuration and add\-on status.

6. For the **Observation item** parameter, select observability items for which you want to collect metrics. For items for which metric collection is not enabled, the system will not collect the corresponding metrics, and the system will prompt you to install the related add\-ons. You can decide whether to install the related add\-ons and select the corresponding observability items based on your business requirements.

7. After the configuration is complete, click **Next** to go to the metric configuration page.

### Step 2: Configure metric collection

1. On the metric configuration page, view the collection interval and metric quantity corresponding to the enabled observability items.

2. Click **Edit metrics**. This enables you to select or discard specific metrics of the add\-on, modify the collection interval, and configure metric relabeling.

   * For **Collection interval**, select a collection interval for the metrics of the add\-on. The supported collection intervals vary for different add\-ons.

   * In the **metric list**, select a metric to collect. To stop collecting a metric, uncheck it. Click the **All**, **Basic metrics**, or **Other metrics** tab to filter metrics by type.

      > **tip**

      * > The impact of adjusting the metric collection interval is as follows. Adjust the interval as needed:

         * > Reducing the collection interval: This increases the number of metrics reported per unit time and improves monitoring accuracy. However, the cost of standard VMP workspaces increases.

         * > Increasing the collection interval: This decreases the number of metrics reported per unit time and lowers the cost of standard VMP workspaces. However, this decreases monitoring accuracy.

      * > Cloud service metrics are categorized into **Basic metrics** and **Other metrics**. The billing method varies based on different types of metrics. For details, see [VMP billing](https://docs.byteplus.com/en/docs/vmp/pay-as-you-go).

   * In the **metricRelabelings** section, click **Add rule** to configure metric relabeling rules. This allows you to rewrite the labels of each metric after collection and before writing to storage. Common use cases include modifying label values, adding new labels, and renaming labels to standardize label naming for queries. For details, see [Metric relabeling](https://docs.byteplus.com/en/docs/vmp/Metric_relabel?lang=en).

      |No. |Feature |Replacement value |Description |
      |---|---|---|---|
      |① |Action type |`action` |The action to apply to the metrics. Currently, only **replace** is supported. The logic is as follows:<br><br><br>* If the values of `targetLabel` and `sourceLabels` are the same, `sourceLabels` is overwritten.<br><br>* If the key specified by `targetLabel` does not exist, a new label is created by default. |
      |② |Source labels |`sourceLabels` |Specify one or more source labels, separated by `\|` if multiple labels are provided. The system reads the values of these labels for matching or extraction. |
      |③ |Regular expression |`regex` |The regular expression pattern used to match source label values.<br><br><br>* The default is `(.*)`, which matches any value.<br><br>* You can use capture groups such as `(.+)` to extract partial content. |
      |④ |Replacement value |`replacement` |The value written to the target label after a successful match.<br><br><br>* The default is `$1`, which refers to the content of the first capture group in the regular expression.<br><br>* A fixed string is also supported. |
      |⑤ |Target label |`targetLabel` |The name of the target label to which the processing result is written.<br><br><br>* If the target label already exists, its existing value is overwritten.<br><br>* If the target label does not exist, a new label is created. |

3. After the configuration is complete, click **Next** to go to the alert and notification configuration page.

### Step 3: Configure alerts and notifications

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

   > Description

   * > In addition to using preset alert templates to configure alert rules directly, you can customize the template configurations or directly use PromQL statements to configure alert rules. For details, see [Alert configuration overview](https://docs.byteplus.com/en/docs/vke/Configuring_alerts?lang=en).

   * > Details of the preset alert rule templates, including rule descriptions, PromQL configurations, and common alert handling procedures. See [Preset alert templates](https://docs.byteplus.com/en/docs/vke/Preset_alert_templates).

## Observability dashboards

> **tip**

> The built\-in dashboards provide features such as period\-over\-period comparisons of monitoring data and the ability to copy dashboard queries. For details, see [Usage of dashboards](https://docs.byteplus.com/en/docs/vke/Using_dashboard).

You can view the built\-in monitoring dashboard in the VKE console. The dashboard presents statistical information such as the total number of requests, number of connections, request success rate, number of configuration reloads, CPU trend, and memory usage trend.

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, click **Network services monitoring** \> **Ingress\-nginx monitoring** to view the monitoring dashboard.

   * From the **Namespace** drop\-down list, select the namespace where the Ingress is located.

   * From the **IngressClass** drop\-down list, select the type of Ingress. Supported types include the system default ingress\-nginx and custom Nginx Ingress Controller.

   * From the **Pod** drop\-down list, specify a pod.

      > **tip**

      > You can also deploy self\-managed Grafana in the cluster and use it to view metrics and create dashboards. For more details, see [Deploying Grafana in a VKE cluster and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster).

## View metrics

* You can use the Explore feature of VMP to quickly query and display metric data. For details, see [Querying metrics](https://docs.byteplus.com/en/docs/vmp/explore-metrics).
