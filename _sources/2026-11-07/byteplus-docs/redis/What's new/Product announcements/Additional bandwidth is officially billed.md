---
title: "Additional bandwidth is officially billed"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/additional_bandwidth_is_officially_billed"
---

Cache for Redis has officially billed for additional bandwidth.

<span id="billing-start-time-and-regions"></span>
## Billing start time and regions


|Billing region |Billing start time |
|---|---|
|Asia Pacific (Johor) |Billing started on July 2, 2024. |
|China (Guangzhou) |Billing started on July 4, 2024. |
|China (Beijing) |Billing started on July 8, 2024. |
|China (Shanghai) |Billing started on July 10, 2024. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Newly opened regions will automatically support billing for additional bandwidth from the service start date.</div>


<span id="billing-impact-range"></span>
## Billing impact range


|Bandwidth usage scenario |Billing explanation |
|---|---|
|Only using default bandwidth |No additional bandwidth billing is involved. |
|Having used additional bandwidth before official billing |* The additional bandwidth you used before official billing can still be used for free after official billing and will not be billed for the time being.<br><br>* After the additional bandwidth is officially billed, if you perform any of the following operations on **an instance that has already used additional bandwidth**, Redis will bill for the additional bandwidth:<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For details on the billing of additional bandwidth and specific prices, refer to <a href="https://docs.byteplus.com/en/docs/redis/billing-item-price">Billing items and prices</a>.   </div><br>   <br><br>* If the instance undergoes operations related to bandwidth changes, and the changed bandwidth is still greater than the default bandwidth or the total bandwidth of the instance has changed, then Redis will bill for the additional bandwidth.<br><br>   The following operations will cause the instance bandwidth to change:<br><br>   * [Modifying bandwidth](https://docs.byteplus.com/en/docs/redis/modify-bandwidth)<br><br>   * [Modifying the number of nodes](https://docs.byteplus.com/en/docs/redis/modify-node-number)<br><br>   * [Modifying the number of shards](https://docs.byteplus.com/en/docs/redis/modify-shard--number)<br><br>   * [Modifying node specifications](https://docs.byteplus.com/en/docs/redis/modify-node-spec)<br><br>   * [Modifying the sharding cluster configuration](https://docs.byteplus.com/en/docs/redis/modify-sharding-cluster-config)<br><br>* If you change the billing type of the instance (including [Switching to yearly or monthly subscription](https://docs.byteplus.com/en/docs/redis/switch-to-subscription) and [Switching to pay-as-you-go](https://docs.byteplus.com/en/docs/redis/switch-to-pay-as-you-go)), then Redis will bill for the additional bandwidth. |
|Needing to use additional bandwidth after official billing |Redis will bill for the additional bandwidth.<br><br>For details on the billing of additional bandwidth and specific prices, refer to [Billing items and prices](https://docs.byteplus.com/en/docs/redis/billing-item-price). |
