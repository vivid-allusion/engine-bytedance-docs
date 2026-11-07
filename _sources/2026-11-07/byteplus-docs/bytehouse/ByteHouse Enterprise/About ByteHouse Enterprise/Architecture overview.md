---
title: "Architecture overview"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/overview"
---

<span id="bb34393c"></span>
## Basic structure

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ba1f50f10f8040b5b273ae1102fdf81e~tplv-goo7wpa0wc-image.image) </span>

The ByteHouse cluster consists of three parts, the ByteHouse engine gateway, the cluster, and the Zookeeper cluster.


* ByteHouse gateway, which provides HTTP/TCP load balancing.

* The ByteHouse engine cluster is used to provide computing and storage capabilities.

* Zookeeper (shared) is an open\-source distributed consistent storage service that supports distributed DDL and coordinates data synchronization between master and standby.


When creating a ByteHouse cluster, there is no need to bind or create a ByteHouse gateway. The ByteHouse cluster is automatically created and integrated with the above components.

<span id="b6d69dae"></span>
## Sharding and replicas

In the ByteHouse engine cluster, each server node can be called a shard. Suppose there are N servers, each server has a data table A, and the data of data table A on each server is not duplicated, then it can be said that data table A has N shards.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3361dfba0a4e40c788e6d0d3a60c9b45~tplv-goo7wpa0wc-image.image) </span>

Replicas are another concept of ByteHouse. In order to solve the problem of high data availability, each sharding can configure 0 or more replicas. As shown in the figure above, the ByteHouse cluster has a total of 2 \* N servers, divided into N shards, and each shard has an additional replica. This cluster can be called a 2\-replica cluster with N shards.

In cluster planning, the number of shardings determines the overall performance and storage capacity of the cluster, and the number of replicas determines the availability of nodes. The number of replicas is usually 2 (i.e. dual replica mode), or 1 (i.e. single replica mode):


* Dual replica mode: higher availability. Usually, when a single node fails, it will not affect the import and query of the cluster.

* Single replica mode: lower cost. However, when a single node fails, it will affect the import and query of the cluster.
