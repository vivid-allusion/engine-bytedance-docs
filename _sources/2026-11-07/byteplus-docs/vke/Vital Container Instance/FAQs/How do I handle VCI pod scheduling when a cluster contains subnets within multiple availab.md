---
title: "How do I handle VCI pod scheduling when a cluster contains subnets within multiple availability zones?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How-do-I-schedule-VCI-pods-when-a-cluster-has-subnets-in-multiple-Availability-Zones"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Problem description

When no VCI pod subnet is specified separately, the subnet of the VCI pod defaults to the pod CIDR of the VPC\-CNI cluster it belongs to. Considering scenarios such as exhaustion of IP addresses in the pod subnet, VCI provides extended support: for VCI pod creation using the Kubernetes approach, additional pod subnets can be specified by using a pod annotation. For details, see [Creating instances with specified subnets](https://docs.byteplus.com/en/docs/vke/Creating-an-instance-based-on-specified-subnets).

vke.volcengine.com/preferred\-subnet\-ids `vke.volcengine.com/preferred-subnet-ids` annotation are in a different availability zone (for example, `Subnet-B-1 in availability zone B`) from the subnets specified for the VPC\-CNI cluster where this VCI pod is located (for example, `Subnet-A-1 in availability zone A`), the cluster has subnets from two different availability zones. In the VPC\-CNI cluster with subnets from two different availability zones, when a new VCI pod is created with no subnets specified for the VCI pod, there is a 50% chance that the pod will be scheduled to `Subnet-B-1 in availability zone B`, where the VCI pod will fail to have an IP address.

<span id=".6Kej5Yaz5pa55rOV"></span>
## Solution

For the above problem, solutions are provided for two scenarios:


* Schedule the new VCI pod to a subnet in the new availability zone (not the one specified when creating the cluster):

   The VCI pod must have the subnet specified for it by using the `vke.volcengine.com/preferred-subnet-ids` annotation. For details, see [Creating instances with specified subnets](https://docs.byteplus.com/en/docs/vke/Creating-an-instance-based-on-specified-subnets).

* Schedule the new VCI pod to the subnet in the availability zone specified when creating the cluster:

   When creating the VCI pod, use node affinity to schedule the VCI pod to the specified virtual node (VirtualNode). To do so, follow the steps below:

   1. Log in to the [VKE console](https://console.byteplus.com/vke).

   2. In the left navigation bar, click **Cluster**.

   3. On the Cluster page, click the name of the target cluster.

   4. In the left navigation bar of the cluster management page, click **Nodes** \> **Virtual node**. On the page that appears, find the target virtual node and click its name.

   5. On the **Label** tab of the **Node details page**, find the `cluster.vke.volcengine.com/node-name` **key** and obtain the corresponding **value**.

   6. When you create a VCI pod (that is, when you create a workload and choose to deploy it on VCI), configure node affinity with the `cluster.vke.volcengine.com/node-name` value obtained in the previous step so that the VCI pod is scheduled to the specified virtual node. For details, see [Workloads](https://docs.byteplus.com/en/docs/vke/Workload-overview).

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">VCI does not support DaemonSets. For more information, see <a href="https://docs.byteplus.com/en/docs/vke/VCI-limits">Limits</a>.      </div>
