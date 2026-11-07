---
title: "Statistical Time Period"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_en"
---

Based on your specified `StartTime`, `EndTime`, and `Interval`, CDN collects a series of data points. `Interval` represents the time interval at which CDN collects these data points. For example, when `Interval` is `5min`, CDN collects 1 data point every 5 minutes.

The examples in the table below show the number of data points collected by CDN based on different `Interval` values and the time intervals corresponding to each data point.


|**StartTime** |**EndTime** |**Interval** |**Number of Data Points Collected by CDN** |**Time Intervals Corresponding to Collected Data Points** |**Actual Statistical Period** |
|---|---|---|---|---|---|
|15:07 |15:21 |5 Minutes |4 |[15:05,15:10)、[15:10,15:15)，[15:15,15:20)，[15:20,15:25) |[15:05,15:25) |
|15:07 |15:25 |5 Minutes |5 |[15:05,15:10)、[15:10,15:15)，[15:15,15:20)，[15:20,15:25)、[15:25,15:30) |[15:05,15:30) |
|15:05 |15:25 |5 Minutes |5 |[15:05,15:10)、[15:10,15:15)，[15:15,15:20)，[15:20,15:25)、[15:25,15:30) |[15:05,15:30) |
|15:07 |18:21 |1 Hour |4 |[15:00,16:00)、[16:00,17:00)、[17:00,18:00)、[18:00,19:00) |[15:00,19:00) |
|15:07 |19:00 |1 Hour |5 |[15:00,16:00)、[16:00,17:00)、[17:00,18:00)、[18:00,19:00)、[19:00,20:00) |[15:00,20:00) |


As shown above, the **actual statistical period** corresponding to the data points collected by CDN may differ from your specified statistical time period.

<span id="detailed-data"></span>
#### Detailed Data

The data points collected by CDN based on `Interval` are the detailed data of the specified metrics. Detailed data reflects the trend of metric data.

<span id="aggregated-data"></span>
#### Aggregated Data

CDN aggregates metric data based on detailed data. Different metrics have different aggregation methods. For details, see [Metric Reference](https://docs.byteplus.com/en/docs/byteplus-cdn/QzMnM4).

Example: Your specified `StartTime` is 15:07, `EndTime` is 15:20, `Interval` is `5min`, and the specified `Metric` is `traffic`. In this case, CDN aggregates traffic data using the following steps:


1. Calculate traffic data for the following time intervals: [15:05,15:10), [15:10,15:15), [15:15,15:20), [15:20,15:25). The actual statistical period is [15:05,15:25).

2. Sum up these traffic data as the aggregated data for the traffic metric within the specified statistical period.
