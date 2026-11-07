---
title: "Description of node domain name rules"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs_domain_name_rules"
---

This document focuses on the domain name rules for nodes in each release version of Volcano Engine E\-MapReduce (EMR).

<span id="emr-3-4-0-2-3-0-及之前版本"></span>
## EMR 3.4.0/2.3.0 and earlier versions

EMR release versions include 3.4.0, 2.3.0, and earlier versions.


* Short domain name

   * emr\-the name of the role to which the node belongs\-node index, applicable for communication between nodes within a cluster, for example, emr\-master\-1.

* Medium domain name

   * emr cluster ID\-the name of the role to which the node belongs\-node index, applicable for communication between nodes in different clusters within the same VPC. For example, emr\-xxxxxxxxx\-master\-1.

* Long domain name

   * emr cluster ID\-the name of the role to which the node belongs\-node index.regionid.emr\-VPC ID of the cluster.internal.

   * Long domain names are applicable for node authentication across VPCs and between services. For example, emr\-xxxxxxxxx\-master\-1.cn\-beijing.emr\-xxxxxxx.internal.


<span id="emr-3-5-0-2-4-0-及之后版本"></span>
## EMR 3.5.0/2.4.0 and later versions

EMR release versions include 3.5.0, 2.4.0, and later versions.


* Short domain name

   * the name of the role to which the node belongs\-node group index\-node index, applicable for communication between nodes within a cluster, for example, master\-1\-1.

* Medium domain name

   * the name of the role to which the node belongs\-node group index\-node index.emr cluster ID.

   * Medium domain names are applicable for communication between nodes in different clusters within the same VPC. For example, master\-1\-1.emr\-xxxxxxxxx.

* Long domain name

   * the name of the role to which the node belongs\-node group index\-node index.emr cluster ID.regionid.domain name of the Volcano Engine product.

   * Long domain names are applicable for node authentication across VPCs and between services.

   * If a public IP is enabled, this domain name can also be used to access the corresponding node over the public network. For example, master\-1\-1.emr\-xxxxxxxxx.cn\-beijing.emr\-volces.com.


<span id="区域与regionid对应关系"></span>
## Region and RegionID mapping


|Region name |RegionID |
|---|---|
|Asia Pacific（Johor） |ap\-southeast\-1 |
