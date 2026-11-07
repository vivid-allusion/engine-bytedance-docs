---
title: "Monitoring alerts"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/ce-monitoring-alerts"
---

<span id="c1be7407"></span>
# Monitoring metrics

The ByteHouse Enterprise Edition monitoring alert feature provides multiple types of monitoring for clusters and nodes, including operating system load, ByteHouse load, query load, data import, and Zookeeper.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To facilitate display, monitoring alert charts automatically adjust units according to data volume, with the actual display prevailing. For example, when replication latency is high, the unit changes from μs to ms; when latency is even higher, the unit changes from ms to s.</div>


* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/cloudmonitor/GetMetricData">GetMetricData</a> API to query monitoring metric data and alert information. When calling this query API, you need to obtain the product's Namespace, the SubNamespace of the metrics to query, and the MetricName of the metrics to query. The Namespace for ByteHouse Enterprise Edition is <strong>VCM_ByteHouse_Ce</strong>. The MetricName and SubNamespace of each metric are shown in the table below.</div>


* <div data-tips="true" data-tips-type="tip">You can also get detailed information about each monitoring metric at <a href="https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_ByteHouse_Ce&tabKey=metric">ByteHouse Enterprise Edition Monitoring Metric Query</a>.</div>


* <div data-tips="true" data-tips-type="tip">You can also use the SDK to query monitoring metric data. For details, please refer to <a href="https://docs.byteplus.com/docs/bytehouse/ce-use-sdk-to-query-bytehouse-monitoring-data">Use SDK to query ByteHouse monitoring data</a>.</div>




|**Category** |Metric name |MetricName |SubNamespace |Metric dimension |Metric unit |Metric purpose |
|---|---|---|---|---|---|---|
|Node ByteHouse load |Number of parts |parts |Clickhouse |Node, ResourceID, ENI (optional) |Count |alert, consumption |
|node ByteHouse load |number of MergeTree tables |MergeTreeTableNum |Clickhouse |ResourceID, Node, ENI (optional) |Count |alert, consumption |
|node ByteHouse load |number of kafka tables |KafkaTableNum |Clickhouse |ResourceID, Node, ENI (optional) |Count |Alert, consumption |
|Node ByteHouse load |Maximum primary\-secondary sync delay table count |HaQueueCount |Clickhouse |ResourceID, Node, ENI (optional) |Count |alert, consume |
|Node ByteHouse load |Number of distributed table files pending to send |ClickHouseMetrics_DistributedFilesToInsert |Clickhouse |ResourceID, Node, ENI (optional) |Count |alert, consume |
|Node ByteHouse load |Broken Tables Count |Broken_tables |Clickhouse |Node, ResourceID, ENI (optional) |Count |Alert, Consumption |
|Node ByteHouse Load |Merge Memory Usage |ClickHouseMetrics_MergeMemoryUsage |Clickhouse |Node, ResourceID, ENI (optional) |Bytes(IEC) |alert, consumption |
|Node ByteHouse load |Merge task count |ClickHouseProfileEvents_Merge |Clickhouse |ResourceID, Node, ENI (optional) |Count/Second |alert, consumption |
|Node ByteHouse load |Unique table index memory usage |ClickHouseMetrics_UniqueIndexMemoryUsage |Clickhouse |Node, ResourceID, ENI (optional) |Bytes(IEC) |Alert, consumption |
|Node ByteHouse load |Map keys count |ClickHouseMetricsMapKeyCount |Clickhouse |Node, ResourceID, ENI (optional) |Count |Alerts, Consumption |
|Node ByteHouse Load |Number of Active Parts |ActiveParts |Clickhouse |ResourceID, Node, ENI (optional) |Count |alert |
|node ByteHouse load |concurrent count (including subquery) |ClickHouseMetrics_Process_Count |Clickhouse |ResourceID,ENI,Node |Count |alert, running query count including subqueries |
|node ByteHouse load |mutation count |ClickHouseMetrics_mutations_count |Clickhouse |ResourceID,ENI,Node |Count |Alert: number of mutations currently executing |
|Node ByteHouse load |Longest mutation execution time |ClickHouseMetrics_mutations_max_execution_time |Clickhouse |ResourceID,ENI,Node |Second |Alarm |
|ByteHouse cluster load |Number of parts |ClusterParts |ClusterClickhouse |ResourceID |Count |Alarm, consumption |
|ByteHouse cluster load |Number of MergeTree tables |ClusterMergeTreeTableNum |ClusterClickhouse |ResourceID |Count |Alert, consumption |
|Cluster ByteHouse load |Number of Kafka tables |ClusterKafkaTableNum |ClusterClickhouse |ResourceID |Count |Alarm, Consumption |
|Cluster ByteHouse Load |Max Number of Master\-Slave Sync Delay Tables |ClusterHaQueueCount |ClusterClickhouse |ResourceID |Count |Alarm, Consumption |
|Cluster ByteHouse load |Number of files to be sent for distributed table |ClusterClickHouseMetrics_DistributedFilesToInsert |ClusterClickhouse |ResourceID |Count |Alarm, consumption |
|Cluster ByteHouse load |Number of broken tables |ClusterBroken_tables |ClusterClickhouse |ResourceID |Count |Alert, consumption |
|Cluster ByteHouse load |Merge memory usage |ClusterClickHouseMetrics_MergeMemoryUsage |ClusterClickhouse |ResourceID |Bytes(IEC) |Alert, consumption |
|Cluster ByteHouse load |Number of merge tasks |ClusterClickHouseProfileEvents_Merge |ClusterClickhouse |ResourceID |Count/Second |Alert, consumption |
|Cluster ByteHouse load |Number of map keys |ClusterClickHouseMetricsMapKeyCount |ClusterClickhouse |ResourceID |Count |Alarm, consumption |
|Cluster ByteHouse load |Unique table index memory usage |ClusterClickHouseMetrics_UniqueIndexMemoryUsage |ClusterClickhouse |ResourceID |Bytes(IEC) |Alert, consumption |
|Cluster ByteHouse load |Number of HA tables with zero leaders |ClickHouseMetrics_no_leader_ha_table_count |ClusterClickhouse |ResourceID |Count |Alert, consumption |
|Cluster ByteHouse load |Active part count |ClusterActiveParts |ClusterClickhouse |ResourceID |Count |Alert |
|Cluster ByteHouse load |Maximum concurrent nodes (including subquery) |ClusterClickHouseMetrics_Process_Count |ClusterClickhouse |ResourceID |Count |Alert: the highest current concurrency of a node in the cluster, including subquery |
|Cluster ByteHouse load |Number of mutations in progress |ClusterClickHouseMetrics_mutations_count |ClusterClickhouse |ResourceID |Count |Alert: number of mutations in progress, cluster total |
|Cluster ByteHouse load |Longest mutation execution time |ClusterClickHouseMetrics_mutations_max_execution_time |ClusterClickhouse |ResourceID |Second |Alert: longest mutation execution time |
|Cluster data import |Kafka consumption rate (rows per second) |ClusterClickHouseMetrics_KafkaMetricsPerSecond |ClusterDataImport |ResourceID |Count/Second |Alert, consumption |
|Cluster data import |Kafka consumption rate (bytes per second) |ClusterClickHouseMetrics_KafkaBytesPerSecond |ClusterDataImport |ResourceID |Bytes/Second(IEC) |Alert, consumption |
|Cluster data import |kafka error count (count per second) |ClusterClickHouseMetrics_KafkaErrorsPerSecond |ClusterDataImport |ResourceID |Count/Second |Alert, consumption |
|Cluster query load |Query concurrency |cluster_qps |ClusterQuery |ResourceID |Count/Second |alert, consumption |
|cluster query load |Query success rate |cluster_query_success_rate |ClusterQuery |ResourceID |Percent |alert, consumption |
|cluster query load |query latency |cluster_query_latency |ClusterQuery |ResourceID |Millisecond |alert, consumption |
|cluster query load |Select concurrency |cluster_select_qps |ClusterQuery |ResourceID |Count/Second |Alert, consumption |
|Cluster query load |Select success rate |cluster_select_query_success_rate |ClusterQuery |ResourceID |Percent |Alert, consumption |
|Cluster query load |Select latency |cluster_select_query_latency |ClusterQuery |ResourceID |Millisecond |Alert, consumption |
|cluster operating system load |cpu usage |cluster_cpu_usage_percentage |ClusterSystem |ResourceID |Percent |alert, consumption |
|cluster operating system load |memory usage |cluster_memory_usage_percentage |ClusterSystem |ResourceID |Percent |Alarm, consumption |
|Cluster Operating System Load |Memory usage |cluster_memory_usage |ClusterSystem |ResourceID |Gibibytes |Alarm, consumption |
|Cluster operating system load |Disk usage rate |cluster_disk_usage_percentage |ClusterSystem |ResourceID |Percent |Alarm, consumption |
|Cluster operating system load |Disk free space |cluster_disk_free_space |ClusterSystem |ResourceID |Gibibytes |alert, consumption |
|cluster operating system load |disk read IOPS |cluster_disk_read_iops |ClusterSystem |ResourceID |Count/Second |Alarm, consumption |
|Cluster operating system load |Disk write IOPS |cluster_disk_write_iops |ClusterSystem |ResourceID |Count/Second |Alarm, consumption |
|Cluster operating system load |disk read bandwidth |cluster_disk_read_byte |ClusterSystem |ResourceID |Kibibytes/Second |alert, consumption |
|cluster operating system load |disk write bandwidth |cluster_disk_write_byte |ClusterSystem |ResourceID |Kibibytes/Second |Alarm, consumption |
|Cluster operating system load |inode usage ratio |cluster_inode_usage |ClusterSystem |ResourceID |Percent |Alarm, consumption |
|Cluster operating system load |Number of node crashes |bad_node_count |ClusterSystem |ResourceID |Count |Alarm, consumption |
|Cluster operating system load |Number of shard failures |bad_shard_num |ClusterSystem |ResourceID |Count |alert, consumption |
|Cluster Zookeeper |Number of watches on client side |ClusterClickHouseMetrics_ZooKeeperWatch |ClusterZookeeper |ResourceID |Count |alert, consumption |
|cluster Zookeeper |ZK session creation count |ClusterClickHouseProfileEvents_ZooKeeperInit |ClusterZookeeper |ResourceID |Count |alert, consumption |
|node data import |kafka consumption rate (rows per second) |ClickHouseMetrics_KafkaMetricsPerSecond |DataImport |Node, ResourceID, ENI (optional) |Count/Second |Alert, Consumption |
|Node Data Import |Kafka Consumption Rate (bytes per second) |ClickHouseMetrics_KafkaBytesPerSecond |DataImport |Node, ResourceID, ENI (optional) |Bytes/Second(IEC) |Alert, Consumption |
|Node Data Import |kafka error rate (count per second) |ClusterClickHouseMetrics_KafkaErrorsPerSecond |DataImport |Node, ResourceID, ENI (optional) |Count/Second |Alert, Consumption |
|Node Query Load |Query concurrency |qps |Query |Node, ResourceID, ENI (optional) |Count/Second |Alarm, consumption |
|Node query load |Query success rate |query_success_rate |Query |Node,ResourceID,ENI (optional) |Percent |Alarm, consumption |
|Node query load |Query delay |QueryLatency |Query |Node,ResourceID,ENI (optional) |Millisecond |Alarm, consumption |
|node query load |Select concurrency |select_qps |Query |Node, ResourceID, ENI (optional) |Count/Second |Alarm, consumption |
|node query load |Select success rate |select_query_success_rate |Query |Node, ResourceID, ENI (optional) |Percent |Alarm, consumption |
|Node query load |Select latency |SelectQueryLatency |Query |Node, ResourceID, ENI (optional) |Millisecond |alert, consumption |
|node operating system load |cpu usage rate |cpu_usage_percentage |System |ResourceID, Node, ENI (optional) |Percent |alert, consumption |
|node operating system load |memory usage rate |node_memory_usage_percentage |System |Node, ResourceID, ENI (optional) |Percent |Alarm, consumption |
|Node operating system load |Memory usage |memory_usage |System |Node, ResourceID, ENI (optional) |Gibibytes |Alarm, consumption |
|Node operating system load |Disk usage rate |disk_usage_percentage |System |Node, ResourceID, ENI (optional) |Percent |Alarm, consumption |
|Node operating system load |Disk Free Space |node_disk_free_space |System |Node, ResourceID, ENI (optional) |Bytes(IEC) |Alert, Consumption |
|Node Operating System Load |Disk Read IOPS |disk_read_iops |System |Node, ResourceID, ENI (optional) |Count/Second |Alert, consumption |
|Node operating system load |Disk write IOPS |disk_write_iops |System |Node, ResourceID, ENI (optional) |Count/Second |Alert, consumption |
|node operating system load |disk read bandwidth |disk_read_byte |System |node, resourceID, ENI (optional) |Kibibytes/Second |alert, consumption |
|node operating system load |disk write bandwidth |disk_write_byte |System |Node, Resource ID, ENI (optional) |Kibibytes/Second |Alert, Consumption |
|Node Operating System Load |inode Usage Ratio |inode_usage |System |Node, Resource ID, ENI (optional) |Percent |alert, consumption |
|Node Zookeeper |Client\-side watch count |ClickHouseMetrics_ZooKeeperWatch |Zookeeper |Node, ResourceID, ENI (optional) |Count |alert, consumption |
|Node Zookeeper |ZK session creation count |ClickHouseProfileEvents_ZooKeeperInit |Zookeeper |Node, ResourceID, ENI (optional) |Count |Alert, Consume |


<span id="3ed7e71a"></span>
# View monitoring information

<span id="4eca5044"></span>
## Steps


1. Log in to the ByteHouse Enterprise Console, click **Cluster Management**, then click the target cluster in the cluster list to enter the cluster details page.

2. Click **Monitoring Alerts** to view the monitoring details of the current cluster and its nodes.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/672430249f724e6eafb0a483fbb9a74b~tplv-goo7wpa0wc-image.image) </span>


<span id="7e99703b"></span>
# Set alerts

ByteHouse Enterprise Edition integrates with cloud monitoring services for managing alert policies. This article explains how to create alert policies. For more details on alert processes and principles, see [Alert Principles - Cloud Monitoring](https://docs.byteplus.com/en/docs/cloudmonitor/Alarm-mechanism).

<span id="caa925fa"></span>
## Steps


1. Log in to the ByteHouse Enterprise Edition Console, click **Cluster Management**, then select the target cluster from the list to enter the cluster details page.

2. Click **Create an alert policy**, and the system will automatically redirect to the cloud monitoring service's create alert policy page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb0e8818b9f2436b8f560cec7f77efb5~tplv-goo7wpa0wc-image.image) </span>

3. On the **Create Alert Policy** page, configure the parameters according to your business requirements. For detailed parameter configuration instructions, see [Creating an alarm strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When configuring alarm targets on the <strong>Create</strong> <strong>an alert policy</strong> page, select the resource type as <strong>Data Middle Platform \> ByteHouse Enterprise Edition</strong>.   </div>
   

<span id="b2cd27ca"></span>
## Recommended alert policies

You can configure alert policies for clusters or nodes based on business scenarios and actual needs. The recommended alert policies are as follows:


|Monitoring Metrics |Supported Dimensions for Configuration |Recommended Alarm Strategies |
|---|---|---|
|Query Success Rate |* Cluster query load<br><br>* Node query load |Trigger an alert if Query success rate is below 97%. |
|CPU success rate |* Cluster OS load<br><br>* Node OS load |Trigger an alert if CPU usage exceeds 95%. |
|Memory usage |* Cluster OS load<br><br>* Node OS load |Recommend alerting when memory usage exceeds 85% |
|Disk usage |* Cluster operating system load<br><br>* Node operating system load |Recommend alerting when disk usage exceeds 95% |
|Number of node failures |* Cluster operating system load |Recommend alerting when the number of node failures is greater than 0 |


<span id="e0f72638"></span>
# Related links


* [View an alarm policy](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-an-alarm-strategy)

* [Modify an alarm policy](https://docs.byteplus.com/en/docs/cloudmonitor/Modifying-an-alarm-strategy)

* [Enable an alarm policy](https://docs.byteplus.com/en/docs/cloudmonitor/Enabling-an-alarm-strategy)

* [Disable an alarm policy](https://docs.byteplus.com/en/docs/cloudmonitor/Disabling-an-alarm-strategy)

* [Delete an alarm policy](https://docs.byteplus.com/en/docs/cloudmonitor/Deleting-an-alarm-strategy)

* [View alarm history](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-alarm-history)

* [Instructions for using alarm callbacks](https://docs.byteplus.com/en/docs/cloudmonitor/Webhook-instructions)

* [Connect alarm callbacks with Lark groups](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-Feishu-groups)

* [Alarm callback linked to DingTalk groups](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-DingTalk-groups)

* [Alarm callback linked to WeCom groups](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-WeChat-groups)
