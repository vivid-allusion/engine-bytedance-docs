---
title: "AI resource observability"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/AI-resource-observability"
---

VKE supports monitoring AI resources (GPU resources and RDMA resources) within clusters. This topic describes how to configure AI resource observability.

## Limits

* RDMA metrics collection currently supports only NVIDIA GPU mode, not mGPU mode.

* In shared mode, only RDMA metrics of nodes are reported.

* In exclusive mode, only RDMA metrics of pods are reported.

## Prerequisites

* Cloud\-native observability has been enabled. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

* The VKE observability feature has been enabled. For details, see [VKE observability](https://docs.byteplus.com/en/docs/vke/VKE-observability).

* The following add\-ons have been installed:

   * **GPU observability**: The nvidia\-device\-plugin and dcgm\-exporter add\-ons have both been installed. For details, see [nvidia-device-plugin](https://docs.byteplus.com/en/docs/vke/nvidia-device-plugin-add-on).

   * **mGPU observability**: The mgpu and mgpu\-exporter add\-ons have both been installed. For details, see [mgpu](https://docs.byteplus.com/en/docs/vke/mgpu-add-on).

   * **RDMA observability**: The rdma\-device\-plugin add\-on has been installed. For details, see [rdma-device-plugin](https://docs.byteplus.com/en/docs/vke/rdma-device-plugin-add-on).

* The prometheus\-agent add\-on has been upgraded to v2.2.0 or later. For details, see [Add-on release notes](https://docs.byteplus.com/en/docs/vke/prometheus-agent).

* (Optional) An alert notification policy has been created in the Observability Platform or VMP. For details, see [Creating notification policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_notification_policies?lang=en) and [Creating alert notification policies](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-notification-rules?lang=en).

* (Optional) An alert aggregation policy has been created in the Observability Platform or VMP. For details, see [Creating aggregation policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_aggregation_policies?lang=en) and [Creating alert aggregation policies](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-aggregation-rules?lang=en).

## Enabling observability

### Step 1: Configure observability items

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Find the target cluster and click its name.

3. In the left navigation pane of the cluster management page, click **Observability settings**, and select the **Basic observability** tab.

4. Find the **AI resources** card and click **Enable observation** to go to the observability item configuration page.

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
      |Label |Configure the label of the alert rule. It is mainly used for alert identification, grouping, deduplication, and routing matching. A label consists of a key and a value. Where:<br><br><br>* **Key**: A string. It can start with a letter or an underscore (`_`), but cannot start with a double underscore (`__`). It can contain letters, digits, and underscores (`_`) and can be 1 to 256 characters in length.<br><br>* **Value**: A string. It can contain Chinese characters, English letters, digits, and special characters, and can be 1 to 512 characters in length.<br><br><br>Common configuration example:<br><br>```YAML```<br>```labels:```<br>```  severity: critical   # The alert level.```<br>```  business: pay        # The business line.```<br>```  alert_type: resource # The alert type.```<br><br><br> |
      |Annotation |Configure the annotation of the alert rule. It is mainly used to display key information. An annotation consists of a key and a value. Where:<br><br><br>* **Key**: A string. It can start with a letter or an underscore (`_`), but cannot start with a double underscore (`__`). It can contain letters, digits, and underscores (`_`) and can be 1 to 256 characters in length.<br><br>* **Value**: A string. It can contain Chinese characters, English letters, digits, and special characters, and can be 1 to 512 characters in length.<br><br><br>Common configuration example:<br><br>```YAML```<br>```annotations:```<br>```  summary: "High CPU usage on instance {{ $labels.instance }}"```<br>```  description: "Current CPU usage is {{ $value \| humanizePercentage }}, threshold is 80%"```<br>```  runbook_url: "https://xxx/docs/cpu-alert"```<br>```  dashboard_url: "https://grafana/xxx"```<br><br><br> |

5. Click **Complete the configuration**.

   > Description

   * > In addition to using preset alert templates to configure alert rules directly, you can customize the template configurations or directly use PromQL statements to configure alert rules. For details, see [Alert configuration overview](https://docs.byteplus.com/en/docs/vke/Configuring_alerts?lang=en).

   * > Details of the preset alert rule templates, including rule descriptions, PromQL configurations, and common alert handling procedures. See [Preset alert templates](https://docs.byteplus.com/en/docs/vke/Preset_alert_templates).

## Observability dashboards

> **tip**

> The built\-in dashboard provides features such as comparing monitoring data across periods of time and copying dashboard statements. For details, see [Using dashboards](https://docs.byteplus.com/en/docs/vke/Using_dashboard).

### Cluster\-level GPU monitoring

The cluster\-level GPU monitoring dashboard displays GPU metrics of a cluster, such as the total number of GPUs in the cluster, the number of allocated GPUs, and the number of GPUs in use. This dashboard provides an overview of GPU resource utilization across the cluster. You can specify a custom time range for querying information and set the information refresh mode to manual refresh or automatic refresh.

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, click **GPU monitoring** \> **Cluster GPU Monitoring** to view the monitoring dashboard.

### GPU instance\-level monitoring

The GPU instance\-level monitoring dashboard displays GPU monitoring information at the GPU card instance level, such as GPU utilization, GPU memory usage, GPU temperature, and GPU power consumption. This dashboard provides an overview of a specific GPU card. You can specify a custom time range for querying information and set the information refresh mode to manual refresh or automatic refresh.

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, click **GPU monitoring** \> **GPU instance monitoring** to view the monitoring dashboard.

### Pod\-level GPU monitoring

The pod\-level GPU monitoring dashboard displays pod\-level GPU metrics, such as GPU utilization, GPU memory utilization, and the amount of GPU memory used. This dashboard provides an overview of GPU resource utilization of a specific pod. You can specify a custom time range for querying information and set the information refresh mode to manual refresh or automatic refresh.

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, click **GPU monitoring** \> **Pod GPU monitoring** to view the monitoring dashboard.

### Node\-level GPU monitoring

The node\-level GPU monitoring dashboard displays node\-level GPU metrics, such as node resource usage, node GPU usage details, GPU utilization, and GPU memory usage. This dashboard provides an overview of GPU resource utilization on a specific node. You can specify a custom time range for querying information and set the information refresh mode to manual refresh or automatic refresh.

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, click **GPU monitoring** \> **Node GPU monitoring** to view the monitoring dashboard.

   * In the node resource usage**** list, click a node to view the monitoring information for that node.

   * In the **node GPU usage details** list, click a GPU card to view its monitoring information.

### User\-level GPU monitoring

The user\-level GPU monitoring dashboard displays AI training monitoring information at the team level. This information includes the number of training jobs, number of GPU workers, GPU utilization by the training jobs, and Xid errors of team training jobs. This dashboard provides an overview of GPU resource utilization by team. You can specify a custom time range for querying information and set the information refresh mode to manual refresh or automatic refresh.

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, click **GPU monitoring** \> **User GPU Monitoring** to view the monitoring dashboard.

   * In the team training job**** list, click a specific team to view the monitoring information for that team.

   * In the team member training job overview****, click a specific team member to view the monitoring information for that team member.

> **tip**

> To include the monitoring information for team training jobs in the dashboard, you need to add the `ai.vke.volcengine.com/task`, `ai.vke.volcengine.com/job`, `ai.vke.volcengine.com/team`, and `ai.vke.volcengine.com/user` labels to the training jobs. For details, see [AI training job monitoring](https://docs.byteplus.com/en/docs/vke/Monitoring-AI-training-Jobs).

## Metrics

### rdma\-device\-plugin monitoring

No observability dashboard is provided for RDMA network performance metrics. You can get monitoring information by checking the list of metrics of the rdma\-device\-plugin add\-on.

|Metric category |Metric name |Metric type |Metric meaning |
|---|---|---|---|
|Node metrics |rdma_exporter_node_infiniband_implied_nak_seq_err_total |Counter |Read response out\-of\-order count. |
||rdma_exporter_node_infiniband_local_ack_timeout_err_total |Counter |Outbound timeout count. |
||rdma_exporter_node_infiniband_np_cnp_sent_total |Counter |Number of CNP packets sent by the NIC during the outbound collection period. It indicates congestion on the receiving path, and the sender needs to be notified to reduce its sending rate. |
||rdma_exporter_node_infiniband_np_ecn_marked_roce_packets_total |Counter |Number of ECN\-marked packets received by the NIC during the inbound collection cycle. It indicates congestion on the path. |
||rdma_exporter_node_infiniband_out_of_sequence_total |Counter |Inbound out\-of\-order count. An increase in this metric may indicate a link issue. |
||rdma_exporter_node_infiniband_packet_seq_err_total |Counter |Outbound out\-of\-order count. |
||rdma_exporter_node_infiniband_port_data_received_bytes_total |Counter |Inbound traffic at the driver level, including TCP/IP and RDMA. |
||rdma_exporter_node_infiniband_port_data_transmitted_bytes_total |Counter |Outbound traffic at the driver level, including TCP/IP and RDMA. |
||rdma_exporter_node_infiniband_port_packets_received_total |Counter |Inbound packet count at the driver level, including TCP/IP and RDMA. |
||rdma_exporter_node_infiniband_port_packets_transmitted_total |Counter |Outbound packet count at the driver level, including TCP/IP and RDMA. |
||rdma_exporter_node_infiniband_rdma_data_received_bytes_total |Counter |Inbound RDMA traffic. |
||rdma_exporter_node_infiniband_rdma_data_transmitted_bytes_total |Counter |Outbound RDMA traffic. |
||rdma_exporter_node_infiniband_rdma_packets_received_total |Counter |Inbound RDMA packet count. |
||rdma_exporter_node_infiniband_rdma_packets_transmitted_total |Counter |Outbound RDMA packet count. |
||rdma_exporter_node_infiniband_rp_cnp_handled_total |Counter |Number of CNP packets processed by the NIC during the inbound collection cycle. Reduce the packet sending rate. |
||rdma_exporter_node_infiniband_rp_cnp_ignored_total |Counter |Number of CNP packets ignored by the NIC during the inbound collection cycle. This metric should not increase. If it increases, check whether the congestion control configuration of the NIC is normal and whether ECN/CNP is enabled. |
||rdma_exporter_node_infiniband_rx_pause_duration_seconds |Counter |Inbound pause duration. This metric generally indicates network congestion. It represents PFC packets received by the NIC as the sender. It means the receiver is severely congested and requires the NIC to stop sending. |
||rdma_exporter_node_infiniband_tx_pause_duration_seconds |Counter |Outbound pause duration. This metric generally indicates a host anomaly, where the NIC sends PFC packets. It means the NIC (as the receiver) is severely congested and requires the sender to stop sending. |
||rdma_exporter_node_infiniband_rx_pause_total |Counter |Number of PFC pause packets received in the inbound direction. Currently, priority 5 is used. |
||rdma_exporter_node_infiniband_tx_pause_total |Counter |Number of PFC pause packets sent in the outbound direction. |
|Pod metrics |rdma_exporter_pod_infiniband_implied_nak_seq_err_total |Counter |Read response out\-of\-order count. |
||rdma_exporter_pod_infiniband_local_ack_timeout_err_total |Counter |Outbound timeout count. |
||rdma_exporter_pod_infiniband_np_cnp_sent_total |Counter |Number of CNP packets sent by the NIC during the outbound collection period. It indicates congestion on the receiving path, and the sender needs to be notified to reduce its sending rate. |
||rdma_exporter_pod_infiniband_np_ecn_marked_roce_packets_total |Counter |Number of ECN\-marked packets received by the NIC during the inbound collection cycle. It indicates congestion on the path. |
||rdma_exporter_pod_infiniband_out_of_sequence_total |Counter |Inbound out\-of\-order count. An increase in this metric may indicate a link issue. |
||rdma_exporter_pod_infiniband_packet_seq_err_total |Counter |Outbound out\-of\-order count. |
||rdma_exporter_pod_infiniband_port_data_received_bytes_total |Counter |Inbound traffic at the driver level, including TCP/IP and RDMA. |
||rdma_exporter_pod_infiniband_port_data_transmitted_bytes_total |Counter |Outbound traffic at the driver level, including TCP/IP and RDMA. |
||rdma_exporter_pod_infiniband_port_packets_received_total |Counter |Inbound packet count at the driver level, including TCP/IP and RDMA. |
||rdma_exporter_pod_infiniband_port_packets_transmitted_total |Counter |Outbound packet count at the driver level, including TCP/IP and RDMA. |
||rdma_exporter_pod_infiniband_rdma_data_received_bytes_total |Counter |Inbound RDMA traffic. |
||rdma_exporter_pod_infiniband_rdma_data_transmitted_bytes_total |Counter |Outbound RDMA traffic. |
||rdma_exporter_pod_infiniband_rdma_packets_received_total |Counter |Inbound RDMA packet count. |
||rdma_exporter_pod_infiniband_rdma_packets_transmitted_total |Counter |Outbound RDMA packet count. |
||rdma_exporter_pod_infiniband_rp_cnp_handled_total |Counter |Number of CNP packets processed by the NIC during the inbound collection cycle. Reduce the packet sending rate. |
||rdma_exporter_pod_infiniband_rp_cnp_ignored_total |Counter |Number of CNP packets ignored by the NIC during the inbound collection cycle. This metric should not increase. If it increases, check whether the congestion control configuration of the NIC is normal and whether ECN/CNP is enabled. |
||rdma_exporter_pod_infiniband_rx_pause_duration_seconds |Counter |Inbound pause duration. This metric generally indicates network congestion. It represents PFC packets received by the NIC as the sender. It means the receiver is severely congested and requires the NIC to stop sending. |
||rdma_exporter_pod_infiniband_tx_pause_duration_seconds |Counter |Outbound pause duration. This metric generally indicates a host anomaly, where the NIC sends PFC packets. It means the NIC (as the receiver) is severely congested and requires the sender to stop sending. |
||rdma_exporter_pod_infiniband_rx_pause_total |Counter |Number of PFC pause packets received in the inbound direction. Currently, priority 5 is used. |
||rdma_exporter_pod_infiniband_tx_pause_total |Counter |Number of PFC pause packets sent in the outbound direction. |

Some rdma\-device\-plugin metrics have custom labels, which can be used to filter and query metrics. The commonly used metric labels are described in the following table.

|Label name |Description |
|---|---|
|Pod |The ID of the pod using the RDMA device, for example, `pcji9mk1***`. |
|Namespace |The namespace where the pod using the RDMA device is located. |
|RdmaMode |RDMA network mode. The available values are:<br><br><br>* **exclusive**: exclusive mode.<br><br>* **shared**: shared mode. |
|Container |The name of the container using the RDMA device. |
|Device |The name of the RDMA network device, for example, `mlx5_1`. |

> **tip**

> General Prometheus labels, such as `cluster` and `instance`, are not described here.

### node\-exporter monitoring

For the list of RDMA metrics collected by node\-exporter, see [this documentation](https://github.com/prometheus/node_exporter/blob/master/collector/infiniband_linux.go). You can query these metrics in Explore using the `node_infiniband_` prefix.

## View metrics

* You can use the Explore feature of VMP to quickly query and display metric data. For details, see [Querying metrics](https://docs.byteplus.com/en/docs/vmp/explore-metrics).

## Recommendations for GPU monitoring and alerts

When configuring GPU monitoring and alerts in your cluster, we recommend paying additional attention to the following issues:

* After enabling XID health checks in the nvidia\-device\-plugin, you may not be aware of GPUs being automatically isolated due to XID errors. To avoid this, we recommend configuring GPU XID monitoring and alerting policies to help you identify potential risks early. For more details, see [[Product announcement] The XID error isolation feature is disabled for the nvidia-device-plugin add-on](https://docs.byteplus.com/en/docs/vke/Product_Announcement_The_nvidia-device-plugin_add-on_disables_XID_exception_isolation).

* An nvidia\-device\-plugin exception may cause GPU resources to be reported as 0 on a node. This can make GPU, RDMA, or other resources unschedulable. To avoid this, we recommend configuring monitoring and alerting policies for this issue to help you identify potential risks early. For more details, see [[Product announcement] VKE add-on optimization - addressing resource reporting exceptions in the Kubernetes Device Plugin framework](https://docs.byteplus.com/en/docs/vke/Product-announcement_VKE_add-on_optimization).

### Monitoring

After enabling GPU observability, you can use PromQL statements to query related metrics in the VMP console. For details, see [Querying metrics](https://docs.byteplus.com/en/docs/vmp/explore-metrics).

1. Log in to the [VMP console](https://console.byteplus.com/prometheus).

2. In the left navigation bar, click **Explore** to go to the Explore page.

3. In the upper\-right corner of the page, specify the **workspace**, **time range**, and **data refresh method** for metric query.

4. Use the following PromQL statements to query related metrics.

   * Query metrics related to GPU XID health check.

      **Method 1: Query metrics related to ECS GPU resources being unschedulable.**

```JSON
      kube_node_status_capacity{node!~"vci.*", resource=~"nvidia_com_gpu|vke_volcengine_com_mgpu_core"} - kube_node_status_allocatable{node!~"vci.*", resource=~"nvidia_com_gpu|vke_volcengine_com_mgpu_core"} > 0
      ```

      **Method 2: Query metrics related to GPU XID errors.**

```JSON
      DCGM_EXP_XID_ERRORS_COUNT{node!~"vci.*"} > 0
      ```

   * Query metrics related to GPU resources reported as 0.

      ```JSON
      kube_node_status_capacity{node!~"vci.*", resource=~"nvidia_com_gpu|vke_volcengine_com_mgpu_core|vke_volcengine_com_mgpu_memory"} == 0
      ```

### Alerting

After enabling GPU observability, you can configure related alerts in the VMP console. For details, see [Creating alert rules](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rules).

1. In the left navigation bar, click **Alert Center** \> **Alert rule**.

2. On the **Alert rule** page, select **Create** \> **Create manually**. Then, configure alerts related to GPU XID health check and GPU resources reported as 0 according to the above observability metrics. For detailed configuration instructions, see [Creating alert rules](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rules).
