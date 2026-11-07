---
title: "Query Configuration"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Query_Configuration"
---

<span id="_1-概述"></span>
# 1. Overview

Visualization queries support query configuration, including cache and sampling features. After enabling the cache, when querying charts with the same conditions before the data is updated, cached data will be read to shorten query time. If the cache is disabled, each page refresh or chart query will perform a real\-time query. In addition, the sampling feature can also be enabled in the query configuration, which, once enabled, can improve query speed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9cf376db23b54de7932eae6fa3ab7669~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-功能介绍"></span>
# 2. Feature introduction

<span id="_2-1-缓存设置"></span>
## 2.1 Cache settings

Cache is enabled by default for visualization queries. When the cache is enabled, the cache will be refreshed when the corresponding dataset is synchronized, ensuring that the query data is up to date.

You can uncheck and apply to disable the cache. After disabling the cache, each query and refresh will perform a real\-time query, which may increase data query time.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9cf376db23b54de7932eae6fa3ab7669~tplv-goo7wpa0wc-image.image) </span>

For real\-time datasets (Kafka, ClickHouse), you can also set the cache duration, which is the cache refresh interval.

After setting the cache duration for real\-time datasets, the data will be refreshed once every cache interval, ensuring that the time difference between the query data and the actual production data is within the cache duration, while also improving query performance.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3420cd90919b4112803f697b0e528781~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-抽样设置"></span>
## 2.2 Sampling settings

The sampling feature is supported. Selecting the [Enable sampling] feature can improve query speed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa9175a6e0eb4631ae0ab6d27549190b~tplv-goo7wpa0wc-image.image) </span>

After enabling sampling, sampling fields will be visible, and you can configure the sampling type as needed.

<span id="_2-2-1-抽样类型"></span>
### 2.2.1 Sampling types

(1) Random sampling

Applicable scenario: Large data volume with slow queries, quickly view results through sampling

Applicable data volume: Only available for large data volumes (greater than 100,000 rows)

Feature description: Sampling is performed by block (each block contains 8,192 rows), so the sampling row count error is significant for small data volumes and is not suitable.

(2) Default sampling

Applicable scenario: Sample 200 rows from 100,000 rows of data to view detailed data

Applicable data volume: Suitable for small data volumes (less than 100,000 rows)

Feature description: Sampling is performed by row, but updated partitions are more likely to be sampled, so it is not suitable for large data volumes or for metric calculation. In this sampling mode, if the data is not updated, the result of each sampling is the same. Therefore, it is suitable for scenarios where the same detailed data needs to be viewed through multiple samplings.

<span id="_2-2-2-抽样百分比"></span>
### 2.2.2 Sampling percentage

During visualization queries, sampling is performed based on the sampling field. The smaller the percentage, the less data is processed, and the faster the query speed.

<span id="38f53bd7"></span>
## 2.3 Cluster query parameters

\**Supported in private deployment since version 2.68*

In query configuration, ClickHouse\-based charts can improve query speed by enabling cluster query parameters.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ef869475ce54715bb1eade0644ba491~tplv-goo7wpa0wc-image.image) </span>


* enableOptimizer: Enables the optimizer to accelerate queries by adjusting parameters and other means to improve performance.

* enableRuntimeFilter: Enables the runtime filter, which dynamically generates filter conditions at runtime to reduce the amount of data scanned and accelerate queries.

* logQueriesCutToLength: Limits the query length and truncates the query result to a certain length to improve performance. The truncation length can be customized.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70d2364ded6e43549eb1bee01aba658b~tplv-goo7wpa0wc-image.image) </span>
