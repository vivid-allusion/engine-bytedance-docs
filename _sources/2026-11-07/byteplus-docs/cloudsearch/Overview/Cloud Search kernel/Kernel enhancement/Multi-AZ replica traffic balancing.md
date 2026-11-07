---
title: "Multi-AZ replica traffic balancing"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Multi-AZ_replica_traffic_balancing"
---

<span id="75bfc149"></span>
## Background

In cloud search services, the default replica selection strategy routes queries to nodes that have the same Node Attributes as the ingress node. However, in multi\-AZ (Availability Zone, AZ) configurations, the AZ information is assigned to node attributes, which may lead to uneven query traffic distribution across different AZs. Therefore, the `cluster.search.ignore_awareness_attributes` parameter is introduced to modify this behavior.

Setting this parameter to `true` allows query replica selection without considering the ingress node's attributes, balancing query traffic across different AZs.

<span id="85c2a740"></span>
## Version information

Currently, this parameter supports:


* Elasticsearch 6.7.1 and later versions, default off

* OpenSearch 2.9.0 and later versions, default on


<span id="f6e55162"></span>
## Parameter description

`cluster.search.ignore_awareness_attributes`: whether to ignore node properties when selecting replicas during queries. The parameter default value varies by instance type; for Elasticsearch instances, the default value is `false`. The default value for OpenSearch instances is `true`.

<span id="96781b76"></span>
## Configuration method


1. Log in to the visualization tool console of the target instance. For detailed actions, refer to [logging in to Kibana/Dashboards](https://docs.byteplus.com/docs/cloudsearch/logging-tool).

2. Click the menu button in the top left corner, then navigate to **Management \> Dev Tools**.

3. Execute the following command to modify the relevant cluster configuration.

   ```Java
   PUT _cluster/settings
   {
     "persistent": {
       "cluster.search.ignore_awareness_attributes": true
     }
   }
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The parameter is enabled by default on OpenSearch instances. To turn it off, set the corresponding configuration to <code>false</code>.   </div>
