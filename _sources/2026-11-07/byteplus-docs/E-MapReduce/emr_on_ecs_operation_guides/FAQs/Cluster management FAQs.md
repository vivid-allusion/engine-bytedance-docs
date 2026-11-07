---
title: "Cluster management FAQs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs_cluster_management_FAQs"
---

<span id="b12bc84e"></span>
## Why are three Master nodes deployed in a high\-availability cluster?

When high availability is enabled for a Hadoop\-type cluster, three Master nodes are deployed to support high availability for ResourceManager and NameNode. High\-availability deployment is recommended for production environments.

<span id="bb35ebd0"></span>
## Can a non\-high\-availability cluster be upgraded to a high\-availability cluster?

Currently, upgrading a non\-high\-availability cluster to a high\-availability cluster is not supported. It is recommended to enable high availability when creating a production cluster.

<span id="1bf22a7d"></span>
## Cluster creation failed with the error: "Insufficient balance." How should this be handled?


* Issue description:

   102008 DownStreamServiceError Message:

   error code:Insufficient. Balance,

   error message: The request is denied due to the lack of balance.

* Issue analysis: The account balance is insufficient (when the account balance is negative, coupons cannot be used).

* Solution: Go to **Billing \> Account Overview \> Available Balance** to recharge your account.


<span id="0ad49016"></span>
## Cluster creation failed with the error: "Insufficient inventory." How should this be handled?


* Issue description: Failure occurs when creating a new cluster, adding a node group, or expanding a node group. The failure reason is displayed as follows

   Message:

   error code: Insufficient.InstanceCapacity

   error Message: There is not enough capacity to fulfill your request.

* Issue analysis: Insufficient inventory for the corresponding instance type.

* Solution: Select another ECS instance type with sufficient inventory that meets your business requirements, or contact the Byteplus team.


<span id="371c47a4"></span>
## Cluster creation failed with the error: "Insufficient quota, please apply in the Quota Center." How should this be handled?


* Issue description: Failure occurs when creating a new cluster, adding a node group, or expanding a node group. The failure reason is displayed as follows:

   * Project：ecs/ebs

   * Region：cn\-beijing

   * Request ID：xx

* Issue analysis: Insufficient ECS or EBS quota.

* Solution: Click **Quota Center** to apply for the required product quota as needed. Important: Select the required region and billing type.
