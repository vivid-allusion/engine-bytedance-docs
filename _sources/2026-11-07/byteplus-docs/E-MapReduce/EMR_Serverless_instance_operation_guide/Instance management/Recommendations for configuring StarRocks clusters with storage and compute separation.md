---
title: "Recommendations for configuring StarRocks clusters with storage and compute separation"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Recommendations_for_configuring_StarRocks_clusters_with_storage_and_compute_separation"
---

<span id="_1-选型原则"></span>
## 1 Selection principles


1. FE resources


FE resources are determined by the query QPS, number of tables, and number of tablets. Generally, 32GB supports fewer than 100,000 tablets. The number of FE nodes must be odd; in high availability mode, at least 3 nodes are required.


2. CN resources


CN resources are determined by the query QPS and the amount of data queried. For 1TB of data, it is recommended to configure CN compute resources with approximately 64 cores.


3. Storage specifications


In compute\-storage separation clusters, storage size only affects the cache space available during queries and writes. Therefore, it is recommended to determine the storage size based on the amount of data queried. Typically, a 16\-core configuration uses 256GB of storage space.

<span id="_2-推荐配置"></span>
## 2 Recommended configurations

<span id="_2-1-小型（32vcpu-64vcpu"></span>
### 2.1 Small (32vCPU ~ 64vCPU)


|Type |Compute specifications |Storage specifications |Number of nodes |Remarks |
|---|---|---|---|---|
|FE |8 vCPU 32GB/<br><br>16 vCPU 64GB |120GB |3 |Select different memory specifications based on the number of databases and table data. For tablet counts above 100,000, choose the 64GB memory specification; for counts below, choose the 32GB memory specification. |
|CN |8 vCPU 32GB |128GB |4 ~ 8 | |


<span id="_2-2-中型（64vcpu-128vcpu"></span>
### 2.2 Medium (64vCPU ~ 128vCPU)


|Type |Compute specifications |Storage specifications |Number of nodes |Remarks |
|---|---|---|---|---|
|FE |16 vCPU 64GB |120GB |3 | |
|CN |16 vCPU 128GB |256G+ |4 ~ 8 |Set different storage specifications based on the amount of data to be cached. Each node with 256GB can cache 256GB \* number of nodes of data. |


<span id="_2-3-大型（128vcpu-512vcpu"></span>
### 2.3 Large (128vCPU ~ 512vCPU)


|Type |Compute specifications |Storage specifications |Number of nodes |Remarks |
|---|---|---|---|---|
|FE |16 vCPU 64GB |160GB |3 | |
|CN |32 vCPU 128GB |512G+ |4 ~ 16 |Set different storage specifications based on the amount of data to be cached. Each node with 512GB can cache 512GB \* number of nodes of data. |


<span id="_2-4-超大型（512vcpu以上"></span>
### 2.4 Extra large (above 512vCPU)


|Type |Compute specifications |Storage specifications |Number of nodes |Remarks |
|---|---|---|---|---|
|FE |16 vCPU 64GB/<br><br>32 vCPU 128GB |160GB |3 |For high query QPS requirements and tablet counts above 200,000, high\-spec FE can be selected. |
|CN |32 vCPU 128GB |512G+ |4 ~ 16 |Set different storage specifications based on the amount of data to be cached. 512GB means each node can cache 512GB \* number of nodes of data. |


For extra large clusters, contact Volcano EMR operations personnel for evaluation.
