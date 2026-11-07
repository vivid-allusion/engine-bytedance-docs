---
title: "Efficient bandwidth usage guide"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/bandwidth-suggestion"
---

As a caching database, Redis often performs numerous data access tasks, which consume substantial network bandwidth. Different Redis instance specifications come with varying default bandwidths. When service traffic exceeds the default bandwidth of an instance, the data access performance of application services can be affected. This topic puts forward some suggestions for improvement to ensure the optimum use of instance bandwidth for your reference.

<span id=".5bim5a696Zeu6aKY5b2x5ZON"></span>
## Impact of bandwidth issues

Cache for Redis supports a bandwidth throttling mechanism. When service traffic exceeds the default bandwidth of an instance, the system accumulates the excess bandwidth per second. If this accumulation persists for an extended length of time, it may lead to client timeouts and impact service data access performance (for example, an increase in **P99 request response latency** or **Maximum request response latency**), or an error message such as `Error reading from the server: Connection reset by peer` when writing data. Once the service traffic drops below the default bandwidth limit, the previously accumulated traffic is automatically processed by the Redis server nodes

<span id=".5bim5a695L2_55So5bu66K6u"></span>
## Bandwidth usage recommendations

<span id=".5bim5a6955uR5o6n5ZKM5ZGK6K2m"></span>
### Bandwidth monitoring and alerts

Cache for Redis supports visual display of performance monitoring data on different nodes of the instance. To help you fully understand bandwidth usage by instance, quickly locate issues related to bandwidth utilization, and avoid performance issues caused by bandwidth throttling, we recommend that you pay close attention to two performance metrics **Network input bandwidth utilization rate** and **Network output bandwidth utilization rate**.

In addition, we recommend that you set the alert trigger threshold for both metrics at or above 80%, which means that an alert will be triggered when the bandwidth utilization rate is greater than or equal to 80% during the monitoring period, allowing you to detect any upward trend in bandwidth usage in a timely manner and avoid triggering bandwidth throttling.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For details about monitoring metrics, refer to <a href="https://docs.byteplus.com/en/docs/redis/monitoring-metric">Monitoring metrics</a>.</div>


* <div data-tips="true" data-tips-type="tip">To view monitoring data and set alerts, refer to <a href="https://docs.byteplus.com/en/docs/redis/view-monitoring-data">Viewing monitoring data</a> and <a href="https://docs.byteplus.com/en/docs/redis/set-alert">Setting alerts</a>.</div>



<span id=".5omL5Yqo6LCD5pW05a6e5L6L5bim5a69"></span>
### Manually adjusting bandwidth

Cache for Redis supports adding read and write bandwidth to individual instances without changing the instance specification. Adding bandwidth does not affect businesses and allows you more time to troubleshoot problems without substantially affecting online businesses. For specific procedures, refer to [Modifying bandwidth](https://docs.byteplus.com/en/docs/redis/modify-bandwidth).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The bandwidth modification feature is available only with instances created after May 25, 2023. If you need to modify the shard bandwidth instance created before May 25, 2023, you must first create a new instance and use this feature on the new instance. You can use tools such as DTS to migrate the data of old instances to new instances. For the specific steps, refer to <a href="https://docs.byteplus.com/en/docs/redis/data-migration">Data migration</a>.</div>


* <div data-tips="true" data-tips-type="tip">For details on the cost of additional bandwidth,  refer to Billing rules for additional bandwidth.</div>



<span id=".5a-55aSnLWtleeOAgeeDrS1rZXkt6L-b6KGM6ZKI5a-55oCn5LyY5YyW"></span>
### Optimizing big keys and hot keys

Big keys and hot keys cause high CPU usage and bandwidth consumption, resulting in unbalanced instance load and data skew issues, causing other queries to time out and become inaccessible. This not only weakens Redis performance, but also affects other services or applications on the server.

Therefore, when the service traffic volume is not balanced with the expected bandwidth consumption (for example, when the trend in bandwidth utilization deviates significantly from changes in read and write QPS), you can use such features as [Big key analysis](https://docs.byteplus.com/en/docs/redis/big-key-analysis), [Hot key analysis](https://docs.byteplus.com/en/docs/redis/hot-key-analysis), and [RDB analysis](https://docs.byteplus.com/en/docs/redis/rdb-analysis) to quickly identify the big keys and hot keys in the instance, understand relevant information such as memory usage, distribution, and expiry time of keys, and optimize the big keys or hot keys according to the analysis results. For example, you can distribute the hot keys to different servers, split the big keys, reduce access to the big keys, or delete unnecessary big keys.

<span id=".6K6-572u6K-75YaZ5YiG56a7"></span>
### Setting read/write splitting

Cache for Redis sends all read and write requests to the primary node by default, but when low **Network input bandwidth utilization rate** occurs along with high **Network output bandwidth utilization rate**, it indicates that there are fewer write requests and more read requests in the instance, which puts considerable pressure on the read bandwidth of the primary node. You can also enable the instance read/write splitting mode (set the value of the read/write splitting parameter as `read_primary_node_and_secondary_nodes` or `read_secondary_nodes_only`) and send some or all read requests to the secondary nodes, which will reduce the read bandwidth pressure of the primary node. For specific procedures, refer to [Setting read/write splitting](https://docs.byteplus.com/en/docs/redis/set-read-write-splitting).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Only primary\-secondary instances support the read/write splitting mode. Single\-node instances only contain a primary node and do not support read/write splitting. For more information on the different architectures and supported functional features of the two types of instances, refer to <a href="https://docs.byteplus.com/en/docs/redis/product-component-architecture">Product architecture</a> and <a href="https://docs.byteplus.com/en/docs/redis/feature-faq">Feature differences</a>.</div>


* <div data-tips="true" data-tips-type="tip">When the read/write splitting mode is enabled, dirty data may be read, so it is not advisable to enable the read/write splitting mode when relatively high data consistency is required.</div>



<span id=".5omp5a655a6e5L6L5Yy56YWN5Lia5Yqh6LSf6L29"></span>
### Scaling up instances to match service load

If bandwidth utilization remains high after these optimization precautions are implemented, you need to evaluate whether you need to scale up vertically (by upgrading node specifications) or horizontally (by increasing the number of shards) to match your business load. You can choose the appropriate upscaling solution according to the instance architecture:


* **Instances with sharding cluster enabled**

   You can choose to increase the overall bandwidth of the instance by either [upgrading node specifications](https://docs.byteplus.com/en/docs/redis/modify-node-spec) (increasing the bandwidth of a single shard) or [increasing the number of shards](https://docs.byteplus.com/en/docs/redis/modify-shard--number) (increasing the total bandwidth of the instance).

* **Instances with sharding cluster disabled**

   Instances with sharding cluster disabled only contain one shard, so instance bandwidth can be increased only by [upgrading node specifications](https://docs.byteplus.com/en/docs/redis/modify-node-spec).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before formally modifying the instance configuration, we recommend that you purchase a Pay\-as\-you\-go instance to test whether the upgraded target configuration meets the business load requirements. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/redis/delete-instance">Deleting instance</a>.</div>
