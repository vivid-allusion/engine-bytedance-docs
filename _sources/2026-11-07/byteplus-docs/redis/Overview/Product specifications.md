---
title: "Product specifications"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/product-specification"
---

This topic describes the instance specifications and performance of Cache for Redis.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For detailed prices of instances of various specifications, refer to  <a href="https://docs.byteplus.com/en/docs/redis/billing-item-price">Billing items and prices</a>.</div>


<span id=".5LiN5ZCv55So5YiG54mH6ZuG576k55qE5a6e5L6L6KeE5qC8"></span>
## Specifications of instances with sharding cluster disabled

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only the primary\-secondary instances support the use of 256 MiB node specification. The single\-node instance does not support it.</div>



|Node specification |Memory (GiB) |Default bandwidth (MB/s) |Default max connections |New connections per second limit |QPS reference value |
|---|---|---|---|---|---|
|256 MiB |0.25 |24 |10,000 |10,000 |100,000 |
|512 MiB |0.5 |24 |10,000 |10,000 |100,000 |
|1 GiB |1 |48 |10,000 |10,000 |100,000 |
|2 GiB |2 |96 |10,000 |10,000 |100,000 |
|4 GiB |4 |96 |10,000 |10,000 |100,000 |
|8 GiB |8 |96 |10,000 |10,000 |100,000 |
|16 GiB |16 |96 |10,000 |10,000 |100,000 |
|24 GiB |24 |96 |10,000 |10,000 |100,000 |
|32 GiB |32 |96 |10,000 |10,000 |100,000 |
|64 GiB |64 |96 |10,000 |10,000 |100,000 |


<span id=".5ZCv55So5YiG54mH6ZuG576k55qE5a6e5L6L6KeE5qC8"></span>
## Specifications of instances with sharding cluster enabled

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The table lists the memory, bandwidth, max connections, new connections per second limit and QPS reference value for a single shard in the instance.</div>



|Node specification |Memory (GiB) |Default bandwidth (MB/s) |Default max connections |maximum number of new connections per second |QPS reference value |
|---|---|---|---|---|---|
|1 GiB |1 |48 |10,000 |10,000 |100,000 |
|2 GiB |2 |96 |10,000 |10,000 |100,000 |
|4 GiB |4 |96 |10,000 |10,000 |100,000 |
|8 GiB |8 |96 |10,000 |10,000 |100,000 |
|16 GiB |16 |96 |10,000 |10,000 |100,000 |


<span id=".5oCn6IO96K-05piO"></span>
## Performance description

<span id=".5bim5a696K-05piO"></span>
### Bandwidth description


* The **Default bandwidth** in the above table is applied to both the read bandwidth (i.e., downstream bandwidth) and the write bandwidth (i.e., upstream bandwidth). For example, if the default bandwidth of a certain specification is 10 MB/s, then the default read and write bandwidths of the instance with this specification are both 10 MB/s.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the instance bandwidth cannot meet the peak service traffic requirements (such as time\-limited flash sales), you can easily cope with traffic peaks by increasing the read and write bandwidth of the instance separately without changing the instance specifications. For specific procedures, see <a href="https://docs.byteplus.com/en/docs/redis/modify-bandwidth">Modifying bandwidth</a>.   </div>
   

* **The overall bandwidth of a Redis instance cannot exceed 2.5 GB/s**. Therefore, the upper limit of the overall bandwidth of an instance = min[(number of shards x upper limit of bandwidth for a single shard), 2.5 GB/s]. For more details, refer to [Bandwidth modification range](https://docs.byteplus.com/en/docs/redis/modify-bandwidth).

* The Cache for Redis supports a bandwidth throttling mechanism. When the business traffic exceeds the **Default bandwidth** of the instance, bandwidth throttling will be triggered.  If bandwidth throttling occurs, you can solve it by manually adjusting the bandwidth, optimizing large/hot keys, setting read\-write separation, or expanding the instance, etc. For more details, refer to [Suggestions for reasonable instance bandwidth](https://docs.byteplus.com/en/docs/redis/bandwidth-suggestion).


<span id=".6L-e5o6l5pWw6K-05piO"></span>
### Connection number description


* The default connection number of each Redis single shard for all specifications is 10,000, and **the overall number of connections of an instance cannot exceed 1,000,000 at most**. Therefore, the upper limit of the overall number of connections of an instance = min[(number of shards × maximum number of connections of a single shard), 1,000,000].

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also modify the maximum number of single sharding connections according to your business needs, with a maximum support of 50,000. For specific procedures, see <a href="https://docs.byteplus.com/en/docs/redis/modify-max-conn-number">Modifying maximum number of connections</a>.   </div>
   

* The maximum number of new connections per second for each specification of Redis single sharding is 10,000, and the **maximum number of new connections per second for the entire instance cannot exceed 200,000 ** . Therefore, the maximum number of new connections per second for the entire instance = min [ (number of shardings x maximum number of new connections per second for single shardings), 200,000].

* The actual number of connections that can be established during the operation of an instance will be affected by both the maximum connection number and the upper limit of the newly established connections per second.

   For example, for a Redis instance with a 2\-shard cluster enabled, if the maximum connection number of a single shard is increased to 20,000 (i.e., the overall upper limit of the maximum connection number of the instance is 40,000), and the upper limit of the newly established connections per second of the instance is 20,000, the actual number of connections that can be established in different situations is as follows:

   * If the actual connection number of the instance at the nth second is 12,000, then the maximum connection number at the n + 1th second can only be 32,000 (i.e., 12,000 + 20,000).

   * If the actual connection number of the instance at the nth second is 32,000, then the maximum connection number at the n + 1th second can only be 40,000 (32,000 + 20,000 \> 40,000).

* After the maximum number of connections is reached, the system will refuse to create new connections.


<span id=".cXBzLeivtOaYjg=="></span>
### QPS description

The QPS values in the above table are all reference values for the QPS of a single shard. Due to the single\-threaded mechanism of Redis natively, there is not much difference in the read\-write performance of the QPS of normal keys in a single shard. Therefore, the reference values of the QPS of a single shard for Redis instances of different specifications are the same.

<span id=".5a6e5L6L5pW05L2T5oCn6IO96K-05piO56S65L6L"></span>
### Example of overall performance description for instance


|Instance type |Performance description |
|---|---|
|Instances with sharding cluster disabled |The overall performance of the instance is consistent with the corresponding performance in the instance node specification table. |
|Instances with sharding cluster enabled |Each shard in the same instance has the same specification and performance. Therefore, the overall performance of the instance = the number of shards × the performance corresponding to the specification of each shard.<br><br>Among them, the performance of each shard:<br><br><br>* **Memory**: 1 GiB.<br><br>* **Bandwidth**: 32 MB/s.<br><br>* **Maximum connections**: 10,000.<br><br>* **New connections per second limit**: 10,000.<br><br>* **QPS reference value**: 100,000.<br><br><br>Then, for a Redis instance with 4 shards, the overall performance is as follows:<br><br><br>* **Memory ** : 4 GiB.<br><br>* **Bandwidth**: 128 MB/s.<br><br>* **Maximum connections**: 40,000.<br><br>* **New connections per second limit**: 40,000.<br><br>* **QPS reference value**: 400,000. |
