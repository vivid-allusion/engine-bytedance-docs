---
title: "Performance guide"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/performance_guide"
---

The service performance of data transformation is related to factors such as data volume and rule complexity. This topic describes various factors that may affect data transformation performance to facilitate troubleshooting performance issues during data transformation.

<span id="性能影响因素"></span>
## Factors

Based on how data transformation works, the overall rate of data transformation tasks mainly depends on the following factors:


* Write speed of a target topic: The number of shards in the target topic determines the data write speed.

* Capability of a source topic for concurrent transformation: The number of read and write shards of the source topic determines its overall capability for concurrent transformation. You can plan the number of shards based on the general traffic processing speed of each shard: 1 MiB/s (before compression). For example, if the data write speed of the source topic is 10 MiB/s, you should split the shard in the source log into 10 shards based on the following: 10 MiB / 1 MiB = 10.

* Complexity of a transformation rule: The logic and complexity of a transformation rule configured by a user can affect the data transformation rate. They are reflected in the following aspects.



|Aspect |Description |
|---|---|
|Output log volume |A transformation rule can specify the output mode used after log data processing. The size and number of output logs can affect the data transformation rate.<br><br>If data splitting occurs in transformation, the output content is longer when the number of output event fields is larger. When the number of output event fields is larger, the request for output consumes more computing power and network bandwidth, which ultimately leads to slow data transformation. |
|Number of output targets |A transformation rule can specify the targets to which transformed data is delivered. When the number of output targets is larger, the data transformation rate is lower.<br><br>When the system outputs data to more targets, more log groups (LogGroup) are in the output data packets. This results in more network interactions and slower transformation. |
|Transformation logic |Torch Log Service (TLS) supports various data transformation function syntax and logic. The complexity of transformation logic affects the data transformation rate.<br><br>When the configured transformation logic is more complex, TLS consumes more computing power, causing slower processing. |


<span id="性能提升方式"></span>
## Performance improvement methods

Besides making transformation rules less complex, you can accelerate processing by modifying your topic configuration.


* Source topic: The processing speed of the TLS data transformation feature can be enhanced by increasing the number of shards in the read and write status.

* Target topic:

   * We recommend that you evaluate the number of shards of the target topic to avoid affecting the overall log transformation rate due to the write limit of the target topic. The number of shards in the target topic is mainly evaluated based on the data write rate. The maximum write rate of a single shard in a topic is 5 MiB/s. The number of shards in the target topic can be estimated based on the number of shards in the source topic and the number of concurrent transformations. For example, if the source topic has 10 shards, specify at least 2 shards for the target topic.

   * You can also enable the auto shard splitting capability for the target topic. When you enable the capability and the write limit is frequently reached, a shard in the topic is automatically split. For more information on the capability, refer to [Automatic sharding](https://docs.byteplus.com/docs/tls/Managing_shards#%E8%87%AA%E5%8A%A8%E5%88%86%E8%A3%82%E5%88%86%E5%8C%BA).
