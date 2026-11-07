---
title: "Managing node pools"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Managing-NodePools"
---

After you create node pools in a cluster, you can go to the node pool management page to manage them. This topic describes the scenarios, impacts, and procedures for node pool operations.

<span id=".57yW6L6R6IqC54K55rGg"></span>
## Editing node pools

You can modify configurations related to the node pool, including basic information, worker nodes, system, and security configurations.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The default node pool <code>vke-default-nodepool</code> is not editable in <strong>node pool information</strong>, <strong>worker nodes</strong>, and <strong>system configurations</strong>.</div>


* <div data-tips="true" data-tips-type="tip">Except for the parameters that are explicitly described as only effective for new nodes, the rest are either for the node pool or for both existing and new nodes. For details, see the description for each parameter.</div>


1. Log in to the [VKE console](https://console.byteplus.com/vke).In the left navigation bar, click **Cluster**.

2. Click the target cluster name. In the left navigation bar of the cluster management page, click **Nodes** \> **Node pool**.

3. Click **Edit** in the **Actions** column that corresponds to the target node pool to edit parameters based on the following descriptions. After you edit parameters, click **Confirm**.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Node pool information** ||
   |Name |Modify the node pool name based on the naming rules prompted by the system. A node pool name must be unique within the same cluster. |
   |Billing method |The billing method of the nodes in the current node pool.<br><br><br>* You can change the billing method from **Subscription** to **Pay\-as\-you\-go** for a node pool.<br><br>* You can change the billing method from **Pay\-as\-you\-go** to **Subscription** for a node pool when the following conditions are met:<br><br>   * **Autoscaling** is disabled.<br><br>   * The elastic scheduled scale\-out rule is disabled.<br><br>* **Spot instance**: This billing type cannot be changed.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">After you change <strong>Pay\-as\-you\-go</strong> to <strong>Subscription</strong>, you also need to specify the <strong>Duration of purchase</strong> parameter, the <strong>Automatic renewal</strong> parameter, and the <strong>Automatic renewal duration</strong> parameter.</div><br><br><br>* <div data-tips="true" data-tips-type="default">After you update the billing method, billing duration, or other configurations of nodes, the new configurations will only take effect on newly added nodes. For existing nodes, go to the <a href="https://console.byteplus.com/ecs">ECS console</a> to manually modify their configurations.</div><br> |
   |Check and self\-healing |You can edit this parameter for a managed node pool. Specify whether to enable the node check and self\-healing feature.<br><br><br>* **Enable**: By configuring node self\-healing rules, the system automatically checks for kubelet and runtime failures, GPU card status, and other node failures. When a node fails, the system promptly cordons the node to prevent Pods from being scheduled to it. For more information, see [Check and self-healing overview](https://docs.byteplus.com/en/docs/vke/Check_and_self-healing_overview).<br><br>* **Disable:**  Does not enable this feature. This is the default setting. |
   |Check and self\-healing rules |After you enable node check and self\-healing, you can specify node self\-healing rules. If you have not configured a self\-healing rule, click **Create check and self\-healing rule** to create one. For details, see [Configuring check and self-healing for nodes in a node pool](https://docs.byteplus.com/en/docs/vke/NodePool-health-check-and-auto-repair). |
   |Autoscaler |Modify the enabling status and related configurations of the node pool.<br><br><br>* **Number of nodes**: the nodes in this pool will be adjusted by the autoscaler dynamically within the range you set here. Enter integers from 0 to 2000.<br><br>   If the nodes actually required exceed the total node quota of the cluster, you can log in to [Quota center ](https://console.byteplus.com/quota)to apply for a higher node quota.<br><br>* **Priority**: When the elastic scale\-out algorithm uses the priority strategy, scale\-out is performed on the node pool with a higher priority. The larger the number, the higher the priority. Valid values: 0 to 100. |
   |Node subnet |Update the subnets of the node pool by adding one or more subnets within the following scope to provide network support for the nodes:<br><br><br>* If the cluster uses the VPC\-CNI network mode, all subnets in the subnet availability zone of the cluster will be displayed.<br><br>* If the cluster uses the Flannel network mode, all subnets in the VPC where the cluster is located are displayed.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">You cannot modify the configurations of configured subnets. You can add subnets based on existing subnets.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can drag and drop subnets to reorder them as needed.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">A node pool can be associated with up to eight subnets.</div><br> |
   |Instance type |The list of available instance types in the current subnet. Select an instance type based on your business requirements. For detailed descriptions of instance types, see [Instance specification list](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">After you update the instance type of the node pool, new nodes will be added based on the updated instance type during scale\-out. Existing nodes of the original instance type are not affected.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">An instance type may be unselectable for the following reasons:</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">ECS resources of this type are no longer available for purchase.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">Instance types cannot span CPU/GPU categories or different GPU vendors.</div><br> |
   |Selected Specifications |The selected instance specifications for nodes in the node pool. You can select up to 10 instance specifications.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If you select multiple instance types, the system sorts node specifications in the order in which they are selected.</div><br><br><br>   * <div data-tips="true" data-tips-type="default">When Cluster Autoscaler (CA) scales nodes, it first chooses an instance specification with higher priority in the sequence of the instance specifications. When higher\-priority specifications cannot be provisioned due to insufficient inventory or other failures, the system sequentially switches to lower\-priority specifications for scale\-out.</div><br><br><br>   * <div data-tips="true" data-tips-type="default">If you use Karpenter to implement auto scaling, the node pool scales out with nodes of various specifications based on resource requirements. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Configure_node_instant_autoscaler_Karpenter">Configuring instant autoscaling (Karpenter)</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can prioritize instance specifications in the list. To do so, hover over the icon before the sequence number of an instance specification, and then drag and drop it to the desired position.</div><br> |
   |Pricing |This parameter is displayed after **Billing method** is set to **Spot instance**.<br><br>Pricing of spot instances:<br><br><br>* **Auto\-bid**: Uses the pay\-as\-you\-go instance type price as the upper limit. This means that the real\-time market price is always used as the billing settlement price of the spot instance. When resource supply and demand change, the instance is automatically released. Back up your data in advance.<br><br>* **Set single\-instance price cap**: Sets the highest price that you accept for the instance. This price only indicates your purchase intention. The market price is still used for billing settlement. After an instance is purchased, if the market price exceeds your bid or if resource supply and demand change, the instance is automatically released. Back up your data in advance.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Updating the pricing of spot instances takes effect only for newly added nodes. Existing nodes are not affected.</div><br><br><br>* <div data-tips="true" data-tips-type="default">We recommend using this parameter together with the <strong>Spot instance compensation</strong> parameter in the <strong>Advanced settings</strong> section to perform data backup and other operations when instances are released.</div><br> |
   |High\-performance computing cluster |This parameter is available if you select **High Performance Computing Optimized** for **Instance type**.<br><br>Select the HPC cluster and project for the HPC\-optimized nodes. If no HPC cluster is available, click **Create high\-performance computing cluster** to create one.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The availability zone of the selected HPC cluster must be within the availability zone of the current node pool subnet.</div><br> |
   |Project of ECS instances |Specify the owning project for the ECS instances corresponding to nodes in the node pool. This allows operations and maintenance, authorization, resource management, and other actions on the ECS instances at the project level. For more project operations and details, see [Project management](https://docs.byteplus.com/en/docs/vke/Project-management).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After the update, the project only takes effect on newly added nodes in the node pool. Existing nodes still belong to the previous project.</div><br> |
   |Buy affinity group |[[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] This parameter is displayed only after an instance type that supports affinity groups is selected or Buy affinity group is enabled for the node pool.<br><br>You can modify the status of Buy affinity group only if no nodes exist in the node pool.<br><br><br>* When the affinity group feature is not enabled for the node pool, if the number of nodes in the node pool is 0 and you select an ECS specification that supports affinity groups, you can enable Buy affinity group. Otherwise, you cannot enable it.<br><br>* When the affinity group feature is enabled for the node pool, if the number of nodes in the node pool is 0 and you select an ECS specification that supports affinity groups, you can disable Buy affinity group or modify Affinity group size. Otherwise, you cannot perform the preceding operations.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">To obtain the list of ECS instance types that support affinity groups, contact your BytePlus account manager.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Node pools purchased as an affinity group are subject to the following constraints:</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">You cannot select multiple instance types.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">You cannot enable autoscaling.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">Only instances that use the pay\-as\-you\-go or subscription billing methods are supported. Spot instances and elastic scheduled instances are not supported.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">You need to set <strong>Number of nodes</strong> to an integer multiple of <strong>Affinity group size</strong> subsequently.</div><br> |
   |**More configurations** ||
   |Node pool tags |Custom tags for classifying, retrieving, and aggregating node pools with similar characteristics from different dimensions. Node pool tags enable you to manage node pools more flexibly and efficiently. |
   |Scheduling policy for multi\-subnets |Specify scheduling priorities for multiple subnets in the node pool. Worker nodes are scheduled based on the subnet priority during scale\-out. The following two policies are available:<br><br><br>* **Balancing policy**: Newly added nodes during a scale\-out are evenly distributed across multiple subnets. Under this policy, the order of subnets does not matter.<br><br>* **Subnet priority**: The subnets that appear earlier in the sequence have higher priorities. During scaling, nodes are first added to subnets with higher priority. |
   |Network communication mode |[[Beta · Apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] The network communication mode between nodes. Valid values: TCP communication mode and RDMA communication mode.<br><br><br>* **TCP communication mode**: A communication method for data transmission based on Transmission Control Protocol (TCP).<br><br>* **RDMA communication mode**: A communication method for data transmission based on Remote Direct Memory Access (RDMA). This enables faster data transmission and improved communication efficiency and is suitable for applications that require large\-scale data transfer and high\-performance network communication.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Only instance types with vRDMA NICs can use the RDMA communication mode.</div><br><br><br>* <div data-tips="true" data-tips-type="default">After you update the network communication mode, the new configurations only take effect on newly added nodes.</div><br> |
   |ECS tags |VKE binds BytePlus platform labels to new ECS instances to facilitate searching and management.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The updated ECS labels only take effect on nodes that are subsequently added to the node pool. The ECS labels added to existing nodes are not affected.</div><br> |
   |**System configuration** ||
   |Operating system |Select an operating system image for nodes based on your business requirements. Valid values: Public images, Custom images, and Shared images.<br><br><br>* **Public images**: official, copyrighted images provided by BytePlus. These images combine basic OS with initialization components, delivering security, high availability, and open access for all users.<br><br>   For the public images supported by VKE and the associated specification families, see [Public images supported by VKE](https://docs.byteplus.com/en/docs/vke/Overview-of-operating-system-images).<br><br>* **Custom images**: Images created and uploaded by you. In addition to the operating system, the images also have public or private applications pre\-installed. These images are suitable for redeploying complex initialization systems or deploying multiple systems with the same configurations. Note that custom image support is in beta. To use custom images, apply for a trial first.<br><br>   VKE allows you to specify custom images as node operating systems. For more details, see [Overview of operating system images](https://docs.byteplus.com/en/docs/vke/Overview-of-operating-system-images).<br><br>* **Shared images**: images shared by other BytePlus users. You can use a shared image to quickly deploy a software environment the same as that created by other users. Conversely, you can share your custom image with other BytePlus users.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">You need to create custom images and shared images by using VKE base images. Check whether a GPU version is required based on your business requirements.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Custom images are available at the Project of the node pool level.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Changing the operating system only takes effect on newly added nodes, and does not affect existing nodes.</div><br> |
   |Security reinforcement |Update the status of Security reinforcement.<br><br><br>* **On** (default): The host\-based intrusion detection system (HIDS) provides free alerting capabilities targeting risks such as abnormal login attempts. While ensuring compatibility of the operating system image, it offers security hardening features for nodes (ECS instances). These features include real\-time monitoring, file monitoring, process monitoring, and dynamic system analysis.<br><br>* **Off**: The security hardening feature is not enabled.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Changing the status of Security reinforcement only takes effect on the nodes that are subsequently added to the node pool, and does not take effect on existing nodes.</div><br> |
   |Storage |Configure storage for the node pool. You need to configure the following parameters:<br><br><br>* **System volume**: Provides the storage space required for the operating system and log storage.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Available volume types may vary by region. For a list of volume types, see <a href="https://docs.byteplus.com/en/docs/ecs/Volume-specifications">Volume specifications</a>.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">ESSD offers multiple performance levels. Different ESSD performance levels provide varying specifications for metrics including maximum IOPS, maximum throughput, and latency.   </div><br>   <br><br>* **local disks**: [[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] Some instance specifications allow you to mount local disks. For instance specifications that support local disks, see [Instance specifications](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The data reliability of local disks depends on the reliability of the physical servers. Using local disks may introduce data loss risks. If the application layer does not include a data redundancy mechanism, we recommend using data volumes for business data storage.   </div><br>   <br><br>* **Data volume**: Provides additional storage space required for data storage in daily operations. A single node can have up to 15 data volumes.<br><br>   * Available volume types may vary by region. For a list of volume types, see [Volume specifications](https://docs.byteplus.com/en/docs/ecs/Volume-specifications).<br><br>      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">ESSD offers multiple performance levels. Different ESSD performance levels provide varying specifications for metrics including maximum IOPS, maximum throughput, and latency.      </div><br>      <br><br>   * **Format and mount the volume to /var/lib/containerd and /var/lib/kubelet**. By default, the first data volume supports formatting and mounting for use by the `/var/lib/containerd` and `/var/lib/kubelet` directories, which are related to containers, images, and the kubelet.<br><br>      If you do not select this option, the `/var/lib/containerd` and `/var/lib/kubelet` directories will be mounted to the partition in the system volume where the operating system is running. Monitor the remaining capacity in the system volume.<br><br>   * **Specify mount directory**. This option is not selected by default. To mount a data volume to a specific directory, select the check box and specify the directory.<br><br>      For example, if the mount directory is `/vke`, when the first volume is formatted and mounted to the `/var/lib/containerd` and `/var/lib/kubelet` directories, the two directories will be bind\-mounted to `/vke/var/lib/containerd` and `/vke/var/lib/kubelet`, respectively.<br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Description      </div><br>      <br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Changing the mount directory only takes effect on newly added nodes, and does not affect existing nodes.      </div><br>      <br><br>   * **File system**: [[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] Select a file system for the data volume. You can select **Ext4** or **Xfs**.<br><br>   * **Use snapshots to create EBS**: Use an existing snapshot to create a data volume. This option allows you to quickly copy the data from the snapshot to the new data volume. For more details, see [Creating snapshots](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot), [Creating volumes through snapshots](https://docs.byteplus.com/en/docs/ecs/Create-a-volume-through-snapshot), and [Accelerating node scale-out by using data volume snapshots](https://docs.byteplus.com/en/docs/vke/Accelerating_node_scale-out_by_using_data_volume_snapshots).<br><br>      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Only data volume snapshots in the Available state are supported.      </div><br>       |
   |**Security configuration** ||
   |Security group |The default security group of the cluster cannot be modified or deleted. The name of the security group is in the format of `<cluster ID>-common`. For more information on the default security group for clusters, see [Security group settings](https://docs.byteplus.com/en/docs/vke/Security-group-settings).<br><br>If you need to configure or modify custom security groups, make sure that they do not conflict with the default security group rules of the cluster. For recommended scopes and minimum scopes of custom access rules in security groups, see [Cluster access rules](https://docs.byteplus.com/en/docs/vke/Cluster-access-rules).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">A single node pool can be associated with up to four custom security groups.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When you configure custom security groups, you cannot select the managed security groups of VPCs. For more information about managed security groups, see <a href="https://docs.byteplus.com/en/docs/vpc/Security-group-overview">Security group overview</a>.</div><br> |
   |Node access configuration |Updating the login method for nodes that are subsequently added to the node pool does not affect existing nodes. If you select this option, it indicates that the login credentials and corresponding password or SSH key pair for subsequently added nodes will be modified.<br><br><br>* **Password**: You use a password to log in as a root user. If you select this option, set a root password and confirm it.<br><br>* **SSH key pair**: You use an SSH key pair (a public key and a private key) to log in to nodes. This login method is more secure and available only to Linux instances. If there are no SSH key pairs available, click **Create key pair** at the bottom of the Key pair dropdown menu to create one. For an introduction to key pairs, see [Key pairs](https://docs.byteplus.com/en/docs/ecs/Key-pair-overview). |
   |**Advanced settings** ||
   |Node labels |Add or remove node labels. Labels are used to define various attributes of nodes, facilitating batch filtering and other operations.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Custom node taints cannot conflict with system taints. For details of system labels, see <a href="https://docs.byteplus.com/en/docs/vke/System-labels-and-taints">System labels and taints</a>.</div><br> |
   |Node taints |Add or remove node taints. Taints allow nodes to repel specific pods and therefore prevent those pods from being scheduled to the nodes.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Custom node taints cannot conflict with system taints. For a list of system taints, see <a href="https://docs.byteplus.com/en/docs/vke/System-labels-and-taints">System labels and taints</a>.</div><br> |
   |Enable auto renew for node labels and taints |Configure automatic updating for node labels and taints.<br><br><br>* **Selected (default)** : enables automatic updating. The labels or taints added to or modified in a node pool will be automatically synchronized to both the existing and new nodes. In addition, if you modify the labels or taints for existing nodes, the configurations of the nodes will be overwritten by the configurations of the node pool.<br><br>* **Cleared**: does not enable automatic updating. The labels or taints added to or modified in a node pool will be synchronized only to the new nodes, but not the existing ones. In addition, if you modify the labels and taints for existing nodes, the modified configurations take effect and will not be overwritten by the configurations of the node pool.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Disabling automatic updating for node labels and taints may cause anomalies on features that use fixed node labels. You need to proceed with caution.</div><br> |
   |Kubelet configs |Specify custom kubelet parameters for nodes in the node pool to adjust node behavior. For details, see [Configuring ](https://docs.byteplus.com/en/docs/vke/Configuring-kubelet-parameters-for-a-NodePool)[kubelet parameters](https://docs.byteplus.com/en/docs/vke/Configuring-kubelet-parameters-for-a-NodePool)[ for a node pool](https://docs.byteplus.com/en/docs/vke/Configuring-kubelet-parameters-for-a-NodePool). |
   |Containerd configuration |Node pools support custom containerd configuration, which includes the Container Registry proxy address for container images and disabling self\-signed certificate verification. For detailed instructions, see [Specifying the containerd parameters of node pools](https://docs.byteplus.com/en/docs/vke/Configuring_containerd_for_node_pools). |
   |Spot instance compensation |This parameter is displayed after you select **Spot instance** for the **Billing method** parameter for the node pool. After the feature is enabled, new instances will be automatically created for replacement about 5 minutes before spot instance reclamation. For details, see [Node pools of spot instances](https://docs.byteplus.com/en/docs/vke/Preemptible_instance_node_pool). |
   |Supplement spot capacity by pay\-as\-you\-go instances |This parameter is displayed after you select **Spot instance** for the **Billing method** parameter for the node pool. After the feature is enabled, pay\-as\-you\-go instances will be used for supplementation when spot instances are insufficient due to reasons such as inventory or pricing. When pay\-as\-you\-go instances are running, even if spot instances meet the conditions, rebalancing will not be performed. Only when the node pool is being scaled in, pay\-as\-you\-go instances are preferentially released. For details, see [Node pools of spot​ instances](https://docs.byteplus.com/en/docs/vke/Preemptible_instance_node_pool). |
   |Node distribution ratio policy |This parameter is displayed after you select **Spot instance** for the **Billing method** parameter for the node pool. After you enable the feature, set the proportion of pay\-as\-you\-go instances to spot instances in the node pool. For details, see [Node pools of spot​ instances](https://docs.byteplus.com/en/docs/vke/Preemptible_instance_node_pool). |
   |Custom name |Select and configure the custom name types for nodes in the node pool as needed. You can configure multiple custom name types at the same time.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">VKE provides a tool for automatically specifying custom names for all nodes in a node pool. To use the tool, click <strong>Auto generation</strong>. After custom names are automatically configured, we recommend that you click <strong>Generate random names</strong> to add random suffixes. This prevents the names of the newly scaled\-out nodes from conflicting with each other and ensures smooth node scale\-out.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Nodes added during subsequent scale\-out operations in the node pool will use the custom name set here or be named according to the custom naming rule set here.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The names of existing nodes in the node pool are not affected.</div><br><br><br>* **Node name**: used to quickly identify nodes in VKE or ECS. You can use one of the following two methods to specify node names:<br><br>   * **Node name**: Specify the node name based on the displayed naming rules. Two naming patterns are available: fixed\-range incrementing and dynamically extended incrementing. For detailed naming formats, see [Naming formats](https://docs.byteplus.com/en/docs/as/Setting-sequential-and-unique-names-or-hostnames-for-instances?lang=en#.5ZG95ZCN5qC85byP).<br><br>   * **Node name prefix**: Specify the node name prefix based on the displayed naming rules.<br><br>* **Node host name**: Set the host name corresponding to the node. Two naming patterns are available: fixed\-range incrementing and dynamically extended incrementing. For detailed naming formats, see [Naming formats](https://docs.byteplus.com/en/docs/as/Setting-sequential-and-unique-names-or-hostnames-for-instances?lang=en#.5ZG95ZCN5qC85byP).<br><br>* **Node metadata name**: Specify the metadata name (metadata.name) of a node object in Kubernetes. The metadata name is used to identify resources in external systems such as monitoring and alerting systems. You can use one of the following two methods to specify metadata names:<br><br>   * **Use node hostname**: Use the hostname of the node as the node metadata name.<br><br>   * **Set prefix and suffix for node metadata name**: Specify the prefix or suffix of the node metadata name. The system generates the complete node metadata name in the `prefix-nodeIP-suffix` format. |
   |Image lazy loading |[Public beta] This feature is not enabled by default. After you enable the feature, nodes in the node pool can use the container image acceleration feature on demand. For more information, see [Container image lazy loading solutions](https://docs.byteplus.com/en/docs/vke/Container-image-lazy-loading-solution).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Updating the image lazy loading feature of the node pool only takes effect on subsequently added nodes. Existing nodes are not affected.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Only the nodes with a containerd version 1.4.13\-vke.3 or later can use this feature. To view containerd versions, see <a href="https://docs.byteplus.com/en/docs/vke/What-container-runtimes-does-VKE-currently-support">FAQ</a>.</div><br> |
   |The script executed before node deployment |Enter a shell script. The script will automatically be executed before Kubernetes components are deployed on nodes. You need to implement the script commands yourself and ensure that the script supports reentrancy and retry logic.<br><br>The script and the related logs can be found in the `/usr/local/vke/userscripts` directory on the node. This feature is typically used for preprocessing operations, such as setting environment variables and creating temporary directories.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The updated script takes effect only for new nodes provisioned from scale\-out behavior.</div><br> |
   |InitializeScript |Enter a shell script. After the node deploys the Kubernetes add\-on, the script will be automatically executed. You need to implement the script commands yourself and ensure that the script supports reentrancy and retry logic. The script and the related logs can be found in the `/usr/local/vke/userscripts` directory on the node. This feature is commonly used in scenarios such as modifying kubelet configurations.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The updated deployment execution script only takes effect on newly added nodes instead of existing nodes.</div><br> |
   |Bind EIP to node |Specify whether to automatically bind EIPs to nodes in the cluster.<br><br><br>* Disable: By default, the system does not automatically bind EIPs to nodes. If you need to access nodes over the public network later, see [Applying for an EIP and associating it with an ECS instance](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP-and-associating-an-ECS-instance).<br><br>* Enable: The system automatically binds EIPs to nodes in the cluster. In this case, you need to specify custom EIPs.<br><br>   * **Billing type**: EIPs support **Pay\-as\-you\-go \- by bandwidth limit** and **Pay\-as\-you\-go \- by actual traffic**.<br><br>   * **Line type**: Only **BGP (multi\-line)**  is supported.<br><br>   * **Shared bandwidth packet**: After you select this option, select the target items and shared bandwidth package to add the public IP addresses to the package. If no shared bandwidth package is available, refer to [Creating shared bandwidth packages](https://docs.byteplus.com/en/docs/bandwidthpackage/Creating-a-Bandwidth-Package) to create one.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">An EIP address can be added to a shared bandwidth package only when ‌all of the following conditions are met:      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The <strong>line type</strong> of both is identical.      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The shared bandwidth package is of type IPv4.      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">No security protection is configured for the shared bandwidth package.      </div><br>      <br><br>   * **Bandwidth limit**: Specify an upper bandwidth limit.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You will be charged for using EIP. For details, see <a href="https://docs.byteplus.com/en/docs/eip/Billing-overview">EIP billing overview</a>. If the EIP quota is insufficient, submit an application in the EIP console. For more information, see <a href="https://docs.byteplus.com/en/docs/eip/Limits">EIP limits</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When a node is deleted or removed, the associated EIP will be simultaneously released.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Automatic EIP binding is supported only for new nodes added to the node pool and does not apply to existing nodes.</div><br> |
   |Cordon node |After you enable the cordon node feature, the nodes in the node pool are set to the cordoned and unschedulable status. Newly created pods cannot be scheduled to nodes in the node pool, but pods already running on the nodes are not affected. You can execute the `kubectl uncordon` command to disable it manually.<br><br>Cordoning a node will reduce the remaining resource quota of the cluster to which the node belongs. If the cluster does not reserve sufficient available resources, node cordoning will affect the scheduling of new applications and the running of existing applications. |
   


<span id=".5re75Yqg5bey5pyJ6IqC54K5"></span>
## Existing node adding

In addition to the default node pool, some qualified custom node pools support adding existing ECS instances as nodes to meet business requirements such as resource reuse and node warm\-up.

For operations related to adding existing nodes to the default node pool, see [Adding existing nodes](https://docs.byteplus.com/en/docs/vke/Adding-existing-nodes).

<span id=".5L2_55So6ZmQ5Yi2"></span>
### Usage limits

Only custom node pools and Elastic Compute Service (ECS) instances that meet the following conditions support this feature:


* For custom node pools, the following conditions need to be met:

   * **Autoscaling** is not enabled for the node pool.

   * The current node pool status is **running**.

   * The current node pool billing mode is **Pay\-as\-you\-go** or **Subscription**.

* For ECS instances, the following conditions need to be met:

   * Running in the same VPC as the current cluster.

   * Be under the same project as the target node pool.

   * The instance has not been added to any cluster or scaling group of the Auto Scaling service.

   * The instance only has one network interface card.

   * The system volume of the instance has a `capacity` ≥ (`image size configured for the target node pool` + `10 GiB`).

   * If you do not specify the data volumes to be mounted on the node (i.e., the option **Disk mount** is not selected), the instance has to include the data volume with both type and size the same as required by the target node pool. For example, if the target node pool is configured with five data volumes (including local disks), and the first data volume has "**Format and mount to the container and image storage directory**" enabled, while the third data volume has "**Specify mount directory**" enabled, then the ECS instance needs to have two data volumes (including local disks) that are the same as the first and the third ones of the target node pool in terms of type and size.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke).In the left navigation bar, click **Cluster**.

2. Click the target cluster name. In the left navigation bar of the cluster management page, click **Nodes** \> **Node pool**.

3. Find the target node pool and in the Actions column, click `...` \> **Add existing node**.

4. In the **All Servers** list, select the nodes that need to be added to the node pool, and add them to the **Selected servers** list.

   
   |**Parameter** |**Description** |
   |---|---|
   |All servers |The list displays all ECS instances within the same VPC as the cluster and in the same project as the current node pool. Select the ECS instances as needed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If <strong>Buy affinity group</strong> (beta) is enabled for the current node pool, the selected ECS instances must meet the following conditions at the same time:</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">Consistent size: The affinity group sizes of the selected ECS instances and the node pool must be consistent.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">Add the entire group: You must select all ECS instances in the affinity group.</div><br><br><br>   <div data-tips="true" data-tips-type="warning">For example, if the affinity group size of the node pool is 4, you need to select one or more affinity groups with the same size of 4 and select all ECS instances in the groups. To change the affinity group size of the node pool, see <a href="https://docs.byteplus.com/en/docs/vke/Managing-NodePools">Managing node pools</a>.   </div><br>   <br><br>* <div data-tips="true" data-tips-type="warning">If <strong>Buy affinity group</strong> (beta) is not enabled for the current node pool, but you select ECS instances added to affinity groups, unexpected behavior may occur. We recommend not selecting ECS instances added to affinity groups for node pools for which Buy affinity group is not enabled.</div><br> |
   |Selected servers |This list displays the ECS instances that you have selected. |
   |Keep ECS instance name |Keep ECS instance name<br><br><br>* Enable: will keep the original ECS instance name.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the names retained contain any Chinese characters, the system label <code>cluster.vke.volcengine.com/node-name</code> for that node will become invalid. Therefore, you need to avoid using the <code>cluster.vke.volcengine.com/node-name</code> label in scenarios such as affinity\-based scheduling.   </div><br>   <br><br>* Disable: will not keep the original ECS instance name. VKE will rename the node based on the current node pool configuration. |
   |Disk mount |If enabled, you need to specify the mount directory so that the data volume of the node can be mounted to this directory.<br><br>Before specifying the mount directory, carefully read the prompts displayed on the page. |
   |Reinstall OS |* If you **select** this option, the operating system (OS) of the ECS instance will be reinstalled using the OS configuration of the current node pool. The existing data on the system volume of the instance will be cleared and cannot be restored.<br><br>* If you **do not select** this option, the ECS instance will retain its existing operating system and system volume data.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you continue to use the existing operating system and system volume data of the ECS instance, make sure that the ECS instance meets the following requirements. Otherwise, the node will fail to be added.   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The ECS instance must be in the <strong>RUNNING</strong>  state.   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The ECS instance must have the Cloud Assistant Agent installed, and the Cloud Assistant Agent must be in the <strong>Running</strong> state.   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Go to the <a href="https://console.byteplus.com/ecs">ECS console</a> to view the status of the ECS instance and its related resources.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you do not reinstall the operating system for an ECS instance, existing data on the ECS instance may result in node adding failures or other unknown issues. We strongly recommend that you reinstall the operating system.   </div><br>    |
   |Restart now to install cloud assistant Agent |The Agent is installed by default and cannot be modified. Using Agent to manage nodes can facilitate fault monitoring and self\-healing. |
   

5. Click **Confirm**.


<span id=".5YWL6ZqG6IqC54K55rGg"></span>
## Cloning node pools

VKE supports cloning node pools. You can create different node pools with similar configurations to serve multiple upper\-layer services.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The default node pool does not support cloning.</div>



1. Log in to the [VKE console](https://console.byteplus.com/vke).In the left navigation bar, click **Cluster**.

2. Click the target cluster name. In the left navigation bar of the cluster management page, click **Nodes** \> **Node pool**.

3. Find the target node pool and click `...` \>  **Clone**.

4. On the **Clone node pool** page, set the node pool name and node login password/SSH key pair. The rest of the parameters can be configured as needed. For parameter descriptions, see [Editing node pools](https://docs.byteplus.com/en/docs/vke/Managing-NodePools#.57yW6L6R6IqC54K55rGg) described at the beginning of this topic.

5. Click **Next: Confirm configuration**. And then click **Confirm** if you checked the configurations on the page and ticked the checkbox for **I have read and agree** at the bottom.


<span id=".56e76Zmk6IqC54K55rGg"></span>
## Removing node pools

You can remove the node pools no longer needed, as well as the associated nodes, provided that normal business operations are not affected.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">When you remove a node pool, all nodes within it will be removed from the current container cluster and cannot be restored. Proceed with caution.</div>


* <div data-tips="true" data-tips-type="warning">The pods on all nodes in the node pool will be deleted, which may trigger rescheduling. If rescheduling fails, your business may be affected. Make sure that the cluster has sufficient resources for rescheduling.</div>


* <div data-tips="true" data-tips-type="warning">After you remove the node pool and synchronously destroy ECS instances, the data on ECS system volumes and data volumes will be deleted and cannot be restored. Proceed with caution.</div>


* <div data-tips="true" data-tips-type="warning">You can destroy only pay\-as\-you\-go and spot ECS instances instead of subscription ECS instances. To destroy subscription ECS instances, go to the <a href="https://console.byteplus.com/ecs">ECS console</a> to cancel the subscription.</div>


1. Log in to the [VKE console](https://console.byteplus.com/vke).In the left navigation bar, click **Cluster**.

2. Click the target cluster name. In the left navigation bar of the cluster management page, click **Nodes** \> **Node pool**.

3. Find the target node pool and click `...` \>  **Remove** in the Actions column.

4. In the pop\-up window, select **Simultaneously destroy ECS instances** as needed, then click **Remove** to start.


<span id=".5pWF6Zqc6K-K5pat"></span>
## Diagnosis

Node pool troubleshooting helps users identify potential risks in node pools within a VKE cluster based on different information, including abnormal node pool status, CA add\-on status, node quota status, and ECS inventory.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The default node pool does not support diagnosis.</div>



1. Log in to the [VKE console](https://console.byteplus.com/vke). In the left navigation bar, click **Cluster**.

2. Click the target cluster name. In the left navigation bar of the cluster management page, click **Nodes** \> **Node pool**.

   You have two options for initiating a diagnosis on a node pool and nodes within the node pool.

   
   <Tabs>
   <Tab zoneid="W3mchboj2j" title="Node pool details page">
   <TabTitle>Node pool details page</TabTitle>
   
   1. On the **Node pool** page, click the name of the target node pool to go to the **node pool details page**.
   
   2. On the **Diagnosis** tab, click the corresponding button to initiate a diagnosis on the current node pool and its nodes.
   
      * **Node pool diagnosis**: Initiate a diagnosis on the current node pool. When the diagnosis is complete, you can view the result. For details, see [Node pool diagnosis](https://docs.byteplus.com/en/docs/vke/NodePool-diagnosis).
   
      * **Node diagnosis**: Select a node within the node pool to initiate a diagnosis on that node. For details, see [Node diagnosis](https://docs.byteplus.com/en/docs/vke/Node-diagnosis).
   
   
   </Tab>
   <Tab zoneid="MCVRIsiyQA" title="Diagnosis page">
   <TabTitle>Diagnosis page</TabTitle>
   
   1. On the **Node pool** page, find the target node pool, and in the **Actions** column, click `...` \> **Diagnosis**.
   
   2. On the **Create diagnosis job** page, configure a diagnosis task for the node pool. For details, see [Node pool diagnosis](https://docs.byteplus.com/en/docs/vke/NodePool-diagnosis) and [Node diagnosis](https://docs.byteplus.com/en/docs/vke/Node-diagnosis).
   
   
   </Tab>
   </Tabs>
   


<span id="AgLqzJk7"></span>
## Runtime upgrade

VKE has supported containerd 2.1.x since Kubernetes v1.34 and will no longer support nodes or node configurations using containerd 1.x after Kubernetes v1.36. You can use the **Runtime upgrade** feature to upgrade the containerd version on the nodes.


1. Log in to the [VKE console](https://console.byteplus.com/vke). In the left navigation bar, click **Cluster**.

2. Click the target cluster name. In the left navigation bar of the cluster management page, click **Nodes** \> **Node pool**.

3. Find the target node pool and click `...` \>  **Runtime upgrade**.

4. On the **Node Kubernetes upgrade** page, upgrade the containerd version on the nodes. For detailed parameter configurations and upgrade considerations, see [Upgrading nodes](https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster?lang=en#.6IqC54K55Y2H57qn).


<span id="ntb1IVdu"></span>
## Edit runtime

VKE supports updating the containerd configuration of nodes in a node pool.


1. Log in to the [VKE console](https://console.byteplus.com/vke). In the left navigation bar, click **Cluster**.

2. Click the target cluster name. In the left navigation bar of the cluster management page, click **Nodes** \> **Node pool**.

3. Find the target node pool and click `...` \>  **Edit runtime**.

4. In the **Edit container runtime** dialog box, select the target runtime version and click **Confirm**. For runtime version details, see [Runtime release notes](https://docs.byteplus.com/en/docs/vke/Containerd_Runtime_release_notes).


<span id="SIfDvCnq"></span>
## Enable or disable managing

You can convert a normal node pool to a managed node pool. You can also convert a managed node pool to a normal node pool by disabling management mode.


1. Log in to the [VKE console](https://console.byteplus.com/vke). In the left navigation bar, click **Cluster**.

2. Click the target cluster name. In the left navigation bar of the cluster management page, click **Nodes** \> **Node pool**.

3. Find the target node pool and click `...` \> **Disable managing** or **Enable managing**.

   
   <Tabs>
   <Tab zoneid="d82yuIxDvQ" title="Enable management">
   <TabTitle>Enable management</TabTitle>
   
   In the **Check and self\-healing settings** dialog box, specify parameters based on the on\-screen prompt and then click **Confirm**. For more information about managed node pools, see [Creating managed node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-managed-NodePool).
   
   
   |Parameter |Description |
   |---|---|
   |Check and self\-healing |Specify whether to enable the node check and self\-healing feature.<br><br><br>* **On**: Enables the feature. The system automatically checks node health. It cordons a node or restarts node components in case of a node failure based on the configured check and self\-healing rules.<br><br>* **Off**: Does not enable this feature. This is the default setting. |
   |Check and self\-healing rules |Configure check and self\-healing rules for the node pool. This feature is in the beta stage. The rules fall within two categories:<br><br><br>* **Recommended rule** \- Enables the recommended check and self\-healing rule for the node pool. For details, see [Recommended rules](https://docs.byteplus.com/en/docs/vke/Creating-a-managed-NodePool#.5o6o6I2Q6KeE5YiZ).<br><br>* **Custom rule** \- a custom check and self\-healing rule. If no custom rules have been configured, you can click **Create check and self\-healing rules** to create one. For details, see [Node checking and self-healing](https://docs.byteplus.com/en/docs/vke/NodePool-health-check-and-auto-repair).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you select <strong>Recommendation rule</strong>, the system automatically generates a check and self\-healing rule in one of the following formats:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>GPU node pool self-healing rule-{node pool name}-{random number}</code> for a GPU node pool.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>node pool self-healing rule-{node pool name}-{random number}</code> for a non\-GPU node pool.</div><br> |
   
   
   
   
   
   </Tab>
   <Tab zoneid="ZjINq5bciX" title="Disable management">
   <TabTitle>Disable management</TabTitle>
   
   In the message that appears, confirm the information and click **Confirm**.
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default">Managed node pools provide a simple and efficient way to improve fault management for GPU computing resources and increase node pool resource utilization. After you disable managed mode, the preceding capabilities are no longer available, and the check and self\-healing rules will be unbound. We strongly recommend that you enable managed mode for node pools.</div>
   
   
   
   </Tab>
   </Tabs>
