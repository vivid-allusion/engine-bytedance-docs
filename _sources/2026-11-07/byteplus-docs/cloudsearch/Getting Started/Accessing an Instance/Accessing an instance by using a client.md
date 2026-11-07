---
title: "Accessing an instance by using a client"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/accessing-by-client"
---

Elasticsearch and the community have rolled out SDKs in various programming languages for your convenience. This topic describes the clients supported by Elasticsearch and their benefits.

<span id=".6K6_6Zeu5LyY5Yq_"></span>
## Access benefits

Cloud Search provides your virtual private cloud (VPC) with a virtual IP address (VIP) to access your Cloud Search instance and mounts the VIP to all the nodes in the Cloud Search instance through load balancing. This access method has the following benefits:


* Adapts to the elastic scaling of the instance and ensures its high availability. When a change occurs to the nodes of the Cloud Search instance, the VIP automatically updates the node information.

* Simplifies operations without the need to pay attention to changes in the information such as node IP addresses and port numbers.


<span id=".5a6i5oi356uv6K-05piO"></span>
## Client description


* Elasticsearch provides clients in various development languages such as Java and Python to meet the needs of different developers. For more information, refer to [Elasticsearch Clients](https://www.elastic.co/guide/en/elasticsearch/client/index.html).

* Starting from version 5.6.0, Elasticsearch has released the official Java High Level REST Client, which can be used to perform search, index, delete, update, and bulk operations. This client is consistent with the core Java classes used by TransportClient and is designed to replace TransportClient. For more information, refer to [Java High Level REST Client](https://www.elastic.co/guide/en/elasticsearch/client/java-api-client/current/index.html).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In terms of version compatibility, we recommend that you use a client version that is consistent with the instance version. For more information, refer to <a href="https://www.elastic.co/guide/en/elasticsearch/client/java-rest/6.0/java-rest-high-compatibility.html">Compatibility</a>.</div>


<span id="96652961"></span>
## Related documents


* [Connecting to a cluster using Java](https://docs.byteplus.com/en/docs/cloudsearch/connecting-cluster-Java)

* [Connecting to a cluster using Python](https://docs.byteplus.com/en/docs/cloudsearch/connecting-cluster-Python)
