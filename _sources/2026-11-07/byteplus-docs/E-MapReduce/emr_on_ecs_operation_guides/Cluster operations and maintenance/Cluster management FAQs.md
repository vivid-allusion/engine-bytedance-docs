---
title: "Cluster management FAQs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs_cluster_FAQs"
---

<span id="高可用集群为什么部署3个master节点？"></span>
## Why are three Master nodes deployed in a high availability cluster?

When high availability is enabled for a Hadoop\-type cluster, three Master nodes are deployed to support high availability for ResourceManager and NameNode. High availability deployment is recommended for production environments.

<span id="是否支持非高可用集群升级为高可用集群？"></span>
## Is it supported to upgrade a non\-high availability cluster to a high availability cluster?

Currently, upgrading a non\-high availability cluster to a high availability cluster is not supported. It is recommended to enable high availability when creating a production cluster.

<span id="集群创建失败报错：“余额不足”，该如何处理？"></span>
## Cluster creation failed with the error: "Insufficient balance." How should this be handled?


* Issue description:

   102008 DownStreamServiceError Message:

   error code:Insufficient. Balance,

   error message: The request is denied due to the lack of balance.

* Issue analysis: Insufficient account balance (when the account balance is negative, coupons cannot be used)

* Solution: Go to **Billing \> Account Overview \> Available Balance** to recharge your account


<span id="集群创建失败报错：“库存不足”，该如何处理？"></span>
## Cluster creation failed with the error: "Insufficient inventory." How should this be handled?


* Issue description: Failure occurs when creating a new cluster, adding a node group, or expanding a node group. The failure reason is displayed as follows

   Message:

   error code: Insufficient.InstanceCapacity

   error Message: There is not enough capacity to fulfill your request.

* Issue analysis: Insufficient inventory for the corresponding instance type

* Solution: Select another ECS instance type with sufficient inventory that meets your business requirements, or contact the Volcano Engine team.


<span id="集群创建失败报错：“配额不足，请前往配额中心申请”，该如何处理？"></span>
## Cluster creation failed with the error: "Insufficient quota. Please go to the quota center to apply." How should this be handled?


* Issue description: Failure occurs when creating a new cluster, adding a node group, or expanding a node group. The failure reason is displayed as follows:

   * Project：ecs/ebs

   * Region：cn\-beijing

   * Request ID：xx

* Issue analysis: Insufficient ECS or EBS quota

* Solution: Click **Quota Center** to apply for the required product's quota limit as needed. Caution: Select the required region and payment type.
