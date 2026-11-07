---
title: "Creating a managed heterogeneous computing cluster"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating_a_managed_heterogeneous_computing_cluster"
---

VKE supports quick creation of managed clusters for heterogeneous computing in AI inference scenarios. This topic describes the procedure for creating a managed cluster for heterogeneous computing.

<span id="lf9PAugw"></span>
## Cluster description

A managed cluster for heterogeneous computing involves simplified cluster parameter configuration, which enables quick cluster creation for heterogeneous computing scenarios. A managed cluster for heterogeneous computing offers the same capabilities as a standard managed cluster.

<span id="Aot4jPTk"></span>
## Prerequisites


* You have already registered an account on the BytePlus platform and completed necessary preparations such as identity verification, account recharge, and authorization. For details, see [Preparations](https://docs.byteplus.com/en/docs/vke/Preparations).

* Your BytePlus account balance, excluding vouchers, is not zero. For details, see [Billing overview](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-2).

* Permissions to use Vital Kubernetes Engine (VKE) and for VKE to access cloud resources have been granted. For details, see [Cloud service dependencies](https://docs.byteplus.com/en/docs/vke/Dependencies-between-VKE-and-other-cloud-services).

* ‌Check the quota limits for the VKE cluster and the dependent cloud services. For details, see [Limits](https://docs.byteplus.com/en/docs/vke/Limits).

* Currently, some GPU Accelerated and High Performance Computing Optimized instance specifications, for example, `ecs.hpcpni3ln` required for deploying DeepSeek\-R1, are in the **beta** stage. If you want to use a GPU Accelerated or High Performance Computing Optimized instance specification in the beta stage, ensure that you have requested it and understood the regions, availability zones, and billing methods of the instance specification.

* To use the **High Performance Computing Optimized** instance specification to create a managed heterogeneous computing cluster, you can create an HPC cluster for nodes in advance. For details, see [Creating HPC clusters](https://docs.byteplus.com/en/docs/gpu/Creating-HPC-clusters).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The HPC cluster must be deployed in the same <strong>availability zone</strong> as the VKE node.   </div>
   

* A VMP workspace has been created. For details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).


<span id="Ecbnt18Q"></span>
## Cost information

Creating a heterogeneous computing cluster may incur costs for cloud infrastructure resources such as load balancers, NAT Gateway instances, and Elastic IP addresses. You can see actual billing information by checking the **Configuration fee** field in the right side of the Create cluster page. For billing details, see [Product billing](https://docs.byteplus.com/en/docs/vke/Billing).

<span id="G6yXBS4F"></span>
## Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. Select the target region in the top navigation bar.

3. In the left navigation bar, click **Cluster**. On the page that appears, click **Create cluster**. 

4. In the **Create cluster** dialog box, go to the **Managed clusters for heterogeneous computing** section and click **Create now**. 

5. Configure cluster parameters described in the following table. For parameter details, see [Creating managed clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster). 

   
   |Parameter |Description |
   |---|---|
   |**Cluster and node pool configuration** ||
   |Availability zone |Select the availability zone to which the node pools in the managed heterogeneous computing cluster belong.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">To use the <strong>High Performance Computing Optimized</strong> specification, the availability zone that you select needs to include the availability zone where the HPC cluster resides.</div><br> |
   |Node\-based billing model |The billing method for the ECS resources within the node pool. You can select one of the following options:<br><br><br>* **Pay\-as\-you\-go**: a postpaid mode in which you use first and pay later<br><br>* **Subscription**: a prepaid model in which payment is made in advance before use.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For ECS billing details, see <a href="https://docs.byteplus.com/en/docs/ecs/Billing-methods">Product billing</a>.</div><br> |
   |Instance type |Managed heterogeneous clusters support **High Performance Computing Optimized** and **GPU Accelerated** instance types.<br><br>Select an instance type and specification that best suits your business scenario. For a detailed description of the specifications, see [Instance types and specifications](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types). |
   |High\-performance computing cluster |This parameter is available if you select **High Performance Computing Optimized** for **Instance type**.<br><br>Select the HPC cluster to which the HPC optimized nodes belong and its project. If no high\-performance compute cluster is available, click **Create high\-performance computing cluster** to create one. For details, see [Creating HPC clusters](https://docs.byteplus.com/en/docs/gpu/Creating-HPC-clusters).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The availability zone for the HPC cluster must be the same as the availability zone selected for the VKE cluster.</div><br> |
   |Number of nodes |Enter the number of nodes to create. The total number of nodes, including new and existing ones, cannot exceed the cluster's node quota. For quota details, see [Limits](https://docs.byteplus.com/en/docs/vke/Limits).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The expected number of nodes on the VKE side and the ECS side varies. For details, see <a href="https://docs.byteplus.com/en/docs/vke/How_does_the_expected_number_of_nodes_change">FAQ</a>.</div><br> |
   |Login credentials |Select a node login method.<br><br><br>* **Password**: Enter the root password twice to confirm.<br><br>* **SSH key pair**: You use an SSH key pair (a public key and a private key) to log in to the node. This login method is more secure and available to Linux instances.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You must configure a node login method, regardless of whether the node is a newly created or existing one. This is because each node in the created cluster will have a new operating system. The login method specified here will also apply to other nodes in the node pool where this node resides.</div><br> |
   |**Networking** ||
   |VPC |Select the VPC to which the managed heterogeneous computing cluster belongs. A VPC provides an isolated, self\-configurable, and self\-managed virtual network environment for the cluster.<br><br>If no VPC is available, follow the steps described in [Creating VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) to create one. |
   |Pods and Node Subnets |Select the subnet to which the pods and nodes of the managed cluster for heterogeneous computing belong.<br><br>If no subnet is available, click **Create subnet** to create one. For detailed steps, see [Creating subnets](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet). |
   |**Observability configuration** ||
   |Container observability |Configure basic container monitoring and control\-plane service monitoring to monitor metrics of fundamental resources (nodes, kubelet, kube\-state\-metrics, and more) and control\-plane services (kube\-apiserver, kube\-scheduler, etcd, and more).<br><br><br>* Configure the observability metric scope. Available options include:<br><br>   * **Basic**: (Default) Basic metrics for the monitored object. They provide insights into the basic status of the object and resource usage.<br><br>   * **Standard**: (Recommended) Basic metrics plus important metrics of the monitored object. The combination of basic and important metrics provides a more comprehensive view of the object status.<br><br>   * **Full set of metrics**: Basic, important, and advanced metrics of the monitored object. This tier includes all metrics of the monitored object.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The billing method and cost vary based on the observability metric scope and the VMP workspace's storage duration. For details, see <a href="https://docs.byteplus.com/en/docs/vmp/pay-as-you-go">Pay\-as\-you\-go</a>.   </div><br>   <br><br>* **Prometheus workspace**: Select a VMP Prometheus workspace where VKE observability metrics are stored.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">This configuration is only used to bind the workspace to the cluster. It will not collect metric data. To collect data, install the prometheus\-agent add\-on in the cluster. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Creating-a-cluster#.57uE5Lu26YWN572u">Configuring the add\-on</a> or <a href="https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.cHJvbWV0aGV1cy1hZ2VudC3nu4Tku7Y=">Installing the add\-on</a>.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If no VMP workspace is available, create one first. For details, see <a href="https://docs.byteplus.com/en/docs/vmp/Creating-workspaces">Creating workspaces</a>.   </div><br>   <br><br>* **Observational enhancement**: If you enable this feature, when any of the core add\-ons (core\-dns, vpc\-cni, and csi\-ebs) are installed in the cluster, the system will automatically enable observability for these add\-ons and provide dashboards and alerting capabilities. For details, see [DNS service observability](https://docs.byteplus.com/en/docs/vke/DNS-service-observability), [CNI network observability](https://docs.byteplus.com/en/docs/vke/CNI-network-observability), and [CSI storage observability](https://docs.byteplus.com/en/docs/vke/CSI-storage-observability). |
   |**Advanced settings** ||
   |Control plane subnets |Select a subnet that is used for the Kubernetes API server to create a load balancer. If you do not specify a subnet, the system will randomly select one.<br><br>If no subnet is available, click **Create subnet** to create one. For detailed steps, see [Creating subnets](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet). |
   |Data volume |Additional storage space for daily operational data. A single node can have up to 15 data volumes.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">It is recommended to keep the system default data volumes in a managed cluster for heterogeneous computing.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The <code>date01</code> directory will be used as a dependency later and therefore cannot be modified.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Ensure the data that needs long\-term storage has been <a href="https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration">backed up</a> properly in case of computer crashes or disk damage which causes data loss.</div><br> |
   

6. Confirm the **configuration details** and **configuration fee**. If nothing is wrong, select the checkbox before the Terms of Service and click **Create now**.


<span id="3ANBhR0g"></span>
## Subsequent operations

After the managed heterogeneous computing cluster is created successfully, you can perform heterogeneous computing, AI inference, and service deployment. For detailed instructions, see [AI cloud native](https://docs.byteplus.com/en/docs/vke/Cloud-native_Al).
