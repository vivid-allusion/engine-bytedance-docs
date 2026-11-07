---
title: "Viewing cluster information"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Cluster-basics"
---

After a cluster is created, you can view and manage cluster information on the Basic information page, including cluster information, resource usage, network information, node information, connection information, and event information.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The target cluster is in the **Running** state.

<span id=".5p-l55yL5ZKM566h55CG6ZuG576k"></span>
## Viewing and managing clusters


1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. In the left navigation bar, click **Cluster**. In the right part of the page, click the target cluster name to open the management page of this cluster.

3. Select **Overview** in the left navigation pane, and then you can view the general information and manage configurations of the current cluster by switching among the tabs on the **Overview** page.



<Tabs>
<Tab zoneid="XsPhKeov7p" title="Overview">
<TabTitle>Overview</TabTitle>

<span id="bAW9af99"></span>
#### Basic information

It includes the name, ID, status, Kubernetes version of the cluster or node, and local domain name. The items listed in the following table are configurable.


|Parameter |Description |
|---|---|
|Name |Cluster name. Click the edit icon to change the cluster name. |
|Deletion protection |Enable or disable cluster deletion protection. If enabled, the cluster cannot be deleted through either the console or API. It can prevent accidental deletion of clusters. |
|Project |Display the project to which the cluster belongs. Click the project name to navigate to the details page for the current project, where you can view resources under the project or manage project permissions.  For details, see [Resource project management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-project-management). |
|Description |Cluster description. Click the edit icon to add or modify the cluster description. |
|Tag |Cluster resource label (Tag). Click the edit icon to add or modify cluster labels. |
|IRSA OIDC |IRSA (IAM Role for Service Account) switch for the cluster. For details, see [IRSA overview](https://docs.byteplus.com/en/docs/vke/IRSA-overview). |
|Custom certificate SAN  |Allows you specify custom IP addresses, domain names, or URIs that meet the requirements. Click the edit icon to add or modify the custom certificate SAN.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Modifying configuration of SAN certificate will lead to a quick restart of cluster API server. We recommend doing it during low\-traffic periods.</div><br> |


<span id="fZMptNGM"></span>
#### Cluster network configuration


|Parameter |Description |
|---|---|
|VPC |The VPC to which the current cluster belongs. Click the VPC name to go to the [VPC console](https://console.byteplus.com/vpc) and view and manage VPCs associated with the cluster. For details, see [What is VPC](https://docs.byteplus.com/en/docs/vpc/What-is-VPC). |
|Network model |The network model of the current cluster (CNI). For details, see [Pod networking](https://docs.byteplus.com/en/docs/vke/Container-networks). |
|Pod CIDR |It is displayed only if the cluster is running on a Flannel network. This refers to the CIDR (Classless Inter\-Domain Routing) for pods (container groups) in the Flannel cluster. CIDR is an IP address allocation method. |
|Pod subnets |It is displayed only if the cluster is running on a VPC\-CNI network. In a VPC\-CNI cluster, if the existing pod subnet has insufficient IP addresses, you can add additional pod subnets to the pod network.<br><br><br>* Click **Add** to select subnets available on the VPC where the cluster is running.<br><br>* Click **Remove** to remove Pod subnets that are not used by resources within the cluster. |
|Service CIDRv4 |IPv4 CIDR address for the services in the cluster. |
|Single\-node Pod upper limit |It is displayed only if the cluster is running on a Flannel network. The maximum number of pods that a single node in a Flannel cluster can have. |
|Service forwarding mode |The forwarding mode of the current cluster. There are two modes available in VKE currently:<br><br><br>* **ipvs**: IPVS (IP Virtual Server) mode. This mode is applicable to flannel clusters.<br><br>* **eBPF**: [eBPF](https://ebpf.io/what-is-ebpf/) mode. This mode is applicable to VPC\-CNI cluster. |
|Default security group for nodes |The default security group for nodes in the current cluster. It is named with the pattern `<cluster ID>-common` (for example, `cc9l5hi6rsfek********-common`). For details, see [Security group settings](https://docs.byteplus.com/en/docs/vke/Security-group-settings).<br><br>Click the security group name to redirect to the [VPC console](https://console.byteplus.com/vpc), where you can view and manage the security groups associated with the cluster. For details, see [Security groups](https://docs.byteplus.com/en/docs/vpc/Security-group-overview).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">We recommend managing and operating security groups with caution. Modifications to the default node security groups can cause access failures for associated nodes.</div><br> |
|Default security group for pods |It is displayed only if the cluster is running on a VPC\-CNI network. In addition to providing default node security groups, the VPC\-CNI cluster also automatically creates a default pod security group named with the pattern `<clusterID>-pod` (for example, `cc9l5hi6rsfek********-pod`). This group is used to configure security group policies for pods. For details, see [Security group settings](https://docs.byteplus.com/en/docs/vke/Security-group-settings).<br><br>Click the security group name to go to [VPC console – Security group](https://console.byteplus.com/vpc/securityGroup) to view and manage security groups associated with the cluster. For details, see [Security groups](https://docs.byteplus.com/en/docs/vpc/Security-group-overview).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">We recommend managing and operating security groups with caution. Modifications to the default pod security groups can cause access failures for business.</div><br> |
|NAT gateway |The NAT Gateway associated with the cluster allows nodes and applications within the cluster to access the public network. Click the NAT Gateway name to be redirected to the [NAT Gateway console](https://console.byteplus.com/nat), where you can view and manage the NAT Gateways associated with the cluster. For details, see [What is a NAT Gateway](https://docs.byteplus.com/en/docs/natgateway/What-is-NAT-Gateway)?<br><br><br>* Click **Close** to disable the public access feature for the cluster. After you disable this feature, the cluster will automatically clean up the route entries for the NAT Gateway instance. If the NAT Gateway instance is not reused, it will also be deleted.<br><br>* You can enable **Public NAT for internet endpoint** when [creating a cluster](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster). To learn how to enable it after creating, see [FAQ](https://docs.byteplus.com/en/docs/vke/How-do-I-manually-enable-internet-facing-access-for-a-cluster).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is displayed for clusters with <strong>Public NAT for internet endpoint</strong> enabled during creation. You can use this parameter to disable the created managed NAT gateway for the cluster. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Creating-a-cluster">Creating clusters</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If you did not enable <strong>Public NAT for internet endpoint</strong> when you created the cluster, but configured a NAT gateway for the cluster manually or through operation and maintenance, this parameter will not be displayed, and you cannot delete the corresponding NAT gateway by using this parameter.</div><br> |


<span id="g3ERfiHX"></span>
#### Cluster API server configuration


|Parameter |Description |
|---|---|
|Control plane subnets |The network segments used when creating load balancers for Kubernetes API servers.<br><br><br>* Hovering your mouse over a subnet name can display its basic information.<br><br>* Clicking a subnet name will take you to the [VPC console](https://console.byteplus.com/vpc), where you can view the subnet details.<br><br>* Clicking **Add** will display a slide\-out panel providing a list of available subnets.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">To ensure high availability of the cluster, we recommend selecting subnets (if necessary) from different availability zones.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">There will be a quick restart of the API server after subnets are added. Do not take any actions on the cluster during the restart.   </div><br>    |
|Private access |The private network address of the API Server of the current cluster. |
|Internet access to API Server |The public IP of the current API Server. You can enable or disable Internet access to the API Server as needed. |
|Load balancer |The name of the LoadBalancer (CLB) instance associated with the current cluster API Server. Click the LoadBalancer name to go to the [LoadBalancer console](https://console.byteplus.com/clb), where you can view and manage LoadBalancer instances associated with the cluster. For details, see [What is LoadBalancer](https://docs.byteplus.com/en/docs/clb/Product-Overview-01). |


<span id="OmGvrVKv"></span>
#### Resource usage

It displays the CPU and memory usage of **Elastic Compute Service (ECS)**  and **Vital Container Instance (VCI)**  in the cluster. The following table contains descriptions of usage information.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The total node resources equal the sum of CPU or memory capacity across all worker nodes in the cluster.</div>



|Parameter |Description |
|---|---|
|**ECS resource usage** ||
|Usage |CPU or memory usage of all worker nodes in the cluster. |
|Remaining available |The remaining available CPU/memory of all worker nodes in the cluster, which is calculated by using the following formula: `Remaining available resources` = `Total node resources` \- `Unschedulable resources` \- `Used resources`. |
|Unschedulable |The unschedulable resource quota from the total resource amount allocated for all the worker nodes in a cluster, which usually refers to the reserved resources for nodes. For details, see [Policy for node reserved resources](https://docs.byteplus.com/en/docs/vke/Node-resource-reservation-policies). |
|**VCI resource usage** ||
|Instance family |Select a VCI instance family from the drop\-down menu to view the resources used for that instance family, which include CPU, memory, GPU, and the number of VCI instances. |


<span id="nmLh9ySq"></span>
### 


</Tab>
<Tab zoneid="bEW24qGNpv" title="Node information">
<TabTitle>Node information</TabTitle>

Displays information for all nodes in the current cluster, including node status, associated node pool, availability zone, corresponding ECS specifications, resource usage, and billing information.

You can click the button in the **Actions** column to manage the corresponding node. For details, see [Node management](https://docs.byteplus.com/en/docs/vke/Managing-nodes).


</Tab>
<Tab zoneid="ijwtU5e7qE" title="Connection information">
<TabTitle>Connection information</TabTitle>

Provides operational guidance for connecting to and accessing the Kubernetes clusters from a local computer, as well as management of related access credentials. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).


</Tab>
<Tab zoneid="WHaWFafiyO" title="K8s events">
<TabTitle>K8s events</TabTitle>

Displays events related to all Kubernetes objects in the current cluster, including the event time, the type (warning or normal), the corresponding Kubernetes object, specific resource name, the event content and message, and the number of times each event has occurred. Event information helps you quickly understand the health and performance status of the cluster.

For details, see [Event management](https://docs.byteplus.com/en/docs/vke/Configuring-and-viewing-persistent-events).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The event retention duration (event\-ttl) is automatically set by the system. Events can be retained for up to 1 hour. However, when the cluster scale is large or the event volume surges, earlier events may be cleaned up in advance, and the actual visible duration may be shorter than 1 hour. To retain events for an extended period of time or to view historical events, we recommend installing the <a href="https://docs.byteplus.com/en/docs/vke/event-collector-add-on">event\-collector</a> add\-on to achieve event persistence. For more information, see <a href="https://docs.byteplus.com/en/docs/vke/Configuring-and-viewing-persistent-events">Configuring and viewing persistent events</a>.</div>



</Tab>
<Tab zoneid="YuRXUPl5MU" title="Control plane observability">
<TabTitle>Control plane observability</TabTitle>

Out\-of\-the\-box observability and log audit capabilities are provided for the cluster control plane. You do not need to manually configure monitoring dashboards or write log queries. This helps you quickly understand the status of the cluster control plane and identify API Server request exceptions. For details, see [Control plane observability](https://docs.byteplus.com/en/docs/vke/Control_plane_observability?lang=en).


</Tab>
<Tab zoneid="gW82N6VrIf" title="Control plane parameter configuration">
<TabTitle>Control plane parameter configuration</TabTitle>

Manage and update the control\-plane parameters for the cluster. For supported control plane parameters and detailed configuration instructions, see [Configuring control plane parameters](https://docs.byteplus.com/en/docs/vke/Configuring_control_plane_parameters).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Modifying the parameters of the control plane configuration will cause a cluster restart. Proceed with caution!</div>



</Tab>
</Tabs>
