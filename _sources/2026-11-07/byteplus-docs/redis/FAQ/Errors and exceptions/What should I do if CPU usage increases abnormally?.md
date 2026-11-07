---
title: "What should I do if CPU usage increases abnormally?"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/what-should-I-do-if-cpu-usage-increases-abnormally"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Problem phenomenon

When viewing Redis monitoring data, the **CPU usage** monitoring metric for instance server nodes and proxy nodes is abnormally elevated.

<span id=".5o6S5p-l5q2l6aqk"></span>
## Troubleshooting step

When the business traffic is too high or the traffic is uneven, the CPU usage monitoring indicator of the instance will increase abnormally. You can refer to the following steps to locate the cause of the problem and solve the corresponding problem.


|Troubleshooting step |Solutions |
|---|---|
|1. Unbalanced business traffic |View the **CPU usage** monitoring metrics of server nodes and proxy nodes in Redis instances, whether only some server nodes or proxy nodes have abnormal increases in monitoring metrics.<br><br>If there is an abnormal increase in some node monitoring indicators, it means that business traffic is concentrated in these nodes. Then refer to the following methods to try to solve them:<br><br><br>* Uneven server node traffic:<br><br>   * Business transformation. You can use [Hot key analysis](https://docs.byteplus.com/en/docs/redis/hot-key-analysis) function to help quickly discover hot keys in an instance, understand the key's occupancy, distribution, expiration time, and other information in memory, and do targeted optimization of hot keys based on the analysis results. For example, distribute hot keys to different servers.<br><br>   * Vertical upscaling. That is to increase the number of instances of sharding, the traffic will be distributed to more shards, to reduce the traffic carried on a single shard. For specific procedures, refer to [Increasing the number of shards](https://docs.byteplus.com/en/docs/redis/modify-shard--number).<br><br>* Uneven proxy node traffic:<br><br>   * When there are many long connections in the business, confirm whether there is only some client side traffic or whether there are actions such as instance configuration (such as increasing the number of sharding), these situations will lead to uneven traffic. Then it is recommended to balance the business side by adding more connections or reconnecting.<br><br>   * When most of the connections used in the business are short, but there is still uneven traffic on the proxy node, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support. |
|2. Business traffic is too high |View whether the **Total**  **QPS** indicator of the proxy node in the Redis instance is too large. If the value is too large, it indicates that the business traffic may be too high.<br><br>If the traffic is too high, it is recommended to horizontally expand instances (that is, increase the number of sharding instances) to distribute the traffic to more shards to reduce the traffic carried on a single shard. For specific procedures, refer to [Increasing the number of shards](https://docs.byteplus.com/en/docs/redis/modify-shard--number). |
|3. Other scenarios |If the CPU usage is still high after the above optimization, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support. |
