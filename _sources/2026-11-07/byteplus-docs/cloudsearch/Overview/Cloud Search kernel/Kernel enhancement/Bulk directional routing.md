---
title: "Bulk directional routing"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Bulk_directional_routing"
---

During bulk writes, instance write requests are routed to different shards for execution based on default routing rules. In scenarios with a large number of instance nodes or indexes containing numerous shards, write long\-tail effects are prone to occur. This will lead to slow bulk request responses and queue buildup.

You can enable bulk directional routing by setting the configuration `index.shard_routing.enabled`. Once enabled, bulk write requests will be randomly routed to a single shard to mitigate write long\-tail effects.

<span id="2562aaca"></span>
## Background

The default value of the configuration `index.shard_routing.enabled` is `false`, which means using the default routing rule, that is, using `_id` as the routing for single document writes; setting it to **true** enables bulk directional routing and prevents write long\-tail effects.

Enabling bulk directional routing in scenarios with a large number of instance nodes or indices containing numerous shards can improve consumption rate, reduce cluster load and decrease write rejection frequency.

<span id="a4d3762e"></span>
## Functional limitations


* Currently, only Elasticsearch 7.10.2 instances created after October 2023 and OpenSearch 2.9.0 instances support turning on bulk directional routing.

* The configuration `index.shard_routing.enabled` only takes effect when the written data does not include a primary key.

* When bulk directional routing is enabled, doc information cannot be obtained from `_id` directly.

* When bulk directional routing is enabled, deletebyquery and updatebyquery operations are not supported.


<span id="87852a9f"></span>
## Enabling bulk directional routing

You can set the `index.shard_routing.enabled` configuration at index creation or update the `index.shard_routing.enabled` configuration dynamically after creating the index.


* Enabling bulk directional routing during index creation

   ```HTTP
   PUT <index-name>
   {
     "settings": { 
       "index.shard_routing.enabled": true
     } 
   }
   ```
   

* Updating bulk directional routing configuration dynamically

   ```HTTP
   PUT <index-name>/_settings
   {
      "index.shard_routing.enabled": true
   }
   ```
   


<span id="44cb2635"></span>
## FAQs


* After enabling adaptive write optimization, why can't documents be retrieved directly using `_id`?

   After enabling adaptive write optimization, bulk write operations automatically route to higher\-performance shards. Then the fixed mapping between `_id` and shards will no longer exist. At this time, document retrieval by `_id` requires explicit routing values to locate the original document. The routing value can be obtained through standard query operations.

* Why does enabling adaptive write optimization fail?

   Only instances that meet specific requirements support turning on adaptive write optimization. For detailed requirements, refer to [Functional limitations](https://docs.byteplus.com/docs/cloudsearch/Adaptive_write_optimization#119ff7bf).

   If you encounter any other issues during operation, [submit a ticket](https://console.byteplus.com/workorder/create/?step=1) for technical assistance.
