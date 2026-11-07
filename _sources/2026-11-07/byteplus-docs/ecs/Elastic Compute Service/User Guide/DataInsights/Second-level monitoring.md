---
title: "Second-level monitoring"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/second-levelmonitoring"
---

This topic is about the second\-level monitoring capability offered by Elastic Block Storage (EBS).

> **tip**

> The second\-level monitoring module of DataInsights is currently in closed beta. Contact your account manager to have your account added to the allowlist and start using it.

## Prerequisites

You have enabled the [DataInsights](https://docs.byteplus.com/en/docs/ecs/data-insights-overview) feature.

## Notes

* The default log retention period is 30 days. To modify this period, go to "DataInsights \> Second level monitoring \> Integrated configuration \> Target storage topic".

* Disabling second\-level monitoring does not automatically delete historical data stored in Torch Log Service (TLS). However, you can still view monitoring data collected before the feature was disabled. To delete the data, go to the [TLS console](https://console.byteplus.com/tls) and manually remove it from the corresponding topic.

## Introduction

This module tracks the performance metrics of individual EBS volumes, including read/write throughput, read/write IOPS, average I/O size, IOPS utilization, and BPS utilization.

After you enable second\-level monitoring for a volume, the system collects and stores request metrics in a TLS topic at a second\-level frequency. This module also provides data dashboards with visual trend charts of more granular performance data for analyzing volumes.

## Billing notes

Once second\-level monitoring is enabled, data is collected through TLS at the second level. This process incurs TLS fees. For more information, see [TLS billing overview](https://docs.byteplus.com/docs/tls/billable_items).

## Enabling or disabling second\-level monitoring

Based on your needs, you can enable or disable second\-level monitoring in the following ways.

* From the "DataInsights" page:

   1. Log in to the [ECS console](https://console.byteplus.com/ebs).

   2. In the top menu bar, select the region where your volume resides.

   3. In the left navigation pane, select "Storage \> DataInsights".

   4. On the "DataInsights" page, select "Second level monitoring \> Integrated configuration".

   5. On the "Integrated configuration" tab, click "Integrated Management".

      * To enable or disable the feature for a single volume, turn on or off the "Second Level Monitoring" switch located to the right of its row.

      * To enable or disable the feature for multiple volumes at once, select the desired volumes. Then, click "Batch enabled/Batch disabled" at the bottom of the page.

   6. In the confirmation dialog box, verify the volume details and click "OK".

* From the "Create volume" page:

   You can enable "Second level monitoring" when creating a volume. For more information, see [Creating a volume](https://docs.byteplus.com/docs/ecs/Create-a-volume).

## Viewing second\-level monitoring data

1. On the "DataInsights" page, select "Second level monitoring \> Data dashboard".

2. On the "data dashboard" page, set the filtering criteria to view the performance metrics of the desired volume.

   |Metric |Description |
   |---|---|
   |Volume read/write throughput |The actual rate of successful data transfer within the current volume during the query period in Mbps.<br><br>Higher throughput means that a greater volume of data can be transmitted in a given amount of time. This is ideal for scenarios with high bandwidth requirements, such as sequentially reading or writing large files, backing up databases, or migrating large amounts of data. |
   |Volume read/write IOPS |The number of input/output (I/O) operations that the current volume processes per unit of time. It indicates EBS's ability to handle read/write operations at a rate of counts per second.<br><br>A higher IOPS indicates that the volume can process more read and write operations per second. This makes it ideal for applications requiring high random I/O performance, such as processing database transactions and reading and writing small files with high concurrency. |
   |Average I/O size (read/write) |The amount of data, in bytes, read or written within the current volume per I/O operation. The I/O size affects the storage system's throughput and efficiency.<br><br><br>* An average I/O size below 4 KB indicates a workload dominated by random, small I/Os, which demand higher IOPS performance.<br><br>* A larger average I/O size indicates a workload dominated by sequential, large I/Os, which demand higher throughput.<br><br><br>In order to evaluate the current volume specification against the actual workload, it is necessary to combine IOPS and throughput data. |
   |BPS utilization |The ratio of the actual throughput to the maximum allowed for the current volume.<br><br>It is used to monitor throughput utilization of a volume. When this ratio consistently approaches 100%, it means the volume's data transfer capacity is nearly maxed out. Increasing the load further may cause performance bottlenecks and affect application response times. If utilization remains high for an extended period, we recommend upgrading the volume specification or optimizing the data transfer strategy. |
   |IOPS utilization |The ratio of the actual IOPS to the maximum allowed for the current volume.<br><br>It is used to monitor the utilization of a volume's I/O processing capacity. When this ratio consistently approaches 100%, it means the volume's concurrent I/O processing capacity is nearly maxed out. This can result in increased latency or failed requests, which can affect the stability of upper\-layer applications. If utilization remains high for an extended period, we recommend upgrading the volume specification or optimizing the concurrent access strategy. |
