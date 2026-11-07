---
title: "Add existing nodes"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Adding-existing-nodes"
---

Worker nodes in a cluster can provide computing and storage resources for applications. You can add one or more nodes to a cluster by adding existing Elastic Compute Service (ECS) instances. This topic describes the detailed steps and parameter configuration for adding existing nodes.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The target cluster is in the **Running** state.

* You have available ECS instances in the same VPC as the cluster. For instructions, see [Purchase Elastic Compute Service](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Considerations


* The ECS instances that you selected will be rebound to security groups.

* To ensure the ECS instances can be added successfully, make sure that you format their data volumes to clear all the data. Otherwise, these data volumes will fail to be mounted to the storage directories `/var/lib/containerd` and `/var/lib/kubelet` respectively for the containers and images, and ECS instances cannot be added successfully.

* The [bare metal](https://docs.byteplus.com/en/docs/ecs/General-purpose-EBM) or certain High Performance Computing Optimized GPU nodes will be shut down when they are added to a cluster. For more details, see [StopInstance](https://docs.byteplus.com/en/docs/ecs/StopInstance).

* This topic describes the procedure of adding existing nodes to the default node pool `vke-default-nodepool`. Some custom node pools with certain restrictions also support adding existing nodes. For details, see [Manage node pools](https://docs.byteplus.com/en/docs/vke/Managing-NodePools#.5re75Yqg5bey5pyJ6IqC54K5).


<span id=".6ZuG576k6aaW5qyh5re75Yqg5bey5pyJ6IqC54K5"></span>
## Adding existing nodes to a cluster for the first time

If existing nodes are added to a cluster for the first time, a node pool needs to be configured to manage the nodes (ECS instances) to be added. The node pool name `vke-default-nodepool` is specified by VKE. After you add nodes, you can view them on the **Node pool** page. Other parameters for `vke-default-nodepool` need to be configured according to the instructions below.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After <code>vke-default-nodepool</code> is created, it will serve as the default node pool for the cluster. Any existing nodes added to this cluster in the future will be managed in the <code>vke-default-nodepool</code> node pool.</div>


* <div data-tips="true" data-tips-type="tip">The default node pool does not consume your node pool quota. For details about quota, see <a href="https://docs.byteplus.com/en/docs/vke/Limits">Limit</a>.</div>


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, select **Cluster**.

3. In the cluster list, click the name of the target cluster to which you want to add nodes.

4. In the left navigation bar, select **Nodes** \> **Node**.

5. On the **Node** page, click **Add existing node**.

6. Configure node parameters according to the following parameter descriptions.

   * Elastic Compute Service Choose

      
      |**Parameter** |**Description** |
      |---|---|
      |Target node project |The project to which the ECS instance to be added belongs. VKE will list the ECS instances in the selected project that can be added to the VKE cluster. |
      |All servers |This list displays all ECS instances that are in the same VPC as the current cluster in the selected project. Select the ECS instances as needed. |
      |Selected servers |This list displays the ECS instances that you have selected. |
      |Keep ECS instance name |* If this option is **selected**, the original name of the ECS instance will be retained after it is added to the cluster.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the names retained contain any Chinese characters, the system label <code>cluster.vke.volcengine.com/node-name</code> for that node will become invalid. Therefore, you need to avoid using the <code>cluster.vke.volcengine.com/node-name</code> label in scenarios such as affinity\-based scheduling.   </div><br>   <br><br>* If this option is **unselected**, the ECS instance will be renamed by VKE after it is added. |
      |Disk mount |* **If you select this checkbox**, the data volume will be formatted and mounted to `/var/lib/containerd` and `/var/lib/kubelet` **.** <br><br>   * **Device name**: (Required) Specify the data volume device. You can enter the device name of the data volume, e.g., `/dev/vdb`, or the partition name of the data volume, e.g., `/dev/vdb1`.<br><br>   * **Mount point**: Specify the mount point path. If the mount point is not specified, the default mount point will be used, such as `/mnt/vdb`.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Before enabling it, make sure that the data volumes of the selected ECS instances to be added to the cluster do not have any residual data. Otherwise, adding existing nodes will fail. For actions to clear residual data from the data volume, see <a href="https://docs.byteplus.com/en/docs/vke/How-do-I-clean-up-residual-data-on-the-data-volumes-of-existing-nodes">FAQ</a>.   </div><br>   <br><br>* **If it is not enabled** (default), the `/var/lib/containerd` and `/var/lib/kubelet` directories are mounted to the system volume partition where the operating system runs. |
      |Reinstall OS |* **If you select this option**, the operating system of the ECS instance will be reinstalled, and the existing data on the system volume of the instance will be cleared.<br><br>* If you **do not select** this option, the ECS instance will retain its existing operating system and system volume data.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you continue to use the existing operating system and system volume data of the ECS instance, make sure that the ECS instance meets the following requirements. Otherwise, the node will fail to be added.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The ECS instance must be in the <strong>RUNNING</strong> state.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The ECS instance must have the Cloud Assistant Agent installed, and the Cloud Assistant Agent must be in the <strong>Running</strong> state.   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Go to the <a href="https://console.byteplus.com/ecs">ECS console</a> to view the status of the ECS instance and its related resources.   </div><br>    |
      |Operating system |This parameter is displayed after you select **Reinstall OS**.<br><br>Select an operating system image for nodes based on your business requirements. Valid values: Public images, Custom images, and Shared images.<br><br><br>* **Public images**: official, copyrighted images provided by BytePlus. These images combine basic OS with initialization components, delivering security, high availability, and open access for all users.<br><br>   For the public images supported by VKE and their associated instance families, see [Overview of operating system images](https://docs.byteplus.com/en/docs/vke/Overview-of-operating-system-images).<br><br>* **Custom images**: Images created and uploaded by you. In addition to the operating system, the images also have public or private applications pre\-installed. These images are suitable for redeploying complex initialization systems or deploying multiple systems with the same configurations.<br><br>   VKE allows you to specify custom images as node operating systems. For more details, see [Overview of operating system images](https://docs.byteplus.com/en/docs/vke/Overview-of-operating-system-images).<br><br>* **Shared images**: the images shared by other BytePlus accounts. You can use shared images to quickly deploy the same software environment as that of nodes created by other users, or share custom images that you have created or uploaded with other BytePlus accounts.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">You need to create custom images and shared images by using VKE base images. Check whether a GPU version is required based on your business requirements.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Custom images are available at the node pool project level.</div><br> |
      |Restart and install cloud assistant Agent |This parameter is displayed after you select **Reinstall OS**.<br><br>The agent is installed by default. This setting cannot be modified. Using the Agent to manage nodes can facilitate fault monitoring and self\-healing. |
      |ECS tags |VKE will bind the BytePlus platform labels to the ECS instances added to the cluster to facilitate search and management.<br><br>Click **Add new**, and enter the **key** and **value** as prompted on the page. |
      

   * Security configuration

      
      |**Parameter** |**Description** |
      |---|---|
      |Security group |To ensure the proper functioning of clusters and nodes, VKE provides a security group by default.<br><br>If you need to add custom security group rules, ensure the new rules do not conflict with the default ones. For more information about the default security group, see [Security group settings](https://docs.byteplus.com/en/docs/vke/Security-group-settings). |
      |Login methods |Configure the login method for nodes of the cluster running on VKE.<br><br><br>* **Password**: Enter the root password twice to confirm.<br><br>* **SSH key pair**: A secure login authentication method that consists of a public key and a private key and supports only Linux instances. If there are no SSH key pairs available, click **Create key pair** at the bottom of the Key pair dropdown menu to create one. For an introduction to key pairs, see [Key pairs](https://docs.byteplus.com/en/docs/ecs/Key-pair-overview).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The reason for configuring login methods here is that the operating systems on the ECS to be added will be reinstalled with the image you selected in the <strong>Operating system</strong> settings. Any ECS instances added afterward to the default node pool <code>vke-default-nodepool</code>  will inherit this login method. You can change the login method by editing the default node pool.</div><br> |
      |Security reinforcement |Configure host security hardening.<br><br><br>* **Enable** (default): The host\-based intrusion detection system (HIDS) provides free risk alerting services, such as alerts for abnormal logins. While maintaining compatibility with host operating system images, HIDS provides security hardening features for nodes (ECS instances), including real\-time monitoring, file monitoring, process monitoring, and dynamic system analysis.<br><br>* **Disable**: The security hardening feature is not enabled. |
      

   * More configuration

      
      |**Parameter** |**Description** |
      |---|---|
      |Node labels |Labels in VKE function identically to Kubernetes labels. Labels can be used to define attributes for nodes, facilitating node operations and management. A label can be added in batches to all the nodes in the node pool.<br><br>Click **Add node labels** and enter a key and its value****.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Custom node labels cannot be the same as system labels. For details of system labels, see <a href="https://docs.byteplus.com/en/docs/vke/System-labels-and-taints">System labels and taints</a>.</div><br> |
      |Node taints |Taints allow nodes to repel specific pods and therefore prevent those pods from being scheduled to the nodes. You can add the same taint to multiple nodes in the node pool at the same time.<br><br>Click **Add node taints**, and enter the **key** and **value** as prompted on the page.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Custom node taints cannot conflict with system taints. For a list of system taints, see <a href="https://docs.byteplus.com/en/docs/vke/System-labels-and-taints">System labels and taints</a>.</div><br> |
      |Enable auto renew for node labels and taints |Configure automatic updating for node labels and taints.<br><br><br>* **Selected (default)** : enables automatic updating. The labels or taints added to or modified in a node pool will be automatically synchronized to both the existing and new nodes. In addition, if you modify the labels or taints for existing nodes, the configurations of the nodes will be overwritten by the configurations of the node pool.<br><br>* **Cleared**: does not enable automatic updating. The labels or taints added to or modified in a node pool will be synchronized only to the new nodes, but not the existing ones. In addition, if you modify the labels and taints for existing nodes, the modified configurations take effect and will not be overwritten by the configurations of the node pool.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Disabling automatic updating for node labels and taints may cause features that use fixed node labels to behave unexpectedly. Proceed with caution.</div><br> |
      |Node pool tags |Custom resource tags, which are used to flexibly manage the default node pool `vke-default-nodepool`.<br><br>Click **Add new**, and enter the **key** and **value** based on the on\-screen prompts. |
      

   * Advanced settings

      
      |**Parameter** |**Description** |
      |---|---|
      |Custom name |Select and configure the custom name types for nodes in the node pool as needed. You can configure multiple custom name types at the same time.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">VKE provides a tool for automatically specifying custom names for all nodes in a node pool. To use the tool, click <strong>Auto generation</strong>. After custom names are automatically configured, we recommend that you click <strong>Generate random names</strong> to add random suffixes to prevent the custom names of the newly scaled\-out nodes from conflicting with each other. This ensures smooth scale\-out of nodes in the node pool.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Nodes added during subsequent scale\-out operations in the node pool will use the custom name set here or be named according to the custom naming rule set here.</div><br><br><br>* **Node name**: used to quickly identify nodes in VKE or ECS. You can use one of the following methods to specify node names:<br><br>   * **Node name prefix**: Specify the node name prefix based on the displayed naming rules.<br><br>* **Node metadata name**: Specify the metadata name (metadata.name) of a node object in Kubernetes. The metadata name is used to identify resources in external systems such as monitoring and alerting systems. You can use one of the following two methods to specify metadata names:<br><br>   * **Use node hostname**: Use the hostname of the node as the node metadata name.<br><br>   * **Set prefix and suffix for node metadata name**: Specify the prefix or suffix of the node metadata name. The system generates the complete node metadata name in the `prefix-node IP-suffix` format. |
      |Image lazy loading |[Public beta] This feature is not enabled by default. If it is enabled, the nodes in the node pool `vke-default-nodepool` can use the container image acceleration feature as needed. For more information, see [Container image lazy loading solutions](https://docs.byteplus.com/en/docs/vke/Container-image-lazy-loading-solution).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Only nodes that run containerd 1.4.13\-vke.3 or later can use this feature. To view containerd versions, see <a href="https://docs.byteplus.com/en/docs/vke/What-container-runtimes-does-VKE-currently-support">FAQ</a>.</div><br> |
      |InitializeScript |Enter a shell script. After Kubernetes add\-ons are deployed on the node, the script is automatically executed. You need to implement the script commands yourself and ensure that the script supports reentrancy and retry logic. The script and the related logs can be found in the `/usr/local/vke/userscripts` directory on the node.<br><br>This feature is commonly used in scenarios such as modifying kubelet configurations. |
      |Cordon node |Disabled by default. If enabled, new pods cannot be scheduled to that node. This action only applies to worker nodes. You can also execute the `kubectl uncordon` command to disable it manually. |
      

7. Check the configurations and then click **Confirm** to start adding nodes.

   On the **Node** page, view the status of the node you just added. The **status** showing **Running** indicates that the node was added successfully.


<span id=".6ZuG576k6Z2e6aaW5qyh5re75Yqg5bey5pyJ6IqC54K5"></span>
## Adding more existing nodes to a cluster

At this point, the default node pool `vke-default-nodepool` already exists. You can continue to add existing nodes according to the following instructions.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, select **Cluster**.

3. In the cluster list, click the name of the target cluster to which you want to add nodes.

4. In the left navigation bar, select **Nodes** \> **Node**.

5. On the **Node** page, click **Add existing node**.

6. Configure node parameters according to the following parameter descriptions.

   * Default node pool information

      
      |**Parameter** |**Description** |
      |---|---|
      |Node pool management |Displays the default node pool name and configuration information.<br><br>The existing nodes added to the cluster will inherit all configurations of the default node pool. This parameter cannot be updated. |
      

   * Elastic Compute Service Configuration

      
      |**Parameter** |**Description** |
      |---|---|
      |Target node project |The project to which the ECS instance to be added belongs. VKE will list the ECS instances in the selected project that can be added to the VKE cluster. |
      |All servers |This list displays all ECS instances under your account in the current region that are in the same VPC as the current cluster. Select the ECS instances as needed. |
      |Selected servers |This list displays the ECS instances that you have selected. |
      |Keep ECS instance name |* If this option is selected, the original name of the ECS instance will be retained after it is added to the cluster.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the names retained contain any Chinese characters, the system label <code>cluster.vke.volcengine.com/node-name</code> for that node will become invalid. Therefore, you need to avoid using the <code>cluster.vke.volcengine.com/node-name</code> label in scenarios such as affinity\-based scheduling.   </div><br>   <br><br>* If this option is unselected, the ECS instance will be renamed by VKE after it is added. |
      |Disk mount |* If you select this checkbox, the data volume will be formatted and mounted to `/var/lib/containerd` and `/var/lib/kubelet`. You also need to set the **Device name** parameter to specify a device name. You can enter the device name of the data volume, e.g., `/dev/vdb`, or the partition name of the data volume, e.g., `/dev/vdb1`.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Before enabling it, make sure that the data volumes of the selected ECS instances to be added to the cluster do not have any residual data. Otherwise, adding existing nodes will fail. For actions to clear residual data from the data volume, see <a href="https://docs.byteplus.com/en/docs/vke/How-do-I-clean-up-residual-data-on-the-data-volumes-of-existing-nodes">FAQ</a>.   </div><br>   <br><br>* If it is not enabled (default), the `/var/lib/containerd` and `/var/lib/kubelet` directories are mounted to the system volume partition where the operating system runs. |
      |Reinstall OS |* **If you select this option**, the operating system of the ECS instance will be reinstalled, and the existing data on the system volume of the instance will be cleared.<br><br>* If you **do not select** this option, the ECS instance will retain its existing operating system and system volume data.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you continue to use the existing operating system and system volume data of the ECS instance, make sure that the ECS instance meets the following requirements. Otherwise, the node will fail to be added.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The ECS instance must be in the <strong>RUNNING</strong> state.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The ECS instance must have the Cloud Assistant Agent installed, and the Cloud Assistant Agent must be in the <strong>Running</strong> state.   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Go to the <a href="https://console.byteplus.com/ecs">ECS console</a> to view the status of the ECS instance and its related resources.   </div><br>    |
      |Operating system |This parameter is displayed after you select **Reinstall OS**.<br><br>Select an operating system image for nodes based on your business requirements. Valid values: Public images, Custom images, and Shared images.<br><br><br>* **Public images**: official, copyrighted images provided by BytePlus. These images combine basic OS with initialization components, delivering security, high availability, and open access for all users.<br><br>   For the public images supported by VKE and their associated instance families, see [Overview of operating system images](https://docs.byteplus.com/en/docs/vke/Overview-of-operating-system-images).<br><br>* **Custom images**: Images created and uploaded by you. In addition to the operating system, the images also have public or private applications pre\-installed. These images are suitable for redeploying complex initialization systems or deploying multiple systems with the same configurations.<br><br>   VKE allows you to specify custom images as node operating systems. For more details, see [Overview of operating system images](https://docs.byteplus.com/en/docs/vke/Overview-of-operating-system-images).<br><br>* **Shared images**: the images shared by other BytePlus accounts. You can use shared images to quickly deploy the same software environment as that of nodes created by other users, or share custom images that you have created or uploaded with other BytePlus accounts.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">You need to create custom images and shared images by using VKE base images. Check whether a GPU version is required based on your business requirements.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Custom images are available at the node pool project level.</div><br> |
      |Restart and install cloud assistant Agent |This parameter is displayed after you select **Reinstall OS**.<br><br>The agent is installed by default. This setting cannot be modified. Using the Agent to manage nodes can facilitate fault monitoring and self\-healing. |
      

   * More configuration

      
      |**Parameter** |**Description** |
      |---|---|
      |Node labels |Labels in VKE function identically to Kubernetes labels. Labels can be used to define attributes for nodes, facilitating node operations and management. A label can be added in batches to all the nodes in the node pool.<br><br>Click **Add node labels** and enter a key and its value****.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Custom node labels cannot be the same as system labels. For details of system labels, see <a href="https://docs.byteplus.com/en/docs/vke/System-labels-and-taints">System labels and taints</a>.</div><br> |
      |Node taints |Taints can prevent specific pods from being scheduled to this node. You can add the same taint to multiple nodes in a node pool in batch.<br><br>Click **Add node taints**, and enter the **key** and **value** as prompted on the page.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Custom node taints cannot conflict with system taints. For a list of system taints, see <a href="https://docs.byteplus.com/en/docs/vke/System-labels-and-taints">System labels and taints</a>.</div><br> |
      

   * Advanced settings

      
      |**Parameter** |**Description** |
      |---|---|
      |Image lazy loading |[Public beta] This feature is not enabled by default. If it is enabled, the nodes in the node pool `vke-default-nodepool` can use the container image acceleration feature as needed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Only the nodes with a containerd version 1.4.13\-vke.3 or later can use this feature. To view containerd versions, see <a href="https://docs.byteplus.com/en/docs/vke/What-container-runtimes-does-VKE-currently-support">FAQ</a>.</div><br> |
      |InitializeScript |Enter a shell script. After Kubernetes add\-ons are deployed on the node, the script is automatically executed. You need to implement the script commands yourself and ensure that the script supports reentrancy and retry logic. The script and the related logs can be found in the `/usr/local/vke/userscripts` directory on the node.<br><br>This feature is commonly used in scenarios such as modifying Containerd configuration parameters. |
      |Cordon node |Disabled by default. If enabled, new pods cannot be scheduled to that node. This action only applies to worker nodes. You can also execute the `kubectl uncordon` command to disable it manually. |
      

7. Check the configurations and then click **Confirm** to start adding nodes.

   On the **Node** page, view the status of the node you just added. The **status** showing **Running** indicates that the node was added successfully.
