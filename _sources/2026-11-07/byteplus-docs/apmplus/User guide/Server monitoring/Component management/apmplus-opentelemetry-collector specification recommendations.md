---
title: "apmplus-opentelemetry-collector specification recommendations"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Usage_specification_recommendations_for_the_apmplus-opentelemetry-collector_component"
---

<span id="rxkxYKww"></span>
#### **Background**

The OpenTelemetry Collector is a core component within the OpenTelemetry ecosystem. It collects, processes, and exports traces, metrics, and logs. On the VKE add\-on platform, we offer an enhanced OpenTelemetry Collector that is developed based on the community edition and supports quick deployment via a visual interface. To help users optimize resource allocation, we conducted rigorous performance stress testing to determine appropriate Collector specifications and replica counts.


---



<span id="mzaQS52m"></span>
#### **Objectives of stress testing**


1. **Performance evaluation**: Measure the collector's throughput, latency, and stability under varying loads to identify its processing capacity limits.

2. **Resource usage analysis**: Assess the collector's CPU and memory consumption across different workload scenarios.

3. **Cluster size planning**: Calculate the required replica count of the collector in production environments based on test results.



---



<span id="RUN0IHXE"></span>
#### **Results of stress testing**

The baseline data: When idle, the collector's CPU usage is about 0.25%, and memory usage is about 1.5%.


|**Specifications** |**Throughput (spans/s)**  |CPU |MEM |
|---|---|---|---|
|<div style="text-align: center"><br>1C2G</div><br> |4w |60% |4.5% |
||6w |90% |4.6% |
||7.3w |100% |5.8% |
|<div style="text-align: center"><br>2C2G</div><br> |9w |67% |3% |
||12w |86% |3% |
||14.5w |100% |3.8% |
|<div style="text-align: center"><br>4C4G</div><br> |16w |56% |1.8% |
||24w |83% |2% |
||29w |100% |2.5% |



1. **CPU consumption and throughput**: The collector's CPU consumption is linearly correlated with span throughput. The findings of the test are as follows:

   * A throughput of 10,000 spans per second consumes roughly 15% of a single CPU core.

   * The maximum data processing capacity of a single CPU core is approximately 70,000 spans per second.

2. **Memory usage**: The collector has low memory consumption, with memory utilization remaining below 6% even under high load.

3. **Stability**: No data loss or rejection occurred on the collector througout the entire test, demonstrating stable performance.



---



<span id="o1wN7t2r"></span>
#### **Usage recommendations**

Based on the test results and the complexity of production environments, the following specifications and throughput thresholds are recommended:


|**Specifications** |**Recommended throughput** |
|---|---|
|1C2G |4w/s |
|2C2G |8w/s |
|4C4G |18w/s |


To ensure service stability, we recommend maintaining CPU utilization below 80% whenever possible and reserving 20% to 50% replica redundancy.


---



<span id="kwBtr46e"></span>
#### **How to select an appropriate collector count**


1. **Estimate the cluster's span throughput**:

   * Method 1: Contact the APMPlus R&D team to query the current tenant's span throughput.

   * Method 2: Estimate span throughput based on business QPS. For example, if the overall QPS is 1,000, each request generates an average of 20 spans, and the instance count is 20, the total throughput is:


```Plain Text
1000/s * 20 * 20 = 40w/s
```



2. **Calculate the required instance count**:


According to the recommended ratio, a throughput of 400,000 span/s requires approximately 400,000 / 40,000 = 10 collector instances with the 1\-core 2GB (1C2G) specification. We recommend deploying 12 to 15 instances for redundancy. The same logic applies to instances of other specifications.


---



<span id="KuJLQdqn"></span>
#### **Conclusion**

The APMPlus OpenTelemetry Collector delivers stable performance in high\-load scenarios, with its performance primarily limited by CPU resources. You can select appropriate specifications and replica counts based on business requirements and span throughput to ensure data processing efficiency and system stability.
