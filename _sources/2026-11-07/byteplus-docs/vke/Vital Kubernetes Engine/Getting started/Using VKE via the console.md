---
title: "Using VKE via the console"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-Vital-Kubernetes-Engine-in-the-console"
---

This topic describes how to create a cluster and deploy applications in the cluster in the VKE console.

<span id=".5q2l6aqk5LiA77ya5Yib5bu66ZuG576k"></span>
## Step 1: Create a cluster


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the top navigation bar, select the region closest to your business.

3. In the left navigation bar, click **Cluster**.

4. On the **Cluster** page, click **Create cluster**.

5. In the **Create cluster** dialog box, go to the **Custom managed clusters** section and click **Create now**.

6. On the **Create cluster** page, follow the wizard to configure the cluster.

   This quick start uses the parameter settings shown in the table below. For unmentioned parameters, keep their default settings. For details, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

   
   |Parameter |Description |Example |Screenshot |
   |---|---|---|---|
   |**Basic configuration** |||<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_89d6bc9cd32c8e32ee85eddb9d91e3e4.png) </span> |
   |Name |Specify a name for the cluster. |**demo\-cluster** ||
   |Kubernetes version |Select the version of the Kubernetes cluster to deploy. |Latest Kubernetes version ||
   |**Networking** ||||
   |VPC |Select the VPC to which the cluster belongs. Select the VPC created in [Prerequisites](https://docs.byteplus.com/en/docs/vke/Preparations). |**demo\-vpc (192.168.0.0/16)**  ||
   |Network model |Configure pod networking (CNI) solution for the cluster.<br><br><br>* **VPC\-CNI**: an underlay container network solution implemented based on the elastic network interface (ENI) of a VPC. Under the VPC\-CNI network model, VPC subnets can be selected for pod networking.<br><br>* **Flannel**: an underlay network solution (Flannel HostGateway) that allows you to use custom CIDR for pod networking of Kubernetes clusters. |**VPC\-CNI** ||
   |Control plane subnets |Select subnets in the VPC. |**demo\-vpc\-subnetA** and **demo\-vpc\-subnetB** ||
   |Pod subnets |Select the VPC subnets that pods deployed in the cluster will use. |**demo\-vpc\-subnetA** and **demo\-vpc\-subnetB** ||
   |Public NAT for internet endpoint |After this feature is enabled, use a NAT gateway to provide public access for nodes and applications within the cluster.<br><br><br>* If the VPC of cluster has a NAT gateway, VKE will use that gateway.<br><br>* If the VPC of cluster does not have a NAT gateway, VKE creates one and automatically configures SNAT rules. The newly created NAT gateway uses the **Pay\-by\-CU** billing mode. For billing details, see [NAT Gateway billing](https://docs.byteplus.com/en/docs/natgateway/Pay-by-CU). |Enable ||
   |Internet access to API Server |After this feature is enabled, VKE automatically creates an EIP of the BGP (Multipath) type and associates it with a CLB instance. This enables the cluster to be accessed over the public network. |Enable ||
   |**Operation and maintenance configuration** ||||
   |Container observability |This feature is enabled by default. When enabled, this feature monitors the metrics of basic cluster resources (such as nodes, kubelet, and kube\-state\-metrics) and control plane components (such as kube\-apiserver, kube\-scheduler, and etcd). |Disable ||
   

6. In the lower\-right corner of the page, click **Next: Node pool configuration** to configure a node pool.

   
   |Parameter |Description |Example |Screenshot |
   |---|---|---|---|
   |**Node** |||<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_abf43ceb6ecf7ba0dd9107aa82b5a910.png) </span> |
   |Node pool management |Configure whether to create a node pool:<br><br><br>* **Create now**: Creates a node pool containing ECS nodes. This node pool also supports simultaneous creation of virtual nodes, and by default, uses ECS nodes to deploy add\-ons.<br><br>* **Create later**: The system automatically creates virtual nodes, and by default, deploys add\-ons to VCIs. |**Create now** ||
   |Node source |The way in which the worker nodes are obtained. |**Create node** ||
   |**Node pool setting** ||||
   |Name |Specify a name for the node pool. |**demo\-nodepool** ||
   |Billing type |The billing model applied to ECS resources allocated to nodes. |**Pay\-as\-you\-go** ||
   |Availability zone |Select the availability zone for the new node. AZs refer to physical areas isolated from each other in terms of electricity and network in the same region. AZs communicate with each other over internal networks. |**Multiple availability zones** ||
   |Node subnet |Select the subnet for the new node. |**demo\-vpc\-subnetA** and **demo\-vpc\-subnetB** ||
   |Instance type |Select the instance specifications for the new node (ECS instance). You can select multiple instance specifications. For details about the instance specifications, see [Instance specification list](https://docs.byteplus.com/en/docs/ecs/General-purpose-EBM). |**General\-purpose ecs.g3i.xlarge ** (4 vCPU \| 16 GiB) ||
   |Number of nodes |Specify the number of nodes. The fees for ECS resources depend on the number of nodes. Make sure only the necessary nodes are running in the cluster. |**1** ||
   |**Security configuration** ||||
   |Login methods |Two authentication mechanisms are supported for logging into nodes: **Password** and **SSH key pair**. |Select **Password** and specify a strong password ||
   

7. In the lower\-right corner of the page, click **Next: Addon configuration**. You need to configure all functional add\-ons and essential system add\-ons supported by the cluster.

   In this case, you can keep the default configuration.

8. In the lower\-right corner of the page, click **Next: Configuration confirmation**. Confirm your cluster configuration. If nothing is wrong, select the **I have read and agree to Vital Kubernetes Engine Specific Terms of Service** check box and then click **Confirm** in the lower\-right corner of the page to start creating the cluster.

   Cluster creation takes 15 to 20 minutes. You can click **Cluster list** to perform other operations or stay on the cluster creation page to monitor the creation progress.


<span id=".5q2l6aqk5LqM77ya6YOo572y5bqU55So"></span>
## Step 2: Deploy an application

After the cluster is created, deploy an application using a Deployment.


1. In the left navigation bar of the **demo\-cluster** cluster management page, click **Workload** \> **Deployment**.

2. On the **Deployment** page, click **Create Deployment**.

3. On the **Create Deployment** page, specify the parameters of the Deployment by following the wizard.

   This quick start uses the parameter settings shown in the table below. For unmentioned parameters, keep their default settings. For parameter details, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

   1. **Basic Information**

      
      |Parameter |Description |Example |
      |---|---|---|
      |Name |Enter the name of the workload. |**demo\-vke\-deployment** |
      |Namespace |Select a namespace for the workload. |**default** |
      |Number of instances |Enter the number of Pod instances for the Deployment. |**1** |
      |Computing power type |Select infrastructure resources where the workload is deployed. Valid values:<br><br><br>* **Elastic Compute Service instance**: The workload is deployed on ECS nodes in the cluster.<br><br>* **Vital Container Instance**: The workload is deployed on VCIs, which are virtual nodes in the cluster. For an introduction to VCI, see [?](https://docs.byteplus.com/en/docs/vke/What-is-Vital-Container-Instance?lang=en)[?](https://docs.byteplus.com/en/docs/vke/What-is-Vital-Container-Instance?lang=en) |**Elastic Compute Service instance** |
      

   2. **Container configuration**

      
      |Parameter |Description |Example |
      |---|---|---|
      |**Basic Information** |||
      |Container name |Enter a name for the container. |**demo\-vke\-container** |
      |Container image |Enter an image address without an image tag, or click **Choose your own image** to select an image that has already been uploaded to a CR instance as described in [Preparations](https://docs.byteplus.com/en/docs/vke/Preparations). |**doc\-cn\-beijing.cr.volces.com/vke/nginx\-demo** |
      |Image tag |Select the version of the image. If you do not select a version, the **latest** version is pulled by default.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the selected image does not have the <strong>latest</strong> version, you need to enter or select a specific image tag. Otherwise, you cannot create the workload.</div><br> |**v1.0** |
      |**Container port** |||
      |Port |Configure the port that the containerized application uses to connect to external services. |* Protocol: **TCP**<br><br>* Port number: **80**<br><br>* Port name: **demo\-port** |
      

   3. **Advanced settings**

      No advanced configuration is required in this example. Keep all default settings and then click **Confirm** in the lower\-right corner of the page.

4. On the **Deployment** page, view the created Deployment.

   Click the Deployment name to go to the details page. Then, click the **List of instances** tab to view the running status of the pod instances for the Deployment. If **Running** is displayed in the Status column, it indicates that the Deployment runs as expected.


<span id=".5q2l6aqk5LiJ77ya6K6_6Zeu5bqU55So"></span>
## Step 3: Access the application

After you deploy the application, you can access the application on the **Service** tab to check whether the application is deployed.


1. On the **Deployment details page**, click the **Access method** tab.

2. On the **Access method** tab, click the **Service** tab, and then click **Create Service**.

3. On the **Create Service** page, configure service information. After you complete the configuration, click **Confirm** in the lower\-right corner of the page.

   This quick start uses the parameter settings shown in the table below. For unmentioned parameters, keep their default settings. For detailed parameter settings, see [Creating CLB services using the console](https://docs.byteplus.com/en/docs/vke/Creating-a-LoadBalancer-Service-in-the-console).

   
   |Parameter |Description |Example |
   |---|---|---|
   |**Basic Information** |||
   |Name |Specify a name for the service. |**demo\-service** |
   |**Access configuration** |||
   |Access type |Specify the access type of the service. |**LoadBalancer** |
   |LB\-to\-pod direct access mode |After you enable the feature, the ENIs of pods are specified as the backend servers of the load balancer. Note that the CLB cannot handle too many backend servers. Therefore, you need to make sure the number of servers is acceptable to the CLB in the topology. For details about the limitations, see [Constraints and limits of CLB ](https://docs.byteplus.com/en/docs/clb/Product-Overview-07). |Enable |
   |Load balancer |Configure a load balancer for the service. |Select **Public NAT for internet endpoint** and **Automatically create**, and specify the **Name** and **Subnet** parameters of the Load Balancer. Keep the default configurations of other parameters. |
   |Port mapping |Create the mapping between the service port and the container port. |* Name: **test**<br><br>* Service level port: **80** |
   

4. After you create the service, copy the address in the **External endpoint** column on the **Service** tab of the **Access method** tab.

5. Enter the **external endpoint** address in the browser address bar to go to the Nginx welcome page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_065b97d393a5f72cf045e78822734b77.png) </span>


<span id=".5q2l6aqk5Zub77ya55uR5o6n5bqU55So"></span>
## Step 4: Monitor the application

After the application is deployed, you can use cloud\-native observability to monitor its status, including CPU and memory usage, to facilitate subsequent O&M work. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

<span id=".6YeK5pS-6LWE5rqQ"></span>
## Release resources

If you no longer need a cluster, delete it and its associated resources by following the instructions in [Deleting Clusters](https://docs.byteplus.com/en/docs/vke/Deleting-a-cluster). To continue using the cluster, ensure that your BytePlus account balance (excluding vouchers) is not zero. For details, see [Billing overview](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-2).

If you continue to use VKE clusters, you will be charged the following two types of fees. For details, see [Product billing](https://docs.byteplus.com/en/docs/vke/Billing).


* Cluster management fees charged by VKE.

* Cloud infrastructure costs: BytePlus resources used in the cluster, such as NAT Gateway, CLB, EIP, and EBS,  are billed separately by the corresponding cloud services.
