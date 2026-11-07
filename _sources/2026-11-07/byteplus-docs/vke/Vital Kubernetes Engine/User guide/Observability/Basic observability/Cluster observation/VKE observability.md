---
title: "VKE observability"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/VKE-observability"
---

VKE observability allows you to monitor the basic resources and operational status of VKE clusters. This topic describes how to configure VKE observability.

## Prerequisites

* Cloud\-native observability has been enabled. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

* (Optional) An alert notification policy has been created in the Observability Platform or VMP. For details, see [Creating notification policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_notification_policies?lang=en) and [Creating alert notification policies](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-notification-rules?lang=en).

* (Optional) An alert aggregation policy has been created in the Observability Platform or VMP. For details, see [Creating aggregation policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_aggregation_policies?lang=en) and [Creating alert aggregation policies](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-aggregation-rules?lang=en).

## Enabling observability

### Step 1: Configure observability items

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Find the target cluster and click its name.

3. In the left navigation pane of the cluster management page, click **Observability settings**, and select the **Basic observability** tab.

4. Find the **Container service** card and click **Enable observation** to go to the observability item configuration page.

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

   * Click the name of the preset rule that you want to configure to expand the preset alert rule configuration page, and configure the trigger conditions for alerts of different levels (P0, P1, or P2) in the **Triggering condition** section.

      |Parameter |Description |
      |---|---|
      |Alert level |Select the check box in the **Enable** column that corresponds to each alert level (P0, P1, or P2) to activate its trigger condition. If you do not select an option, alerts at this level are not configured. |
      |Comparison condition |Specify the comparison condition between the PromQL statement and the threshold. You can configure multiple comparison conditions, including **Greater than**, **Greater than or equal to**, **Less than**, **Less than or equal to**, **Equal to**, and **Not equal to**. |
      |Threshold |Configure the metric threshold. |
      |The duration of the condition |Configure the duration for which the metric continuously meets the trigger condition. The system triggers the alert at the corresponding level only if the metric continuously meets the comparison condition within this duration. |
      |Label |Configure the label of the alert rule. It is mainly used for alert identification, grouping, deduplication, and routing matching. A label consists of a key and a value. Where:<br><br><br>* **Key**: A string. It can start with a letter or an underscore (`_`), but cannot start with a double underscore (`__`). It can contain letters, digits, and underscores (`_`) and can be 1 to 256 characters in length.<br><br>* **Value**: A string. It can contain Chinese characters, English letters, digits, and special characters, and can be 1 to 512 in length.<br><br><br>Common configuration example:<br><br>```YAML```<br>```labels:```<br>```  severity: critical   # The alert level.```<br>```  business: pay        # The business line.```<br>```  alert_type: resource # The alert type.```<br><br><br> |
      |Annotation |Configure the annotation of the alert rule. It is mainly used to display key information. An annotation consists of a key and a value. Where:<br><br><br>* **Key**: A string. It can start with a letter or an underscore (`_`), but cannot start with a double underscore (`__`). It can contain letters, digits, and underscores (`_`) and can be 1 to 256 characters in length.<br><br>* **Value**: A string. It can contain Chinese characters, English letters, digits, and special characters, and can be 1 to 512 in length.<br><br><br>Common configuration example:<br><br>```YAML```<br>```annotations:```<br>```  summary: "High CPU usage on instance {{ $labels.instance }}"```<br>```  description: "Current CPU usage is {{ $value \| humanizePercentage }}, threshold is 80%"```<br>```  runbook_url: "https://xxx/docs/cpu-alert"```<br>```  dashboard_url: "https://grafana/xxx"```<br><br><br> |

5. Click **Complete the configuration**.

   > Description

   * > In addition to using preset alert templates to configure alert rules directly, you can customize the template configurations or directly use PromQL statements to configure alert rules. For details, see [Alert configuration overview](https://docs.byteplus.com/en/docs/vke/Configuring_alerts?lang=en).

   * > Details of the preset alert rule templates, including rule descriptions, PromQL configurations, and common alert handling procedures. See [Preset alert templates](https://docs.byteplus.com/en/docs/vke/Preset_alert_templates).

## Cluster observability dashboards

> **tip**

> The built\-in dashboards provide features such as period\-over\-period comparisons of monitoring data and the ability to copy dashboard queries. For details, see [Usage of dashboards](https://docs.byteplus.com/en/docs/vke/Using_dashboard).

### Cluster monitoring

This dashboard displays overall cluster monitoring information, including cluster node information (number of nodes and number of nodes in the NotReady state), cluster memory information (memory usage and memory utilization), and cluster CPU information (CPU usage and CPU utilization). You can specify a custom time range for querying information and set the information refresh mode to manual refresh or automatic refresh.

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, click **Cluster monitoring** \> **Cluster monitoring overview** to view the monitoring dashboard.

### Cluster namespace monitoring

This dashboard displays monitoring information at the cluster namespace level, including the number of Deployments, StatefulSets, and DaemonSets in the NotReady state within namespaces, as well as memory usage, CPU usage, and PVC usage within namespaces. You can specify a custom time range for querying information and set the information refresh mode to manual refresh or automatic refresh.

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, click **Cluster monitoring** \> **Cluster namespace monitoring** to view the monitoring dashboard.

## Node observability dashboards

### Overview of nodes

This dashboard provides an overview of node information, including the node memory usage rate, node CPU usage rate, node disk usage rate, and more. You can select multiple nodes to compare node resource usage. You can specify a custom time range for querying information and set the information refresh mode to manual refresh or automatic refresh.

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, click **Node monitoring** \> **Node overview** to view the monitoring dashboard.

### Node details monitoring

This dashboard displays monitoring information for a specified node, including node memory information (memory usage and memory usage rate), node CPU information (CPU usage, CPU usage rate, and CPU load), disk information (disk usage rate, disk read and write IOPS), and more. You can specify a custom time range for querying information and set the information refresh mode to manual refresh or automatic refresh.

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, click **Node monitoring** \> **Node details monitoring** to view the monitoring dashboard.

### Virtual node monitoring

This dashboard displays monitoring information of virtual nodes in the cluster. It includes memory information (total memory and memory usage), CPU information (total CPUs and CPU usage), GPU information (total GPU resources and GPU usage), and more. You can specify a custom time range for querying information and set the information refresh mode to manual refresh or automatic refresh.

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, click **Node monitoring** \> **Virtual node monitoring** to view the monitoring dashboard.

## Workload observability dashboards

### Deployment monitoring

This dashboard displays monitoring information of Deployments in the specified namespace, including instance information (desired number of instances, number of Ready instances, and ratio of Ready instances), CPU information (CPU request and CPU limits), memory information (memory request and memory limits), network information, disk information, and more. You can specify a custom time range for querying information and set the information refresh mode to manual refresh or automatic refresh.

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, click **Workload monitoring** \> **Deployment monitoring** to view the monitoring dashboard.

### StatefulSet monitoring

This dashboard displays monitoring information of StatefulSets in the specified namespace, including instance information (desired number of instances, number of Ready instances, and ratio of Ready instances), CPU information (CPU request and CPU limits), memory information (memory request and memory limits), network information, disk information, and more. You can query resource usage by time period and set the information refresh mode to manual or automatic refresh. You can specify a custom time range for querying information and set the information refresh mode to manual refresh or automatic refresh.

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, click **Workload monitoring** \> **StatefulSet monitoring** to view the monitoring dashboard.

### DaemonSet monitoring

This dashboard displays monitoring information of DaemonSets in the specified namespace, including CPU information (CPU request and CPU limits), memory information (memory request and memory limits), network information, disk information, and more. You can specify a custom time range for querying information and set the information refresh mode to manual refresh or automatic refresh.

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, select **Workload monitoring** \> **DaemonSet monitoring** to view the monitoring dashboard.

### Pod monitoring

This dashboard displays monitoring information of pods in the specified namespace, including memory information (memory usage and memory usage rate), CPU information (CPU usage and CPU usage rate), network information (inbound rate and outbound rate), and more. You can specify a custom time range for querying information and set the information refresh mode to manual refresh or automatic refresh.

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, click **Workload monitoring** \> **Pod monitoring** to view the monitoring dashboard.

> **tip**

> You can view the monitoring information of a single pod, or select **All** to view the monitoring information of all pods.

### Container monitoring

This dashboard displays monitoring information of containers in the specified namespace. It includes memory information (memory usage and memory usage rate), CPU information (CPU usage and CPU usage rate), and more. You can specify a custom time range for querying information and set the information refresh mode to manual refresh or automatic refresh.

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, click **Workload monitoring** \> **Container monitoring** to view the monitoring dashboard.

> **tip**

> You can view the monitoring information of a single container, or select **All** to view the monitoring information of all containers.

### Elastic scaling monitoring

This dashboard displays the HorizontalPodAutoscaler (HPA) monitoring information of all or specified pods in a namespace, including the expected number of replicas, current number of replicas, and more. You can specify a custom time range for querying information and set the information refresh mode to manual refresh or automatic refresh.

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, click **Workload monitoring** \> **Elastic scaling monitoring** to view the monitoring dashboard.

### Smart scaling monitoring

This dashboard displays monitoring information of IntelligentHorizontalPodAutoscaler (IHPA) resources within a namespace, including the number of replicas, CPU usage, memory usage, and more. You can specify a custom time range for querying information and set the information refresh mode to manual refresh or automatic refresh.

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, click **Workload monitoring** \> **Smart scaling monitoring** to view the monitoring dashboard.

## Storage observability dashboards

### PVC monitoring

This dashboard displays monitoring information of all or specified PersistentVolumeClaims (PVC) within a namespace, including the capacity usage rate and inode usage rate. You can specify a custom time range for querying information and set the information refresh mode to manual refresh or automatic refresh.

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, click **Storage service monitoring** \> **PVC monitoring** to view the monitoring dashboard.

## Core addon observability dashboards

### Metrics\-server monitoring

This dashboard displays observability metrics for the core add\-on metrics\-server. You can specify a custom time range for querying information and set the information refresh mode to manual refresh or automatic refresh.

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, click **Core addon monitoring** \> **Metrics\-server monitoring** to view the monitoring dashboard.

   The following table describes the charts on the metrics\-server monitoring dashboard.

   > Description

   > For the method of obtaining the PromQL statements that correspond to the charts, see [Using dashboards](https://docs.byteplus.com/en/docs/vke/Using_dashboard).

   |Chart name |Unit |Chart description |
   |---|---|---|
   |**Overview/One Screen Overview** |||
   |Number of nodes |Count |The current number of nodes monitored by metrics\-server in the cluster, reflecting the collection coverage of node metrics.<br><br><br>* Under normal circumstances, the number of nodes should be consistent with the actual number of nodes in the cluster and change as nodes are added or removed.<br><br>* If the node count is significantly lower than the actual node count or drops suddenly, this usually indicates that metrics for some nodes are not being collected properly. Check the node status, kubelet availability, and add\-on collection logs. |
   |number of containers |Count |The current number of containers monitored by metrics\-server in the cluster, reflecting the coverage of container metric collection.<br><br><br>* Under normal circumstances, the number of containers should change with the scale of the workload and be generally consistent with the actual number of containers running in the cluster.<br><br>* If the number of containers drops abnormally or is significantly inconsistent with the actual scale, it usually indicates that partial container metrics are not being collected properly. We recommend checking the relevant nodes, Pod status, and add\-on collection logs. |
   |Kubelet QPS |Times per second |The number of requests per second that metrics\-server sends to kubelet (calculated based on data from the past 5 minutes). This information reflects the collection request load on the add\-on.<br><br><br>* Under normal circumstances, the number of requests should change steadily with the node scale and collection frequency.<br><br>* If the number of requests continues to rise abnormally, it usually indicates an excessively high collection frequency, rapid growth in node scale, or repeated requests. If it drops abnormally, a collection interruption may have occurred. Check the add\-on configuration, node scale, and collection logs. |
   |capture success rate |% |The kubelet collection success rate (calculated based on data from the past 5 minutes). It reflects the reliability of node metric collection.<br><br><br>* Under normal circumstances, the collection success rate should be close to 100%.<br><br>* If the success rate continues to decrease, this usually indicates that some kubelet requests are failing, which may result in missing node or container metrics. Check the kubelet status, network connectivity, certificate, and permission configuration. |
   |Crawling P99 takes time |s |The P99 latency of a single collection\-and\-write cycle initiated by metrics\-server to kubelet, reflecting the tail latency of each collection cycle.<br><br><br>* Under normal circumstances, the P99 collection latency should remain stable and be lower than the add\-on's collection cycle.<br><br>* If P99 continues to rise, it usually indicates that some nodes are slowing down in collection, which may cause metric update delays. Check kubelet response duration, network quality, and add\-on resource usage. |
   |indicator freshness |s |The average gap between the collection time of existing metrics and the current time, reflecting the freshness of metric data.<br><br><br>* Under normal circumstances, metric freshness should be less than the collection cycle.<br><br>* If this value continues to increase and exceeds the collection cycle, This usually indicates that metric updates are not timely, which may be caused by collection delays or failures. Further investigate the issue by reviewing the collection success rate, collection duration, and kubelet status. |
   |**Storage & API/Resources & Core State** |||
   |Store Point Trend |Count |The trend of resource changes monitored by metrics\-server by node and container type, reflecting the scale of metric data currently stored by the add\-on.<br><br><br>* Under normal circumstances, the counts of node and container storage points should change steadily with the cluster size and should generally match the actual number of nodes and containers, respectively.<br><br>* If the storage point count of a certain type suddenly drops or is not updated for a long time, it usually indicates an anomaly in the corresponding metric collection or storage. Check the node, container status, and add\-on log. |
   |fetch time |s |Average collection latency and P99 latency (calculated based on data from the past 5 minutes), reflecting overall collection efficiency and tail latency.<br><br><br>* Under normal circumstances, the average duration and P99 should remain stable, and P99 is usually higher than the average value.<br><br>* If the average duration or P99 continues to increase, it usually indicates that metric collection for all or some nodes is slowing down. Check kubelet response duration, network quality, and add\-on resource usage. |
   |Index freshness trend |s |The trend of metric freshness, with 15 seconds as a reference line. This information reflects whether metric updates are timely.<br><br><br>* Under normal circumstances, metric freshness should remain stable and preferably be lower than the reference line (15 seconds).<br><br>* If metric freshness is continuously higher than the reference line or keeps increasing, it usually indicates a delay in metric updates. Further investigate the issue by reviewing the collection success rate, collection duration, and kubelet status. |
   |**Kubelet/external dependencies** |||
   |Kubelet requests |Times per second |Shows the number of kubelet requests per second by success and failure results (calculated based on data from the past 5 minutes), reflecting collection requests and result distribution.<br><br><br>* Under normal circumstances, requests should change smoothly with the scale of nodes, and successful requests should account for the majority.<br><br>* If failed requests continue to increase or the total requests fluctuate abnormally, it usually indicates abnormal kubelet access or changes in collection load. We recommend checking network connectivity, kubelet status, and add\-on collection logs. |
   |Kubelet request delay |s |The average and P99 latency of kubelet requests (calculated based on data from the past 5 minutes), reflecting request processing efficiency and tail latency.<br><br><br>* Under normal circumstances, the average latency and P99 should remain stable, and P99 is usually higher than the average value.<br><br>* If the average latency or P99 continues to rise, it usually indicates that some kubelet responses are slowing down, which may affect metric collection timeliness. Check node load, kubelet status, and network quality. |
   |Latest fetch delay |s |Shows the interval since the most recent kubelet metric collection request by node, reflecting whether the metric collection job on each node is running continuously.<br><br><br>* Under normal circumstances, the most recent collection latency for each node should be close to the configured collection cycle and remain stable.<br><br>* If the latency for a particular node continues to increase, it usually indicates that metrics have not been successfully collected from the node for an extended period. Check the node status, kubelet availability, and network connectivity. |
   |Kubelet request success rate trend |% |The trend of kubelet request success rate (calculated based on data from the past 5 minutes). This information reflects the stability of node metric collection.<br><br><br>* Under normal circumstances, the request success rate should remain close to 100% for an extended period, and the curve should stay steady.<br><br>* If the success rate continues to decrease or fluctuates frequently, it usually indicates abnormal kubelet requests, which may lead to missing or delayed metrics. Check kubelet status, network connectivity, certificate, and permission configuration. |

### kube\-proxy monitoring

This dashboard displays observability metrics for the core add\-on kube\-proxy. You can specify a custom time range for querying information and set the information refresh mode to manual refresh or automatic refresh.

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, click **Core addon monitoring** \> **Kube\-proxy monitoring** to view the monitoring dashboard.

   The following table describes the charts on the kube\-proxy monitoring dashboard.

   > Description

   > For the method of obtaining the PromQL statements that correspond to the charts, see [Using dashboards](https://docs.byteplus.com/en/docs/vke/Using_dashboard).

   |Chart name |Unit |Chart description |
   |---|---|---|
   |**Overview** |||
   |Targets |Count |Shows the total number of kube\-proxy instances in the cluster that can be discovered by the monitoring system at the current time, reflecting the deployment scale of the add.<br><br><br>* Under normal circumstances, this value should be consistent with the number of nodes in the cluster that need to run kube\-proxy, and should change synchronously with node scaling.<br><br>* If this value decreases abnormally or is inconsistent with the expected number of nodes, it usually indicates that some kube\-proxy instances are not running or that metric collection has failed. We recommend checking the kube\-proxy Pod status, ServiceMonitor configuration, and monitoring collection targets on the abnormal nodes. |
   |Down Targets |Count |Shows the number of kube\-proxy instances that cannot be collected by the monitoring system at the current time. This indicates the availability of add\-on instances.<br><br><br>* Under normal circumstances, this value should be 0.<br><br>* If this value is abnormally greater than 0, it usually indicates that one or more kube\-proxy instances are unreachable, the process is abnormal, or the metric collection link is interrupted. We recommend checking the kube\-proxy Pod status, network connectivity, and monitoring collection configuration on the corresponding nodes. |
   |Max Network Programming P99 |seconds |Shows the P99 duration of network rule programming for each node and IP protocol family. This value is calculated based on samples from the past 5 minutes and is used to identify the highest network rule effective latency.<br><br><br>* Under normal circumstances, this value should remain stable and should not continuously show significant increases.<br><br>* If this value rises abnormally or remains high, it usually indicates that some nodes are slowing down in writing network rules. We recommend checking the CPU, memory, and kernel network status of the corresponding nodes and identifying the cause based on the rule count and kube\-proxy logs. |
   |Max Rule Sync P99 |seconds |Shows the P99 duration of proxy rule synchronization for each node and IP protocol family. This value is calculated based on samples from the past 5 minutes and is used to identify the slowest rule synchronization process.<br><br><br>* Under normal circumstances, this value should remain stable and fall back within a short time after rule changes.<br><br>* If this value increases abnormally or remains high, it usually indicates that some nodes are slowing down in synchronizing Service or Endpoint rules. We recommend checking the rule scale, number of pending changes, node resource usage, and kube\-proxy logs. |
   |Max FD Usage Ratio |% |Shows the proportion of open file descriptors to the upper limit for the kube\-proxy process on each node at the current time. This is used to identify the risk of file descriptor exhaustion.<br><br><br>* Under normal circumstances, this proportion should remain stable and maintain a sufficient margin from 100%.<br><br>* If this proportion rises abnormally or approaches 100%, it usually indicates that a kube\-proxy process is continuously opening more files or connections. We recommend checking the connection scale, process resource limits, and kube\-proxy logs on the corresponding node to troubleshoot file descriptor leaks. |
   |Restarts (1h) |Count |Shows the total number of times the start time of all kube\-proxy processes changed in the past hour. This is used to determine whether the add\-on restarts frequently.<br><br><br>* Under normal circumstances, this value should be 0. It may increase briefly during add\-on upgrades or node maintenance.<br><br>* If this value increases abnormally or continues to grow, it usually indicates that the kube\-proxy process is restarting repeatedly. We recommend checking the restart reason, exit code, events, resource limits, and node status of the corresponding Pod. |
   |Max Pending Endpoint Changes |Count |Shows the number of Endpoint changes to be synchronized on each node at the current time. This is used to identify backlogs in Endpoint rule processing.<br><br><br>* Under normal circumstances, this value should be close to 0 and fall back quickly after Endpoint changes occur.<br><br>* If this value increases abnormally or does not fall back for a long time, it usually indicates that some nodes are not processing Endpoint changes fast enough. We recommend checking rule synchronization duration, node resource usage, Endpoint change frequency, and kube\-proxy logs. |
   |Max Pending Service Changes |Count |Shows the number of Service changes to be synchronized on each node at the current time. This is used to identify backlogs in Service rule processing.<br><br><br>* Under normal circumstances, this value should be close to 0 and fall back quickly after Service changes occur.<br><br>* If this value increases abnormally or does not fall back for a long time, it usually indicates that some nodes are not processing Service changes fast enough. We recommend checking rule synchronization duration, node resource usage, Service change frequency, and kube\-proxy logs. |
   |Max Services Without Local Endpoints per Node |Count |Shows the number of Services without local Endpoints on each node at the current time. This is used to identify the risk that local traffic policies may be unable to forward traffic.<br><br><br>* Under normal circumstances, this value should match the deployment expectations of Services using the Local traffic policy and remain stable.<br><br>* If this value rises abnormally, it usually indicates that some nodes lack available local Endpoints. We recommend checking the externalTrafficPolicy or internalTrafficPolicy of the related Services, pod scheduling distribution, EndpointSlice status, and pod readiness. |
   |REST QPS |req/s |Shows the total number of requests per second that kube\-proxy calls to the API Server. This value is calculated based on samples from the past 5 minutes and is used to observe the load of the add\-on accessing the Kubernetes API.<br><br><br>* Under normal circumstances, this value needs to match the cluster scale and resource change frequency and remain stable overall.<br><br>* If this value rises abnormally or fluctuates frequently, it usually indicates frequent changes to resource objects, increased client retries, or abnormal add\-on behavior. We recommend performing troubleshooting based on the request method, response status code, API Server load, and kube\-proxy logs. |
   |API 429/5xx Ratio |% |Shows the proportion of requests that return 429 or 5xx responses when kube\-proxy calls the API Server. This value is calculated based on samples from the past 5 minutes and is used to identify throttling and server\-side exceptions.<br><br><br>* Under normal circumstances, this proportion should be 0 or remain low.<br><br>* If this proportion rises abnormally, it usually indicates throttling, overload, and server\-side errors on the API Server. We recommend checking the API Server request volume, throttling, and resource usage, and locating abnormal requests based on status codes and kube\-proxy logs. |
   |**Pod Resource Usage** |||
   |Pod CPU Usage — Top 10 |cores |Shows the CPU usage of each kube\-proxy pod and shows the top 10 Pods. This value is calculated based on samples from the past 5 minutes and is used to locate instances with high CPU consumption.<br><br><br>* Under normal circumstances, the CPU usage of each Pod should be stable, and the difference between nodes of the same specification should not be large for a long time.<br><br>* If the CPU usage of some Pods rises abnormally or remains at the top, it usually indicates frequent rule changes, a large rule scale, or increased process processing pressure. We recommend performing troubleshooting based on the node scale, rule synchronization duration, resource limits, and kube\-proxy logs. |
   |Pod Memory Working Set — Top 10 |Bytes |Shows the memory working set of each kube\-proxy Pod at the current time and the top 10 Pods. This is used to locate instances that actually occupy a high amount of physical memory.<br><br><br>* Under normal circumstances, the memory working set of each Pod should be stable and below the configured memory limit.<br><br>* If the memory working set of some Pods grows abnormally or remains at the top, it usually indicates an expanded rule scale, a cache increase, or a memory leak risk. We recommend checking the Pod memory limit, rule count, process restart status, and kube\-proxy logs. |
   |**Rule Sync & Network Programming** |||
   |Cluster Rule Sync Duration P50/P95/P99 |seconds |Shows the P50, P95, and P99 duration of proxy rule synchronization in the cluster under different IP protocol families. This value is calculated based on samples from the past 5 minutes and is used to observe the overall latency distribution of rule synchronization.<br><br><br>* Under normal circumstances, each percentile should remain stable, and P50, P95, and P99 should increase in order without the gap continuously widening.<br><br>* If P95 or P99 rises abnormally, it usually indicates that long\-tail latency occurs in the synchronization of some rules. We recommend checking the rule scale, change frequency, node resource usage, number of pending changes, and kube\-proxy logs. |
   |Cluster Network Programming Latency P50/P95/P99 |seconds |Shows the P50, P95, and P99 durations of network rule programming for the cluster under different IP protocol families. These values are calculated based on samples from the past 5 minutes and are used to observe the latency distribution of rules written to the data plane.<br><br><br>* Under normal circumstances, each percentile value should remain stable, and the high\-percentile duration needs not to continuously deviate significantly from the median.<br><br>* If P95 or P99 increases abnormally, it usually indicates long\-tail latency in writing network rules on some nodes. We recommend checking node resources, kernel network status, rule scale, and kube\-proxy logs. |
   |Top 10 Nodes by Rule Sync Duration P99 |seconds |Shows the P99 duration of proxy rule synchronization for each node and IP protocol family, and shows the top 10 nodes. The value is calculated based on samples from the past 5 minutes. This is used to locate the nodes with the slowest rule synchronization.<br><br><br>* Under normal circumstances, the P99 duration of each node should be stable, and the difference between nodes of the same type needs not to be too large for a long time.<br><br>* If the P99 duration of some nodes increases abnormally or remains at the top, it usually indicates that these nodes have bottlenecks in rule scale, resources, or kernel processing. We recommend comparing the node load, number of pending changes, number of rules, and kube\-proxy logs. |
   |Top 10 Nodes by Network Programming Latency P99 |seconds |Shows the P99 duration of network rule programming for each node and IP protocol family, and shows the top 10 nodes. This value is calculated based on samples from the past 5 minutes and is used to locate the nodes where data plane rules take effect most slowly.<br><br><br>* Under normal circumstances, the P99 duration of each node should be stable, and the difference between nodes of the same type needs not to be too large for a long time.<br><br>* If the P99 duration of some nodes rises abnormally or remains at the top, it usually indicates that those nodes are slower at writing network rules. We recommend checking node CPU, memory, kernel network status, rule scale, and kube\-proxy logs. |
   |Average Endpoint/Service Change Rate per Instance |Times per second |Shows the number of Endpoint and Service changes processed per second by each kube\-proxy instance and calculates the average value across all instances at the current time. The rate is calculated based on samples from the past 5 minutes and is used to observe the average rule change pressure per instance.<br><br><br>* Under normal circumstances, the two types of change rates need to match business release and scaling activities, and fall after the changes end.<br><br>* If the change rate increases abnormally or remains high for a long time, it usually indicates frequent changes to Services, Endpoints, or EndpointSlices. We recommend checking workload releases, Pod readiness status, elastic scaling activities, and related controller events. |
   |Pending Endpoint/Service Changes — Top 10 per Type |Count |Shows the number of pending Endpoint and Service changes on each node at the current time and shows the top 10 nodes for each type. This is used to locate nodes with a backlog of rule changes.<br><br><br>* Under normal circumstances, the number of pending changes for both types should be close to 0 and fall back quickly after resource changes.<br><br>* If the number of pending changes on some nodes rises abnormally or does not fall back for a long time, it usually indicates that those nodes have insufficient rule synchronization capability or an abnormal synchronization process. We recommend checking the rule synchronization duration, node resources, resource change frequency, and kube\-proxy logs. |
   |Top 10 Nodes by Time Since Last Successful Sync |seconds |Shows the time when the proxy rule was last synchronized for each node and IP protocol family at the current time, and shows the top 10 nodes with the longest interval. This is used to identify instances for which the rule has not been synchronized for a long time.<br><br><br>* Under normal circumstances, this value falls back periodically with rule synchronization and does not continue growing.<br><br>* If the interval for some nodes increases abnormally or continues to grow, it usually indicates that kube\-proxy has not successfully synchronized rules for a long time. We recommend checking the status of the corresponding instance, rule synchronization errors, API Server connectivity, and kube\-proxy logs. |
   |Services Without Local Endpoints — Top 10 Node/Policy Combinations |Count |Shows the number of Services without local Endpoints for each combination of node, IP protocol family, and traffic policy at the current time, and shows the top 10 combinations. This is used to locate local traffic forwarding risks.<br><br><br>* Under normal circumstances, this value should meet the deployment expectations of the Local traffic policy and remain stable with Pod distribution.<br><br>* If the value of some combinations increases abnormally, it usually indicates that the relevant nodes lack ready local Endpoints. We recommend checking the Service traffic policy, Pod scheduling distribution, EndpointSlice status, and Pod readiness status. |
   |Stale UDP Conntrack Entries Deleted (1h) — Top 10 Node/IP Family Combinations |Count |Shows the number of stale UDP Conntrack entries deleted by each node and IP protocol family in the past 1 hour, and shows the top 10 combinations. This is used to observe the cleanup pressure on the connection tracking table.<br><br><br>* Under normal circumstances, this value should match the UDP business traffic and backend change scale, and not continue to surge without business changes.<br><br>* If this value increases abnormally, it usually indicates frequent changes to UDP backends, accumulation of a large number of stale connection tracking entries, or network jitter. We recommend checking UDP Service and Pod changes, Conntrack usage, and node network status. |
   |Cluster Conntrack Reconciliation Duration P99 |seconds |Shows the P99 duration of Conntrack reconciliation across different IP protocol families in the cluster. This value is calculated based on samples from the past hour and is used to observe the long\-tail duration of cleaning up stale UDP connection tracking entries.<br><br><br>* Under normal circumstances, this value should remain stable and not continuously increase significantly.<br><br>* If this value increases abnormally or remains high, it usually indicates a large Conntrack table size, increased cleanup pressure, or slower node network processing. We recommend checking Conntrack table usage, UDP business changes, node resources, and kernel network status. |
   |**API Server Requests** |||
   |API Server Request Rate by Method/Status Code |Times per second |Shows the number of requests per second made by kube\-proxy to the API Server by request method and response status code. This value is calculated based on samples from the past 5 minutes and is used to analyze request composition and sources of error responses.<br><br><br>* Under normal circumstances, the request rate should match the cluster resource change frequency, with successful status codes dominating.<br><br>* If the request rate or the number of requests corresponding to abnormal status codes increases abnormally, it usually indicates frequent resource changes, client retries, API Server rate limiting, or server\-side exceptions. We recommend performing troubleshooting in combination with methods, status codes, API Server load, and kube\-proxy logs. |
   |API Server 429/5xx Response Ratio |% |Shows the proportion of 429 and 5xx responses to all requests when kube\-proxy calls the API Server. This value is calculated based on samples from the past 5 minutes and is used to distinguish throttling from server\-side failures.<br><br><br>* Under normal circumstances, both response proportions need to be 0% or remain low.<br><br>* If the 429 or 5xx proportion rises abnormally, it usually indicates throttling or overload on the API Server, or server\-side errors. We recommend checking the API Server request volume, throttling configuration, resource usage, and logs for the corresponding status codes. |
   |**IPVS Data Plane** |||
   |Top 10 Nodes by IPVS Connection Rate |Times per second |Shows the per\-second rate of new IPVS connections on each node and shows the top 10 nodes. This value is calculated based on samples from the past 5 minutes and is used to locate nodes with high connection establishment pressure.<br><br><br>* Under normal circumstances, this rate should be consistent with changes in business access volume and need not continue to rise abnormally when traffic is stable.<br><br>* If the connection rate of some nodes rises abnormally or remains at the top, it usually indicates traffic spikes, increased short connections, or uneven load distribution. We recommend checking business traffic, connection reuse, Service backend distribution, and node network status. |
   |Top 10 Nodes by IPVS Packet Rate (In/Out) |Packets/second |Shows the number of inbound and outbound packets per second of IPVS on each node and shows the top 10 nodes. This value is calculated based on samples from the past 5 minutes and is used to observe node forwarding packet rate.<br><br><br>* Under normal circumstances, inbound and outbound packet rates should change synchronously with business traffic, and the overall trends should be matched.<br><br>* If the packet rate of some nodes rises abnormally, drops sharply, or the inbound and outbound packets are clearly mismatched for a long time, it usually indicates traffic spikes, packet loss, forwarding exceptions, or uneven load distribution. We recommend checking business traffic, NIC and packet loss metrics, IPVS rules, and node network status. |
   |Top 10 Nodes by IPVS Throughput (In/Out) |bytes per second |Shows the number of inbound and outbound bytes transmitted per second of IPVS on each node and shows the top 10 nodes. This value is calculated based on samples from the past 5 minutes and is used to observe node data plane throughput.<br><br><br>* Under normal circumstances, inbound and outbound throughput need to change synchronously with business traffic and match node capacity.<br><br>* If the throughput of some nodes rises abnormally, drops sharply, or the inbound and outbound bytes are clearly mismatched for a long time, it usually indicates traffic spikes, network congestion, forwarding exceptions, or uneven load distribution. We recommend checking business traffic, NIC bandwidth and error metrics, IPVS rules, and node network status. |

## View metrics

* You can use the Explore feature of VMP to quickly query and display metric data. For details, see [Querying metrics](https://docs.byteplus.com/en/docs/vmp/explore-metrics).
