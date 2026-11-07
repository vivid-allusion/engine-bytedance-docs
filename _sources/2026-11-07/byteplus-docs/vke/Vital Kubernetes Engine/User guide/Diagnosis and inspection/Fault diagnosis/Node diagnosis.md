---
title: "Node diagnosis"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Node-diagnosis"
---

Cluster diagnosis helps you identify risks in various resources within VKE clusters, such as node pools, nodes, and pods. This topic describes how to configure the node diagnosis feature.

<span id=".6YWN572u6K-K5pat"></span>
## Configuring diagnosis


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation pane, click **Diagnosis**. On the page that appears, click **Create diagnosis task** to configure a node diagnostic task.

   
   |Parameter |Description |
   |---|---|
   |Diagnosis type |Specify the type of resource to be diagnosed. For this example, select **Node**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you select <strong>Node</strong> as the diagnostic resource, you can diagnose both ECS nodes and VCI virtual nodes.</div><br> |
   |Nodes |In the **All nodes** list on the left side, select the nodes on which you need to perform diagnosis, and add them to the **Selected nodes** list on the right side. |
   

4. Click **Confirm** to complete the configuration. The system will start the diagnosis and generate a diagnostic report.


<span id=".5p-l55yL6K-K5pat57uT5p6c"></span>
## Viewing diagnostic results

After the diagnostic task is complete, if it is in the **Anomaly** state, it indicates that risks exist in the node. You can click **View details** in the **Actions** column that corresponds to the target diagnostic task to view the diagnostic report.

The diagnostic result will display all diagnostic items, including successful, failed, and warning ones. You need to view these items on the **Pending** tab and resolve the issues.

<span id=".5LiL6L296K-K5pat5oql5ZGK"></span>
## Downloading diagnostic reports

After the diagnostic task is complete, you can download the diagnostic report in PDF format.


1. After the diagnostic task is complete, click **View details** in the **Actions** column that corresponds to the target diagnostic task to view the diagnostic result.

2. Click **Download the report** in the upper\-right corner to download the diagnostic report in PDF format.


<span id=".6K-K5pat6aG56K-05piO5ZKM5L-u5aSN5bu66K6u"></span>
## Diagnostic item descriptions and Fix suggestions

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The diagnostic items slightly vary based on different node types, such as ECS nodes and VCI nodes. The diagnostic items displayed in the console shall prevail.</div>


<span id=".6IqC54K554q25oCB"></span>
### Node status


|Diagnostic item |Check content |Fix suggestions |Reference |
|---|---|---|---|
|Node status |Check whether the node is in the **Running** state. If the node is in an abnormal status, pods cannot be scheduled to the node. |Perform troubleshooting based on the node status. |[Node status](https://docs.byteplus.com/en/docs/vke/Resource-status-description#.6IqC54K5) |
|Whether pods can be scheduled to the node |Check whether pods can be scheduled to the node. If pods cannot be scheduled to the node, the actual resources and available resources of the cluster will be inconsistent. |View the node scheduling configuration (For example, the node is cordoned or set as unschedulable) for troubleshooting. |[Managing nodes](https://docs.byteplus.com/en/docs/vke/Managing-nodes) |
|Whether the node runtime is consistent with the cluster runtime |Check whether the node runtime is consistent with the cluster runtime. |None |None |


<span id=".6IqC54K56LSf6L29"></span>
### Node loads


|Diagnostic item |Check content |Fix suggestions |Reference |
|---|---|---|---|
|Node CPU load |Check whether the average utilization of the node CPU in the last hour reaches or exceeds 90%. |* Increase the number of nodes.<br><br>* Configure the node pool.<br><br>* Check the ResourceQuota of the pod, such as requests and limits. |* [Adding nodes](https://docs.byteplus.com/en/docs/vke/Adding-nodes)<br><br>* [Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool)<br><br>* [Managing Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment) |
|Node memory load |Check whether the average utilization of the node memory in the last hour reaches or exceeds 90%. |||
|Node MaxPod |Check whether the number of new pods that the node can accommodate is less than two. After the upper limit is reached, new pods cannot be scheduled to the node. |* Increase the number of nodes.<br><br>* Create a node pool. |* [Adding nodes](https://docs.byteplus.com/en/docs/vke/Adding-nodes)<br><br>* [Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool) |
|Whether node swap is enabled |Check whether the memory swap of the node is enabled. |None |None |
|Disk capacity of the container directory |Check whether the node disk utilization is greater than 80% (only for system volumes and container data volumes). |Log in to the node and clean up the disk to release disk space. |None |


<span id=".6IqC54K5572R57uc"></span>
### Node network


|Diagnostic item |Check content |Fix suggestions |Reference |
|---|---|---|---|
|Whether unregister_netdevice exists on the node |Checks whether unregister_netdevice errors occur in the node kernel. Network devices may be unable to deregister, which will lead to network connection issues and affect the overall operation of the cluster. |[Submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210) for processing. |None |
|Whether the node can access the public network |Check whether the node can access the public network. If the node cannot access the public network, it may lead to service access failures. |Enable the public network access feature for clusters. |[Enabling public network access for clusters](https://docs.byteplus.com/en/docs/vke/How-do-I-manually-enable-internet-facing-access-for-a-cluster) |
|Node DNS resolution |Check whether the DNS resolution feature of the node functions as expected. If DNS resolution fails, the node cannot access the public network by using domain names. |Check whether the DNS service of the node functions as expected. |None |


<span id=".6IqC54K557O757uf5Z-656GA"></span>
### Node system basics


|Diagnostic item |Check content |Fix suggestions |Reference |
|---|---|---|---|
|Node CNI add\-on status |Check the running status of the network add\-ons for the node, such as VPC\-CNI and Flannel. If the add\-on is abnormal, the pod networking on the node will become unavailable, and container creation and deletion operations cannot be performed. |[Submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210) for processing. |None |
|Node CSI add\-on status |Check the running status of the CSI add\-on for the node. If the add\-on is abnormal, the cluster storage service will become unavailable. |[Submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210) for processing. |None |
|Node containerd status |Check whether the containerd service of the node is in the `Active` state. |None |None |
|Node cgroup leakage |Check whether cgroup leakage has occurred on the node. Cgroup leakage on the node may lead to monitoring data collection errors and even prevent containers from starting. |* We recommend that you temporarily ignore this issue in most cases if the number of leaked cgroup directories is less than ten times the total number of node pods.<br><br>* If the number of leaked cgroup directories is excessive and causes exceptions to add\-ons, such as kubelet, the node needs to be restarted. |None |
|Node kubelet status |Check the kubelet status of the node. |None |None |
|Kube\-Proxy add\-on running status |Check the running status of the Kube\-Proxy add\-on for the node. |None |None |
|Whether the node systemd is hung |Check whether the node systemd is hung. |Log in to the node and restart systemd by using `systemctl daemon-reexec`. |[Logging in to nodes](https://docs.byteplus.com/en/docs/vke/Managing-nodes#ecs-terminal) |
|Node systemd version |Check the systemd version of the node. If the systemd version is low, stability risks may arise. As a result, add\-ons will fail to function as expected. |None |None |


<span id=".6IqC54K557O757uf5YaF5qC4"></span>
### Node system kernel


|Diagnostic item |Check content |Fix suggestions |Reference |
|---|---|---|---|
|Kernel SoftLockupError |Check whether the SoftLockupError error has occurred on the node kernel. This usually indicates that the CPU is occupied by a process for a long period of time and cannot execute other tasks. This may cause the entire system or some key services to become unresponsive. Therefore, when this issue occurs, you need to quickly locate and resolve the issue to prevent more serious issues in the system from occurring or the normal operation of other tasks from being affected. |[Submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210) for processing. |None |
|Kernel RCUStallError |Check whether the RCUStallError error has occurred on the node kernel. RCUStall is a synchronization mechanism used in the Linux kernel. If the RCUStallError occurs, it indicates that an issue exists with this mechanism, which may lead to system issues, such as system call failures and process deadlocks. This will affect the stability of the entire system. |[Submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210) for processing. |None |
|Kernel Oops |Check whether kernel Oops has occurred on the node. Kernel Oops indicates that the operating system kernel has encountered an unhandled condition or a severe system error. This often leads to system malfunction or a complete system crash. Therefore, it directly affects system stability and availability and needs to be treated with the highest priority. |[Submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210) for processing. |None |
|Kernel Ext4FsError |Check whether the Ext4FsError error has occurred on the node kernel. Ext4 is a commonly used file system in Linux systems. If Ext4FsError occurs, it usually indicates that a serious issue has occurred with the file system, such as data corruption and file loss, which will affect the normal operation of the system. More seriously, file system issues may lead to data loss. |[Submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210) for processing. |None |


<span id=".6Jma5ouf6IqC54K56K-K5pat"></span>
### Virtual node diagnosis


|Diagnostic item |Check content |Fix suggestions |Reference |
|---|---|---|---|
|The VCI\-related AccountQuota. Alerting is triggered when the quota is insufficient. |Check whether the remaining ResourceQuota of VCI within the current account is less than 10%. If resources are insufficient, the quota may be insufficient during business operations. |* Clean up resources to release ResourceQuota.<br><br>* [Submit an application](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=vke) to increase the quota. |[Usage limits](https://docs.byteplus.com/en/docs/vke/VCI-limits) |
|Check the running status of the meta\-cluster pod that corresponds to the VCI virtual node. |Check the running status of the meta\-cluster pod that corresponds to the VCI virtual node. If the meta\-cluster pod is abnormal, workloads on the virtual node may not run as expected. |[Submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210) for processing. |None |
|Whether pods on VCI virtual nodes can be created and deleted as expected by creating and deleting pods |Execute the **Create Workload** inspection case on the VCI virtual node to verify whether workloads can be created on the virtual node. |[Submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210) for processing. |None |
|Whether the pods on the VCI virtual node are in a normal status. |Check whether unready pods exist on the VCI virtual node. |Check the status of the pods on the VCI virtual node, promptly confirm the reason why the pods are not ready, and perform appropriate operations. |None |
