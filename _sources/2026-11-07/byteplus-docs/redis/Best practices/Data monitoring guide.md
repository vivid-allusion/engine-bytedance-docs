---
title: "Data monitoring guide"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/data-monitoring-guide"
---

This topic introduces you to some monitoring metrics that merit particular attention for users of Cache for Redis. With these metrics, users can promptly address database performance and stability issues.

<span id=".55uR5o6n5oyH5qCH5YiG57G7"></span>
## Categories of monitoring metrics

Cache for Redis supports displaying monitoring data for individual or aggregated proxy nodes or data server nodes, which are categorized as follows: Where:


* **Proxy nodes and server nodes**

   * Proxy nodes are mainly used to implement database functions such as read/write splitting and load balancing. On proxy nodes, it is important to monitor metrics that affect database performance such as CPU usage, connection count, and QPS.

   * Server nodes, also known as server nodes, are the nodes that actually provide database services. On server nodes, it is important to monitor metrics such as CPU usage, memory usage, slow SQL queries, and usage of Keys.

* **Aggregated metrics and non\-aggregated metrics**

   * Aggregated metrics reflect the current state of the entire instance. We recommend that you prioritize checking aggregated metrics (such as CPU usage, memory usage, QPS, connection count, network input/output rates, etc.) to determine if the current load has exceeded the instance's capacity.

   * When the overall load of an instance is not high but the load of a single shard or node is high (for example, skewed data request volume and connection count), aggregated metrics may not detect any anomalies. In such cases, it is necessary to further examine non\-aggregated metrics. You can troubleshoot issues by examining whether any obvious abnormalities are observed in the monitoring metrics of individual shards or nodes.


<span id=".6ZyA6KaB5YWz5rOo55qE55uR5o6n5pWw5o2u"></span>
## Monitoring data that requires attention

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To promptly detect changes in important metrics, we recommend that you set up alert rules based on service requirements. For more information, refer to <a href="https://docs.byteplus.com/en/docs/redis/monitoring-metric">Monitoring and alerts</a>.</div>



|Category |Monitoring metrics |
|---|---|
|Performance |* Metrics such as QPS, CPU usage, and request response latency on proxy nodes.<br><br>* Metrics such as CPU usage on server nodes.<br><br><br>We recommend that you closely monitor instance CPU usage, as high usage can affect request response latency, potentially leading to errors such as IO timeouts upon submission of service requests. |
|Capacity |Metrics such as CPU usage on server nodes.<br><br>You can define the cache eviction policy by setting the value of the `maxmemory-policy` parameter. We recommend that you select a policy that suits your services to prevent memory capacity issues caused by an insufficiency of evictable keys. For more information on how to set the value of `maxmemory-policy`, refer to [Setting eviction upon expiration policy for keys](https://docs.byteplus.com/en/docs/redis/set-maxmemory-policy). |
|Connections |Metrics such as connections on proxy nodes.<br><br>Each Cache for Redis instance or shard in the instance defaults to providing 10,000 connections. Once the number of connections used reaches the maximum limit, the system will reject new connection requests. If you require more connections, you can modify the maximum connection limit. For specific procedures, refer to [Modifying maximum connections](https://docs.byteplus.com/en/docs/redis/modify-max-conn-number). |
|Bandwidth |Metrics such as network input bandwidth utilization, network output bandwidth utilization, peak input rate, peak output rate on server nodes.<br><br>High network input and output bandwidth utilization can affect request response latency and may even lead to errors such as IO timeouts. |
|Others |* Metrics such as key hit rate, number of expired or evicted keys on server nodes.<br><br>* Slow logs. For more information on slow logs, refer to [Querying slow logs](https://docs.byteplus.com/en/docs/redis/query-slow-log).<br><br>* Big keys, hot keys. For more information on big keys and hot keys, refer to [Big key analysis](https://docs.byteplus.com/en/docs/redis/big-key-analysis) and [Hot key analysis](https://docs.byteplus.com/en/docs/redis/hot-key-analysis). |
