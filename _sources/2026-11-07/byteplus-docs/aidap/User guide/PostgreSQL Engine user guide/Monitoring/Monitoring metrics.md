---
title: "Monitoring metrics"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Monitoring_metrics"
---

This topic introduces the monitoring items and related information provided by the AI Native Database Platform for Workspaces using the PostgreSQL engine.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/cloudmonitor/GetMetricData">GetMetricData </a>API to query monitoring metrics and alarm information. When calling this API, you need to provide the product namespace, the subnamespace of the metrics to be queried, and the metricName. The Namespace of the Workspace using the PostgreSQL engine in the AI Native Database Platform is VCM_Sinlar_PostgreSQL. The MetricName and SubNamespace of each metric are listed in the monitoring items below.</div>



|**Name** |**Metricname** |**Subnamespace** |**Unit** |**Description** |**Dimension** |**Usage** |
|---|---|---|---|---|---|---|
|Compute consumption |BranchComputeDesiredCU |branch_compute_monitor |Count |Real\-time compute consumption of all branches in the workspace |Resource monitor |Alarm |
|CPU utilization |BranchComputeCPUPercent |branch_compute_monitor |Percent |CPU usage of compute |Resource monitor |Monitoring, alarm |
|Memory utilization |BranchComputeMemoryPercent |branch_compute_monitor |Percent |Compute memory usage rate. |Resource monitor |Monitoring, alarm |
|Actual CPU usage |BranchComputeCPUUsed |branch_compute_monitor |Count |Actual CPU usage of compute. |Resource monitor |Monitoring, alarms |
|Total memory application |BranchComputeHostMemoryTotalByte |branch_compute_monitor |Bytes(IEC) |Total memory application requested by branch compute. |Resource monitor |Monitoring, alarms |
|Actual memory usage |BranchComputeHostMemoryUsedByte |branch_compute_monitor |Count |Actual memory usage of compute. |Resource monitor |Monitoring, alarms |
|Number of inserted rows in the database |BranchComputeInsertRows |branch_compute_monitor |Count |Number of inserted rows in compute. |Resource monitor |Monitoring, alarm |
|Number of updated rows in the database |BranchComputeUpdateRows |branch_compute_monitor |Count |Number of updated rows in compute. |Resource monitor |Monitoring, alarms |
|Number of deleted rows in the database |BranchComputedeleteRows |branch_compute_monitor |Count |Number of deleted rows of compute. |Resource monitor |Monitoring, alarms |
|QPS |QPS |branch_compute_monitor |Count |Total compute QPS. |Resource monitor |Monitoring, alarms |
|Number of idle database connections |BranchComputeIdleConnections |branch_compute_monitor |Count |Number of idle compute connections. |Resource monitor |Monitoring, alarms |
|Number of active database connections |BranchComputeActiveConnections |branch_compute_monitor |Count |Number of active compute connections. |Resource monitor |Monitoring, alarms |
|Total connections in the database |BranchComputeTotalConnections |branch_compute_monitor |Count |Total connections in compute. |Resource monitor |Monitoring, alarms |
|Transaction success rate |BranchComputeTransactionSuccessRate |branch_compute_monitor |Percent |Compute transaction success rate. |Resource monitor |Monitoring, alarms |
|Average request time consumption |AverageRequestLatency |branch_compute_monitor |Millisecond |Average request time consumption of compute. |Resource monitor |Monitoring, alarms |
|P99 request time consumption |P99RequestLatency |branch_compute_monitor |Millisecond |P99 request time consumption of compute. |Resource monitor |Monitoring, alarms |
|P95 request time consumption |P95RequestLatency |branch_compute_monitor |Millisecond |P95 request time consumption of compute. |Resource monitor |Monitoring, alarms |
|P50 request time consumption |P50RequestLatency |branch_compute_monitor |Millisecond |P50 request time consumption of compute. |Resource monitor |Monitoring, alarm |
|Number of transaction rollbacks |BranchComputeTransactionRollbackCount |branch_compute_monitor |Count |Number of transaction rollbacks in compute. |Resource monitor |Monitoring, alarms |
