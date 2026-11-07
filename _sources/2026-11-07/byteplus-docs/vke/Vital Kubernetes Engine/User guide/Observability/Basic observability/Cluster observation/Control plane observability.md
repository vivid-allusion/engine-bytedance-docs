---
title: "Control plane observability"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Control-plane-service-observability"
---

Control plane observability allows you to monitor the status of core components of the control plane in a cluster. This topic describes how to configure control plane observability.

## Prerequisites

* Cloud\-native observability has been enabled. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

* (Optional) An alert notification policy has been created in the Observability Platform or VMP. For details, see [Creating notification policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_notification_policies?lang=en) and [Creating alert notification policies](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-notification-rules?lang=en).

* (Optional) An alert aggregation policy has been created in the Observability Platform or VMP. For details, see [Creating aggregation policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_aggregation_policies?lang=en) and [Creating alert aggregation policies](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-aggregation-rules?lang=en).

## Enabling observability

### Step 1: Configure observability items

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Find the target cluster and click its name.

3. In the left navigation pane of the cluster management page, click **Observability settings**, and select the **Basic observability** tab.

4. Find the **Control plane service** card and click **Enable observation** to go to the observability item configuration page.

5. The system automatically checks the necessary conditions for enabling observability, such as the workspace configuration and add\-on status.

6. For the **Observation item** parameter, select observability items for which you want to collect metrics. For items for which metric collection is not enabled, the system will not collect the corresponding metrics, and the system will prompt you to install the related add\-ons. You can decide whether to install the related add\-ons and select the corresponding observability items based on your business requirements.

7. After the configuration is complete, click **Next** to go to the alert and notification configuration page.

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

   > Description

   * > In addition to using preset alert templates to configure alert rules directly, you can customize the template configurations or directly use PromQL statements to configure alert rules. For details, see [Alert configuration overview](https://docs.byteplus.com/en/docs/vke/Configuring_alerts?lang=en).

   * > Details of the preset alert rule templates, including rule descriptions, PromQL configurations, and common alert handling procedures. See [Preset alert templates](https://docs.byteplus.com/en/docs/vke/Preset_alert_templates).

## Observability dashboards

> **tip**

> The built\-in dashboards provide features such as period\-over\-period comparisons of monitoring data and the ability to copy dashboard queries. For details, see [Using dashboards](https://docs.byteplus.com/en/docs/vke/Using_dashboard).

### kube\-apiserver monitoring

After you enable control plane monitoring, you can view the metrics of the control plane components in dashboards. Set the query time range and specify the refresh mode (manual or automatic).

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, click **Core addon monitoring** \> **Kube\-apiserver monitoring** to view the monitoring dashboard.

   The following table describes the charts related to APF rate limiting on the kube\-apiserver dashboard.

   > Description

   > For the method of obtaining the PromQL statements that correspond to the charts, see [Using dashboards](https://docs.byteplus.com/en/docs/vke/Using_dashboard).

   |Chart name |Unit |Chart description |
   |---|---|---|
   |APF currently executing requests (dimension: FS + PL) |Count |Request count metrics categorized by FlowSchema and PriorityLevelConfiguration. The following metrics are included:<br><br><br>* Currently executing: The number of currently executing requests at the corresponding PriorityLevelConfigurations for different FlowSchemas.<br><br>* Pending: The number of queued requests per FlowSchema at its PriorityLevelConfiguration. |
   |The number of APF requests currently pending in the queue (dimension: FS + PL) |Count ||
   |APF nominal concurrency limited number of seats |Count |Metrics for concurrency seats per PriorityLevelConfiguration‌. The following metrics are included:<br><br><br>* Nominal concurrency limit: The nominal maximum concurrency seat limit for a PriorityLevelConfiguration.<br><br>* Current concurrency limit: The actual maximum number of concurrent seats allowed in different PriorityLevelConfigurations after dynamic adjustment (borrowing and lending).<br><br>* Currently executing: The number of seats corresponding to currently executing requests at different PriorityLevelConfigurations.<br><br>* Currently queuing: The number of seats corresponding to the number of queued requests at different PriorityLevelConfigurations. |
   |APF current concurrency limit |Count ||
   |Number of seats currently running in APF |Count ||
   |Number of seats currently queued in APF |Count ||
   |APF request execution time [P90] |seconds |The 90th percentile duration from request execution start to completion per FlowSchema and PriorityLevelConfiguration. |
   |APF request wait time [P90] |seconds |The 90th percentile ‌request wait time from request enqueuing to execution start, per FlowSchema and PriorityLevelConfiguration. |
   |APF successfully dispatched and processed request QPS |req/s |Requests per second successfully scheduled and processed per FlowSchema and PriorityLevelConfiguration. |
   |APF rejects request QPS |req/s |Requests per second rejected (due to exceeding concurrency limits or queue capacity) per FlowSchema and PriorityLevelConfiguration. |

### etcd monitoring

After you enable control plane monitoring, you can view the metrics of the control plane components in dashboards. Set the query time range and specify the refresh mode (manual or automatic).

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, click **Core addon monitoring** \> **ETCD monitoring** to view the monitoring dashboard.

### kube\-scheduler monitoring

After you enable control plane monitoring, you can view the metrics of the control plane components in dashboards. Set the query time range, select an instance, and specify the refresh mode (manual or automatic).

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, click **Core addon monitoring** \> **Kube\-scheduler monitoring** to view the monitoring dashboard.

### cluster\-autoscaler monitoring

After you enable control plane monitoring, you can view the metrics of the control plane components in dashboards. Set the query time range, select an instance, and specify the refresh mode (manual or automatic).

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, click **Core addon monitoring** \> **Cluster\-autoscaler monitoring** to view the monitoring dashboard.

### kube\-controller\-manager monitoring

After you enable control plane monitoring, you can view the metrics of the control plane components in dashboards. Set the request quantile and query time range **,**  and specify the refresh mode (manual or automatic).

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, click **Core addon monitoring** \> **Kube\-controller\-manager monitoring** to view the monitoring dashboard.

   The kube\-controller\-manager monitoring dashboard consists of three parts: Resource, Workqueue, and Kube API. The following table provides detailed descriptions of the charts.

   > Description

   > For the method of obtaining the PromQL statements that correspond to the charts, see [Using dashboards](https://docs.byteplus.com/en/docs/vke/Using_dashboard).

   |Chart name |Unit |Chart description |
   |---|---|---|
   |**Resource** |||
   |Surviving kube\-controller\-manager instances |Count |The number of healthy instances of the kube\-controller\-manager add\-on.<br><br><br>* In normal scenarios, the number of instances of the kube\-controller\-manager add\-on in a cluster is 1. For a small number of large\-scale clusters, two instances exist.<br><br>* ‌If the instance count is abnormal (not 1 or 2, or the instance count is 0), it indicates an anomaly in the kube\-controller\-manager instances within the cluster.<br><br><br>> **tip**<br><br><br>> You can use the PromQL statement for this chart to create alert rules and generate alerts when the instance count is abnormal. For alerting configuration methods, see [Creating alerting rules](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rules).<br> |
   |kube\-controller\-manager process resident memory |MiB |The resident memory usage of the kube\-controller\-manager add\-on.<br><br><br>* In normal scenarios, this value only slightly fluctuates around a baseline value, with no sustained increases or sudden spikes. This value briefly rises only during large\-scale cluster operations (such as batch creation of Pods or Services or node scaling). It falls back to the baseline after the operations are complete.<br><br>* If memory keeps growing or sudden spikes occur, the kube\-controller\-manager add\-on instance is abnormal. |
   |kube\-controller\-manager CPU core usage |Millicores |The CPU utilization of the kube\-controller\-manager add\-on.<br><br><br>* In normal scenarios, this value only slightly fluctuates around a baseline value, with no sustained high utilization or sudden spikes. This value briefly rises only during large\-scale cluster operations (such as batch creation of Pods or Services or node scaling). It falls back to the baseline after the operations are complete.<br><br>* If CPU utilization remains above twice the baseline without falling back or suddenly spikes, the kube\-controller\-manager instance is abnormal. |
   |**Workqueue** |||
   |Workqueue Entry Rate |Count |The number of new tasks added for each controller of the kube\-controller\-manager add\-on, such as a node, Service, and endpoint controller, in the specified interval.<br><br><br>* In normal scenarios, all workqueue rates fluctuate around the baseline. They briefly rise only during cluster operations (such as batch creation of pods or Services or node scaling), and fall back to the baseline after the operations are complete.<br><br>* If a single workqueue rate remains high for a long period of time, multiple workqueue rates spike simultaneously, or the rate of a core queue remains 0 for a long period of time, it indicates that an exception occurs in the instance of the kube\-controller\-manager add\-on. |
   |Workqueue Depth |Count |The average depth of each workqueue for every controller, such as a node, Service, and endpoint controller in the kube\-controller\-manager add\-on. The depth indicates the number of pending tasks in each workqueue.<br><br><br>* In normal scenarios, the average value of all workqueues is stable and at a low level. The value only rises briefly during cluster operations, such as batch creation of pods and Services, and node scaling, and falls back to a stable average value after the operations are complete.<br><br>* If the workqueue depth remains at a high level for a long period of time, it indicates that the controller cannot promptly process tasks in the workqueue. This causes task accumulation. |
   |Workqueue processing duration |seconds |The quantile of task wait time in each workqueue for each controller, such as a node, Service, and endpoint controller of the kube\-controller\-manager component. For example, when the `quantile` is set to `0.9`, it indicates the wait time for 90 percent of tasks.<br><br>> **tip**<br><br><br><br>* > An exception in **Workqueue Depth** is usually accompanied by an increase in the percentile values of **Workqueue processing duration**. This indicates a task backlog, which leads to longer wait time. The two metrics can be correlated for analysis.<br><br><br>* > We recommend focusing on the 0.9 quantile (indicating the wait time for 90% of tasks) and the 0.99 quantile (exposing long\-tail latencies).<br> |
   |**Kube API** |||
   |Request QPS for APIServer |Count |The number of HTTP requests initiated by the kube\-controller\-manager add\-on to the API server per unit of time. Analysis is performed based on the request method and response code.<br><br><br>* In normal scenarios, the percentage of GET requests is greater than 80%, and more than 99% of response codes are 2xx (such as 200/201), with no 5xx errors.<br><br>* If 4xx or 5xx errors occur, the kube\-controller\-manager add\-on is consuming more resources, or logic errors occur in the controller. |
   |Delay distribution of request APIServer |seconds |The quantile of request duration when the kube\-controller\-manager add\-on calls the API server. For example, when the `quantile` is set to `0.9`, it indicates the duration for 90 percent of requests.<br><br>> **tip**<br><br><br>> We recommend focusing on the 0.9 quantile (representing the latency for 90% of requests) and the 0.99 quantile (exposing extremely slow requests).<br> |

## View metrics

* To query integrated or non\-integrated metrics in the cluster, or to understand metric meanings, see [Querying metrics](https://docs.byteplus.com/en/docs/vke/Querying_metrics).

* You can use the Explore feature of VMP to quickly query and display metric data. For details, see [Querying metrics](https://docs.byteplus.com/en/docs/vmp/explore-metrics).
