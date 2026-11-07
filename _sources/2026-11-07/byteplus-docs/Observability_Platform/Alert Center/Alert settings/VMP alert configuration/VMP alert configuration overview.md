---
title: "VMP alert configuration overview"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/VMP_alert_configuration_overview"
---

VMP alert configuration includes four key configurations: query statement, alert resource, notification policy, and aggregation policy, as well as other configurations such as project. These configurations together form a complete VMP alert rule, which defines which objects to monitor, which metrics to monitor, what conditions trigger an alert, whom to notify after an alert is triggered, and how to send the notification.

<span id="FWqP97MR"></span>
## Glossary


* **Query statement**: A PromQL (Prometheus Query Language) expression. PromQL is the standard query language used to retrieve and calculate monitoring metrics from a time series database. Examples include up == 0 (an instance crashes) and rate(http_requests_total[5m]) \> 1000 (the request rate is too high). In an alert rule, the query statement defines the anomaly determination logic. The query statement determines the alert monitor object and the alert evaluation.

* **Alert resource**: Specifies the instance actually monitored in an alert rule. The alert resource determines the effective scope and coverage of the alert. In VMP, you select alert resources by specifying a workspace.

* **Notification policy**: Specifies the methods, channels, contacts, and display format for alert content for receiving notifications when alerts of different severity levels are triggered or resolved.

* **Aggregation policy**: Primarily used to configure the aggregation cycle for alerts. The aggregation policy groups a batch of alerts for notification, preventing a large number of alert messages from being generated in a short period when alerts are triggered frequently.


<span id="xUQP0BNC"></span>
## Resource relationships

Alert templates and preset alert templates contain only partial alert configurations. These resources not only consolidate scattered alert settings into reusable standards but also enable quick batch creation of alert rules, reuse of best practices, and improved configuration efficiency. The key alert configuration differences across various resources are as follows:


|Key settings |Alert rules |Preset alert templates |Alert templates |
|---|---|---|---|
|Query statement |✅ |✅ |✅ |
|Alert resource |✅ |❌ |❌ |
|Notification policy |✅ |❌ |❌ |
|Aggregation policies |✅ |❌ |❌ |


<span id="rF20hBRd"></span>
## Alert rule creation methods

VMP provides multiple methods for creating alert rules. You can select the method that best suits your scenario.


* **Custom creation of alert rules**: If you want to customize alert rules for your scenarios or have only a small number of alert rules, we recommend that you create alert rules manually. Manual creation does not reduce usage efficiency and allows fine\-grained adjustment of alert configurations. For procedure and configuration details, see Method 1 in [Creating VMP alert rules](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_VMP_alert_rules).

* **Use preset alert templates**: If you lack established experience in alert configuration and want to set up an alert monitoring system quickly, we recommend directly using the standardized alert templates officially provided for rapid implementation. When you apply a preset alert template, configure the alert resource, notification policy, and aggregation policy to complete all configurations for an alert rule. You can then quickly create alert rules based on the preset alert template. For procedure and configuration details, see [Creating VMP alert rule groups](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_VMP_alert_rule_groups).

* **Use custom alert templates**: If you already have established experience in alert configuration and want to reuse configurations within the same region while reducing duplicate creation of alert rules, we recommend following the steps below to create and apply alert templates, standardizing and operationalizing the relevant experience.

   1. [Create VMP alert templates](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_VMP_alert_templates): Create alert templates based on accumulated experience to consolidate configurations such as query statements and rules into templates for quick reuse.

   2. [Create VMP alert rule groups](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_VMP_alert_rule_groups): You can complete all configurations for an alert rule by applying a custom alert template and then configuring the alert resource, notification policy, and aggregation policy.

* **Import/export alert rules via JSON**: If suitable alert rules exist in other projects and you wish to batch copy alert rules across accounts, regions, projects, or workspaces, we recommend using the import/export feature to export VMP alert rules from other workspaces and import them into the current project. For procedure and configuration details, see Method 2 in [Creating VMP alert rules](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_VMP_alert_rules).


<span id="XCTlGNi2"></span>
## Common alerts

<span id="c1z4g7Kf"></span>
### Common alerts for Kubernetes


|**Alert type** |**Monitoring object** |**Metric source** |**Monitoring purpose** |**Typical PromQL** |
|---|---|---|---|---|
|Pod/Container |Pod/Container |kube\-state\-metrics |This alert is triggered when a container remains in the CrashLoopBackOff state for the last 5 minutes. This identifies repeated startup failures or ongoing crashes. |```Plain Text```<br>```max_over_time(kube_pod_container_status_waiting_reason{reason="CrashLoopBackOff"}[5m]) >= 1```<br> |
|Pod/Container |Pod |kube\-state\-metrics<br><br> |This alert is triggered when a Pod remains in the Pending or Unknown state and the Pod is not part of a Job. This indicates that the Pod is not ready. |```Plain Text```<br>```sum by (namespace, pod, cluster) (```<br>```  max by (namespace, pod, job, cluster) (```<br>```    kube_pod_status_phase{phase=~"Pending\|Unknown"}```<br>```  ) * on (namespace, pod, cluster) group_left() topk by (namespace, pod, cluster) (```<br>```    1, max by (namespace, pod, owner_kind, cluster) (kube_pod_owner{owner_kind!="Job"})```<br>```  )```<br>```) > 0```<br> |
|Pod/Container |Container |kube\-state\-metrics |This alert is triggered when a container remains in the Waiting state for a long period due to a reason other than CrashLoopBackOff. This indicates issues with image pulling, creation, or dependency initialization. |```Plain Text```<br>```kube_pod_container_status_waiting_reason{reason!="CrashLoopBackOff"} > 0```<br> |
|Workload rollout |Deployment |kube\-state\-metrics |This alert is triggered when the desired number of replicas for a Deployment exceeds that of available replicas, and the number of updated replicas remains unchanged for 10 minutes. This indicates that the rollout is stuck or replicas are unavailable for a long period. |```Plain Text```<br>```(```<br>```  kube_deployment_spec_replicas > kube_deployment_status_replicas_available```<br>```) and (```<br>```  changes(kube_deployment_status_replicas_updated[10m]) == 0```<br>```)```<br> |
|Workload rollout |Deployment |kube\-state\-metrics |This alert is triggered when the Progressing condition of a Deployment is false. This indicates that the rolling update is not progressing as expected. |```Plain Text```<br>```kube_deployment_status_condition{condition="Progressing", status="false"} != 0```<br> |
|Workload rollout |StatefulSet |kube\-state\-metrics |This alert is triggered when the current and updated revisions of a StatefulSet differ, updated replicas are not fully ready, and no progress is made for 5 minutes. This indicates that the StatefulSet update is stuck. |```Plain Text```<br>```(```<br>```  max by (namespace, statefulset, job, cluster) (```<br>```    kube_statefulset_status_current_revision unless kube_statefulset_status_update_revision```<br>```  ) * on (namespace, statefulset, job, cluster)```<br>```  (kube_statefulset_replicas != kube_statefulset_status_replicas_updated)```<br>```) and on (namespace, statefulset, job, cluster) (```<br>```  changes(kube_statefulset_status_replicas_updated[5m]) == 0```<br>```)```<br> |
|Workload rollout |DaemonSet |kube\-state\-metrics |This alert is triggered when the number of scheduled, updated, available, or mis\-scheduled replicas for a DaemonSet is abnormal, and no progress is made within 5 minutes. This identifies that the DaemonSet is not covering nodes as expected. |```Plain Text```<br>```(```<br>```  (kube_daemonset_status_current_number_scheduled != kube_daemonset_status_desired_number_scheduled)```<br>```  or (kube_daemonset_status_number_misscheduled != 0)```<br>```  or (kube_daemonset_status_updated_number_scheduled != kube_daemonset_status_desired_number_scheduled)```<br>```  or (kube_daemonset_status_number_available != kube_daemonset_status_desired_number_scheduled)```<br>```) and (```<br>```  changes(kube_daemonset_status_updated_number_scheduled[5m]) == 0```<br>```)```<br> |
|Autoscaling |HPA |kube\-state\-metrics |This alert is triggered when the desired number of replicas for an HPA differs from the current number of replicas, and the current number remains unchanged within the range between the minimum number and the maximum number for 15 minutes. This indicates that scaling does not take effect.<br><br> |```Plain Text```<br>```(kube_horizontalpodautoscaler_status_desired_replicas != kube_horizontalpodautoscaler_status_current_replicas)```<br>```and (kube_horizontalpodautoscaler_status_current_replicas > kube_horizontalpodautoscaler_spec_min_replicas)```<br>```and (kube_horizontalpodautoscaler_status_current_replicas < kube_horizontalpodautoscaler_spec_max_replicas)```<br>```and changes(kube_horizontalpodautoscaler_status_current_replicas[15m]) == 0```<br> |
|Autoscaling |HPA |kube\-state\-metrics |This alert is triggered when the current number of replicas for an HPA equals the maximum number of replicas, and the maximum number is not equal to the minimum number. This indicates that the autoscaling policy has reached its upper limit.<br><br> |```Plain Text```<br>```(```<br>```  kube_horizontalpodautoscaler_status_current_replicas == kube_horizontalpodautoscaler_spec_max_replicas```<br>```) and on (namespace, horizontalpodautoscaler, cluster) (```<br>```  kube_horizontalpodautoscaler_spec_max_replicas != kube_horizontalpodautoscaler_spec_min_replicas```<br>```)```<br> |
|Scheduling/Maintainability |PDB |kube\-state\-metrics |This alert is triggered when the desired number of healthy replicas for a PDB exceeds the current number of healthy replicas. This indicates insufficient replicas for secure evictions. |```Plain Text```<br>```(```<br>```  kube_poddisruptionbudget_status_desired_healthy - kube_poddisruptionbudget_status_current_healthy```<br>```) > 0```<br> |
|Node resource |Node |node\-exporter |This alert is triggered when the average node CPU utilization (excluding idle and iowait) exceeds 90 percent. This indicates a sustained high CPU load on the node. |```Plain Text```<br>```sum without(mode) (avg without (cpu) (rate(node_cpu_seconds_total{mode!~"idle\|iowait"}[2m]))) * 100 > 90```<br> |
|Node resource |Node |node\-exporter |This alert is triggered when the node memory utilization exceeds 90 percent. This indicates imminent exhaustion of available memory on the node.<br><br> |```Plain Text```<br>```100 - (node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes * 100) > 90```<br> |
|Node resource |Node filesystem |node\-exporter |This alert is triggered when available filesystem space drops below 15 percent, and it is predicted that the space will be exhausted within 24 hours based on the trend over the last 6 hours, while the filesystem is not read‑only. This provides an early warning of a disk space shortage. |```Plain Text```<br>```(```<br>```  node_filesystem_avail_bytes{mountpoint!=""} / node_filesystem_size_bytes{mountpoint!=""} * 100 < 15```<br>```and```<br>```  predict_linear(node_filesystem_avail_bytes{mountpoint!=""}[6h], 24*60*60) < 0```<br>```and```<br>```  node_filesystem_readonly{mountpoint!=""} == 0```<br>```)```<br> |
|Node resource |Node filesystem |node\-exporter |This alert is triggered when available filesystem space falls below 5 percent, and the filesystem is not read‑only. This indicates imminent exhaustion of disk space. |```Plain Text```<br>```(```<br>```  node_filesystem_avail_bytes{mountpoint!=""} / node_filesystem_size_bytes{mountpoint!=""} * 100 < 5```<br>```and```<br>```  node_filesystem_readonly{mountpoint!=""} == 0```<br>```)```<br> |
|Node resource |Node filesystem |node\-exporter |This alert is triggered when the remaining filesystem inode percentage drops below 40 percent, and it is predicted that inodes will be exhausted within 24 hours based on the trend in the last 6 hours, while the filesystem is not read‑only. This provides early warning of an inode shortage. |```Plain Text```<br>```(```<br>```  node_filesystem_files_free{mountpoint!=""} / node_filesystem_files{mountpoint!=""} * 100 < 40```<br>```and```<br>```  predict_linear(node_filesystem_files_free{mountpoint!=""}[6h], 24*60*60) < 0```<br>```and```<br>```  node_filesystem_readonly{mountpoint!=""} == 0```<br>```)```<br> |
|Node resource |Node disk |node\-exporter |This alert is triggered when the weighted I/O time rate of block devices persistently exceeds a threshold. This indicates disk I/O queue congestion or storage layer saturation. |```Plain Text```<br>```rate(node_disk_io_time_weighted_seconds_total[5m]) > 10```<br> |
|Node network |Node network |node\-exporter |This alert is triggered when the ratio of received error packets to total received packets exceeds 1 percent. This indicates errors on the network receiving path of nodes. |```Plain Text```<br>```rate(node_network_receive_errs_total[2m]) / rate(node_network_receive_packets_total[2m]) > 0.01```<br> |
|Node network |Node network |node\-exporter |This alert is triggered when the ratio of transmitted error packets to total transmitted packets exceeds 1 percent. This indicates errors on the network transmission path of nodes. |```Plain Text```<br>```rate(node_network_transmit_errs_total[2m]) / rate(node_network_transmit_packets_total[2m]) > 0.01```<br> |
|Control plane |Kubernetes component |kube\-apiserver/kubernetes_build_info |This alert is triggered when the number of major and minor versions of Kubernetes add\-ons in a cluster exceeds 1. This indicates version inconsistency among control plane add\-ons. |```Plain Text```<br>```count by (cluster) (```<br>```  count by (git_version, cluster) (```<br>```    label_replace(kubernetes_build_info{job!~"kube-dns\|coredns"},"git_version","$1","git_version","(v[0-9]*.[0-9]*).*")```<br>```  )```<br>```) > 1```<br> |
|Control plane |API server client |kube\-apiserver/rest_client_requests_total |This alert is triggered when the ratio of 5xx error requests to total requests from clients accessing the API Server exceeds 1 percent. This indicates control plane access exceptions or dependency failures. |```Plain Text```<br>```(sum(rate(rest_client_requests_total{code=~"5.."}[5m])) by (cluster, instance, job, namespace)```<br>```/```<br>```sum(rate(rest_client_requests_total[5m])) by (cluster, instance, job, namespace)) > 0.01```<br> |


<span id="6exjq9e6"></span>
### Common alerts for etcd


|**Category** |**Common alerts** |**Metric source** |**Description** |**Typical PromQL** |
|---|---|---|---|---|
|Availability |EtcdNoLeader |etcd native metrics |This indicates that etcd has lost its leader. This is a fundamental control‑plane availability indicator. |```Plain Text```<br>```etcd_server_has_leader == 0```<br> |
|Performance |EtcdHighFsyncDurations |etcd native metrics |This indicates increased WAL fsync latencies. This typically indicates disk write jitters or storage performance degradation. |```Plain Text```<br>```histogram_quantile(0.99, sum(rate(etcd_disk_wal_fsync_duration_seconds_bucket[5m])) by (le)) > 0.5```<br> |
|Capacity |EtcdBackendQuotaLowSpace |etcd native metrics |This indicates that the backend space approaches the upper limit. This prevents impacts on control plane stability. |```Plain Text```<br>```(etcd_mvcc_db_total_size_in_bytes / etcd_server_quota_backend_bytes) > 0.95```<br> |
|Write failure |EtcdProposalFailures/EtcdProposalsPendingHigh |etcd native metrics |This indicates proposal failures or backlogs. This helps discover write failures, slow consensus processing, or internal blocking. |```Plain Text```<br>```rate(etcd_server_proposals_failed_total[5m]) > 0 or etcd_server_proposals_pending > 0```<br> |


<span id="CuC5m3MV"></span>
## Rule recommendations


|**Item** |**Recommended practice** |
|---|---|
|Alert level |We recommend configuring alerts with severity levels P0, P1, or P2 to distinguish between trends and critical failures. |
|Condition duration |We recommend setting a "for" condition duration for most alert rules to reduce false positives caused by transient jitters. |
|Namespace filtering |We recommend excluding test environments, temporary tasks, and short‑lived objects to reduce noise. |
|Tag specification |We recommend consistently adding tags such as cluster, namespace, and pod to improve routing and troubleshooting efficiency. |
|Metric availability confirmation |We recommend confirming whether the corresponding metric already exists on the VMP Explore page before you configure an alert rule. If the metric is not found, evaluate and supplement the collection configuration on the source side to prevent the alert rule from being invalid. |
