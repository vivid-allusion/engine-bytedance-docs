---
title: "Billing items and prices"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/billing-item-price"
---

This topic describes the billing items and price details for Cache for Redis.

<span id=".6K6h6LS56aG55qaC6KeI"></span>
## Billing items

The following billing items are involved when using Cache for Redis.

For more information about billing methods, refer to [Pay-as-you-go](https://docs.byteplus.com/en/docs/redis/pay-as-you-go) and [Subscription](https://docs.byteplus.com/en/docs/redis/subscription).


|Billing items |Supported billing methods |Billing rules |
|---|---|---|
|Instance server node |* Pay\-as\-you\-go<br><br>* Subscription |* Charges are incurred based on the node specification, billing type, and purchase or usage time you selected when you created the Redis instance. For specific procedures, refer to [Creating instance](https://docs.byteplus.com/en/docs/redis/create-instance).<br><br>* For more details on server node billing rules and pricing, refer to [Instance server nodes billing rules](https://docs.byteplus.com/en/docs/redis/billing-item-price#.5a6e5L6L5pWw5o2u6IqC54K56K6h6LS56KeE5YiZ). |
|(Optional) Additional bandwidth |Pay\-as\-you\-go |* If the default bandwidth of the instance cannot meet the peak demand for business traffic (such as time\-limited seckill activities), you can increase the instance read and write bandwidth separately without changing the instance specifications. After the bandwidth is increased, the additional bandwidth you choose will be charged according to the size and use time. For specific procedures, refer to [Modifying bandwidth](https://docs.byteplus.com/en/docs/redis/modify-bandwidth).<br><br>* For more details on additional bandwidth billing rules and pricing, refer to [Additional bandwidth billing rules](https://docs.byteplus.com/en/docs/redis/billing-item-price#.6aKd5aSW5bim5a696K6h6LS56KeE5YiZ).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Cache for Redis has officially started billing for additional bandwidth. For details on the billing start time and regions, refer to <a href="https://docs.byteplus.com/en/docs/redis/additional_bandwidth_is_officially_billed">Additional bandwidth is officially billed</a>.</div><br> |


<span id=".5a6e5L6L5pWw5o2u6IqC54K56K6h6LS56KeE5YiZ"></span>
## Instance server node billing rules

<span id=".5Lu35qC86KGo"></span>
### Price table

Cache for Redis supports two types of instances: those with sharding cluster enabled and those with sharding cluster disabled. The prices for different instance types vary across regions.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The prices in the table are for a single server node in a single shard in the instance.</div>


* <div data-tips="true" data-tips-type="tip">For more information on price calculation, refer to <a href="https://www.byteplus.com/en/pricing?product=veDB_for_Redis&tab=2">Redis price calculator</a>.</div>


* <div data-tips="true" data-tips-type="tip">Only instances with Redis 7.0 database version can select direct connection mode without enabling shard cluster feature. The direct connection feature without shard cluster enabled is currently an allowlist feature. To use it, <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> to apply.</div>




<Tabs>
<Tab zoneid="QSmGNrZPgk" title="Instances with shard cluster enabled (Proxy connection mode)">
<TabTitle>Instances with shard cluster enabled (Proxy connection mode)</TabTitle>


|Region |**Pay\-as\-you\-go billing (USD/GiB/hour)**  |**Subscription billing (USD/GiB/month)**  |
|---|---|---|
|* China (Guangzhou)<br><br>* China (Beijing)<br><br>* China (Shanghai) |0.0129 |6.1908 |
|China (Hong Kong) |0.0175 |8.3571 |
|Asia Pacific (Johor) |0.0170 |8.0000 |
|Asia Pacific (Jakarta) |0.0173 |8.3204 |





</Tab>
<Tab zoneid="HkvFiK7qSK" title="Instances with shard cluster disabled (Proxy connection mode)">
<TabTitle>Instances with shard cluster disabled (Proxy connection mode)</TabTitle>


|Region |**Pay\-as\-you\-go billing (USD/GiB/hour)**  |**Subscription billing (USD/GiB/month)**  |
|---|---|---|
|* China (Guangzhou)<br><br>* China (Beijing)<br><br>* China (Shanghai) |0.0114 |5.5029 |
|China (Hong Kong) |0.0154 |7.4286 |
|Asia Pacific (Johor) |0.0150 |7.0600 |
|Asia Pacific (Jakarta) |0.0149 |7.1318 |





</Tab>
<Tab zoneid="yRXMMp1fXo" title="Instances with shard cluster disabled (Direct connection address)">
<TabTitle>Instances with shard cluster disabled (Direct connection address)</TabTitle>


|Region |**Pay\-as\-you\-go billing (USD/GiB/hour)**  |**Subscription billing (USD/GiB/month)**  |
|---|---|---|
|* China (Guangzhou)<br><br>* China (Beijing)<br><br>* China (Shanghai) |0.0114 |5.4783<br><br> |
|China (Hong Kong) |0.0148 |7.1217 |
|Asia Pacific (Johor) |0.0152 |7.2861 |
|Asia Pacific (Jakarta) |0.0153 |7.3628 |





</Tab>
</Tabs>


<span id=".6LS555So6K6h566X5YWs5byP"></span>
### Calculation method

Instance server node payment = Price of stand\-alone server node x Memory size x Number of nodes x Number of shards x Duration

<span id=".6aKd5aSW5bim5a696K6h6LS56KeE5YiZ"></span>
## Additional bandwidth billing rules

<span id=".5Lu35qC86KGo"></span>
### Price table

If the default bandwidth of the instance cannot meet the peak demand for business traffic (such as time\-limited seckill activities), you can increase the instance read and write bandwidth separately without changing the instance specifications. After the bandwidth is increased, the additional bandwidth you choose will be charged according to the size and use time. For specific procedures, refer to [Modifying bandwidth](https://docs.byteplus.com/en/docs/redis/modify-bandwidth).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Additional bandwidth is billed on a gradient basis, meaning that the unit price of the bandwidth will increase as the amount of additional bandwidth increases. Plan your bandwidth usage reasonably. For more details, refer to <a href="https://docs.byteplus.com/en/docs/redis/bandwidth-suggestion">Efficient bandwidth usage guide</a>.</div>


* <div data-tips="true" data-tips-type="tip">The prices in the table are all for the additional bandwidth of <strong>a single server node in a single shard</strong> in the instance. For details on the default bandwidth of each node specification for Redis instances, refer to <a href="https://docs.byteplus.com/en/docs/redis/product-specification">Instance specifications</a>.</div>


* <div data-tips="true" data-tips-type="tip">For more information on price calculation, refer to <a href="https://www.byteplus.com/en/pricing?product=veDB_for_Redis&tab=2">Redis price calculator</a>.</div>




<Tabs>
<Tab zoneid="JL2uDDgSgZ" title="Additional read bandwidth price">
<TabTitle>Additional read bandwidth price</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The default maximum additional read bandwidth displayed on the Redis console is 512 MB/s. If you need to increase the allowed maximum additional read bandwidth, <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> to contact technical support for an application.</div>



|Range of read bandwidth (MB/s) |Prices in Chinese regions (USD/MB/s/hour/shard/node) ||Prices in overseas regions (USD/MB/s/hour/shard/node) ||Prices in Chinese regions (USD/MB/s/hour/shard/node) ||Prices in overseas regions (USD/MB/s/hour/shard/node) ||
|---|---|---|---|---|---|---|---|---|
||Mainland China |China (Hong Kong) |Asia Pacific (Johor) |Asia Pacific (Jakarta) |**Mainland China** |**China (Hong Kong)**  |**Asia Pacific (Johor)**  |**Asia Pacific (Jakarta)**  |
|Default read bandwidth for each node spec ~ 288 |0.0050 |0.0066 |0.0061 |0.0058 |0.0007 |0.0007 |0.0009 |0.0008 |
|289 ~ 576 |0.0066 |0.0084 |0.0080 |0.0075 |0.0009 |0.0009 |0.0011 |0.0010 |
|577 ~ 1152 |0.0091 |0.0117 |0.0110 |0.0104 |0.0013 |0.0013 |0.0016 |0.0014 |
|\> 1152 |0.0126 |0.0162 |0.0153 |0.0144 |0.0018 |0.0018 |0.0022 |0.0020 |





</Tab>
<Tab zoneid="Jq8VuDWreH" title="Additional write bandwidth price">
<TabTitle>Additional write bandwidth price</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The default maximum additional write bandwidth displayed on the Redis console is 288 MB/s. If you need to increase the allowed maximum additional write bandwidth, <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> to contact technical support for an application.</div>



|Range of write bandwidth (MB/s)<br><br> |Prices in Chinese regions (USD/MB/s/hour/shard/node) ||Prices in overseas regions (USD/MB/s/hour/shard/node) ||Prices in Chinese regions (USD/MB/s/hour/shard/node) ||Prices in overseas regions (USD/MB/s/hour/shard/node) ||
|---|---|---|---|---|---|---|---|---|
||Mainland China |China (Hong Kong) |Asia Pacific (Johor) |Asia Pacific (Jakarta) |**Mainland China** |**China (Hong Kong)**  |**Asia Pacific (Johor)**  |**Asia Pacific (Jakarta)**  |
|Default write bandwidth for each node spec ~ 192 |0.0094 |0.0121 |0.0115 |0.0108 |0.0013 |0.0013 |0.0016 |0.0013 |
|193 ~ 384 |0.0131 |0.0168 |0.0159 |0.0149 |0.0019 |0.0019 |0.0022 |0.0019 |
|\> 384 |0.0181 |0.0233 |0.0220 |0.0207 |0.0026 |0.0026 |0.0031 |0.0026 |





</Tab>
</Tabs>


<span id=".6LS555So6K6h566X5YWs5byP"></span>
### Calculation method

Additional bandwidth payment = Bandwidth price of a single server node in a single shard × Additional bandwidth size x Number of nodes × Number of shardings × Duration

<span id=".5paw5bu65a6e5L6L6LSt5Lmw56S65L6L"></span>
## New instance purchase example

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following purchase examples do not consider any product discounts or variants, and are only used as an example purchase reference. The specific purchase fee is subject to the actual order result of the console.</div>



|Instance type |Billing method |Scenario |Payment due |
|---|---|---|---|
|Sharding cluster disabled |Subscription |Purchase a new Redis instance with the following configuration:<br><br><br>* Region: China (Beijing)<br><br>* Number of shards: 1<br><br>* Memory specification per shard: 2 GiB<br><br>* Number of nodes in a single shard: 3<br><br>* Purchase duration: 1 month |5.5029 USD/GiB/month/node × 3 nodes/shard × 2 GiB × 1 shard × 1 month = 33.0174 USD |
|Sharding cluster enabled |Pay\-as\-you\-go |Purchase a new Redis instance with the following configuration:<br><br><br>* Region: China (Beijing)<br><br>* Number of shards: 4<br><br>* Memory specification per shard: 4 GiB<br><br>* Number of nodes in a single shard: 2<br><br>* Usage duration: 720 hours (that is 30 days) |0.0129 USD/GiB/hour/node × 2 nodes/shard × 4 GiB × 4 shards × 720 hours = 297.216 USD |
