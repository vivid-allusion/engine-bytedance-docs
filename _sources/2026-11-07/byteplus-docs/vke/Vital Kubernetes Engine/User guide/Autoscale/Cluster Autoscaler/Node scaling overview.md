---
title: "Node scaling overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How-Cluster-Autoscaler-works"
---

VKE clusters can be automatically scaled based on the scheduling status of pods and the node resource usage in the clusters. You need to control the quantity of cluster resources to reduce costs while ensuring the normal operation of businesses that correspond to pods. This topic introduces node autoscaling solutions supported by VKE clusters.

<span id="5EFQtwU9"></span>
## **Solution introduction**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">A cluster supports only one scaling solution. You cannot mix the two scaling solutions in a cluster. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Creating-a-Cluster-Autoscaler">Enabling node autoscaling</a> and <a href="https://docs.byteplus.com/en/docs/vke/Configure_node_instant_autoscaler_Karpenter">Enabling instant node elasticity</a>.</div>


* <div data-tips="true" data-tips-type="warning">The scaling statistics provided in this topic are theoretical results based on a custom image optimized for scaling. The actual data in your business environment shall prevail.</div>




|Solution |Add\-ons |Description |
|---|---|---|
|Node autoscaling |cluster\-autoscaler |The system periodically maintains and checks cluster status through polling. When it detects that the cluster meets scale\-in or scale\-out conditions, it automatically scales nodes in or out. |
|Instant node elasticity |karpenter |Scales nodes based on events. This solution ensures better delivery of elastic resources if the cluster has multiple node pools that have elastic scaling enabled. |


<span id="r8oBzpcu"></span>
## **Solution differences**

If the node pool of a cluster has autoscaling enabled, instant node elasticity is compatible with the semantics and behavior of the original elastic node pool. It supports seamless enabling and use for all types of applications.

The following table highlights the feature optimizations of instant node elasticity compared to node autoscaling.

&nbsp;


|Feature optimization |Node autoscaling (Cluster AutoScaler) |Instant node elasticity (Karpenter) |
|---|---|---|
|Elastic sensitivity |It uses periodic polling for scaling, which is heavily affected by cluster size and the number of node pools. Elasticity sensitivity typically exceeds 5 seconds. |Based on event\-driven architecture, it responds faster to elastic resource requests for complex production clusters with dozens of node pools. Elasticity sensitivity can reach the accuracy of seconds. |
|Elasticity efficiency |When scaling out, it selects a single node pool based on scaling policies and focuses only on node count, not instance specifications. For non\-GPU instances, scaling takes about 50 seconds. For GPU instances, scaling time varies significantly by instance specification. |If the node pool supports multiple instance specifications, it prefers scaling solutions with fewer nodes during autoscaling, while satisfying node pool/instance specification priority rules. This improves resource delivery efficiency. |
|Certainty of resource delivery |In a single scaling process, it only scales one node pool, and the instance specification is fixed by the configuration of the node pool. |In a single scaling process, it can proactively scale multiple instance specifications across multiple node pools and availability zones simultaneously. This mechanism enhances resource delivery certainty. |


When you evaluate whether to use the instant node elasticity solution, consider the following restrictions for instant node elasticity:


* Prohibiting scale\-in at the cluster level is not supported.

* Supported scale\-in settings and behavior differ from cluster autoscaling.


<span id="8Z40veuc"></span>
## **Solution selection recommendations**

As outlined in the previous solution comparison, if your business has relatively low requirements for scaling speed and resource delivery certainty, and cannot tolerate the limitations of node instant elasticity, the node auto\-scaling solution can meet your business needs. However, if you have the following business requirements, we strongly recommend using node instant elasticity.


* For large\-scale clusters, the scaling efficiency of node autoscaling will significantly degrade, while instant node elasticity maintains consistent performance (with minimal fluctuations).

* Your scenario requires fast resource delivery and highly responsive scaling (for example, minimizing wait time for elastic resource delivery).

* Your workloads use general\-purpose computing resources and you want a larger elastic resource pool (instead of relying on a single instance specification or family).


<span id="iAsWkSIQ"></span>
## Considerations

<span id="ruRKmxEj"></span>
### **Quotas and restrictions**


* In Flannel network mode, the number of Pods that can run on a single node is affected by network configuration, and the node requires routes in the dedicated network. In VPC\-CNI network mode, the number of Pods that can run on a single node is affected by instance specification.

* Properly configure the maximum instance count for autoscaling node pools to ensure sufficient network resources (such as VPC network segments and subnets) and quotas within this limit. This avoids scale\-out failures due to exhausted network resources.

*  Elastic node scaling does not support nodes that use subscription\-based (yearly/monthly) billing. When you create new autoscaling node pools, do not select the subscription\-based billing method. When you enable autoscaling for existing node pools, subscription\-based billing nodes are removed from the cluster (not released) during scale\-in.

* Node scaling does not currently support [Sidecar Containers](https://kubernetes.io/docs/concepts/workloads/pods/sidecar-containers/). You need to deploy workloads that use Sidecar Containers to node pools with autoscaling disabled.


<span id="SnCMXHtT"></span>
### **Maintenance of dependency resources**

When you bind an Elastic IP Address (EIP), do not delete Elastic Compute Service (ECS) nodes created by node scaling (scale\-out) directly through the ECS console. Doing so will prevent EIP addresses from being automatically released.

<span id="V8s3IuYQ"></span>
## Application scenarios

Node autoscaling is mainly used in the following scenarios:


* Online scenario: During business peak hours, Horizontal Pod Autoscaler (HPA) scales out pods, and CA or Karpenter scales out scaling groups. During business off\-peak hours, HPA scales in pods, and CA or Karpenter scales in nodes.

* Offline scenario: Pods are directly created by users or CronJobs, and CA or Karpenter scales out scaling groups. After the task is completed, CA or Karpenter scales in nodes.


&nbsp;

&nbsp;

&nbsp;

&nbsp;
