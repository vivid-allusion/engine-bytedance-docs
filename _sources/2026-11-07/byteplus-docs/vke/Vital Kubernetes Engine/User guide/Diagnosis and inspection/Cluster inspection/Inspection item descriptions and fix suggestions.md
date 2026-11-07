---
title: "Inspection item descriptions and fix suggestions"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Inspection-items-and-repair-suggestions"
---

The cluster inspection feature of the AIOps suite for VKE is built on rich cluster inspection experience and solutions from  internal teams. This topic describes cluster inspection items, check content, and methods for fixing issues.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In this topic, the reference documentation for modifying the number of workload replicas and ResourceQuota for Deployments is used as an example. The configuration method is the same for other types of workloads.</div>


<span id=".6LWE5rqQ6YWN6aKd"></span>
## ResourceQuota


|Inspection item |Check content |Fix suggestion |References |
|---|---|---|---|
|VCI network quota |Check whether the VCI network quota of the cluster is used up. If the quota is used up, VCIs will fail to be created. |[Submit an application](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=vke) to increase the quota. |None |
|VCI quota check |Check whether the VCI quota of the cluster is used up. If the quota is used up, VCIs will be unable to be created for the cluster. |[Submit an application](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=vke) to increase the quota. |[Limit](https://docs.byteplus.com/en/docs/vke/VCI-limits) |
|Cluster CLB resource quota |Check whether the usage of the Internet\-facing CLB quota and the internal\-facing CLB quota for the cluster is greater than 80%. If the quota is used up, services and Ingresses will fail to be created. |[Submit an application](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=vke) to increase the quota. |[Dependent underlying cloud service quotas](https://docs.byteplus.com/en/docs/vke/Limits#.5L6d6LWW5bqV5bGC5LqR5Lqn5ZOB6YWN6aKd6ZmQ5Yi2) |
|Cluster node quota |Check whether the cluster node quota usage is greater than 80%. If the quota is used up, nodes will be unable to be added to the cluster. |[Submit an application](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=vke) to increase the quota. |[Cluster-related quotas](https://docs.byteplus.com/en/docs/vke/Limits#.6ZuG576k6YWN6aKd6ZmQ5Yi2) |
|Node pool quota |Check the node pool quota of the cluster. If the quota is used up, node pools will be unable to be added to the cluster. |[Submit an application](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=vke) to increase the quota. |[Cluster-related quotas](https://docs.byteplus.com/en/docs/vke/Limits#.6ZuG576k6YWN6aKd6ZmQ5Yi2) |


<span id=".6LWE5rqQ5rC05L2N"></span>
## Resource utilization


|Inspection item |Check content |Fix suggestion |References |
|---|---|---|---|
|High node CPU utilization |Check whether the node CPU utilization is greater than 80%. High utilization may cause CPU resource preemption, which affects normal business operations. |* Increase the number of nodes.<br><br>* Configure the node pool.<br><br>* Check the ResourceQuota of the pod, such as requests and limits. |* [Adding nodes](https://docs.byteplus.com/en/docs/vke/Adding-nodes)<br><br>* [Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool)<br><br>* [Managing Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment) |
|High node memory utilization |Check whether the node memory utilization is greater than 80%. High utilization may cause OOM errors, which affect normal business operations. |||
|Insufficient allocatable memory in the cluster |Check whether the allocated memory of the node exceeds 80%. If the allocatable memory is less than the pod request value, the pod cannot be created. |||
|Insufficient allocatable CPU in the cluster |Check whether the allocated CPU of the node exceeds 80%. If the allocatable CPU is less than the pod request value, the pod cannot be created. |||
|Node MaxPod |Check whether the number of new pods that the node can accommodate is less than two. After the upper limit is reached, new pods cannot be scheduled. |* Increase the number of nodes.<br><br>* Create a node pool. |* [Adding nodes](https://docs.byteplus.com/en/docs/vke/Adding-nodes)<br><br>* [Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool) |
|High pod memory utilization |Check whether the workload memory load is greater than 95%. Excessive load may cause Out of memory (OOM) errors, which affect normal business operations. |* Adjust the ResourceQuota.<br><br>* Increase the number of instances.<br><br>* Configure autoscaling. |* [Managing Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment)<br><br>* [Creating HPA](https://docs.byteplus.com/en/docs/vke/Creating-a-Horizontal-Pod-Autoscaler) |
|High pod CPU utilization |Check whether the CPU load of the workload exceeds 95%. Excessive load may cause CPU resource contention and affect normal business operations. |||


<span id=".6IqC54K56K-K5pat"></span>
## Node diagnosis


|Inspection item |Check content |Fix suggestion |References |
|---|---|---|---|
|NotReady node |Check whether NotReady nodes exist in the cluster. If the node is in an abnormal status, pods cannot be scheduled to the node. |View the node status. Add or delete nodes when necessary. |[Node status](https://docs.byteplus.com/en/docs/vke/Resource-status-description#.6IqC54K5) |
|VCI virtual node status |Check the status of VCI virtual nodes in the cluster. If the node status is abnormal, VCI will fail to be created. |Contact technical support for assistance. |None |


<span id=".6ZuG576k6aOO6Zmp"></span>
## Cluster risk


|Inspection item |Check content |Fix suggestion |References |
|---|---|---|---|
|Node security group inconsistency |Check whether the security groups of all nodes in the cluster are consistent. If the security groups are inconsistent, some nodes may be unable to access the network, which will result in network faults. |Make sure that the security groups configured for all nodes are consistent. |* [Configuring security groups](https://docs.byteplus.com/en/docs/vke/Security-group-settings)<br><br>* [Cluster access rules](https://docs.byteplus.com/en/docs/vke/Cluster-access-rules) |
|CoreDNS add\-on status |Check whether the CoreDNS add\-on is not in the **Running** state. If the add\-on is in an abnormal status, DNS resolution in the cluster will fail, which will lead to access failures through the service name. |Check the status of the CoreDNS add\-on and identify and resolve exception causes. |[Add-on FAQ](https://docs.byteplus.com/en/docs/vke/Add-on-FAQs) |
|Cluster kubeconfig certificate expiration |Check whether the kubeconfig certificate in the cluster is about to expire or has expired. After the kubeconfig certificate expires, you will not be able to use the certificate to access the cluster. The alert status varies based on different expiration or near\-expiration times. Valid values:<br><br><br>* **Warning**: The certificate is about to expire, which indicates that the validity period of the certificate is less than seven days.<br><br>* **Exception**: The certificate has expired, which indicates that an expired kubeconfig certificate exists. |Apply for a new certificate and remove expired certificates. |[Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster) |
|Workload replicas |Check whether the expected and actual number of replicas for the workload are consistent. If the number is inconsistent, high reliability requirements are not met. |Identify workloads with an abnormal number of replicas to resolve exception causes and update the number of replicas. |[Managing workloads](https://docs.byteplus.com/en/docs/vke/Managing-Deployments) |
|DaemonSets status |Check whether the number of DaemonSets matches the number of nodes. If the expected number of replicas is not reached, related features may not function as expected. |Identify and resolve the cause of workloads with an abnormal number of replicas, and update the number of replicas. |[Managing workloads](https://docs.byteplus.com/en/docs/vke/Managing-Deployments) |
|Availability of the CR service in the VPC |If the VPC where the cluster is located cannot access CR, the pods that use the specified image will fail to start. |Check whether the VPC where the cluster is located is connected to the CR instance. |[Connecting to the VPC of the current account](https://docs.byteplus.com/en/docs/cr/connect-vpcs-under-the-same-account) |
|CoreDNS high availability |Check whether the number of replicas for the CoreDNS add\-on is greater than 2, and whether different replicas are deployed on different nodes. If the requirements are not met, CoreDNS does not feature high availability and is at risk of a single point of failure. When a node fails or restarts, CoreDNS will be unable to provide services, which affects normal business operations. |Check the status of CoreDNS replicas. Maintain two or more replicas, and distribute replicas across different nodes. |[CoreDNS best practices](https://docs.byteplus.com/en/docs/vke/CoreDNS-best-practices) |
|CoreDNS add\-on status |Check whether the CoreDNS add\-on is not in the **Running** state. If the add\-on is in an abnormal status, DNS resolution in the cluster will fail, which will lead to access failures through the service name. |Check the status of the CoreDNS add\-on and identify and resolve exception causes. |[Add-on FAQ](https://docs.byteplus.com/en/docs/vke/Add-on-FAQs) |
|Node pool configuration |Check the node pool feature of the cluster. If the node pool is missing, it may result in high node load and pod scale\-out failure. |Configure the node pool. |[Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool) |
|Number of worker nodes in the cluster |Check whether the number of worker nodes in the cluster is less than 2. A cluster with a single node has a single point of failure risk. |Scale out nodes or create a node pool. |* [Adding nodes](https://docs.byteplus.com/en/docs/vke/Adding-nodes)<br><br>* [Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool) |
|Cluster deletion protection |Check whether the **deletion protection** feature has been enabled for the cluster. If the deletion protection is not enabled, the cluster may be mistakenly deleted by the console or API, which results in business failures. |Enable the deletion protection feature. |* [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster)<br><br>* [CreateCluster](https://docs.byteplus.com/en/docs/vke/CreateCluster)<br><br>* [UpdateClusterConfig](https://docs.byteplus.com/en/docs/vke/UpdateClusterConfig) |
|Load Balancer service and corresponding CLB instance configuration |Check whether the CLB instance configuration in the annotation when you create the Load Balancer service is consistent with that in the CLB console.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only the <strong>instance billing type</strong> and <strong>instance type</strong> of the CLB instance are checked. The corresponding annotations are <code>volcengine-loadbalancer-billing-type</code> and <code>volcengine-loadbalancer-spec</code>.</div><br> |Modify the annotation in the CLB console to ensure that the configuration in VKE is consistent with that in the CLB console. |[Configuring CLB services by using annotations](https://docs.byteplus.com/en/docs/vke/Configuring-a-LoadBalancer-Service-using-annotations) |
|Cluster CLB instance status |Check whether the CLB instances in the cluster are in a normal status. If the CLB instances are in an abnormal status, the kube\-apiserver service of the cluster will become unavailable. |View the status of CLB instances for the cluster in the [CLB console](https://console.byteplus.com/clb). |[Viewing cluster CLB instances](https://docs.byteplus.com/en/docs/vke/How-do-I-change-the-instance-type-of-the-CLB-instance-automatically-created-during-cluster-creation) |
|Audit log enabling status |Check whether the **cluster auditing** feature has been enabled for the cluster. Enabling the auditing feature facilitates troubleshooting and analysis of daily cluster issues. |Enable the cluster auditing feature. |[Cluster auditing](https://docs.byteplus.com/en/docs/vke/Cluster-auditing) |
