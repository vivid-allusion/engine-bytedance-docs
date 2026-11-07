---
title: "Overview"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/data-insights-overview"
---

DataInsights is a one\-stop data analysis and observability service offered by Elastic Block Storage (EBS). This feature allows you to centrally view volume resource usage and collect performance monitoring data with one\-second granularity at most. With DataInsights, you can efficiently analyze business fluctuations, identify performance bottlenecks, troubleshoot issues, and make informed decisions about resource planning and cost optimization.

> **tip**

> This feature is currently in closed beta. Contact your account manager to have your account added to the allowlist and start using it.

## Introduction

* Global overview

   * "Resource Overview": Once you have enabled DataInsights, it will automatically aggregate basic information about the volumes and snapshots under your account. This information includes the total number of resources, total size, regional distribution, specification distribution, and billing method distribution. Together, these details provide a comprehensive overview of your EBS resources.

   * "Performance Overview": DataInsights collects and stores performance metrics, such as total throughput, read throughput, write throughput, and IOPS, for volumes in real time. It offers multidimensional filtering and aggregation analysis by availability zone, ECS instance, tag, specification, and more.

* Second\-level monitoring

   The second\-level monitoring feature must be enabled separately for each volume. Once enabled, the system collects volume performance metrics every second, providing you with more detailed data on performance changes.

   These metrics are stored in a Torch Log Service (TLS) topic at second\-level intervals. You can use the topic to search the data directly and perform analyses based on the charts.

* System events

   This module continuously monitors volume\-related risks and anomalies, displaying matching events in list and statistical views. It helps you identify performance and data security risks, cost optimization opportunities, and stability issues in a timely manner.

## Notes

* DataInsights is currently in closed beta. Please contact your account manager for access.

* Resource data is retained for 30 days and automatically deleted after that period.

* Minute\-level performance data is provided free of charge and is retained for 30 days.

* Second\-level monitoring data is collected and stored via TLS. You can configure the retention period in the "target storage topic". After the retention period expires, TLS automatically cleans up the data.

* There is a delay of one to five minutes between the second\-level monitoring and the performance data. Therefore, the most recent data points you query may be one to five minutes old.

## Billing

* EBS provides a resource overview, a minute\-level performance overview, and event monitoring free of charge.

* Second\-level monitoring collects, transfers, and stores data via TLS, which generates TLS read/write and storage fees. For a list of billable items, see [TLS billing overview](https://docs.byteplus.com/docs/tls/billable_items).

## Enabling DataInsights

The first time you use DataInsights, you must complete cross\-service authorization. Once authorization is complete, DataInsights will automatically start collecting data for the resource and performance overviews.

> **tip**

* > It may take a short time for data to appear after you first enable DataInsights, as collection and warm\-up take time. Thank you for your patience.

* > Resource data is updated every 10 minutes. However, the snapshot data is updated every hour. Performance data is updated every minute.

1. Log in to the [ECS console](https://console.byteplus.com/ebs).

2. In the top menu bar, select the region that you want to check.

3. In the left navigation pane, select "Storage \> DataInsights" **.**

4. The first time you access the "DataInsights" page, click "Get started" and follow the instructions to create a service\-linked role for EBS and TLS.

5. After authorization, you will be automatically redirected to the DataInsights homepage. You can then view relevant volume data in the "Resource Overview" and "Performance Overview" sections.

## Viewing volume resources and performance

In the [ECS console](https://console.byteplus.com/ebs), click the "Global Overview" tab on the "DataInsights" page to view volume resources and performance.

### Resource overview

The "Resource Overview" tab offers a summary of your EBS resources, including volumes and snapshots. You can filter resources by multiple dimensions, such as region, availability zone, and time.

|Parameter |Description |
|---|---|
|Capacity and quantity |Displays the size and number of volumes and snapshots in the selected region and availability zone(s) for the current account.<br><br><br>* "Total Volumes".<br><br>* "Total Snapshots".<br><br>* "Volumes with Snapshots (%)".<br><br>* "Total Volume Capacity".<br><br>* "Total Snapshot Capacity".<br><br>* "ESSD FlexPL Volumes with Performance Bursting Enabled". |
|Distribution |Displays the distribution of volume count and size for the current account.<br><br><br>* "Volume Count by Specification Type".<br><br>* "Volume Count by Billing Type".<br><br>* "Volume Count by Availability Zone". |

### Performance overview

The "Performance Overview" tab provides real\-time metrics on volume performance. You can filter volumes by multiple dimensions, such as availability zone, ECS instance, tag, and specification.

|Parameter |Description |
|---|---|
|Performance trend |You can use visual charts to view throughput (Mbps) and IOPS (Count/s) data for all or specific volumes in the current account.<br><br>You can filter data using the following options:<br><br><br>* "ECS Instance": All instances are selected by default. You can select one or more ECS instances.<br><br>* "Volume": All volumes are selected by default. You can select one or more volumes.<br><br>* "Volume Type": All options are selected by default. These options include system and data volume.<br><br>* "Volume Specification": All options are selected by default. You can select one or more volume specifications.<br><br>* "Billing Type": All options are selected by default. These options include pay\-as\-you\-go and subscription.<br><br>* "Aggregation": "Sum" is selected by default. These options include "Sum", "Average", and "Maximum". |
|Top 30 volume performance |You can use visual charts to view the following performance metrics for the top 30 volumes in the current account:<br><br><br>* "Write Throughput (Mbps)"<br><br>* "Read Throughput (Mbps)"<br><br>* "Write IOPS (Count/s)"<br><br>* "Read IOPS (Count/s)"<br><br><br>The charts show the minimum, maximum, and current values of the top 30 volumes for each metric. |

## Related documentation

To analyze performance data with charts and explore detailed performance changes, see [Second-level monitoring](https://docs.byteplus.com/en/docs/ecs/second-levelmonitoring) and [System events](https://docs.byteplus.com/en/docs/ecs/system-events).
