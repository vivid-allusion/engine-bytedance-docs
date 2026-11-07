---
title: "Usage notes"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Usage-notes"
---

Vital Kubernetes Engine (VKE) provides managed services for the technical architecture and core components of container workloads. Improper operations on non\-managed components or applications running in VKE clusters may cause service disruptions. To help ensure the security, efficiency, stability, and high availability of your cloud services, and to better assess and avoid operational risks, carefully read the recommendations and considerations in this topic before using VKE.

<span id="Dw0EvWUn"></span>
## Service classification


|Service classification |Component definition |Example component |
|---|---|---|
|Control plane |Kubernetes control plane components |Four control plane components: etcd, kube\-apiserver, kube\-scheduler, and kube\-controller\-manager. |
||VKE\-managed components |VKE managed components such as cloud\-controller\-manager, cluster\-autoscaler, karpenter, and vpc\-cni\-controlplane.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">On the <strong>Addons</strong> page of the VKE console, components with the 'Managed' label are managed components. For more information about managed components, see <a href="https://docs.byteplus.com/en/docs/vke/Add-on-overview">Add\-on overview</a>.</div><br> |
|Data plane |Kubernetes data plane components |Three data plane components: kubelet, kubeproxy, containerd. |
||VKE non\-managed components |Non\-managed components such as pod networking (CNI) related components, container storage (CSI) related components, and nvidia\-device\-plugin.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">On the <strong>Addons</strong> page of the VKE console, components without the 'Managed' label are non\-managed components. For more information about managed components, see <a href="https://docs.byteplus.com/en/docs/vke/Add-on-overview">Add\-on overview</a>.</div><br> |
||Application workloads |Workloads and resources created by users, such as Pods, Deployments, Services, PV/PVCs, and Ingresses. |


<span id="bCSlIBON"></span>
## Control plane component management

The control plane consists of Kubernetes control plane component and VKE\-managed components. VKE continuously monitors the core metrics of the cluster control plane. When metrics reach or exceed preset thresholds, the control plane components are automatically scaled up to provide increased capacity, ensuring reliable business operations.

Kubernetes control plane components and VKE\-managed components expose custom parameters through product features. Through custom parameters exposed on the product side, you can adjust configurations based on the actual cluster conditions, such as modifying the autoscaling settings of the managed component cluster\-autoscaler.

<span id=".5pWw5o2u6Z2i57uE5Lu26L-Q57u0"></span>
## Data plane component and service operations

VKE manages the Kubernetes control plane components, but data plane components still run on user nodes (ECS instances), such as CoreDNS, Ingress, Kube\-Proxy, VPC\-CNI, Kubelet, and CSI\-related components. Therefore, the stability of data plane component requires joint maintenance by VKE and users.

VKE provides the following support for data plane components:


* Provides parameterized settings such as feature optimization, BugFix, and CVE patches, along with guidance documents.

* Provides observability capabilities such as monitoring, logging, and alerting. Core components provide component logs, which can be collected and sent to Torch Log Service (TLS).


When using data plane components, follow these recommendations:


* Use the latest version of components. Components are frequently released in new versions to fix bugs or provide new features. After VKE releases a new version of a component, upgrade it according to the instructions in the component upgrade documentation if the time is appropriate and you can ensure business stability. For details, see [Upgrading components](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

* VKE sends important cluster exception events to the event center of Cloud Monitor. We recommend configuring corresponding alerting policies in Cloud Monitor. For details, see [Cloud product events](https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-events) and [Creating event rules](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-event-rule). 

* We recommend that you enable cloud\-native observability in the cluster and configure alerting accordingly for basic and business resources. VKE will send important cluster metrics of the control plane and data plane to Vital Managed Service for Prometheus (VMP). For detailed operations, see [Enabling cloud-native observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For security reasons, you need to decide whether to enable data plane observability and cluster alerting. We strongly recommend following the preceding suggestions to configure alerts that comprehensively cover cluster and business resource metrics, and to respond to alerts promptly to ensure normal business operations.   </div>
   

* Kubernetes data plane components and VKE non\-managed components expose custom parameters through product features. Through custom parameters exposed on the product side, you can adjust configurations based on the actual cluster conditions, such as modifying the resource and reserved IP settings of the non\-managed add\-on vpc\-cni.

* Use [VKE console](https://console.byteplus.com/vke) or the open API to configure custom parameters for components. Configuring component parameters with other methods may lead to functional failure. Additionally, parameters may be automatically overwritten in certain cases. For details, see [User guide for add-on management](https://docs.byteplus.com/en/docs/vke/Add-on-management) and [API reference for add-on management](https://docs.byteplus.com/en/docs/vke/Add-on-management-API).

* Do not use the IaaS\-layer Open APIs to change the runtime environment of VKE\-related components, including but not limited to using ECS Open APIs to modify the running status of worker nodes (ECS instances), node security group configurations, node network configurations, or using CLB Open APIs to alter CLB configurations created by VKE. Such actions may cause anomalies in data plane components.

* Some data plane components may be affected by upstream open\-source components and may contain bugs or vulnerabilities. Upgrade components timely to avoid business impact caused by bugs or vulnerabilities in upstream open\-source components.


<span id=".56iz5a6a6auY5Y-v55So6YWN572u5o6o6I2Q"></span>
## Configuration recommendations for high availability and stability

<span id=".6ZuG576k"></span>
### cluster

The following table provides configuration recommendations for improving stability and high availability before or during cluster creation. For details, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster). 


|Category |Recommendation |Notes |
|---|---|---|
|Network planning |Before creating a cluster, we recommend planning cluster, pod, and service network segments in advance based on actual requirements to avoid conflicts:<br><br><br>* We recommend that the number of clusters in a single VPC does not exceed 11. The more clusters you create within a VPC, the smaller the subnet that can be allocated to each cluster.<br><br>* If the cluster can be scaled out to more than 100 nodes in the future, we recommend using subnets with a `10` or `172` network prefix and `/16` CIDR notation.<br><br>* If you select a subnet with a `192` network prefix, we recommend using `/18` as the CIDR notation. |A small subnet for the cluster or a small network segment for pods may result in issues such as failing to scale out the cluster and create pods. |
|Deployment |When you create a cluster, select an appropriate pod networking type based on your business requirements. For details, see [Pod networking](https://docs.byteplus.com/en/docs/vke/Container-networks). |After the cluster is successfully created, the network model cannot be changed. Therefore, you need to select carefully. |
||In the **Node pool configuration** step of creating a cluster, a default security group is automatically created and bound. However, you can also configure custom rules in security groups as needed. For details, see [Security group configuration](https://docs.byteplus.com/en/docs/vke/Security-group-settings) and [Cluster access rules](https://docs.byteplus.com/en/docs/vke/Cluster-access-rules). |Security groups are an important means of security isolation. Improper security policy configuration may result in potential security risks, service connectivity issues, and other related problems. |
||When creating a cluster, in the **Networking** section of the **Cluster configuration** step, we recommend selecting subnets from at least two availability zones. |Selecting multiple availability zones for creating a cluster improves the Kubernetes control plane's availability, disaster tolerance, performance, and incident handling capabilities.This enhances business continuity, stability, and security. |
|Reliability |When creating a cluster, we recommend adding a separate data volume and mounting the container and image storage directories respectively to `/var/lib/containerd` and `/var/lib/kubelet`.<br><br>The benefits of using a separate data volume for image storage include:<br><br><br>* Isolated from applications, configurations, and other files, which improves data security.<br><br>* Reduce the pressure on the I/O of the system volume and improve system performance.<br><br>* Higher flexibility in container and image management, which improves the maintainability and scalability of the system. |Issues such as a high load on the system volume I/O may occur without a separate data volume. |
|Security |When creating a cluster, the system enables **Cluster deletion protection** by default. We recommend keeping it enabled to prevent accidental cluster deletion through the console or Open API. |If deletion protection for clusters is disabled, you can delete the clusters via the console or API, which poses a security risk in business clusters. |


<span id=".5a655Zmo572R57uc"></span>
### Pod networking


|Category |Recommendation |Impact description |
|---|---|---|
|Reliability |We recommend selecting the same availability zone for pod subnets and for node subnets. |Pods will fail to start if there are no available nodes for scheduling in the availability zone . |
||We recommend that the security group for the pod networking of the cluster be associated with no more than 2000 pods. |Security groups can be associated with 2,000 IP addresses at most by default. Otherwise, new ENI cannot be created and pods cannot start. |


<span id=".5bel5L2c6LSf6L29"></span>
### Workload


|Category |Recommendation |Impact description |
|---|---|---|
|Deployment |We recommend setting CPU and memory limits when creating workloads to improve the robustness of workloads. |When multiple applications are deployed on the same node, any application without LimitRange configuration can cause other applications to malfunction owing to insufficient resources and inaccurate monitoring information. |
|Reliability |When creating a workload, we recommend enabling pod health checking features, including **Liveness check** and **Readiness check**. For detailed operations, see [Workload configuration](https://docs.byteplus.com/en/docs/vke/Workload_configurations). |If pod health checking is disabled, pods will not be able to restart to restore the services automatically upon business failures. As a result, you will find that the services on pods stopped while the pods themselves seem to be working properly. |
||When creating a service, you need to select the appropriate access method based on your requirements. Currently, four access methods are supported, including Internet access, access only within the cluster (ClusterIP), VPC internal network access, and host port access. |Selecting an inappropriate access method may cause confusing access logic for services internally and externally and the waste of resources. |
||When creating a workload, we recommend setting the number (more than 1 at least) of instances (pod replicas) as required for your business, as well as an appropriate configuration of node scheduling policy. |If only one pod replica is configured, service failures cannot be avoided when nodes or instances malfunction. To ensure successful scheduling for your pods, you need to allocate sufficient resources to the nodes after configuring the scheduling rules. |
||If workloads require high I/O operations, we recommend you mount PVC\-related storage. For details, see [Storage management](https://docs.byteplus.com/en/docs/vke/Storage-management). |By doing that, you can avoid the hang issues in containerd or kubelet that cause nodes to enter NotReady status. |


<span id=".6auY5Y2x5pON5L2c"></span>
## High\-risk operations

High\-risk actions may happen when running and deploying functional modules on VKE, which can adversely affect business stability to different extents. We recommend that you fully learn about high\-risk actions and their impact on VKE before getting started. For details, see [High-risk actions and restoration solutions](https://docs.byteplus.com/en/docs/vke/High-risk-operations-and-recovery-solutions).
