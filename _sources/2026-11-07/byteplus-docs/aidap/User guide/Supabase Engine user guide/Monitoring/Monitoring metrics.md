---
title: "Monitoring metrics"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Monitoring_metrics"
---

This topic introduces monitoring metrics and related information provided by the AI Native Database Platform for workspaces using the Supabase Engine.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/cloudmonitor/GetMetricData">GetMetricData </a>API to query monitoring metrics and alarm information. When calling this API, you need to provide the product namespace, the subnamespace of the metrics to be queried, and the metricName. The namespace of the workspace using the PostgreSQL engine in the AI Native Database Platform is VCM_Sinlar_Supabase. The metricName and subnamespace of each metric are listed in the monitoring items below.</div>



|**Name** |**Metricname**<br><br> |**Subnamespace** |**Unit** |**Description** |**Dimension** |**Usage** |
|---|---|---|---|---|---|---|
|Actual CPU usage rate of Supabase |BranchCpuPecent |branch_monitor |Percent |CPU usage rate of the branch Supabase service. |Resource monitor |Monitoring, alarms |
|Supabase memory usage rate |BranchMemoryPecent |branch_monitor |Percent |Memory usage rate of the branch Supabase service. |Resource monitor |Monitoring, alarms |
|Actual CPU usage of the database |BranchComputeCPUUsed |branch_monitor |Count |Total CPU application requested by the branch compute. |Resource monitor |Monitoring, alarms |
|Total memory application of the database |BranchComputeHostMemoryTotalByte |branch_monitor |Bytes(IEC) |Total memory application requested by branch compute. |Resource monitor |Monitoring, alarms |
|Actual memory usage of the database |BranchComputeHostMemoryUsedByte |branch_monitor |Bytes(IEC) |Actual memory usage of branch compute |Resource monitor |Monitoring, alarms |


&nbsp;
