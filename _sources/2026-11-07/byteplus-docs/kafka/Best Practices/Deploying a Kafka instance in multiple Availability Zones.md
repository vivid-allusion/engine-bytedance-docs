---
title: "Deploying a Kafka instance in multiple Availability Zones"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/best-practices-for-multiple-AZ"
---

An instance deployed in multiple Availability Zones (AZs) has higher availability. This topic describes the impact of multi\-AZ deployment on an instance.

<span id="6ca6ebf5"></span>
## Precautions

Note the following before using a multi\-AZ Kafka instance:


* Deploying Kafka instances in multiple Availability Zones requires at least three Availability Zones. Currently, there are only two Availability Zones in the China(Hongkong) Region and the Pacific Southeast (Johor) Region. Therefore, these two Regions do not support the Multiple Availability Zone deployment.

* The Elastic Compute Service (ECS) instance where the Kafka client is deployed must ideally be in the same Availability Zone as the Kafka instance to avoid issues related to unequal fault domains.

* A multi\-AZ instance may experience a network latency of 2 ms to 3 ms. The network latency per request is slightly longer than that of a single\-AZ instance.

* When API actions are called by clients synchronously, the throughput of the instance can be reduced. Consider countermeasures such as reserving a certain room for performance, upgrading the instance specifications, or changing to calling API actions asynchronously.

* In the split brain scenario of a multi\-AZ instance, dirty data truncation may occur if the ack parameter of the client is not set to \-1.


<span id="51a944b9"></span>
## Setting as multi\-AZ deployment

Message Queue for Kafka allows you to deploy an instance across Availability Zones. Namely, multi\-AZ deployment is supported. Multi\-AZ instances deliver excellent disaster recovery capabilities and can ensure cluster data reliability and service availability.

When you buy a Kafka instance, set its deployment method to multi\-AZ deployment and select three Availability Zones for cross\-AZ disaster recovery. After an instance is created, you cannot modify its deployment method. That is to say, the deployment method of an existing instance cannot be changed from single\-AZ deployment to multi\-AZ deployment. A multi\-AZ instance has no difference in usage for clients. However, we recommend that client hosts be deployed in multiple Availability Zones that are the same as those for the Kafka instance. This improves the overall service availability and avoids failures that may occur in single\-AZ deployment scenarios.

To view the number of Availability Zones for an existing Kafka instance, go to **Instance Details \> Basic information \> Availability Zone**. If the number of Availability Zones is greater than 1, the instance is deployed across Availability Zones.

<span id="21432c1e"></span>
## Descriptions of availability and fault domains

For a multi\-AZ instance, its underlying resources such as network resources, computing nodes, storage nodes, and ZooKeeper nodes are distributed to multiple Availability Zones. Failures, if any, are isolated among these Availability Zones. This ensures that any failed underlying resource in one Availability Zone does not affect the nodes in other Availability Zones. If a computing or storage failure occurs in one Availability Zone, it is possible to switch to another Availability Zone in the Kafka cluster. This ensures business continuity. However, the service availability can be affected if failures occur in two or more Availability Zones.

If the network fails between two Availability Zones, which means no communication available, a split brain may occur in the Kafka cluster. Namely, nodes in both Availability Zones provide services, but the data written to one Availability Zone is deemed as dirty data after cluster network recovery. To avoid dirty data, ack must be set to \-1 or all for the writing processing of the client. Additionally, the minISR parameter, which means the minimum number of in\-sync replicas, must be greater than half the maximum number of replicas. For example, minISR must be 2 or above in the case of 3 replicas.

After the cluster network recovers, message production and consumption can be recovered without any operation on the client. The data of a split node is directly truncated because of data renormalization by the Kafka instance. However, as for the data stored in multiple replicas across Availability Zones, such data truncation does not cause data loss when ack is set to \-1.

<span id="106da4fd"></span>
## Performance impacts

In a multi\-AZ instance, all data, including replicas, and the data request links are distributed to multiple Availability Zones. By default, non\-affinity exists for this deployment method. The network latency among multiple Availability Zones typically ranges from 0.5 ms to 1 ms, slightly higher than that within a single Availability Zone. Consequently, multi\-AZ deployment affects the request latency to some extent and increases the latency in replica synchronization. When the ack parameter of the client is greater than 1, equal to \-1, or set to all, the network latency directly affects the write latency in message production. Compared to single\-AZ deployment, the peak throughput of a multi\-AZ deployment instance typically incurs a loss of up to 20%.
