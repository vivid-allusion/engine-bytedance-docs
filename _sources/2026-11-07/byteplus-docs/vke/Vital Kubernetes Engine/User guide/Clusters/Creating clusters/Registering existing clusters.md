---
title: "Registering existing clusters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Register_the_cluster_by_proxy"
---

You can register clusters from local infrastructure or other cloud providers into VKE for unified management. This topic describes how to connect clusters using a proxy.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>[Beta \- apply for trial]</strong></a> Registered clusters are currently at the beta stage. To use this feature, submit an application.</div>


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information


* Currently, the following clusters can be registered with VKE: Alibaba Cloud ACK clusters, Tencent Cloud TKE clusters, Huawei Cloud CCE clusters, Google Cloud GKE clusters, Amazon EKS clusters, Baidu Cloud CCE clusters, and custom clusters.

* Currently, you can register clusters by using **proxy mode**. This method is suitable when the control plane cannot directly access the target cluster. The control plane exposes a proxy service address, and the target cluster connects to the control plane through the proxy for centralized management.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The cluster to be registered has been prepared, and you can log in to the cluster as expected.

* Make sure that available nodes exist in the cluster to be registered. Otherwise, the proxy configurations cannot be imported as expected, which will disconnect the registered cluster.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits


* Windows clusters cannot be integrated.

* The version range for Kubernetes clusters that can be integrated is from **v1.24.x to v1.31.x**.

* If the cluster to be registered does not have available nodes, the proxy configurations cannot be imported as expected. For clusters that have proxy configurations imported and are connected, if all nodes go offline, the clusters will be disconnected until available nodes are restored.

* We recommend that you make sure that at least one node in the cluster is running as expected. Otherwise, the agent may fail to be installed, which causes the cluster to become disconnected. For detailed information, see [FAQs](https://docs.byteplus.com/en/docs/vke/How_can_you_address_the_cluster_going_offline_due_to_the_lack_of_an_Agent).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

You can register an existing cluster by performing two steps. First, configure the registered cluster and obtain the proxy configurations. Then, import the configurations into the source cluster to integrate with the cluster.

<span id=".5q2l6aqk5LiA77ya6YWN572u5rOo5YaM6ZuG576k"></span>
### Step 1: Configure the registered cluster


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. On the page that appears, click **Create cluster**.

3. In the **Create cluster** dialog box, go to the **Register existing cluster** section and click **Create now**.

4. On the **Create cluster** page, follow the wizard to configure the cluster.


**Basic configuration**



|**Parameter** |**Description** |
|---|---|
|Name |Specify a custom name for the registered cluster. The name must be from 2 to 64 characters in length. It can contain English letters, Chinese characters, digits, and hyphens (\-). |
|Connection mode |Select the connection mode for importing the cluster based on your business requirements. In this scenario, select **Proxy mode**. |
|Cloud provider |For the third\-party platform cluster that is adapted to the distributed cloud\-native platform, you need to select the cloud provider that matches the cluster to be connected. Otherwise, some features may be unavailable. |
|Tag |Specify custom cluster labels. They are used to classify, search, and aggregate clusters with the same characteristics from different dimensions, enabling flexible cluster management.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Click <strong>Add new</strong> to add custom cluster labels. Up to 50 labels can be added to a single resource.</div><br> |


   * **Access ** **configuration**

      
      |**Parameter** |**Description** |
      |---|---|
      |VPC |The VPC used by the registered cluster to be connected. |
      |Subnet |The subnet used by the registered cluster to be connected. Use the subnet to create a load balancer for the cluster API server. |
      |Internet access to API Server |This feature is disabled by default. If you enable this feature, the system will automatically create an EIP (default EIP configuration: BGP, 10 Mbit/s, and pay\-as\-you\-go). You can click **Change EIP configuration** to modify the default EIP configuration based on your business requirements. The system will then associate the EIP with the load balancer of the API server for the registered cluster. This enables the registered cluster to be connected and managed via a public network.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After you register the cluster, the public access policy for the API server cannot be updated. You need to plan the configurations in advance based on your business requirements.</div><br> |
      

   * **Advanced settings**

      
      |**Parameter** |**Description** |
      |---|---|
      |Deletion protection |This feature is enabled by default, which prevents the cluster from being accidentally deleted. After you enable this feature, you cannot delete the cluster by using the console or API. |
      |Cluster project |Project management is a resource management mechanism that allows you to manage cloud resources used by different businesses or projects in groups. IAM authorization based on projects helps maintain resource independence and data security, and enables you to view resource bills from the project perspective, which helps you efficiently calculate cloud resource usage costs. For details, see [Project management](https://docs.byteplus.com/en/docs/vke/Project-management).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">By default, the cluster is associated with the default project, and you can change the project based on your business requirements.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can add cloud resources within a single cloud account to a project for centralized management, but each resource can only belong to one project.</div><br> |
      |Allowlist access control |This feature is disabled by default. It restricts the IP addresses that can access the registered cluster.If you enable the allowlist and specify CIDR blocks in it, access will be restricted to these configured CIDR blocks. This restriction applies to two types of IP addresses:<br><br><br>* The IP address of the agent used to access the cluster<br><br>* IP addresses allowed to access the API server after cluster access<br><br><br>Otherwise, access is denied. You need to configure the allowlist based on the following requirements:<br><br><br>* You can specify the allowlist in the format of CIDR blocks, which is "x.x.x.0/x".<br><br>* Configure a CIDR block in each row and separate them by a newline character.<br><br>* The IP addresses in each row must be unique. |
      

5. After you complete the **Registration Configuration** step, click **Next: Configuration confirmation** in the lower\-right corner of the page.

6. After confirming the configuration, read the **Vital Kubernetes Engine Specific Terms of Service**, select the terms check box, and click **Confirm**. The proxy configuration will be generated, and you will be redirected to the registered cluster list. In this case, the registered cluster is in the **Waiting** state.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">During the configuration confirmation step, a pre\-check will be performed on account status, service authorization, and service quota. You can start creating the registered cluster only after all pre\-check items pass the check. If the items fail to pass the check, fix the issues based on the error messages in the <strong>Detailed information</strong> column and then re\-create the registered cluster.   </div>
   

<span id=".5q2l6aqk5LqM77ya5a-85YWl5Luj55CG6YWN572u"></span>
### Step 2: Import the proxy configurations

After you obtain the access credentials of the registered cluster, complete these steps:


1. On the **Connection** tab of the registered cluster details page, obtain the proxy configurations for the public network or private network based on your business requirements, and save the configurations in a YAML file. For example: `Agent.yaml`.

2. Go to the source platform and run the resource creation command for the cluster to be registered (such as `kubectl apply -f Agent.yaml`) to import the proxy configurations.

   When the status of the registered cluster in VKE changes to **Running**, it indicates that the cluster is connected.
