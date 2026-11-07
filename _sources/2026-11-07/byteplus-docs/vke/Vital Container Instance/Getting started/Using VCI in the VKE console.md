---
title: "Using VCI in the VKE console"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-Vital-Container-Instance-in-the-console"
---

This topic describes how to quickly deploy applications by using VCI in the VKE console. This helps you quickly understand and use VCI.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

This topic takes the quick deployment of an Nginx application in a VPC\-CNI cluster as an example to introduce the procedure for using VCI. For the method of using VCI in a Flannel cluster, see [Using VCI in Flannel clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Flannel-cluster).

<span id=".5q2l6aqk5LiA77ya5Yib5bu6LXZwYy1jbmkt5a655Zmo572R57uc5qih5Z6L55qE6ZuG576k"></span>
## Step 1: Create a VKE cluster

The following content describes how to create a VPC\-CNI cluster without ECS nodes by using a VKE cluster template. This helps you quickly use VCI.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the top navigation bar, select the region closest to your business.

3. In the left navigation bar, click **Cluster**. On the page that appears, click **Create cluster**.

4. In the **Create cluster** dialog box, click **Create now** in the **Custom managed clusters** section.

5. On the **Create cluster** page, configure the cluster based on the on\-screen prompts.

   This quick start uses the parameter settings shown in the table below. For unmentioned parameters, keep their default settings. For more information, see [Creating managed clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

   
   |Parameter |Description |Example |Screenshot |
   |---|---|---|---|
   |**Basic configuration** |||<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d9ee632cfa897c907fb01275c13eb1f1.png) </span> |
   |Name |Specify a name for the cluster. |**vci\-cluster** ||
   |Kubernetes version |Select the version of the Kubernetes cluster to deploy.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The latest Kubernetes version supported by VKE may not support VCI. For details, see the detailed description of each version in <a href="https://docs.byteplus.com/en/docs/vke/Kubernetes-version-release-notes">Kubernetes version release notes</a>.</div><br> |Select the latest Kubernetes version supported by VCI. ||
   |**Networking** ||||
   |VPC |Select the VPC to which the cluster belongs. Select the created VPC as described in [VCI preparations](https://docs.byteplus.com/en/docs/vke/VCI-preparations). |**demo\-vpc (192.168.0.0/16)**  ||
   |Network model |Configure pod networking (CNI) solution for the cluster. |**VPC\-CNI** ||
   |Control plane subnets |Select subnets in the VPC. |**demo\-vpc\-subnetA** and **demo\-vpc\-subnetB** ||
   |Pod subnets |Select the VPC subnet used to allocate IP addresses for pods deployed in the cluster. |**demo\-vpc\-subnetA** and **demo\-vpc\-subnetB** ||
   |Public NAT for internet endpoint |After this feature is enabled, use a NAT gateway to provide public access for nodes and applications within the cluster.<br><br><br>* If the VPC of cluster has a NAT gateway, VKE will use that gateway.<br><br>* If the VPC of cluster does not have a NAT gateway, VKE will create a NAT gateway and automatically generate SNAT rules. The newly created NAT gateway uses the **Pay\-by\-CU** billing mode. For billing details, see [NAT Gateway billing](https://docs.byteplus.com/en/docs/natgateway/Pay-by-CU). |Enable ||
   |Internet access to API Server |After you enable Internet access to API Server, VKE automatically creates an EIP of the BGP (Multipath) type and associates it with a CLB instance. This enables the cluster to be accessed over the public network. |Enable ||
   |**Operation and maintenance configuration** ||||
   |Container observability |This feature is enabled by default. Enabling it allows you to monitor the metrics of basic cluster resources, including nodes, kubelet, and kube\-state\-metrics, and control plane services, including kube\-apiserver, kube\-scheduler, and etcd. |Close ||
   

6. In the lower\-right corner of the page, click **Next: Node pool configuration**.

   For this example, keep the default configuration, which indicates that **Create later** is selected for the **Node pool** parameter. In this way, only virtual nodes are created in the cluster, and VCI is used to deploy add\-ons in the cluster.

7. In the lower\-right corner of the page, click **Next: Addon configuration**. Add\-ons include all functional add\-ons and necessary system add\-ons supported by the cluster.

   You need to install the **vci\-virtual\-kubelet** add\-on in VCI scenarios. Configure other add\-ons based on your business requirements.

8. Click **Next: Configuration confirmation** in the lower\-right corner of the page. After confirming the cluster configuration information and reading the terms of service, scroll to the bottom of the page, select **I have read and agree to Vital Kubernetes Engine Specific Terms of Service**, and click **Confirm** in the lower\-right corner of the page to create the cluster.

   It will take 15 to 20 minutes to create a cluster. You can click **Cluster list** to proceed with other configurations, or stay on this page to view the creation progress.


<span id=".5q2l6aqk5LqM77ya6YOo572y5bqU55So"></span>
## Step 2: Deploy an application

After you create a cluster, you can deploy an application by using a Deployment.


1. In the left navigation bar of the [VKE console](https://console.byteplus.com/vke), click **Cluster**.

2. On the **Cluster** page, find the cluster created in **Step 1** and click the cluster name.

3. In the left navigation bar of the cluster management page, click **Workload** \> **Deployment**.

4. On the **Deployment** page, click **Create Deployment**.

5. On the **Create Deployment** page, specify the parameters of the Deployment by following the wizard.

   This quick start uses the parameter settings shown in the table below. For unmentioned parameters, keep their default settings. For parameter details, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

   1. **Basic Information**

      
      |Parameter |Description |Example |
      |---|---|---|
      |Name |Enter the name of the workload. |**demo\-vci\-deployment** |
      |Namespace |Select a namespace for the workload. |**default** |
      |Number of instances |Enter the number of instances for the workload. |**1** |
      |Computing power type |Select infrastructure resources where the workload is deployed. Valid values: |**VCI** |
      

   2. **Container configuration**

      
      |Parameter |Description |Example |
      |---|---|---|
      |**Basic Information** |||
      |Container name |Enter a name for the container. |**demo\-vci\-container** |
      |Container image |Enter an image address without an image tag, or click **Choose your own image** to select an image that has already been uploaded to a CR instance as described in [Preparations](https://docs.byteplus.com/en/docs/vke/Preparations). |**doc\-cn\-beijing.cr.volces.com/vke/nginx\-demo** |
      |Image tag |Select the version of the image. If you do not select a version, the **latest** version is pulled by default.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the NGINX image tag is not <strong>latest</strong>, you must select a specific image tag. Otherwise, the workload cannot be created.</div><br> |**v1.0** |
      |**Container port** |||
      |Port |Configure the port that the application in the container uses to connect to services outside the container. |* Protocol: **TCP**<br><br>* Port number: **80**<br><br>* Port name: **demo\-port** |
      

   3. **Advanced settings**

      
      |Parameter |Description |Example |
      |---|---|---|
      |**VCI specification configuration** |||
      |Instance family type |Select the method of using the VCI instance family.<br><br>The characteristics, scenarios, and unit prices vary based on different instance families. For details, see [VCI specifications](https://docs.byteplus.com/en/docs/vke/VCI-instance-types) and [Pay-as-you-go](https://docs.byteplus.com/en/docs/vke/Pay-as-you-go). |**Default instance family** |
      |Number of instances |The number of VCI Pods in the workload. |**1** |
      

5. Click **Confirm** in the lower\-right corner of the page to create the Deployment.

   On the **Deployment** page, click the Deployment name to go to the details page. Then, click the **List of instances** tab to view the running status of the Pods for the Deployment. If **Running** is displayed in the Status column, it indicates that the Deployment runs as expected.


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
   |Name |Specify a name for the service. |**demo\-vci\-service** |
   |**Configurations for access** || |
   |Access method |The access type of the service. |**LoadBalancer** |
   |Port mapping |After you enable the feature, the ENI of pods are specified as the backend servers of the load balancer. Note that the CLB is not able to handle too many backend servers. So you need to make sure the number of servers is acceptable to the CLB in the topology. For details about the limitations, see [Constraints and limits of CLB](https://docs.byteplus.com/en/docs/clb/Product-Overview-07). |Enable |
   |Load balancer |Configure a load balancer for the service. |Select **Public NAT for internet endpoint** and **Automatically create**, and specify the **Name** and **Subnet** parameters of the Load Balancer. Keep the default configurations of other parameters. |
   |Port mapping |Create the mapping between the service port and the container port. |* Name: **test**<br><br>* Service level port: **80** |
   

4. After you create the service, copy the address in the **External endpoint** column on the **Service** tab of the **Access method** tab.

5. Enter the **external endpoint** address in the browser address bar to go to the Nginx welcome page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_065b97d393a5f72cf045e78822734b77.png) </span>


<span id="4eOoo2vU"></span>
## Step 4: (Optional) Monitor the application

After the application is deployed, you can use cloud\-native observability capabilities to monitor the running status and resource usage of the application, such as CPU and memory usage, to facilitate operations and maintenance. For related descriptions, see [Monitoring VCI with VMP](https://docs.byteplus.com/en/docs/vke/Monitoring-VCI-instances-using-Vital-Managed-Service-for-Prometheus).

<span id="VePC9aHj"></span>
## Release resources

After you get started with VCI, if you do not need to use applications that are deployed through VCI, refer to the guidance in [Managing workloads](https://docs.byteplus.com/en/docs/vke/Managing-Deployments) to delete the deployments. If you do not need to use the VKE cluster, refer to the guidance in [Deleting clusters](https://docs.byteplus.com/en/docs/vke/Deleting-a-cluster) to delete the cluster and its associated resources.  To continue to use the VKE cluster and the applications deployed in the cluster through VCI, make sure that your BytePlus account balance, excluding coupons, is not zero. For details, see [Billing overview](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-2).

If you continue to use the VKE cluster and the applications deployed in the cluster by using VCI, the following types of fees will be incurred. For detailed billing information, see [Product billing](https://docs.byteplus.com/en/docs/vke/Billing).


* Cluster management fees: The fees are charged by VKE.

* VCI fees: The fees are charged by VCI.

* Basic cloud resource fees: The fees for services used in the cluster, such as NAT Gateway, Load Balancer, EIP, and EBS, and other BytePlus cloud services, are billed separately by the respective cloud services.
