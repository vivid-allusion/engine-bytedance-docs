---
title: "View monitoring"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/View_monitoring"
---

Logstash is integrated with Cloud Monitor. You can view various monitoring metrics in the Cloud Search console or the Cloud Monitor console to analyze the running status of Logstash instances in real time, including information such as node resource usage and event rates. This topic describes how to view monitoring.

<span id="tV2ouIIL"></span>
## Operation steps


1. Log in to the [Cloud Search console](https://console.byteplus.com/es).

2. In the left\-side navigation pane, select **Data Processing** \> **Logstash**.

3. In the Logstash Instances list, click the name of the target instance. You are directed to the **Basic Information** tab.

4. In the left\-side navigation pane, select **Observability** \> **Monitoring Overview** to view the running status of the Logstash instance.

   
   |**Monitoring metrics** |**Statistical method** |**Note** |
   |---|---|---|
   |Node CPU usage |The average CPU usage of each node in the Logstash instance per minute. |This metric increases when the read and write tasks processed by instance nodes exceed the CPU load capacity. High node CPU usage can reduce the processing capabilities of the nodes or even cause downtime. Observe whether this metric is persistently high or has a temporary spike. If the spike is temporary, determine whether a complex task is running. |
   |Node JVM memory usage |The average JVM memory usage of all nodes in the instance over a 1\-minute period. |A high value can cause frequent garbage collection (GC) on the node, or even an out\-of\-memory (OOM) error. A high value usually indicates that the pipeline processing tasks on the node are exceeding the JVM's load capacity. Monitor the tasks running on the Logstash instance, or adjust its configuration. |
   |Node 1\-minute load |The 1\-minute average load of all nodes in the Logstash instance. Metric data source: Logstash node monitoring API `_node/stats/process?pretty`. |Upgrade the node specifications if this value is too high. For the procedure, refer to [Upgrade Logstash instances](https://docs.byteplus.com/en/docs/cloudsearch/Upgrade_a_Logstash_instance). |
   |Node disk usage |The average disk usage of each node in the Logstash instance per minute. |High disk usage prevents Logstash from working properly. You can expand the instance to increase the disk capacity per node. |
   |Events receive rate (events/sec) |The sum of the event reception rates of all nodes in the Logstash instance within a statistical period (1 second). |The total number of Events received per second by all pipelines on all nodes of the Logstash instance. |
   |Events sent rate (events/s) |The total number of Events sent per second from all nodes in the Logstash instance. |The total number of events sent per second by all pipelines on each node in the Logstash instance. |
   |Event processing latency |The average event processing latency of all nodes in the Logstash instance within the statistical period. |The average events processing latency of Logstash nodes. |
