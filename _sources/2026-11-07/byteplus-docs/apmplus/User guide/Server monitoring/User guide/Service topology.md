---
title: "Service topology"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Service_topology"
---

The global topology feature is based on trace data reported by the observability SDK integrated by users. It automatically extracts service nodes and their invocation relationships, rendering a global topology map in real time to visually display microservice dependencies and call chains.

Main highlights:


1. Real\-time: Based on real\-time trace data reporting, the global topology is quickly updated, providing a comprehensive view of service invocations at any time.

2. Automation: No manual configuration is required. As soon as a new service is integrated, it is immediately identified and included in the topology.

3. Visualization: Supports zooming, filtering, and time window switching, enabling multidimensional insights into complex invocation relationships.

4. Fault location: Exception nodes are intelligently highlighted, and invocation paths are precisely traced to quickly pinpoint the source of faults.

5. Performance optimization: Quantitatively counts the invocation frequency and latency of each service, making it easy to identify system bottlenecks at a glance.

6. Customizable: Flexibly configure topology simplification rules to aggregate similar nodes as needed, reduce graph density, and improve readability.


<span id="6y77nTsC"></span>
## Prerequisites

Services must integrate the Apmplus SDK or Opentelemetry SDK and report data to the APMPlus server side. For details, see the service integration section.

<span id="kjgN4HOu"></span>
## Feature introduction

<span id="4LY0ae3U"></span>
### Topology query


1. Log in to the APMPlus console, and in the left navigation bar, select **Service Monitoring \> Service topology.** 

2. Select the workspace and time range.


<span id="5c6CLK0h"></span>
### Service filter

Enter the service name keyword of interest in the top right. The query will return the single\-layer upstream and downstream topology relationships of services containing that keyword.

<span id="uOvcnKU2"></span>
### Topology simplification

Topology simplification is a technique for optimizing the visualization of distributed system topologies. By automatically or manually marking and aggregating nodes, it reduces the number of nodes in the topology and improves readability.

Aggregation rule list:

Supported specific node aggregation rules:


* Manual aggregation:

   * Regex matching: Batch match nodes using regular expressions. Nodes that match the sample regular expression will be aggregated and displayed as `kfztoutiao1`.

   * Manual grouping: Users select multiple nodes and specify a group name. Example: Service nodes that are manually checked will be aggregated and displayed as `manual-group`.

* Automatic aggregation: Currently, automatic aggregation supports the automatic classification and aggregation of nodes of the ip, mq, and db Type.


An ip Type node specifically refers to a node whose service name is in the format `192.168.0.1:8080`.

An mq Type node specifically refers to a node whose service Type is kafka, rocketmq, or other common message queues.

A db Type node specifically refers to a node whose service Type is MySQL, redis, or other common databases.

Different node Types also support aggregation at different levels of granularity. In ip aggregation mode, port\-level granularity is supported, while in mq and db aggregation modes, both URL\-level and type\-level granularity are supported:


   * Port\-level aggregation: IP nodes with the same port are merged into a virtual node (for example, \*\*:9090).

   * URL\-level aggregation: For example, `mysql@127.0.0.1:3306/db1` and `mysql@127.0.0.1:3306/db2` are aggregated into the **`mysql@127.0.0.1:3306`** node, displaying only the URL information of the db node.

   * Type\-level aggregation: For example, `mysql@127.0.0.1:3306/db1` and `mysql@127.0.0.1:3306/db2` are aggregated into the **`mysql`** node, displaying only the type information of the db node.
