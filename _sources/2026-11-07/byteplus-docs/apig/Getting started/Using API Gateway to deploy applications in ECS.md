---
title: "Using API Gateway to deploy applications in ECS"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/ecs-application"
---

API Gateway supports connecting to Elastic Compute Service (ECS) to provide highly available gateway functionality for applications within the ECS. This article uses the Nginx application deployed on the Elastic Compute Service as an example to explain how to use the API Gateway to deploy applications hosted on the ECS.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

API Gateway (APIG) provides managed cloud\-native gateway functionality for [Elastic Compute Service](https://docs.byteplus.com/en/docs/ecs/What-is-Elastic-Compute-Service), enabling highly available, highly scalable Ingress traffic management. Additionally, API Gateway supports connecting to [Vital Managed Service for Prometheus](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus), enabling instance\-level and service\-level observation and alerts.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A ECS instance has been bought. For more information please refer to the [Overview of methods for buying ECS instances](https://docs.byteplus.com/en/docs/ecs/Overview-of-methods-for-buying-ECS-instances).

* The application has been deployed in ECS and the corresponding ports are opened. In this example, the Nginx application is used, based on port 80.

* A Vital Managed Service for Prometheus workspace has been created. For more details, please refer to [Creating a workspace](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* A domain name pending for binding has been obtained from the domain registrar, and an ICP filing or access filing has been completed with the Ministry of Industry and Information Technology. For details, please refer to the [Filing Process](https://docs.byteplus.com/en/docs/6428/68727).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Yib5bu65a6e5L6L"></span>
### Step 1: Create an instance


1. Log in to the [API Gateway Console](https://console.byteplus.com/veapig).

2. In the top navigation bar, select the target region.

3. In the left navigation bar, select **Instance Management**, on the Instance Management page, click **Create Instance**.

4. On the Create Instance page, configure the instance information as required.

   * **Basic Information**: Select **standard gateway** type and configure the name of the APIG instance, in this case, apig\-demo.

   * **Specification Configuration**: Configure the specifications, VPC, and other information for the APIG instance. The private network must be consistent with the VKE cluster.

   * **Observability**: Enable alerts and monitoring, and select the Vital Managed Service for Prometheus workspace.

5. Keep other configurations default, read "API Gateway Terms of Service" and check the box to agree.

6. Click **Confirm order** to start creating the APIG instance.


<span id=".5q2l6aqk5LqM77ya5Yib5bu65pyN5Yqh"></span>
### Step 2: Create a service


1. Select **route management \> Service list (Domain name)**  from the left navigation bar. Click **create service**.

2. In the Create Service dialog, configure the service name and instance.

3. Click **confirm** to complete the configuration of the service.


<span id=".5q2l6aqk5LiJ77ya57uR5a6a6Ieq5a6a5LmJ5Z-f5ZCN"></span>
### Step 3: Bind a custom domain name


1. Click on the target service name in the service list to enter the Overview page of the service.

2. Select the **domain management** tab, click **add domain name**, and configure a custom domain name and protocol in the service.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Public network Domain names need to complete ICP filing or access filing with the Ministry of Industry and Information Technology, the Domain names mentioned in this article are only examples.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You need to ensure the DNS resolution relationship between the custom Domain name and the API Gateway IP address independently, to ensure that the API Gateway instance can be accessed normally via the Domain name.   </div>
   

3. Click **confirm** to complete the binding of the Domain name.


<span id=".5q2l6aqk5Zub77ya5Yib5bu6IFVwc3RyZWFt"></span>
### Step 4: Create a upstream


1. In the left navigation bar, select **Backend Management \> Upstream List**.

2. On the Upstream List page, click **Create Upstream**.

3. On the Create Upstream page, fill in the parameter information as required.

   * **Basic Information**: Configure the name of the Upstream and the associated instance.

   * **Upstream configuration**: Select **Elastic Compute Service** for the backend service.

   * Click **add**, select the ECS instance on the pop\-up configuration page, and configure the service port.

4. Click **confirm** to finish creating an Upstream of Elastic Compute Service type.


<span id=".5q2l6aqk5LqU77ya5Yib5bu66Lev55Sx"></span>
### Step 5: Create a route

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The system supports configuring a single route for a specified service, as well as batch creation of routes for multiple services. This article takes configuring a single route for a specified service as an example.</div>


* <div data-tips="true" data-tips-type="tip">For the procedure to batch create routes for multiple services, please refer to <a href="https://docs.byteplus.com/en/docs/apig/Creating_a_route">Creating a route</a>.</div>


1. Select **route management \> Service list (Domain name)**  from the left navigation bar.

2. On the service list page, click the target service name to enter the current service overview page.

3. Click **add route** to configure route information.

   * **Basic Information**: Configure the route's name, request method, and path.

   * **Upstream Traffic Distribution**: Select **upstream type** from the dropdown menu and choose the configured **Elastic Compute Service** upstream. Set the weight to 100, indicating that 100% of the traffic will be forwarded to this backend.

4. Click **confirm** to complete the route creation.


<span id=".5q2l6aqk5YWt77ya6YWN572u5a6J5YWo57uE"></span>
### Step 6: Configure Security Groups


1. Log in to [the VPC console](https://console.byteplus.com/vpc).

2. In the top navigation bar, select the target region.

3. In the left navigation bar, select **Security groups**, and find the security group for the ECS instance in the list. Click on the security group name to enter the details page of the security group.

4. Select **Access Rules \> Inbound Rules** tab, click **add rule**, allow the APIG security group (named `apig-sg-<accountID>`), to ensure that the gateway can normally access resources on the corresponding ECS port.

5. Click **confirm** to complete the configuration.


<span id=".57uT5p6c6aqM6K-B"></span>
## Result validation

<span id=".6K6_6Zeu5bqU55So"></span>
### Access application

In the local environment, use the following command to access the application.

```bash
curl http://apig-example.com
```


The expected access result is as follows. Indicates that the application deployed on the Elastic Compute Service can be accessed through a custom Domain name.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fa8b1c0e6cb8ece6ff4e3aa0840c387a.png) </span>

<span id=".5p-l55yL55uR5o6n5L-h5oGv"></span>
### View monitoring information


1. In the left **navigation bar**, click on the target instance name and enter the Overview page.

2. Click **Monitoring** to switch to the **Monitoring** tab.

3. Set the query time range to view the current instance's monitoring metrics. Supports viewing up to the past 30 days of monitoring data.
