---
title: "Accessing an ALB across VPCs via PrivateLink"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Accessing-an-ALB-across-VPCs-via-PrivateLink"
---

This topic describes how to use PrivateLink to enable resources in one Virtual Private Cloud (VPC) to access the Application Load Balancer (ALB) service in another VPC within the same region.

<span id="312ba362"></span>
## Scenario examples

This topic demonstrates a scenario illustrated in the following diagram. A company created two VPCs (named VPC01 and VPC02) in China (Shanghai) using a single BytePlus account. VPC01 contains an Elastic Compute Service (ECS) instance (named ECS01). VPC02 contains an ALB instance (named ALB01). The ALB is associated with a server group. The server group contains two ECS instances (named ECS02 and ECS03) located in separate availability zones. The company requires that ECS01 in VPC01 can access ALB01 in VPC02 via private connectivity, thereby gaining access to the applications deployed on ECS02 and ECS03.

To meet these requirements, the [PrivateLink](https://docs.byteplus.com/docs/privatelink/Product-Overview-01) service should be implemented in this scenario.​ To use PrivateLink, you need to create an endpoint and an endpoint service. PrivateLink establishes private connectivity between endpoints and endpoint services. This enables resources in one VPC to access service resources in another VPC through private connectivity, avoiding potential security risks caused by internet access.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_887d80b20b1356ebdcfa4734034b6aa0.png) </span>

<span id="126890b0"></span>
## Limits


* You have contacted your account manager to enable the feature of "ALB instances serve as the PrivateLink endpoint service resource".

* When an ALB instance serves as a resource for PrivateLink endpoint service, the availability zones where the endpoint service's resources are deployed must be a subset of the zone where the ALB instance resides. Additionally, the availability zones of the endpoint must be a subset of the zones where the endpoint service's resources are deployed. Endpoint services and endpoints cannot communicate across availability zones. We recommend deploying your endpoint service resources and VPC endpoints in the same availability zones as your ALB instance for better disaster recovery.


<span id="36169b16"></span>
## Prerequisites


* You have created VPC01 and VPC02 in China (Shanghai). You have deployed a subnet (named VPC01\-Subnet\-A) in Availability Zone A within VPC01. Within VPC02, you have deployed a subnet (named VPC02\-Subnet\-A) in Availability Zone A and a subnet (named VPC02\-Subnet\-B) in Availability Zone B. For procedure, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) and [Creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).

* You have created ECS01 within VPC01 to send requests. Within VPC02, you have deployed ECS02 in Availability Zone A and ECS03 in Availability Zone B to receive and process requests. You have deployed the NGINX service on ECS02 and ECS03. For creation procedure, see [Buying ECS instances](https://docs.byteplus.com/en/docs/ecs/Overview-of-methods-for-buying-ECS-instances).


<span id="db1c036c"></span>
## Procedure

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This procedure only describes required parameters. Use default values for other parameters. For parameter description, see the documents listed in the "Configuration procedure".</div>


<span id="6c1408f1"></span>
### Configuration procedure


|**SN** |**Step** |**Documentation** |
|---|---|---|
|1 |Create an ALB instance |[Create an ALB instance](https://docs.byteplus.com/en/docs/clb/Creating-an-instance) |
|2 |Create a server group |[Create server group](https://docs.byteplus.com/en/docs/clb/Managing-server-groups) |
|3 |Listener |[Create an HTTP listener](https://docs.byteplus.com/en/docs/clb/Creating-HTTP-listener) |
|4 |Create an endpoint service |[Create an endpoint service](https://docs.byteplus.com/en/docs/privatelink/Creating-endpoint-services) |
|5 |Create an endpoint |[Create an interface endpoint](https://docs.byteplus.com/en/docs/privatelink/Endpoint-02) |
|6 |Test connectivity |N/A |


<span id="856c1753"></span>
### Step 1: Create an ALB instance


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the left navigation pane, click **Instance** to enter the **Instance management** page.

3. On the **Instance management** page, click **Create instance**.

4. On the **Create application load balancer** page, configure parameters as shown in the table below.

   
   |**Parameter** |**Description** |**Parameter value** |
   |---|---|---|
   |**Basic Information** |||
   |Region |Select the region where the ALB instance resides. |China (Shanghai) |
   |Name |Enter the name of the ALB instance. |ALB01 |
   |Instance edition |Select the instance edition. |Basic edition |
   |**Network configuration** |||
   |IP type |Select the IP type of ALB instance. |IPv4 |
   |Network type |Set the network type of ALB instance. The system will assign IP addresses to the ALB instance based on your selection.<br><br><br>* **Public**: A public ALB instance has both an elastic IP address (EIP) and a private IP address.<br><br>* **Private**: A private ALB instance only has a private IP address. |Private |
   |VPC |Select the VPC to which the ALB instance belongs. |VPC02 |
   |Availability zone |Select the availability zone to which the ALB instance belongs. At least select one availability zone. When multiple availability zones exist in the region, it is recommended to select at least two availability zones for deploying the ALB instance to improve overall system availability. |Availability Zone A, Availability Zone B |
   |Subnet |Select the subnet to which the ALB instance belongs. The private IP address of the ALB instance will be allocated from the CIDR block of the selected subnet. |VPC02\-Subnet\-A, VPC02\-Subnet\-B |
   

5. After confirming the configuration is correct, and click **Submit**.


<span id="e0426652"></span>
### Step 2: Create a server group


1. On [the Server group page](https://console.byteplus.com/alb/region:alb+cn-shanghai/servergroup), click **Create backend server group**.

2. On the **Create server group** page, configure parameters as shown in the table below, then click **Save**.

   
   |**Parameter** |**Description** |**Parameter value** |
   |---|---|---|
   |Server group type |Select the type for the server group to be created. |Server type |
   |Name |Enter server group name |Group01 |
   |VPC |Select the VPC to which the server group belongs. The server group must be in the same VPC as the ALB instance to be associated. |VPC02 |
   |Load balancing algorithm |Specify the load balancing algorithm. The load balancing algorithm defines how to distribute client requests among backend servers. |Weighted Round Robin (WRR) |
   |Communication protocol |Specify the communication protocol used between the ALB instance and backend servers. |HTTP |
   |Health Check |Health check is enabled by default. After the server group is attached to an ALB instance, the ALB will initiate health check requests to the backend servers in the group according to your specified rules to monitor their health status. |On |
   

3. In the server group list, locate the new server group, then click **Add backend server** in the **Actions** column.

4. On the **Select backend server** page, check the target backend servers of ECS02 and ECS03, then click **Next: configure ports and weights**.

5. On the **Configure ports and weights** page, set the backend server port to 80 and the weight to 100, then click **Save**.


<span id="f0a7e6a9"></span>
### Step 3: Configure a listener

This following demonstrates how to create an HTTP listener.


1. On [the Instance management page](https://console.byteplus.com/alb/region:alb+cn-shanghai/instance), locate the ALB instance created in Step 1, then click **Listener** in the **Actions** column.

2. In the **Listener information** tab, click **Add listener**.

3. On the **Add listener** page, configure parameters according to the table below, then click **Next: default backend server group**.

   
   |**Parameter** |**Description** |**Parameter value** |
   |---|---|---|
   |Name |Enter the listener name. |HTTP\-80 |
   |Listener protocol |Set the listener protocol. |HTTP |
   |Listener port |Set the listener port. |80 |
   

4. On the **Default server group** tab, select the server group created in Step 2 from the dropdown, then click **Next: confirm the configuration**.

5. After confirming the listener’s configuration is correct, click **Save**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After you create a listener, the system generates a default <a href="https://docs.byteplus.com/docs/clb/Forwarding-rule-Overview">forwarding rule</a>.</div>


<span id="1c42c7a2"></span>
### Step 4: Create an endpoint service


1. Log in to [the PrivateLink console](https://console.byteplus.com/pl/region:pl+cn-shanghai/endpoints).

2. In the top menu bar, select the target project and region.

3. In the left navigation pane, click **Endpoint Service**.

4. On the **Endpoint Service** page, click **Create Endpoint Service** and configure parameters based on the table below.

   
   |**Parameter** |**Description** |**Parameter value** |
   |---|---|---|
   |**Basic Information** |||
   |Region |Select the region to which the endpoint service belongs. |China (Shanghai) |
   |Name |You do not need to manually type a name for the endpoint service. After successful creation of the endpoint service, the system automatically generates the name in the format of “com.volces.privatelink.<region ID\>.<endpoint service ID\>.” |N/A |
   |**Service Resource** |||
   |Type |Select the service resource type provided by the endpoint service. |ALB |
   |Service Resource |Check the target ALB instance serving as the service resource. You also need to specify the availability zone where the service resource provides services. The specified availability zone must be within the zone range of the ALB instance. |ALB01, Availability Zone A |
   |**Advanced options** |||
   |Auto accept connection |Select whether this endpoint service automatically accepts connection requests from endpoints.<br><br><br>* **Yes**: The system will automatically accept all connection requests from endpoints to this endpoint service.<br><br>* **No**: Manual acceptance is required for connection requests from endpoints.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you select <strong>No</strong> here, you need to manually accept connection requests from endpoints later. For procedure, see <a href="https://docs.byteplus.com/docs/privatelink/Accepting-Rejecting-endpoint-connection">Accepting an endpoint connection</a>.</div><br> |Yes |
   

5. Click **Create** to complete the action.

6. Check and record the name of the created endpoint service for use in subsequent steps.


<span id="548b241b"></span>
### Step 5: Create an endpoint


1. On the **Endpoint** page, click **Create Endpoint** and configure parameters based on the table below.

   
   |**Parameter** |**Description** |**Parameter value** |
   |---|---|---|
   |**Basic Information** |||
   |Region |Select the region of endpoint. |China (Shanghai) |
   |Name |Enter the name of endpoint. |endpoint01 |
   |Type |Select the type of endpoint.<br><br>When the resource type of the endpoint service to be associated is "ALB," the endpoint type must be specified as **Interface**. |Interface |
   |**Endpoint Service** |||
   |Add method |Select the method for associating an endpoint service. It supports two methods: **Add by Service Name** and **Select available service**. |Select available service |
   |Endpoint Service |Select the endpoint service created in Step 4. |com.volces.privatelink.cn\-shanghai.epsvc\-2fe630gurkl37k5gfuy33\*\*\*\* |
   |**Network configuration** |||
   |VPC |Select the VPC to which the endpoint belongs. |VPC01 |
   |Availability Zone and Subnet |Check the availability zones of the endpoint services and select the corresponding subnet for each. The list displays only availability zones where associated endpoint services reside.<br><br>The system automatically creates an endpoint network interface in the subnet you select. |Availability Zone A, VPC01\-Subnet\-A, auto\-assign IPv4 |
   |Security group |Select the security group(s) to be associated with the endpoint's network interface. |Default |
   

2. **Confirm the order**, and follow the console guidance to review and accept the Legal.

3. Click **Buy now** to check whether the creation is successful.

4. Check and record the name of the created endpoint for use in subsequent steps.


<span id="eb3350ca"></span>
### Step 6: Test connectivity


1. Remotely log in to ECS01 in VPC01. The ECS instance in this example runs the Linux operating system. For procedure, see [Logging on to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the `curl http://<endpoint_domain>:<listener_port>` command to test network connectivity.

   For example, if the endpoint domain is ep\-3qe9ayz306b5\*\*\*\*.cn\-shanghai.privatelink.volces.com and the listener port of the service resource (the ALB instance) is 80, run curl http://ep\-3qe9ayz306b5\*\*\*\*.cn\-shanghai.privatelink.volces.com:80.

   If the response displays the content of the website configured on the backend server, it indicates successful network connectivity.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f86e00b613544ee988c0cbbf46d60776~tplv-goo7wpa0wc-image.image) </span>
