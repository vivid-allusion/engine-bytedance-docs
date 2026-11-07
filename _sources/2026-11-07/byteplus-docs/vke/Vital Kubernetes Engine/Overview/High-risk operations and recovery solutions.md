---
title: "High-risk operations and recovery solutions"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/High-risk-operations-and-recovery-solutions"
---

When you run or deploy workloads on Vital Kubernetes Engine (VKE), you may perform high\-risk operations at different levels, which can lead to varying degrees of service failures. To help you better understand, estimate, and avoid operational risks, this topic describes high\-risk operations, impacts, and recovery solutions from perspectives such as cluster, node pool, node, network and load balancer, storage, log, and add\-on.

<span id=".6ZuG576kLeiKgueCueaxoC3oioLngrk="></span>
## Cluster / Node pool / Node


|Category |High\-risk operation |Impact |Recovery solution |
|---|---|---|---|
|API server |Operations are performed on CLB instances associated with the API server and the subresources, such as listeners and server groups. |Operations cannot be performed on cluster\-related resources. |No recovery solutions are available. |
|Container runtime |Use or install Docker or other runtimes on nodes.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">VKE currently supports only the containerd runtime.</div><br> |The node may become unavailable. |Remove the node and retain the ECS instance. Then, add the retained ECS instance to the VKE cluster using the method of adding an existing node, complete node initialization, and restore the container runtime supported by VKE. For detailed instructions, see [Removing nodes](https://docs.byteplus.com/en/docs/vke/Managing-nodes#.56e76Zmk6IqC54K5) and [Adding existing nodes](https://docs.byteplus.com/en/docs/vke/Adding-existing-nodes).  |
|Worker node |The default security group for a node in a cluster is modified. |The node may become unavailable. |Restore to the default security group settings. For more information on the default security group for nodes, refer to [Security group settings](https://docs.byteplus.com/en/docs/vke/Security-group-settings). |
||The parameters of a core node component such as kubelet are modified. |The node may become unavailable. |Restore the core component to its default configuration. |
||A node is removed without retaining the Elastic Compute Service (ECS) instance. |The node becomes unavailable. |No recovery solutions are available. |
||The IP address of a node is changed. |The node becomes unavailable. |Change the IP address to the original one. |
||The operating system is re\-installed. |The node add\-on is deleted. |Remove the node and retain the ECS instance. Then, add existing nodes to re\-add the retained ECS instance to the VKE cluster. For detailed instructions, see [Removing nodes](https://docs.byteplus.com/en/docs/vke/Managing-nodes#.56e76Zmk6IqC54K5) and [Adding existing nodes](https://docs.byteplus.com/en/docs/vke/Adding-existing-nodes).  |
||The configuration of the operating system is modified. |The node may become unavailable. |Restore to the original configuration. |
||Change the instance specification of the ECS instance corresponding to the node. |Node parameters such as maxPods and other resource reservation parameters may not meet expectations. |Remove the node and retain the ECS instance. Then, add existing nodes to re\-add the retained ECS instance to the VKE cluster. For detailed instructions, see [Removing nodes](https://docs.byteplus.com/en/docs/vke/Managing-nodes#.56e76Zmk6IqC54K5) and [Adding existing nodes](https://docs.byteplus.com/en/docs/vke/Adding-existing-nodes).  |
||The permissions on the directory in a node are modified. |The node may become unavailable. |Restore to the original permission configuration. |
||The kubelet and containerd services of a node are manually stopped. |The node becomes unavailable. |Restart the kubelet and containerd services. |
||The kernel version of the node operating system is upgraded or downgraded. |The node may be abnormal or unable to run pods. |Roll back to the original kernel version of the operating system. |
||Important data is saved in the system disk of an ECS instance. |The data in the system disk is lost when the node is removed. |No recovery solutions are available. |
||A node is removed by running a kubectl command. |The node becomes abnormal. |Remove the node and add it again. |
||Data is not backed up when an existing node is added. |The data on the existing ECS instance may be lost. |Back up data in advance. |
||The ECS instance corresponding to a node is manually stopped. |The node becomes unavailable. |Restart the ECS instance. |
|Node pool management |A node pool is removed. |All nodes in the node pool are removed. |No recovery solutions are available. |
||A custom image is selected when you create a node pool, and it is deleted on the ECS side. |New nodes cannot be added. |Re\-edit the node pool and select an available default image. |
|Others |Modify or delete relevant role policies, such as AssumeRoleForVKE. |The cluster features may become unavailable. |Set a role policy again. For more information, refer to [Configuring IAM user permissions](https://docs.byteplus.com/en/docs/vke/Configuring-IAM-user-permissions). |


<span id=".572R57uc5LiO6LSf6L295Z2H6KGh"></span>
## Network and Load Balancer

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Network and load balancing kernel parameters can be viewed using the <code>sysctl -a</code> command, depending on your operating system.</div>



|High\-risk operation |Impact |Recovery solution |
|---|---|---|
|Modify the CLB/ALB configuration managed by VKE via the Load Balancer console, including the CLB/ALB, listeners, and backend server groups. |CLB/ALB anomalies occur. |Restore the CLB/ALB configuration. |
|The kernel parameters are modified:<br><br><br>* IPv4\-based clusters: `net.ipv4.ip_forward=0`<br><br>* IPv6\-based clusters: `net.ipv6.ip_forward=0` |A network connection fails. |Modify the kernel parameters as follows:<br><br><br>* IPv4 cluster: `net.ipv4.ip_forward=1`<br><br>* IPv6 cluster: `net.ipv6.ip_forward=1` |
|The kernel parameters are modified:<br><br><br>* `net.ipv4.conf.all.rp_filter = 1\|2`<br><br>* `net.ipv4.conf.[eth*].rp_filter = 1\|2`<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>eth*</code> indicates all network interface cards (NICs) starting with <code>eth</code>.</div><br> |A network connection fails. |Modify the kernel parameters as follows:<br><br><br>* `net.ipv4.conf.all.rp_filter = 0`<br><br>* `net.ipv4.conf.[eth*].rp_filter = 0` |
|The kernel parameters are modified:<br><br>`net.ipv4.vs.conn_reuse_mode = 0`<br><br>The kernel parameters for IPv6\-based clusters are modified:<br><br>`net.ipv6.conf.all.disable_ipv6=1` |When traffic in short\-lived connections is highly concurrent and a rolling upgrade is executed for Service Pods, Service access failure may be triggered.<br><br>The IPv6 network becomes unavailable. |Modify the kernel parameters as follows:<br><br>`net.ipv4.vs.conn_reuse_mode = 1`<br><br>Modify the kernel parameters as follows:<br><br>`net.ipv6.conf.all.disable_ipv6=0` |
|The kernel parameters are modified:<br><br><br>* `net.bridge.bridge-nf-call-ip6tables=0`<br><br>* `net.bridge.bridge-nf-call-iptables=0` |A NAT Gateway becomes abnormal. |Modify the kernel parameters as follows:<br><br><br>* `net.bridge.bridge-nf-call-ip6tables=1`<br><br>* `net.bridge.bridge-nf-call-iptables=1` |
|The kernel parameters are modified:<br><br>`net.ipv6.conf.[eth*].accept_ra=1` |The IPv6 routing cannot be learned and a network connection fails. |The kernel parameters are modified:<br><br>`net.ipv6.conf.[eth*].accept_ra=2` |
|The kernel parameters are modified:<br><br>`net.ipv4.tcp_tw_recycle = 1` |A NAT Gateway becomes abnormal. |Modify the kernel parameters as follows:<br><br>`net.ipv4.tcp_tw_recycle = 0` |
|Remove the annotation for reusing an existing CLB instance from a Service: `service.beta.kubernetes.io/volcengine-loadbalancer-id: ${YOUR_LB_ID}`. |The CLB instance becomes abnormal. |Add the annotation to the Service.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Service that reuses the existing CLB instance cannot be directly changed to a Service that uses an automatically created CLB instance. You need to recreate the Service.</div><br> |


<span id=".5a2Y5YKo"></span>
## Storage


|High\-risk operation |Impact |Recovery solution |
|---|---|---|
|A cloud disk is manually unmounted in the console. |An I/O error occurs when a pod writes data. |Restart the pod and manually clean up the residues mounted on the node. |
|Run the umount command for a disk mount path on a node. |A pod writes data to a local disk. |Restart the pod. |
|A cloud disk is directly operated on the node. |A pod writes data to a local disk. |No recovery solutions are available. |
|A FileNAS mount directory is manually deleted. |An I/O error occurs when a pod writes data. |Restart the pod. |
|A FileNAS volume or mount target in use is deleted. |An I/O hang occurs on a pod. |Restart the ECS node. |


<span id=".5pel5b-X"></span>
## Log


|High\-risk operation |Impact |Recovery solution |
|---|---|---|
|The `/var/lib/filebeat-registry` directory of a host is deleted. |A log is repeatedly collected. |No recovery solutions are available. The file in this directory records the log collection location. |
|The `/var/lib/filebeat-data` directory of a host is deleted. |A log is lost. |No recovery solutions are available. This directory contains log cache files to be consumed. |
|A collectrule custom resource definition (CRD) and its resource are deleted. |Log collection does not take effect. |Re\-create the deleted CRD and its resources. The logs generated when it does not take effect cannot be restored.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If a CRD is deleted, all associated instances are deleted. You are required to manually create the deleted instances even if the CRD is restored.</div><br> |
|A collection rule with a VKE tag is deleted on the Torch Log Service (TLS) side. |Log collection does not take effect. |Re\-create the collectrule CRD and its resources. |
|A log add\-on is deleted. |Log collection does not take effect. |Re\-install the log add\-on and manually restore the collectrule CRD and its resources. The logs generated when the add\-on is deleted cannot be restored.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When a log add\-on is deleted, the collectrule CRD, its resource, and log\-collector are deleted. In addition, the log collection capabilities become invalid during this period.</div><br> |


<span id=".57uE5Lu2"></span>
## Add\-ons


|High\-risk operation |Impact |Recovery solution |
|---|---|---|
|Add\-on resources such as workloads and configuration items are deleted. |The add\-on becomes unavailable. |For a non\-system\-required add\-on, you can fix this issue by uninstalling and re\-installing the add\-on. This issue cannot be fixed for a system\-required add\-on. |
|Add\-on resources such as workloads and ConfigMaps are modified. |The add\-on becomes unavailable or the configuration is refreshed. |Restore the add\-on to its original configuration or uninstall and re\-install the add\-on. This issue cannot be fixed if the add\-on is required by the system. |
|A resource with the same name as an add\-on is created in the namespace where the add\-on is to be installed. |The add\-on installation fails. |Delete the resources with the same name in the target namespace. Then install the add\-on. |
