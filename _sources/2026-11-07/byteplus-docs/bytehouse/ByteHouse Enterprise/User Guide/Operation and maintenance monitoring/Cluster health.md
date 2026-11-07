---
title: "Cluster health"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/cluster-health"
---

<span id="健康度定义"></span>
## Health definition

Cluster health is determined by referencing multiple dimensions of health indicators. It is an **important indicator** for assessing the operational status of the cluster and the risk of encountering problems. Compared to monitoring indicators, health indicators are less timely (collected the maximum value of the past hour every hour), reflecting issues that are more targeted towards long\-term governance solutions.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">An analogy: Monitoring is like a vital signs monitor, health status is like a medical report.</div>



* Health Indicators:

   * Health assessment metrics include dimensions such as hardware and system health, ClickHouse health, and query health, comprising three main categories and nine specific indicators (see below for details on indicator meanings and optimization suggestions).

   * Based on thresholds, each monitoring indicator is rated at four different levels: critical, failing, passing, and good.

* Health Level:

   * As an overall summary of the cluster, it abstractly reflects the general health status.

   * There are four levels that correspond to the tiers of health indicators:

      * Danger: There is 1 hazardous indicator;

      * Fail: No hazardous indicators, but more than 1 indicator is failing;

      * Pass: No dangerous or failing indicators, and more than 1 indicator is passing;

      * Good: Each indicator is good.


<span id="66334ff4"></span>
### View Steps

**Prerequisites:** 


* The operating user is the ClusterAdmin role of the current cluster, or the SystemAdmin role.

* The cluster is in the "Running" state.


**Steps**


1. Enter ByteHouse Enterprise console, the default entry is the cluster list page.

2. If on another page, you can choose (top right switch) Operations and Permission Management \> Cluster Management \> Cluster List.

3. Click on the cluster name, enter the cluster details, and select the "Health" TAB.


<span id="3bd0da77"></span>
## Metrics description and optimization suggestions

<span id="04ee316d"></span>
### Maximum Disk Usage Rate

**Meaning of the Metric:**  The usage rate of the data disk (disk where the ByteHouse directory is located). High disk usage rate will affect subsequent data imports.

**Scoring Threshold:** 


|Healthy |Pass |Fail |Danger |
|---|---|---|---|
|（0,60] |（60,80] |（80,95] |（95,100] |


**Optimization Suggestions:** 


* (Cloud Support) Expand the disk by using the "**Change Specification**" button at the top of the interface.

* (No further disk expansion possible for privatization or on cloud):

* Scenarios where data is not needed:

   * Delete unnecessary tables. You can view larger tables in the system using `select database, name, total_bytes from system.tables order by total_bytes desc limit 100` and delete them via the console or by using `Drop xxx.xx on cluster xxx`.

   * Reduce the TTL of tables as needed.

* Scenarios where all data is needed: Refer to [Cold-hot storage](https://docs.byteplus.com/docs/bytehouse/cold-hot-storage) to enable cold storage.


<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">Stop all import tasks when the indicator reads "Danger".</div>


<span id="bb71fc02"></span>
### Maximum File Count Ratio

**Index Meaning:**  Indicates the inode usage rate of the operating system. Too high levels can affect cluster data import and querying. This is usually caused by overly fragmented Parts, which cannot be merged in time.

**Scoring threshold:** 


|Healthy |Pass |Fail |Danger |
|---|---|---|---|
|（0,60] |（60,80] |（80,90] |（90,100] |


**Optimization suggestions:** 

Refer to the methods described in the document [Part 过多](https://docs.byteplus.com/docs/undefined/6593de997d62700306cf3b0d)for processing.

<span id="f3373d26"></span>
### Node failure rate

**Indicator meaning:**  Unreachable nodes / Total number of nodes.

**Scoring threshold:** 


|Healthy |Pass |Fail |Dangerous |
|---|---|---|---|
|0% |（0,20] |（20,50] |（50,100] |


**Optimization suggestions:** 


* ByteHouse Enterprise Edition, based on public cloud ECS products, maintains 99.95% resource availability. If the downtime rate remains high, it is advisable to submit a ticket and replace the underlying infrastructure.

* The underlying infrastructure of ByteHouse Enterprise Edition (private deployment) can be based on any facility. If the downtime rate remains high, the "Node Replacement" feature can be utilized (supported version: 2.4.1 and above) to change node servers.


<span id="53619680"></span>
### Average CPU usage rate

**Meaning of the indicator:** 

This parameter records the average usage rate of the system CPU. It reflects whether the system has exceeded the processing capacity limit of the CPU, leading to performance issues.

**Rating threshold:** 


|Health |Pass |Fail |Danger |
|---|---|---|---|
|(0%,70%] |(70%,80%] |(80%,90%] |(90%,100%] |


**Optimization suggestion:** 


* By using SELECT \* FROM system.query_log ORDER BY total_cpu_seconds DESC limit 20, review large queries that consume a lot of CPU and optimize SQL and Schema as per the recommendations in this section.

* If there is no substantial room for SQL optimization, or the cost of SQL rewriting / schema adjustment is too high, consider whether users consuming more CPU can be limited by placing them in resource groups to restrict CPU resources.

* The recommended score for failing grades is to scale up either horizontally or vertically. Refer to [Reconfigure a cluster](https://docs.byteplus.com/docs/bytehouse/reconfigure-a-cluster).


<span id="2db0f565"></span>
### Average Memory Usage

**Definition:** 

The average memory usage of the system, which reflects whether the system has exhausted available memory, leading to performance issues.

**Scoring Thresholds:** 


|Healthy |Pass |Fail |Danger |
|---|---|---|---|
|(0,50%] |(50%,75%] |(75%,90%] |(90,100%] |


**Optimization Suggestions:** 


* Refer to [内存不足](https://docs.byteplus.com/docs/undefined/6593f2e2776b3f02ee5dadd1) for troubleshooting.

* Check if the users who consume a lot of memory can limit memory resources by putting them into [资源组](https://docs.byteplus.com/docs/undefined/6593f3526ac4360306f849a5).

* If there is no room for optimization, it is recommended to scale horizontally or vertically if the score is below passing. Refer to [Reconfigure a cluster](https://docs.byteplus.com/docs/bytehouse/reconfigure-a-cluster).


<span id="663fa15f"></span>
### Average IO Utilization

**Meaning of Indicator:** 

The average IOPS of system disks, which can indicate whether disk resources have become a performance bottleneck.

**Scoring Threshold:** 


|Healthy |Pass |Fail |Danger |
|---|---|---|---|
|(0%,70%] |(70%,80%] |(80%,90%] |(90%,100%] |


**Optimization Suggestions:** 


* By executing `SELECT * FROM system.query_log ORDER BY read_bytes DESC limit 20` and `SELECT * FROM system.query_log ORDER BY written_bytes DESC limit 20`, identify large queries with significant read and write costs, and optimize SQL and Schema as per the suggestions in [慢查询](https://docs.byteplus.com/docs/undefined/6593ded07d62700306cf3b8a)the section.

* If there is no significant room for SQL optimization, or if the cost of SQL rewriting/Schema adjustment is too high, a score of unsatisfactory or above is suggested to scale horizontally or vertically directly. Refer to [Reconfigure a cluster](https://docs.byteplus.com/docs/bytehouse/reconfigure-a-cluster).


<span id="7206956b"></span>
### Number of Cluster Tables

**Meaning of Indicator:** 

Total number of \*MergeTree tables in the cluster. The greater the number of tables, the more likely it is to cause high pressure on Zookeeper, leading to data synchronization problems.

**Scoring threshold:** 


|Health |Pass |Fail |Danger |
|---|---|---|---|
|[0,500] |(500,1000] |(1000,5000] |> 5000 |


**Optimization suggestions:** 


* Delete some unnecessary tables. If there is a need for thousands of tables, it is recommended to use multiple clusters.


<span id="2a067812"></span>
### Number of Kafka tables

**Meaning of the metric:** 

Total number of HaKafka tables in the cluster. The more tables there are, the more likely it is that the cluster's resources are used for writing, leaving no resources for querying.

**Scoring threshold:** 


|Healthy |Pass |Fail |Critical |
|---|---|---|---|
|[0,20] |(20,50] |(50,90] |> 90 |


**Optimization Suggestions:** 


* Delete some unnecessary import tasks. If there is a need for more than 50 import tasks, it is advised to use multiple clusters to handle them.


<span id="19db5787"></span>
### Maximum primary\-secondary synchronization delay for a single table

**Metric Definition:** 

The primary\-secondary synchronization logs of the [HaMergeTree](https://docs.byteplus.com/docs/bytehouse/hamergetree) engine are recorded in the system table `ha_queue`. This metric indicates the number of unprocessed logs in `ha_queue` for the table with the most backlog, suggesting issues with its primary\-secondary synchronization, most likely only one node has complete data and is handling queries, causing uneven load distribution.

**Scoring Threshold:** 


|Health |Pass |Fail |Critical |
|---|---|---|---|
|[0,100] |(100,1000] |(1000,10000] |> 10000 |


<span id="0ffe1eb7"></span>
### Number of Faulty Tables

**Metric Definition:** 

Recorded the number of tables that could not be started, which are not readable or writable. This may be due to accidental reboot or hardware damage.

**Rating threshold:** 


|Healthy |Pass |Fail |Critical |
|---|---|---|---|
|[0,1) |*  |*  |≥1 |


**Processing steps:** 

Please contact ByteHouse support personnel for assistance.

<span id="c140796b"></span>
### Number of tables with Leader at 0

**Meaning of the metric:** 

This parameter records the number of tables without a Leader replica, which causes these tables to be unwritable.

It is usually due to a problem with ZooKeeper.

**Rating threshold:** 


|Healthy |Pass |Failed |Critical |
|---|---|---|---|
|[0,1) |*  |≥1 |*  |


**Processing Steps:** 


* Please contact ByteHouse support staff for assistance.


<span id="df061efb"></span>
### Maximum Node Part Total Count

**Indicator Meaning:** 

Records the maximum number of Parts per node. Excessive Parts can lead to substantial resource use for merging in the background, slowing down queries, and in more severe cases, can exhaust inodes, preventing further writing.

**Scoring Threshold:** 


|Healthy |Passed |Failed |Critical |
|---|---|---|---|
|[0,100000) |*  |≥ 100000 |*  |


**Processing Steps:** 


* Refer to [Part 过多](https://docs.byteplus.com/docs/undefined/6593de997d62700306cf3b0d)for processing.


<span id="e898339a"></span>
### Distributed Table Delay

**Meaning of Indicator:** 

It shows the number of backend files inserted into a distributed table (back files), representing data insertion delays. If this indicator is too high, a lot of newly written data cannot be queried.

**Scoring Threshold:** 


|Healthy |Pass |Fail |Critical |
|---|---|---|---|
|[0,100) |*  |[100,200) |≥ 200 |


**Processing Steps:** 


* Please contact ByteHouse support staff for assistance.


<span id="c24a2265"></span>
### P95 Query Delay

**Meaning of Indicator:**  The P95 percentile of all query latencies in the cluster (unit: seconds), basically reflects the cluster's query response speed. The larger the number, the worse the health of the cluster.

**Scoring Threshold:** 


|Health |Pass |Fail |Critical |
|---|---|---|---|
|(0,1] |（1,5] |（5,10] |> 10 |


**Optimization suggestions:** 


* This indicator's unhealthy status indicates that the cluster's query speed is very slow, slower than the typical expectations users have for ByteHouse. First, gather feedback from various downstream businesses. If the business queries indeed involve large volumes of data and the current querying speed is acceptable, the issue can be temporarily ignored and monitored continuously later on.

* If feedback from downstream businesses indicates that the queries are unstable and increasingly slower. Then proceed with [慢查询](https://docs.byteplus.com/docs/undefined/6593ded07d62700306cf3b8a)SQL optimization.

* If all large queries cannot be further optimized, consider migrating the data of users with large queries to a separate cluster and setting parameters like `max_execution_time` in the current cluster.


<span id="71ec9f15"></span>
### Query success rate

**Indicator meaning:**  The success rate of all queries in the cluster, reflecting the presence of widespread timeouts and SQL syntax errors, the lower it is, the worse the health situation.

**Rating threshold:** 


|Health |Pass |Fail |Critical |
|---|---|---|---|
|(99,100] |（95,99] |（90,95] |<95 |


**Optimization suggestions:** 


* This type of issue is usually due to high cluster load causing numerous timeouts, or queries being sent in large numbers that do not adhere to syntax; through the `data management and query -> query management -> query history` feature, you can find the failed queries corresponding to this cluster. Identifying the main causes of failure:

   * Timeouts: Often due to high cluster load, refer to [慢查询](https://docs.byteplus.com/docs/undefined/6593ded07d62700306cf3b8a)the handling methods.

   * Too Many Parts: Caused by unreasonable imports. Consult [Part 过多](https://docs.byteplus.com/docs/undefined/6593de997d62700306cf3b0d)the handling methods.

   * Other syntax errors: Mainly check whether there is a specific user continuously sending queries that do not comply with the syntax, and communicate with that user to make adjustments.
