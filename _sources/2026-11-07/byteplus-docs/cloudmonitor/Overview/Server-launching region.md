---
title: "Server-launching region"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Server-launching_region"
---

This topic describes the concept of regions, methods of selecting regions, and the regions where Cloud Monitor is available.

<span id="IvanCUki"></span>
## Basic concept

**Regions**: the geographical locations of physical data centers. After resource creation, you cannot change the corresponding region. The internal networks of different regions are isolated. This ensures the highest stability and fault tolerance between regions.

<span id="v4nKXK7r"></span>
## Method of selecting a region

When you select a region, you need to consider the following factors:


* From the perspective of geographical location, we recommend that you select the region close to you or your target users to reduce network latency and accelerate access.

* From the perspective of resource pricing, resource prices may vary based on different regions. If you or your target users are located in the Chinese mainland, you do not need to consider network latencies caused by different regions. This is because differences between regions in the Chinese mainland are small in terms of infrastructure, BGP network quality, and resource operations and configurations.


<span id="06rd7T1l"></span>
## Server\-launching regions

The following table lists regions where Cloud Monitor is available. However, the regions vary based on different related products or features. The regions displayed in the console shall prevail. For example, you can create an alert policy only in certain regions.


|Area |**Region** |**Region ID** |
|---|---|---|
|Chinese mainland |China (Beijing) |cn\-beijing |
||China (Shanghai) |cn\-shanghai |
||China (Guangzhou) |cn\-guangzhou |
||China (Hong Kong) |cn\-hongkong |
|Asia Pacific |Asia Pacific (Johor) |ap\-southeast\-1 |
||Asia Pacific (Jakarta) |ap\-southeast\-3 |
