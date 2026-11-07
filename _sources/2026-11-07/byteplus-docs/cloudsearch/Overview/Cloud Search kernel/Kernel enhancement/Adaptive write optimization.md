---
title: "Adaptive write optimization"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Adaptive_write_optimization"
---

The cloud search service features adaptive write optimization. When enabled for non\-primary\-key update scenarios (e.g., log writing), the bulk write operation will automatically route to higher\-performance shards, thus improving write performance.

<span id="a065ebab"></span>
## Background

You can enable adaptive write optimization by configuring both `index.shard_routing.enabled` and `indices.bulk.adaptive_shard_selection.enabled`. Once enabled, bulk write requests can be automatically routed to higher\-performance shards, thereby improving overall write performance. Including: 


* `index.shard_routing.enabled`: determines whether bulk routing is enabled. The default value is `false`, which means the system uses the default routing rule, that is, by default `_id` is used as the routing for writing a single document. When set to `true`, it means that bulk directional routing is enabled, which can mitigate the long\-tail effect in writing. For more information, see [Bulk directional routing](https://docs.byteplus.com/docs/cloudsearch/Bulk_directional_routing).

* `indices.bulk.adaptive_shard_selection.enabled`: determines whether adaptive write optimization is enabled. The default value is `false`, which means it is disabled. When set to `true`, it means adaptive write optimization is enabled. During bulk writing, the system will automatically route to higher\-performance shards.


<span id="119ff7bf"></span>
## Functional limitations


* Currently, only the following instances support enabling adaptive write optimization:

   * Elasticsearch 7.10.2 instances created after May 2024.

   * OpenSearch 2.9.0 instances created after March 4, 2024.

* Adaptive write optimization takes effect only when the written data contains no primary keys and **both** the index configuration `index.shard_routing.enabled` and the cluster parameter `indices.bulk.adaptive_shard_selection.enabled` are enabled simultaneously.

* After enabling adaptive write optimization, documents cannot be retrieved directly using `_id`.

* After enabling adaptive write optimization, functions including `deletebyquery` and `updatebyquery` are not supported.


<span id="2ea12fcf"></span>
## Enable adaptive write optimization


1. Enable bulk directional routing for the target index. For detailed steps, see [Bulk directional routing](https://docs.byteplus.com/docs/cloudsearch/Bulk_directional_routing).

2. Use the following command to enable adaptive write optimization at the cluster level.

   ```Bash
   PUT _cluster/settings
   {
       "persistent": {
           "indices.bulk.adaptive_shard_selection.enabled":"true"
       }
   }
   ```
   


<span id="1ad7f3e3"></span>
## FAQs


* After enabling adaptive write optimization, why can't documents be retrieved directly using `_id`?

   After enabling adaptive write optimization, bulk write operations automatically route to higher\-performance shards. Then the fixed mapping between `_id` and shards will no longer exist. At this time, document retrieval by `_id` requires explicit routing values to locate the original document. The routing value can be obtained through standard query operations.

* Why does enabling adaptive write optimization fail?

   Only instances that meet specific requirements support turning on adaptive write optimization. For detailed requirements, refer to [Functional limitations](https://docs.byteplus.com/docs/cloudsearch/Adaptive_write_optimization#119ff7bf).

   If you encounter any other issues during operation, [submit a ticket](https://console.byteplus.com/workorder/create/?step=1) for technical assistance.
