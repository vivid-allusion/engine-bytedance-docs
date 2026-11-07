---
title: "Creating clusters without ECS nodes"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-a-serverless-cluster"
---

Vital Kubernetes Engine (VKE) provides cluster templates, allowing you to quickly create managed VKE clusters without Elastic Compute Service (ECS) nodes. This topic describes how to quickly create a cluster without ECS nodes.

<span id=".6ZuG576k6K-05piO"></span>
## Cluster description

The cluster template (without ECS nodes) simplifies some configurations when you create a VKE cluster, making it easier for you to quickly create a cluster without ECS nodes. However, it offers the same features as a managed cluster. After creating a cluster without ECS nodes, you can still add ECS nodes to it. Using a cluster without ECS nodes allows you to focus on building your applications without purchasing or managing the underlying ECS infrastructure. You pay only for the actual resource consumption incurred by running Vital Container Instances (VCI).

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have already registered an account on the BytePlus platform and completed necessary preparations such as identity verification, account recharge, and authorization. For details, see [Preparation](https://docs.byteplus.com/en/docs/vke/Preparations).

* Your BytePlus account balance, excluding vouchers, is not zero.

* The permissions to use VKE and for VKE to access cloud resources have been granted. For details, see [Cloud Service dependencies](https://docs.byteplus.com/en/docs/vke/Dependencies-between-VKE-and-other-cloud-services).

* Current VKE cluster quota and dependent cloud service limits are within available capacity. For details, see [Limits](https://docs.byteplus.com/en/docs/vke/Limits).


<span id=".6LS555So6K-05piO"></span>
## Billing description

Creating a cluster without ECS nodes may incur costs for cloud infrastructure resources such as LoadBalancer, NAT gateways, and Elastic IP addresses. You can view the actual charges in the **Configuration cost** section at the bottom of the page for creating clusters. For more billing descriptions, see [Product billing](https://docs.byteplus.com/en/docs/vke/Billing).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the cluster list page, click **Cluster template** in the upper\-left corner. Then, in the pop\-up window, select **Template for cluster without ECS nodes** and click **Confirm**.

4. Follow the console wizard to configure the parameters required for cluster creation.

   Compared to the Managed cluster template, the "Template for cluster without ECS nodes" omits the **node pool settings**. All other configurations remain consistent with those of a managed cluster. For detailed parameter configuration, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).  


<span id=".6ZuG576k6YWN572u"></span>
### What to do next

After the cluster is created successfully, on the **Cluster** page, click the cluster name to view cluster information, manage cluster resources, and deploy VCI applications. For more actions, see


* [Node pool management](https://docs.byteplus.com/en/docs/vke/NodePools)

* [Nodes](https://docs.byteplus.com/en/docs/vke/Nodes)

* [Deploy with VCI](https://docs.byteplus.com/en/docs/vke/Integrating-with-VCI)

* [Create instance](https://docs.byteplus.com/en/docs/vke/Creating-an-instance)
