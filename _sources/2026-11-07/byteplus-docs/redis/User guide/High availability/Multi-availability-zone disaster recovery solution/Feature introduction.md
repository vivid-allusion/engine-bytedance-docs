---
title: "Feature introduction"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/feature-introduction"
---

Cache for Redis supports setting multi\-availability zone deployment when creating or restoring data to a new instance. Compared to single availability zone deployment, multi availability zone deployment has higher disaster recovery capability and can withstand server room level failures.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

Only **primary\-secondary** instances support multi\-availability zone deployment, while single\-node instances only support single availability zone deployment. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).

<span id=".5Y-v55So5Yy66YOo572y5pa55qGI"></span>
## Availability zone deployment solution

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Cache for Redis supports close\-by access for multi\-availability zone instances. Once this feature is enabled, read requests will be directed to the node in the availability zone closest to the requesting client, reducing the latency of accessing Redis services. For more details, refer to <a href="https://docs.byteplus.com/en/docs/redis/read-local-node-only">Setting read local node only</a>.</div>


<span id=".5bey5ZCv55So5YiG54mH6ZuG576k5a6e5L6L"></span>
### Instances with sharding cluster enabled


|Deployment plan |Disaster recovery description |Node deployment policy |
|---|---|---|
|Multi\-availability zone deployment |A failure in a given availability zone will only result in the loss of node data in that zone. For more details about failover, refer to [Failover](https://docs.byteplus.com/en/docs/redis/failover). |When using multiple\-availability zone deployment, you can specify the availability zones individually for each node in a single shard, after which the nodes with the same roles in all the shards of the instance will be distributed in the corresponding availability zones. The availability zone deployment architecture diagram is shown below.<br><br> <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2e4d6a901c0f14bc3a6b5ba3a0647b4f.png) </span> |
|Single availability zone deployment |All nodes are located in the same availability zone and when a catastrophic failure occurs in the availability zone, the instance will lose all cached data. |All nodes contained in all the shards in the instance will be deployed in the same availability zone. The deployment architecture flowchart of the availability zone is shown as follows.<br><br><span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_37300a68d110a5b9c88fbf5ecefa4588.jpeg) </span> |


<span id=".5pyq5ZCv55So5YiG54mH6ZuG576k5a6e5L6L"></span>
### Instances with sharding cluster disabled


|Deployment plan |Disaster recovery description |Node deployment policy |
|---|---|---|
|Multi\-availability zone deployment |A failure in a given availability zone will only result in the loss of node data in that zone. For more details about failover, refer to [Failover](https://docs.byteplus.com/en/docs/redis/failover). |When using multiple\-availability zones deployment, you can specify the availability zones individually for each node in a single shard. The availability zone deployment architecture diagram is shown below. <br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9e0b58d09ca50c9bdbf17e2d8e386e37.png) </span> |
|Single availability zone deployment |All nodes are located in the same availability zone and when a catastrophic failure occurs in the availability zone, the instance will lose all cached data. |All nodes in the instance are deployed in the same availability zone. The deployment architecture flowchart of the availability zone is shown as follows.<br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_508fb9e6ea3647b7da9a83cac2a020ff.png) </span> |
