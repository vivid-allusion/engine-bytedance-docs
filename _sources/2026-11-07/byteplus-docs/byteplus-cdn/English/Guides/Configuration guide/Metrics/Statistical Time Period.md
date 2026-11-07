---
title: "Statistical Time Period"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/Jbrkn1"
---

To accurately interpret your CDN metrics, it is crucial to understand how statistical time periods are calculated. This document explains how CDN uses your specified time range and granularity to collect data points. It clarifies why the actual time range used for statistics may differ from your specified range and details the concepts of detailed and aggregated data.

Time granularity represents the time interval at which CDN collects these data points. For example, for a 5\-minute time granularity, CDN collects 1 data point every 5 minutes.

The following table shows how the number of data points and their corresponding time intervals vary based on the specified time granularity.


|**Specified Start Time** |**Specified End Time** |**Specified Time Granularity** |**Number of Data Points Collected by CDN** |**Time Intervals Corresponding to Collected Data Points** |**Actual Statistical Time Range** |
|---|---|---|---|---|---|
|15:07 |15:21 |5 Minutes |4 |[15:05,15:10), [15:10,15:15)，[15:15,15:20)，[15:20,15:25) |[15:05,15:25) |
|15:07 |15:25 |5 Minutes |5 |[15:05,15:10), [15:10,15:15)，[15:15,15:20)，[15:20,15:25), [15:25,15:30) |[15:05,15:30) |
|15:05 |15:25 |5 Minutes |5 |[15:05,15:10), [15:10,15:15)，[15:15,15:20)，[15:20,15:25), [15:25,15:30) |[15:05,15:30) |
|15:07 |18:21 |1 Hour |4 |[15:00,16:00), [16:00,17:00), [17:00,18:00), [18:00,19:00) |[15:00,19:00) |
|15:07 |19:00 |1 Hour |5 |[15:00,16:00), [16:00,17:00), [17:00,18:00), [18:00,19:00), [19:00,20:00) |[15:00,20:00) |


As the examples show, the actual statistical time range for which the CDN collects data can differ from the specified statistical time range.

<span id="detailed-data"></span>
#### Detailed Data

Detailed data consists of the data points that the CDN collects at the specified time granularity. This data reflects trends for the metric.

<span id="aggregated-data"></span>
#### Aggregated Data

CDN aggregates metric data based on detailed data. Different metrics have different aggregation methods. For details, see [Metrics Reference](https://docs.byteplus.com/en/docs/byteplus-cdn/QzMnM4).

Example: Your specified start time is 15:07, end time is 15:20, time granularity is 5 minutes, and the specified metric is traffic. In this case, CDN aggregates traffic data using the following steps:


1. Calculate traffic data for the following time intervals: [15:05,15:10), [15:10,15:15), [15:15,15:20), [15:20,15:25). The actual statistical time range is [15:05,15:25).

2. Sum up the data as the aggregated value for the traffic metric within the statistical time range.
