---
title: "FAQs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/pulsar_FAQs"
---

This article lists some FAQs you may encounter when exploring and using the Pulsar cluster type in Volcano Engine E\-MapReduce (EMR). The content is continuously updated.

<span id="_1-网络访问相关"></span>
## 1 Network access

<span id="_1-1-如果需要通过公网访问-pulsar-集群生产、消费数据，应该如何操作？"></span>
### 1.1 To access and produce or consume data in the Pulsar cluster via the public network, what steps should be taken?

The ECS nodes of the Pulsar cluster in Volcano Engine EMR are located in the VPC you specified when creating the cluster. By default, ECS nodes in your Pulsar cluster cannot be accessed from outside the VPC (for example, via the public network).

To access the Pulsar cluster via the public network, you must first enable public network access for the ECS nodes in the Pulsar cluster. A quick method is to enable public IPs for each node in the Pulsar cluster and configure the corresponding security group rules. Next, you need to configure Pulsar. You can choose one of the following two solutions:


* Solution 1: Configure the advertisedAddress parameter of the Pulsar Broker to the public IP of the node where the Broker is located. You can use the dynamic configuration feature of the Pulsar Broker to configure parameters for each Pulsar Broker. For detailed instructions, refer to the documentation: [https://pulsar.apache.org/docs/2.9.x/admin-api-brokers/#dynamic-broker-configuration](https://docs.byteplus.com/docs/E-MapReduce/109407#dynamic-broker-configuration)

* Solution 2: Configure the Pulsar Proxy and access the Pulsar Proxy via the public network. For details, refer to the documentation: [https://pulsar.apache.org/docs/administration-proxy/](https://pulsar.apache.org/docs/administration-proxy/)


After completing the above steps, you can access and produce or consume data in the Pulsar cluster via the public network.
