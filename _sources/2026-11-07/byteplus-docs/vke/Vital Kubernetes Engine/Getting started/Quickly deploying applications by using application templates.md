---
title: "Quickly deploying applications by using application templates"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Deploying-an-application-using-an-application-template"
---

This topic describes how to deploy applications in a VKE cluster by using application templates.

<span id=".5q2l6aqk5LiA77ya5Yib5bu66ZuG576k"></span>
## Step 1: Create a cluster

For the detailed procedure and parameter descriptions, see the **Step 1: Create a cluster** section in the [Using VKE via the console](https://docs.byteplus.com/en/docs/vke/Using-Vital-Kubernetes-Engine-in-the-console) topic.

<span id=".5q2l6aqk5LqM77ya6YOo572y5bqU55So"></span>
## Step 2: Deploy an application

After you create a cluster, you can deploy an application by using an application template. The following example uses the nginx template.


1. In the left navigation bar of the [VKE console](https://console.byteplus.com/vke), click **Application center \> Application template**.

2. On the **Application template** page, find the **nginx** application template section and click **Deploy**.

3. On the **Deploy application** page, specify the parameters based on the parameter descriptions in the following table.

   
   |Parameter |Description |Example |
   |---|---|---|
   |**Orchestration template** |||
   |Application templates |Select the Chart version for the nginx application. |Choose the latest version |
   |Parameter configuration |Specify a method of accessing parameter values passed to the Chart. |Keep the default configuration |
   |Name |Specify a name for the application. |**nginx** |
   |**Deployment environment** |||
   |Cluster |Select the VKE cluster created in **Step 1**. |**demo\-cluster** |
   |Namespace |Select a namespace for the target cluster. |**default** |
   |Protocol |Read and understand the agreement before selecting it. | **√**  |
   

4. Click **Confirm** to start deployment.

   After the application is deployed, it is displayed on the **Helm** page.

5. Obtain the external access address of the application to access the application and view its deployment status.

   1. On the **Helm** page, click the name of the deployed application, **nginx**.

   2. On the **Helm details** page, click the workload name in the **Workload** section.

   3. On the **Deployment details page**, click the **Access method** tab. Copy the address in the **External endpoint** column on the **Service** tab.

   4. In the browser address bar, enter the **External endpoint** address to go to the Nginx welcome page.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_065b97d393a5f72cf045e78822734b77.png) </span>


<span id=".5q2l6aqk5LiJ77ya55uR5o6n5bqU55So"></span>
## Step 3: Monitor the application

After the application is deployed, you can use cloud\-native observability to monitor its status, including CPU and memory usage, to facilitate subsequent O&M work. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

<span id=".6YeK5pS-6LWE5rqQ"></span>
## Release resources

If you no longer need a cluster, delete it and its associated resources by following the instructions in [Deleting Clusters](https://docs.byteplus.com/en/docs/vke/Deleting-a-cluster). To continue using the cluster, ensure that your BytePlus account balance (excluding vouchers) is not zero. For details, see [Billing overview](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-2).

There are two types of fees for ongoing use of VKE clusters. For details, see [Product billing](https://docs.byteplus.com/en/docs/vke/Billing).


* Cluster management fees charged by VKE.

* Cloud infrastructure costs: BytePlus resources used in the cluster, such as NAT Gateway, CLB, EIP, and EBS,  are billed separately by the corresponding cloud services.
