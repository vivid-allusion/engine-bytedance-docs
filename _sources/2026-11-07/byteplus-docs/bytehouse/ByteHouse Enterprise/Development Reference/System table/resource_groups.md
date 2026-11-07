---
title: "resource_groups"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/resource_groups"
---

After the resource group feature is enabled, this table displays the configuration details, resource usage status, and operational metrics for all resource groups in the current system, helping administrators monitor and adjust resource allocation strategies.

<span id="043c94d0"></span>
## Column name


|Field name |Data types |Field meanings |
|---|---|---|
|name |String |Resource group name, a unique identifier within the system, used to distinguish different resource groups. |
|enable |UInt8 |Status indicator showing whether the resource group is enabled. 1 indicates that the resource group is enabled, allowing it to allocate resources and receive queries. 0 indicates that the resource group is disabled, so it does not participate in resource allocation, and queries matching this resource group cannot use its configured resources. |
|can_run_more |UInt8 |Flag indicating whether new queries can currently be executed in the resource group. 1 indicates that the current number of concurrent queries has not reached the maximum limit, and new queries can be executed. 0 indicates that the concurrency limit has been exceeded, so no new queries can be executed; you must wait for existing queries to finish or enter the waiting queue if it is not full. |
|can_queue_more |UInt8 |Indicator of whether the resource group waiting queue can accept new queries. 1 indicates that the waiting queue is not full and additional waiting queries can be added; 0 indicates that the waiting queue is full, and any subsequent queries matching this resource group will immediately result in an error and cannot enter the queue. |
|soft_max_memory_usage |UInt64 |The maximum memory available to this resource group on a single machine, measured in bytes. The default value is 0, which means there is no limit on memory usage. If a specific value is set, when the memory usage of the resource group on a single machine approaches or exceeds this value, memory over\-limit protection may be triggered, such as restricting the execution of new queries. |
|cached_memory_usage |UInt64 |The amount of cache memory currently used by this resource group, in bytes. When `cached_memory_usage` approaches or exceeds `soft_max_memory_usage`, it means that the resource group's memory usage on a single machine has already exceeded the limit, which may affect the execution efficiency of new queries or trigger resource restrictions. |
|initial_query_only |UInt8 |Whether only the initial query—typically referring to the core query triggered during system startup or resource group initialization—is permitted to use the identifier of this resource group. '1' indicates that only initial queries are permitted; non\-initial queries will be rejected. '0' indicates no restrictions, and all queries matching the resource group can use its resources. |
|max_concurrent_queries |UInt64 |Maximum number of concurrent queries allowed by a resource group (concurrent query limit). The default value is 0, which means there is no limit on the number of concurrent queries. If a specific value is set, when `running_queries` reaches this value, new queries cannot be executed directly and must either enter the waiting queue (if the queue is not full) or an error will be reported. |
|running_queries |UInt64 |The number of queries currently being executed in the resource group reflects the query execution load of the resource group in real time. If this value approaches or equals `max_concurrent_queries`, it indicates that the execution resources of the resource group are nearly saturated. |
|max_queued |UInt64 |The maximum number of queries that match resource groups that can enter the waiting queue (queue capacity limit). Setting the value to 0 means there is no limit on the queue size (theoretically, queries can wait indefinitely). If a specific value is set, when `queued_queries` reaches that value, any subsequent new queries will immediately return an error and will not be added to the queue. The default value is 0. |
|queued_queries |UInt64 |The resource group is currently in the waiting queue, with a number of queries waiting for resource release execution. If this value approaches or equals `max_queued`, it indicates that the waiting queue is nearly full and new queries may be at risk of encountering errors. |
|priority |UInt32 |The priority level of a resource group, used to determine the order of resource allocation when multiple resource groups compete for idle system resources. The larger the value, the higher the priority. When the system has idle resources such as CPU and memory, resource groups with higher priority will be the first to receive supplementary resources. |
|cpu_shares |UInt64 |The CPU share occupied by the resource group in cgroups (Linux control groups) using the soft isolation mechanism. The default value is 0, which means cgroups CPU isolation is not used. If users want to increase overall CPU utilization by allowing a resource group to use idle CPU from other resource groups, and can accept some deviation in isolation effectiveness (for example, when a share ratio of 1:4 is configured, actual CPU usage may fall back to 1:2), they can set the share ratio using this parameter (for example, 1024, 2048, and so on, where the ratio corresponds to the share value ratio). |
|max_cpu_cores |Int64 |The maximum number of CPU cores that a resource group can use (hard limit). The default value is \-1, which means there is no limit on CPU core usage. If a specific positive integer is set, for example, 12, the resource group's CPU usage will never exceed the specified number of CPU cores, ensuring that other resource groups' CPU resources are not excessively used. |
|cpu_set_cpus |String |Specify the CPU core numbers that this resource group will be bound to in order to configure CPU affinity. By default, an empty string indicates that no specific CPU core is bound. The configurable format is a range of core numbers (for example, "0\-3" binds to CPU cores 0 through 3). After binding, queries for the resource group are executed only on the specified cores, reducing CPU context switching overhead. |
|hardware_cpu_cores |UInt64 |The total number of physical CPU cores available to the current resource group reflects the underlying CPU hardware resources of the group. This value is automatically calculated by the system based on resource group configuration (such as `cpu_set_cpus`) and node hardware specifications, and serves as the fundamental reference for CPU resource allocation within the resource group. |
|cpu_cfs_period_us |UInt64 |Adjust the period duration of the CPU CFS (Completely Fair Scheduler) in cgroups. The unit is microseconds (μs), and the default value is 100000 (that is, 0.1 seconds). This parameter controls the scheduling period for CPU resources. Used together with `cpu_cfs_quota_us` (which is typically calculated automatically by the system), it enables CPU usage limits. The shorter the period, the finer the scheduling granularity. |
|parent_resource_group |String |The name of the parent resource group is used to enable hierarchical management of resource groups. For example, the parent resource group allocates total resources, and the child resource group is allocated a portion of resources from the parent resource group. If the value is an empty string, this resource group is a top\-level resource group with no parent resource group and directly obtains resources from the system. |
|cpu_average_usage_1 |Double |The average CPU usage of the resource group over the past minute, typically measured in number of CPU cores (for example, 0.5 indicates an average usage of 0.5 CPU cores), provides a real\-time reflection of the recent CPU load of the resource group. |
|cpu_average_usage_5 |Double |The average CPU usage of the resource group over the past 5 minutes, with the unit being "number of cores", provides a better indication of the resource group's mid\-term CPU load trends compared to the 1\-minute average, reducing the impact of short\-term fluctuations. |
|cpu_average_usage_10 |Double |The average CPU usage rate of the resource group over the past 10 minutes, measured in number of cores, indicates the long\-term trend of CPU load for the resource group. This metric is suitable for determining whether the CPU resource allocation for the resource group is reasonable; for example, if the usage rate remains high over time, scaling up may be required. |
|max_disk_read_bandwidth |Int64 |The resource group imposes a limit on the maximum read rate for local disks (only traffic that bypasses the PageCache is counted, that is, data read directly from the disk rather than from the memory cache). The unit is typically bytes per second (Byte/s). The default is \-1, which means the disk read rate is not limited. If a specific value is set, the disk read rate will be rate\-limited when it exceeds that value. |
|max_disk_write_bandwidth |Int64 |The maximum write rate to local disks for a resource group is a configurable metric that only accounts for data bypassing the PageCache—that is, data written directly to disk rather than to the memory cache. The unit is typically bytes per second (Byte/s). The default value of \-1 indicates that the disk write rate is not limited. If a specific value is set, the disk write rate will be throttled when it exceeds the specified value. |
|cpu_isolation_effect |UInt8 |Status indicator for CPU isolation effectiveness, used to determine whether CPU isolation is effective for a resource group. 1 indicates that CPU isolation has taken effect (for example, the `cpu_shares` or `max_cpu_cores` configuration has taken effect); 0 indicates that CPU isolation has not taken effect (which may be due to configuration errors or system limitations). |
|exception |String |Description of exception information for the resource group. If the resource group encounters issues such as configuration errors, resource allocation failures, anomalies in the isolation mechanism, and other issues, this field records the specific cause of the exception. If the resource group is operating normally, this field is an empty string. |
|customized_settings |Map/String |Custom configuration items added by users when creating a resource group are stored as key\-value pairs. For example, users can customize non\-default parameters such as "query_timeout" (query timeout period), "memory_overcommit_ratio" (memory overcommit ratio), and more. If a parameter is left empty, it indicates that no custom setting has been configured. |


<span id="762ce61b"></span>
## Example

```SQL
SELECT * FROM system.resource_groups LIMIT 1
```


```SQL
Row 1:
──────
name:                     doc_demo
enable:                   1
can_run_more:             1
can_queue_more:           1
soft_max_memory_usage:    51539607552 -- 51.54 billion
cached_memory_usage:      0
initial_query_only:       0
max_concurrent_queries:   50
running_queries:          0
max_queued:               50
queued_queries:           0
priority:                 0
cpu_shares:               0
max_cpu_cores:            12
cpu_set_cpus:
hardware_cpu_cores:       16
cpu_cfs_period_us:        100000
parent_resource_group:
cpu_average_usage_1:      0
cpu_average_usage_5:      0.000002
cpu_average_usage_10:     0.000001
max_disk_read_bandwidth:  -1
max_disk_write_bandwidth: -1
cpu_isolation_effect:     1
exception:
customized_settings:      {}
```
