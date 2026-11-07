---
title: "Cross-VPC ECS instances as backend servers (CEN)"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Cross-VPC-ECS-instances-as-backend-servers-CEN"
---

This article explains how to configure Network Load Balancer (NLB) with Cloud Enterprise Network (CEN) to enable cross\-VPC Elastic Compute Service (ECS) instances as NLB backend servers.

## Scenarios

By leveraging CEN, the NLB routes traffic to ECS instances across VPC boundaries for processing.

This topic uses a same\-region deployment scenario as an example, as illustrated below:

> **tip**

> For cross\-region scenarios, in addition to completing the configurations described in this document, you must also configure cross\-region bandwidth settings for your CEN instance by [Creating a bandwidth package](https://docs.byteplus.com/en/docs/cen/CEN-bandwidth-packages-01) and [Allocating inter\-region bandwidth](https://docs.byteplus.com/en/docs/cen/Inter-region-bandwidth-01).

> The diagram displays sample configurations for each service. Modify these values according to your actual network architecture during implementation.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d727303b198bd0869e7e5fa5de3cc080.png)

All resources in the diagram above are located in the China (Beijing) region. Other data annotations in the diagram are explained below:

* Virtual Private Cloud VPC\-A: CIDR block `172.16.0.0/16`.

   * The CIDR block of Subnet\-A1 is `172.16.1.0/24`.

   * The CIDR block of Subnet\-A2 is `172.16.2.0/24`.

   * The private IP address of ECS\-A is `172.16.1.10`.

* Virtual Private Cloud VPC\-B: CIDR block `192.168.0.0/16`.

   * The CIDR block of Subnet\-B is `192.168.1.0/24`.

   * The private IP address of ECS\-B is `192.168.1.10`.

## Preparations

1. Using your BytePlus account, create two VPCs in the China (Beijing) region, with configurations matching the parameters described in the [background section above](https://docs.byteplus.com/en/docs/natgateway/Configuring-multiple-Internet-NAT-Gateways-in-a-VPC#.6IOM5pmv5LuL57uN). For specific actions, see [Creating a Virtual Private Cloud](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

2. Create ECS\-A (172.16.1.10) in Subnet\-A1 of VPC\-A and ECS\-B (192.168.1.10) in Subnet\-B of VPC\-B. Neither ECS has an EIP bound to it. For more information, see [Purchasing an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

3. Deploy backend services on ECS\-B. For operations, see [Configuring the backend services](https://docs.byteplus.com/en/docs/clb/Creating-an-HTTP-static-page#.5q2l6aqk5LqM77ya5pCt5bu65ZCO56uv5pyN5Yqh).

## Configuration procedures

> **tip**

> The following section only covers essential parameters and their recommended values when configuring each service resource. For all parameters not explicitly discussed, retain the default settings unless otherwise required by your specific use case.

### Step 1: Configure CEN

####  **(1) Create a CEN instance**

   1. Log in to the[ CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

   2. Click **Create CEN**.

   3. Configure relevant parameters based on the table below.

      |Parameter |Explanation |Value |
      |---|---|---|
      |Name |Type the name of the CEN instance. |cen\-01 |
      |Attaching a network instance |Load a network instance |On |
      |Regions |Select the region to which the network instance belongs. |China (Beijing) |
      |Instance type |Select the type of network instance. |VPC |
      |Network Instances |Select the network instance to be attached. |VPC\-A |

   4. Click **Create** to complete the action.

####  **(2) Load network instance**

   1. Click the target CEN instance name.

   2. On the **Network Instances** tab, click **Attach Network Instance**.

   3. Configure relevant parameters based on the table below.

      |Parameter |Explanation |Value |
      |---|---|---|
      |Account |Select the account to which the network instance belongs. |My account |
      |Regions |Select the Region where the network instance resides. |China (Beijing) |
      |Instance type |Select the type of network instance. |VPC |
      |Network Instances |Select the network instance to be attached. |VPC\-B |

   4. Click **Attach** to complete the action.

   Log in to ECS\-A and execute the command `ping <ECS-B's IP address>` to verify whether the two VPCs can communicate.

### Step 2: Configure the NLB instance

#### (1) Create the NLB instance

   1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

   2. In the top menu bar, select the target project and region.

   3. Click **Create NLB**, and configure related parameters according to the table below.

      |Parameter |Explanation |Example |
      |---|---|---|
      |**Basic information** |||
      |Regions |Select the Region where the NLB instance resides. After you select a region, the created NLB instance can only be used by resources in the selected region and cannot be migrated. You must confirm that the region of the instance is the same as that of the backend server instance. |China (Beijing) |
      |Name |Type the name of NLB instance. |nlb\-01 |
      |**Network Configuration** |||
      |IP version |Select the private IP address type of the NLB instance. |IPv4 |
      |Network Type (IPv4) |Select the network type for the NLB instance's IPv4 address. |Internet |
      |VPC |Select the Virtual Private Cloud (VPC) to which the NLB instance belongs.  |vpc01 |
      |AZs and Subnets |Select the supported Availability Zone for the NLB instance, and specify the subnet, IP address, and Elastic IP (EIP) for each availability zone.<br><br>NLB supports multi\-AZ active\-active disaster recovery by default, and please select at least 2 availability zones. If higher business reliability is required, you may optionally choose 2 or more availability zones.<br><br><br>* **Subnet**: Provides a private network deployment environment for the NLB instance. The system automatically creates a network interface within the subnet and attaches it to the NLB.<br><br>* **IPv4 address**: Select the allocation method for the IPv4 address of the NLB instance. After the instance is created, all assigned IPv4 addresses cannot be modified.<br><br>   * **Auto IP Assignment**: The system automatically allocates 3 private IPv4 addresses for the network interface associated with the NLB, including 1 VIP and 2 LIPs.<br><br>   * **Custom\-assign IP**: Please manually input an IPv4 address within the subnet range. When typing an IPv4 address as the VIP for the network interface attached to the NLB. The system will automatically assign 2 LIPs.<br><br>* **EIP**: Provides internet capabilities for the NLB instance. Configure this parameter only when the network type (IPv4) is **Internet**.<br><br>   * **Newly purchased EIP**: The ElP is created along with the NLB instance, defaults to pay\-by\-data\-transfer billing method, adopts BGP (Multi\-ISP) as the ISP, and has a bandwidth cap of 200 Mbps. |* Availability zone A<br><br>   * Subnet\-A1 \| 172.16.1.0/24<br><br>   * Automatic IP assignment<br><br>   * New Elastic IP (EIP)<br><br>* Availability Zone B<br><br>   * Subnet\-A2 \| 172.16.2.0/24<br><br>   * Automatic IP assignment<br><br>   * New Elastic IP (EIP) |
      |Security group |Select at least one security group for the NLB instance. |Default |

   4. Follow the console guidance to review and accept the Legal.

   5. Click **Buy now** to complete instance creation.

   6. Click **Go to console** to view the newly created instance.

#### (2) Create server group

   1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

   2. In the left navigation pane, select **Server group**.

   3. In the top menu bar, select the target project and region.

   4. In the left navigation pane, select **Server Group**.

   5. Click **Create server group**, and see the table below to configure the basic information of the server group.

      |Parameter |Explanation |Example |
      |---|---|---|
      |Name |Enter server group name |rsp01 |
      |Server Group Type |Select the type of the server group. **For backend servers across VPCs, you must choose the IP type.**  |**IP type** |
      |IP version |Protocol type for the backend server's private IP address. |IPv4 |
      |VPC |Select a server group in the same Virtual Private Cloud (VPC) as the NLB instance. |VPC\-A |
      |Backend protocol |The protocol used by the NLB instance to forward traffic to the backend server. |TCP |
      |Scheduling algorithm |Select the algorithm for forwarding requests to the backend server. |Weighted Round Robin (WRR) |
      |Session Persistence |Enable session persistence<br><br><br>* After the sticky session feature is enabled, the NLB forwards access requests from the same Source IP address to the same backend server for processing.<br><br>* **Session persistence timeout period** ranges from 1 to 3600 seconds. |Disable |
      |Connection Draining |Enable Connection Draining<br><br><br>* After enabling, when a backend server is deleted or a health check exception occurs, existing connections will transmit normally within the connection draining timeout period.<br><br>* **Timeout period of connection draining** ranges from 0 to 900 seconds. |Disable |
      |Client IP Preservation |Whether to enable client IP address preservation. Cannot be enabled when the server group type is set to IP type. |Do not enable |
      |Proxy\-Protocol |Enable the Proxy\-Protocol<br><br>After enabling, NLB instance forwards the Source IP address of the client to the server group through the Proxy\-Protocol protocol. The Proxy\-Protocol needs to be configured on the server. For detailed information on this feature, see [Obtaining client source IP through Proxy Protocol](https://docs.byteplus.com/en/docs/clb/Configuring-a-Layer-4-listener-to-obtain-the-client-source-IP-address). |Disable |
      |All\-port forwarding |When the service ports of all backend servers in the server group are the same as the listening port, you can enable all\-port forwarding.<br><br>When enabled, this server group only supports attaching listeners with all\-port forwarding enabled, and backend servers in the group do not need to specify ports. NLB forwards traffic to backend servers based on the front\-end request port (i.e., listening port) by default. |Disable |

   6. Configure health check information according to the table below.

      |Parameter |Explanation |Example |
      |---|---|---|
      |Health check |Select whether to enable the health check feature. After enabling health checks, NLB can check whether the backend server status is normal, stop forwarding requests to abnormal backend servers, and ensure overall service availability.<br><br>> **tip**<br><br><br><br>* > Disabling health checks may result in requests being forwarded to abnormal backend servers. To ensure continuous availability of the service, it is discouraged to disable health checks.<br><br><br>* > Health checks consume a certain amount of network resources. To minimize their impact on your business operations, it is advised to reduce the health check frequency and increase the interval between checks based on your specific workload.<br> |Check |
      |Health check protocol |The protocol type of the health check request. |TCP |
      |Health check port |Configure the port used for the health check. |Use backend server port |
      |Response timeout |Configure the waiting time for the health check response.<br><br><br>* If no valid response is received from the backend server within the response timeout period, the health check is considered abnormal.<br><br>* Value range: 1 to 60 seconds. Default timeout period: 3 seconds. |3 seconds |
      |Detect interval |Enter the interval for performing health checks.<br><br><br>* The detect interval must be greater than or equal to the response timeout period.<br><br>* Value range: 3 to 300 seconds. The default interval is 10 seconds, meaning a health check is performed on the backend server every 10 seconds. |10 seconds |
      |Healthy threshold |After enabling health checks, specify the number of consecutive successful health checks required to consider a backend server normal.<br><br><br>* When the same backend server undergoes consecutive health checks for a specified number of times and all results are **Normal**, its status changes from **Abnormal** to **Normal**.<br><br>* Value range: 2 to 10 times. Default: 3 times. |3 times |
      |Unhealthy threshold |After enabling health checks, enter the number of consecutive health check failures required to determine backend server failure.<br><br><br>* When the same backend server undergoes consecutive health checks for a specified number of times and all results are **Abnormal**, its status changes from **Normal** to **Abnormal**.<br><br>* Value range: 2 to 10 times. Default: 3 times. |3 times |

   7. Click **OK** to complete the action.

#### (3) Add backend server

   1. Click the name of server group rsp\-01.

   2. Click **Add server**.

   3. Configure relevant parameters based on the table below.

      |Parameter |Explanation |Value |
      |---|---|---|
      |IP Address |Input the private IP address of the cross\-VPC Elastic Compute Service (ECS). |192.168.1.10 |
      |Port |Type the port of cross\-VPC Elastic Compute Service (ECS). |80 |
      |Weight |Type the weight of the cross\-VPC Elastic Compute Service (ECS) instance. |100 |

   4. Click **Confirm** to complete the action.

#### (4) Add Listener

   1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

   2. In the top menu bar, select the target project and region.

   3. Click **Edit listener** on the right side of the target NLB instance.

   4. Click **Add listener** and see the table below to configure the listener.

      |Parameter |Explanation |Example |
      |---|---|---|
      |Listener name |Enter the listener name. If left blank, it defaults to **Protocol\-port**, such as **TCP\-80**. |listener01 |
      |Listening protocol |Select the protocol type for NLB instance listener. This article uses TCP. [Prerequisite](https://docs.byteplus.com/en/docs/clb/NLB-Listener-overview#.55uR5ZCs5Y2P6K6u57G75Z6L) |TCP |
      |Listening port |Enter the listening port. The range is 1 to 65535. |80 |
      |Timeout period |Set the timeout period. If no data is transferred over the connection within the timeout period, it will be automatically disabled.<br><br>For TCP listeners, the timeout period ranges from 10 to 900 seconds, with a default value of 900 seconds. |900 seconds |
      |Tags |A tag consists of a key\-value pair and is used for categorizing and searching resources [Learn more](https://docs.byteplus.com/en/docs/clb/NLB-Tag-Management). |* Tag key: listener\-key<br><br>* Tag value: listener\-test |

   5. Click **Next** and select a **Server group with TCP protocol**.

   6. Click **Next** to confirm the configuration information.

   7. Click **Confirm** to complete the action.

#### (5) Configure Network ACL and Security Group

> **tip**

> If the subnets hosting the NLB and backend servers are not associated with any network ACL, no network ACL configuration is required for the NLB or backend servers.

   * **Security Groups and Network ACLs associated with the NLB instance**

      * Security Group configuration example:

         |Rule direction |Priority |Strategy |Protocol type |Port range |Source/destination address |Description |
         |---|---|---|---|---|---|---|
         |Inbound |1 |Allow |Listening protocol: TCP |Listening port: 80 |Client address: 0.0.0.0/0 |Allow inbound client traffic to the NLB |
         ||1 |Allow |ICMP |ALL |100.64.0.0/10 |Allow traffic to detect the availability of the NLB instance private IPv4 address |
         ||1 |Deny |TCP |80 |Access to the NLB's IP address is not allowed |Deny specified IP addresses from accessing the NLB |
         |Outbound |100 |Allow |ALL |ALL |0.0.0.0/0 |Allow\-all fallback policy |

      * Network ACL Configuration Example (NOTE: If no network ACLs are associated with the NLB's subnets, this configuration is unnecessary and may be ignored):

         |Rule direction |Priority |Policy |Agreement |Source/destination address |Destination port |Description |
         |---|---|---|---|---|---|---|
         |Inbound |1 |Allow |Listening protocol (TCP) |0.0.0.0/0 |Listening port<br><br>(80) |Allow inbound client traffic to the NLB |
         ||2<br><br> |<br>Allow<br><br><br><br><br> |Listening protocol and health check protocol<br><br>(Both are TCP) |Backend server private IP address (192.168.1.10) |Backend server port and health check port (both port 80) |Allow health check response traffic from backend servers to the NLB, allow client\-originated response traffic from backend servers to the NLB |
         ||3 |Allow |ICMP |100.64.0.0/10 |ALL |Allow traffic for system probes to detect the availability of the NLB private IPv4 address |
         |Outbound |1 |Allow |ALL |0.0.0.0/0 |ALL |Allow all IPv4 traffic |

   * **Security Groups and Network ACLs associated with the backend servers**

      * Security Group configuration example:

         |Rule direction |Priority |Policy |Protocol type |Port range |Source |Description |
         |---|---|---|---|---|---|---|
         |Inbound |1 |Allow |Listening protocol and health check protocol<br><br>(both TCP) |Backend server port and health check port (both port 80) |CIDR block of the subnet where the NLB instance resides. (172.16.1.0/24, 172.16.2.0/24) |Allow both request forwarding traffic and health check traffic from NLB to backend servers |

      * Network ACL Configuration Example (NOTE: If no network ACLs are associated with the backend servers, this configuration is unnecessary and may be ignored)

         |Rule direction |Priority |Policy |Agreement |Source/destination address |Destination port |Description |
         |---|---|---|---|---|---|---|
         |Inbound<br><br> |1 |Allow<br><br> |Listening protocol and health check protocol<br><br>(both TCP) |Source address: CIDR blocks of the subnet where the NLB instance resides (172.16.1.0/24, 172.16.2.0/24) |Backend server port and health check port (both port 80) |Allow both request forwarding traffic and health check traffic from NLB to backend servers |
         |Outbound |1 |Allow |ALL |Destination: 0.0.0.0/0 |ALL |Allow all traffic |

      For more details, see [Configuring the NLB security groups and Network ACLs](https://docs.byteplus.com/en/docs/clb/Configuring-security-group-and-Network-ACL-for-NLB) and [Configuring the backend server security groups and Network ACLs](https://docs.byteplus.com/en/docs/clb/NLB-Configuring-backend-server-security-group-and-Network-ACL).

### Step 3: Resolve your custom domain name to the NLB domain name

BytePlus does not allow users to **Directly** use the default domain name provided by the NLB service for **Internet** access. If you need to provide services to the internet through an NLB instance, please use your own domain name and resolve it via CNAME to the NLB domain name. If you do not have your own domain, see [BytePlus Domain Names](https://docs.byteplus.com/en/docs/domain-names/introduction_en).

> Explanation

> This example uses configuring resolution records in BytePlus's DNS service. If you manage your business domain name on another platform, please configure resolution records on the corresponding platform.

1. Log in to the [DNS Console](https://console.byteplus.com/dns-suite/dns/publiczone/zones?).

2. See [Map Your Domain Name to a CDN CNAME](https://docs.byteplus.com/en/docs/byteplus-dns-suite/Map_Your_Domain_Name_to_a_CDN_CNAME) to resolve your own domain name to the NLB instance's domain and verify if the configuration takes effect. The parameter description is shown in the table below.

   |Parameter |Description |
   |---|---|
   |Domain name |Set it to the host record (domain prefix) of your own domain name. For example: `www`. |
   |Record type |Set to **CNAME**. |
   |Record value |Set to the domain name of your NLB instance. In this example: `nlb-2fe5ahfkoi9s059gp683y****.cn-beijing.nlb.volces.com`. |
   |> **tip**<br><br><br>> For parameters not mentioned above, please keep the default values.<br> ||

## Verification

1. Open the browser on your local computer.

2. Input `http://<your custom domain name>:80`, if the application page deployed by the backend server is displayed, it indicates that your business has successfully configured the NLB.
