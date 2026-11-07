---
title: "Create virtual clusters"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Create_virtual_clusters"
---

This article provides a detailed guide to creating a cluster based on Kubernetes in the BytePlus E\-MapReduce (EMR) console.

<span id="_1-前提条件"></span>
# **Prerequisites**


1. After completing the relevant [Preparation](https://docs.byteplus.com/docs/undefined/6a192e643156df055be4a065), you must complete to create a cluster.

2. Before purchasing and creating a cluster, ensure that your account balance (that is, cash balance) is greater than or equal to 0.


<span id="_2-操作步骤"></span>
# Create a virtual cluster

<span id="_2-1-创建虚拟集群入口"></span>
## **Virtual cluster entry point**


1. Log in to the [EMR console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home).

2. In the top menu bar, select the region and project space from the dropdown menu according to your actual scenario:

   1. Region: The created cluster and corresponding resources will be deployed in the selected region. Once created, the region cannot be changed.

   2. Project: The default project is displayed. For details, see [Project configuration](https://docs.byteplus.com/docs/E-MapReduce/105422).

3. On the **on VKE** cluster list page, click the Create virtual clusterentry point to start creating a virtual cluster.


<span id="_2-2-创建虚拟集群配置"></span>
## **Virtual cluster configuration**

<span id="996a327c"></span>
### Cluster configuration


|Configuration items |Configuration note |
|---|---|
|Product version |The latest software version is used by default. |
|Resource type |Select Create VKE resource, or VKE resources available (supported only for allowlist users).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">It is recommended to install the ingress component in existing VKE clusters; otherwise, the EMR on VKE cluster <strong>access link</strong> functionality will be affected.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Create VKE resourceCurrently, ZooKeeper and Kyuubi services are not supported.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Create VKE resourceFor parameter configuration, refer to: <a href="https://docs.byteplus.com/en/docs/vke/Creating-a-cluster">Creating managed clusters</a>.</div><br><br><br>* Select VKE resources available: You need to select an existing VKE cluster. After selecting the service, set the Namespace parameter. See the parameter details below for more information.<br><br>* Select: Create VKE resource: After selecting the service and payment parameters, you also need to configure network\-related parameters. See the parameter details below for more information. |
|Services |* Currently, Spark, Celeborn, Hive MetaStore, Ray, Volcano, ZooKeeper, Kyuubi, and Proton services are supported. You can select one or more services.<br><br>* Celeborn provides Remote Shuffle service, addressing the dependency on local disks in Kubernetes scenarios.<br><br>* Ray provides a distributed computing framework, covering scenarios such as machine learning and model training.<br><br>* Proton is a data lake acceleration engine launched by the Volcano Engine E\-MapReduce (EMR) team. Its deeply optimized TOS access and caching capabilities can significantly improve the efficiency of computing task execution.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">To request access, please contact Volcano Engine technical support by <a href="https://console.byteplus.com/workorder/create?ref=L2xhcy9yZWdpb246bGFzK2FwLXNvdXRoZWFzdC0xL25leHQvaG9tZQ%3D%3D">submitting a ticket</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If subsequent deployment of Celeborn or Proton services is required, the VKE cluster node pool on which the deployment depends must have the <code>emr-local-disk=true</code> tag. If this tag is not present, the deployment of Celeborn or Proton services will remain in Pending status and cannot be completed successfully.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Any VKE node pool newly created from the EMR on VKE side will automatically add the <code>emr-local-disk=true</code> tag, whereas node pools created directly from the VKE side require manual addition of the corresponding tag.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">For example, when creating an EMR on VKE cluster, if an existing VKE cluster is used instead of creating a new one, no new node pool will be created during cluster creation. In this scenario, to deploy Celeborn or Proton services, you must manually add the corresponding node pool tag in the VKE console to prevent subsequent deployment failures of Celeborn or Proton services.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">For instructions on manually adding tags in the VKE console, see: Apply the EMR tag to the selected nodes. The configured nodes are allowed to run EMR services.</div><br> |
|Namespace<br><br>(VKE resources available required configuration) |Configure the VKE namespace for service deployment. It is randomly generated by default, or can be customized.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the installed service depends on an external RDS, to avoid network access issues, only data connection instances in the same VPC as existing VKE resources are supported.</div><br> |
|Cluster name |The cluster name must be between 1 and 64 characters in length and can only contain Chinese characters, letters, numbers, hyphens (\-), and underscores (_). |
|Payment type |Currently, only Pay\-as\-you\-go is supported. |
|Network configuration<br><br>(Create VKE resource required configuration) |* If you do not have an available network, select Create new: the system will automatically create a VPC, subnet, and security group for you.<br><br>* If you have an available network, select Use existing:<br><br>   * Select the required VPC, subnet, and security group.<br><br>      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If the installed service depends on an external RDS, to avoid network access issues, the cluster VPC must be the same as the VPC where the RDS is located.      </div><br>      <br><br>   * You also need to configure the Open API Server Public Network switch: after enabling, the VKE cluster will allow public access, create a NAT gateway, and incur service and traffic charges. |
|Availability zone<br><br>(Create VKE resource required configuration) |Select the availability zone for the cluster. |


<span id="cde72ac7"></span>
### Resource configuration: Create VKE resource


|Configuration items |Configuration note |
|---|---|
|Node pool name |Customize the name of the node pool for the current cluster. |
|Node pool specification、Operating System、System disk、Data disk、Number of nodes |Select the instance type and other parameters for the node pool of the current cluster. For parameter configuration, refer to: [Creating managed clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster). |
|Pod specification |Set the Pod specifications for the current cluster. Supports selecting Default specification or Custom specifications.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A pod is the smallest unit created or deployed by Kubernetes. A pod encapsulates one or more containers and storage resources (volumes), includes a unique network IP, and provides policy options for managing and controlling how containers run.</div><br><br><br><br>* Default specification: The system sets the Pod specifications for you. Hover your mouse over the Default specification option to view the detailed specifications of the current default rule.<br><br>* Custom specifications: You can also adjust container group parameters as needed and configure Configure Pod deployment related parameters yourself, allocating CPU, memory, and Pod count for each service's Pod. |
|Enable elastic container (VCI) to run jobs |Set whether to enable the elastic container job switch. After enabling, resources can be automatically, flexibly, and efficiently scaled based on business load, reducing costs and ensuring service performance. For details, see: [VIC Product advantages](https://docs.byteplus.com/en/docs/vke/VCI-benefits). |


<span id="1e7d43ab"></span>
### Resource configuration: VKE resources available


|Configuration items |Configuration note |
|---|---|
|Dedicated node |Click **Configure dedicated node** to configure an EMR dedicated node pool or configure a dedicated node. After selecting a node pool or node:<br><br><br>* If you need to deploy Celeborn or Proton services later, go to the VKE console and manually add the `emr-local-disk=true` tag to the corresponding node pool. Only nodes with this tag are allowed to run EMR services. Without this tag, Celeborn and Proton services cannot be deployed properly. For instructions on manually adding tags in the VKE console, see: [VKE node pool management - Edit node pool documentation](https://docs.byteplus.com/en/docs/vke/Managing-NodePools).<br><br>* When configuring a dedicated node pool, expansion nodes based on this node pool will also be automatically configured as EMR dedicated nodes.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can go to the Container Service console to add nodes or change node configurations.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A dedicated ShuffleService cluster requires at least three dedicated nodes, which must be <strong>local disk models</strong>, such as i2g, i3s, and more.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Deploying CelebornWorker requires configuring at least three dedicated nodes of <strong>local disk models</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Deploying Proton requires configuring at least two dedicated nodes of <strong>local SSD models</strong>. It is recommended to deploy Proton separately from CelebornWorker. You can set the node scheduling policy in the pod deployment configuration.</div><br> |
|Pod specification |Configure Configure Pod deployment related parameters yourself to allocate CPU, memory, and the number of Pods for the Pods of each service. |
|Taint tolerance |To set taints and tolerations for component containers, you can configure tolerations. Currently, taint toleration supports selection based on "**effect**". |
|Enable elastic container (VCI) to run jobs |Set whether to enable the elastic container job switch. Once enabled, resources can be automatically, flexibly, and efficiently scaled based on business workloads, reducing costs and ensuring service performance. For details, see: [VIC Product advantages](https://docs.byteplus.com/en/docs/vke/VCI-benefits). |


<span id="e80eada0"></span>
### Other configuration


|Configuration items |Configuration note |
|---|---|
|Access credentials<br><br>(Create VKE resource required configuration) |Set the access credentials for the current cluster. You can set them as Key pair or password, and select the corresponding key pair or set a password based on the chosen credential type. |
|TOS bucket |Select an existing Bucket, or create a new Bucket in the TOS object storage console. |
|AccessKey |AK/SK is used to read and write TOS data. It is recommended to use a separate IAM account to create a dedicated AK/SK for TOS. |
|SecretKey |AK/SK is used to read and write TOS data. It is recommended to use a separate IAM account to create a dedicated AK/SK for TOS. |
|Project the virtual cluster belongs to |Volcano Engine provides you with a set of cloud resource management methods for centralized orchestration and management of cloud resources. |
|Label |You can tag the cluster and its corresponding VKE cluster |
|Service binding |* Associate with Shuffle Service cluster: Supports associating ShuffleService clusters during and after Spark creation. After associating a ShuffleService cluster, the Spark Shuffle part will run on the associated ShuffleService cluster. |


<span id="4d35c40d"></span>
## Preview, confirm, and place the order

After completing the above configurations, you can review the results of the cluster creation parameter configuration on the preview page. If everything is correct, follow the interface prompts to complete the order and payment to finish the cluster creation process.
