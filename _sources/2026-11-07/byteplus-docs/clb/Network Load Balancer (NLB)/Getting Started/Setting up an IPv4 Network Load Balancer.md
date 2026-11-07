---
title: "Setting up an IPv4 Network Load Balancer"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Setting-up-an-IPv4-NLB"
---

## Scenarios

This article explains how to quickly configure an IPv4 internet type Network Load Balancer with basic service capabilities. After configuration is completed, the NLB instance listens to requests from TCP port 80, and the ECS instances in the server group provide services through TCP port 80.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1c2139e8762418612365b2ad1425e99d.png)

## Prerequisites

* Users have their custom domain name.

* Data planning and resource preparation have been completed following Quick start.

## Configuration procedures

> **tip**

> The following steps only describe parameters required for this configuration. Keep other parameters at their default values. For more information about parameters, see [User Guide](https://docs.byteplus.com/en/docs/clb/Creating-an-NLB-instance).

### Step 1: Create an NLB instance

1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

   > **tip**

   > During initial login, follow the on\-screen instruction to complete cross\-service role authorization.

2. Click **Create NLB**, and configure related parameters according to the table below.

   |Parameter |Explanation |Example |
   |---|---|---|
   |**Basic information** |||
   |Regions |Select the Region where the NLB instance resides.<br><br>After you select a region, the created NLB instance can only be used by resources in the selected region and cannot be migrated. You must confirm that the region of the instance is the same as that of the backend server instance. |China (Guangzhou) |
   |Name |Type the name of NLB instance. |nlb01 |
   |**Network Configuration** |||
   |IP version |Select the private IP address type of the NLB instance.<br><br><br>* IPv4: Only IPv4 is supported.<br><br>* Dual\-stack: Both IPv4 and IPv6 are supported.<br><br><br>> **tip**<br><br><br>> NLB IPv6 feature is currently in Beta testing. For trial requests, please contact the account manager.<br> |IPv4 |
   |Network Type (IPv4) |Select the network type for the NLB instance's IPv4 address. The two network types can be interchanged. For detailed information, see [Changing IPv4 network type](https://docs.byteplus.com/en/docs/clb/Changing-Network-Load-Balancer-instance-network-type).<br><br><br>* **Public**: The NLB instance can be accessed by both the IPv4 private network and the IPv4 internet.<br><br>* **Private**: This NLB instance can only be accessed by the IPv4 private network. |Internet |
   |VPC |Select the Virtual Private Cloud (VPC) to which the NLB instance belongs. |VPC\-X |
   |AZs and Subnets |Select the supported Availability Zone for the NLB instance, and specify the subnet, IP address, and Elastic IP (EIP) for each availability zone.<br><br>NLB supports multi\-AZ active\-active disaster recovery by default, and please select at least 2 availability zones. If higher business reliability is required, you may optionally choose 2 or more availability zones.<br><br><br>* Subnet: Provides a private network deployment environment for the NLB instance. The system automatically creates a network interface within the subnet and attaches it to the NLB.<br><br>* IPv4 address: Select the allocation method for the IPv4 address of the NLB instance. After the instance is created, all assigned IPv4 addresses cannot be modified.<br><br>* EIP: Provides internet capabilities for the NLB instance. Configure this parameter only when the network type (IPv4) is **Internet**. |* Availability zone A<br><br>   * Subnet\-A \| 192.168.1.0/24<br><br>   * Automatic IP assignment<br><br>   * New Elastic IP (EIP)<br><br>* Availability Zone B<br><br>   * Subnet\-B \| 192.168.2.0/24<br><br>   * Automatic IP assignment<br><br>   * New Elastic IP (EIP) |
   |Security group |Select at least one security group for the NLB instance.<br><br><br>* In addition to the specified security group, the NLB instance will be automatically associated with an entrusted security group. After the instance is successfully created, you can view the detailed information of the security group on the instance details page.<br><br>* The specified security group and the entrusted security group are jointly used for controlling inbound and outbound traffic of the NLB instance. |default |

3. In the **Configuration Details** window on the right side of the page, check and confirm the Legal as guided by the console.

4. Click **Submit order** to complete the instance creation.

5. Click **Go to console** to view and record the domain name of the newly created NLB instance.

### Step 2: Create server groups and add backend servers

1. In the left\-side navigation pane, select Server Group.

2. Click Create Server Group and configure basic information and health check information by referring to the table below.

   * Basic information

      |Parameter |Explanation |Example |
      |---|---|---|
      |Name |Enter server group name |rsp01 |
      |Server Group Type |Select the type of the server group.<br><br><br>* Server Type: Only the Elastic Compute Service (ECS) instances or secondary network interfaces within the same VPC as the server group can be added as backend servers.<br><br>* IP Type: You can only add IP addresses as backend servers. You can add IP addresses from other VPCs or on\-premises IDCs as backend servers, as long as they are network\-reachable. |Server type |
      |IP version |Protocol type for the backend server's private IP address.<br><br><br>* IPv4: only IPv4 backend servers are supported.<br><br>* IPv6: only IPv6 backend servers are supported. IPv6 is only supported when the NLB instance is dual\-stack and the backend server group uses Server\-type targets.<br><br><br>> **tip**<br><br><br><br>* > When IPv6 access requests are forwarded to IPv4 backend servers, the IPv6 will first be converted to IPv4, and then forwarded to the IPv4 backend servers.<br><br><br>* > When forwarding IPv4 access requests to an IPv6 backend server, IPv4 is first converted to IPv6 and then forwarded to the IPv6 backend server.<br> |IPv4 |
      |VPC |Select a server group in the same Virtual Private Cloud (VPC) as the NLB instance. |VPC\-X |
      |Backend protocol |The protocol used by the NLB instance to forward requests to the backend server.<br><br><br>* Applicable to scenarios that require high reliability and high data accuracy, and have relatively low speed requirements, such as file transmissions, email communications, and remote log\-ins.<br><br>* Applicable to scenarios that require real\-time performance and have relatively low requirements for reliability, such as video chatting and real\-time push of financial market updates. |TCP |
      |Scheduling algorithm |Select the rules that the server group follows to forward requests.<br><br><br>* Weighted Round Robin (WRR): In this case, higher weights values receive more frequent polling attempts (higher probability).<br><br>* Weighted Least Connection (WLC): First calculate the current connections/weight value of the backend server, then dispatch the request to the backend server with the smallest value.<br><br>* Source hashing (SH): A consistency hash based on the Source IP address, allowing the same source to be scheduled to the same backend server. |Weighted Round Robin (WRR) |

   * Health check information

      |Parameter |Explanation |Example |
      |---|---|---|
      |Health check |Health Check Switch When enabled, the NLB can automatically isolate abnormal backend servers to eliminate single points of failure.<br><br>> **warning**<br><br><br><br>* > Disabling health checks may result in requests being forwarded to abnormal backend servers. To ensure continuous availability of the service, it is discouraged to disable health checks.<br><br><br>* > Health checks consume a certain amount of network resources. It is recommended to minimize the impact on the service by increasing detect intervals, lowering the healthy threshold and unhealthy threshold according to the business situation.<br> |Check |
      |Health check protocol |The protocol type of the health check request.<br><br><br>* TCP: Sends SYN handshake packets to detect whether the backend server port status is normal. [Prerequisite](https://docs.byteplus.com/en/docs/clb/NLB-Health-check-overview)<br><br>* HTTP: Sends HEAD or GET requests to simulate browsing behavior, thereby detecting whether the backend server application is functioning normally. [Prerequisite](https://docs.byteplus.com/en/docs/clb/NLB-Health-check-overview) |TCP |
      |Health check port |Port used for health check. |Use backend server port |
      |Response timeout |Time to wait for a health check response. The timeout is 3 seconds by default and ranges from 1 to 60 seconds. If no valid response is received from the backend server within the response timeout period, the health check is considered abnormal. |3 seconds |
      |Detect interval |The time interval for performing health checks. The default interval is 10 seconds, meaning a health check is performed on the backend server every 10 seconds. Value range: 1 to 300 seconds.<br><br>> **warning**<br><br><br>> The detect interval must be greater than or equal to the response timeout period.<br> |10 seconds |
      |Healthy threshold |Number of health checks to determine that the backend server is normal. The value ranges from 2 to 10 times. The default is 3, meaning 3 consecutive health checks are conducted on the same backend server, and if all results are normal, the backend server is marked as normal. |3 times |
      |Unhealthy threshold |Number of health checks to determine that the backend server is abnormal. The value ranges from 2 to 10 times. The default is 3, meaning 3 consecutive health checks are conducted on the same backend server, and if all results are abnormal, the backend server is marked as abnormal. |3 times |

3. Click **Create** to complete the creation of the server group.

4. Click  **··· \> Add Server** on the right side of the target server group.

5. Click **Add Server** and select the target Elastic Compute Service (ECS) instance.

6. Click **Next** to configure ports and weights for the added backend servers.

   * When the same server provides external services on different ports, click the Add Port button on the right side of the target server and add the required ports one by one.

   * If different servers use the same port to provide external services, select the target server, then click the Modify Port button above the list to set for ports in batch.

      |Parameter |Explanation |Example |
      |---|---|---|
      |Port |The port where the backend server provides services. |80 |
      |Weight |The probability of the backend server receiving a request (probability = the server weight / the sum of all servers' weights in the group).<br><br><br>* The higher the weight, the more requests are forwarded; default is 100.<br><br>* Setting the weight to 0 means the server will no longer accept new requests.<br><br>* If the scheduling algorithm is Source IP Hash (SH), weights only distinguish between 0 and non\-zero values. |100 |

7. Click **Migrate** to complete the action.

### Step 3: Add listener

1. In the left\-side navigation pane, select **Instances**.

2. Click **Configure Listener** on the right side of the target NLB instance.

3. Click **Add Listener** and refer to the table below to configure relevant parameters.

   |Parameter |Explanation |Example |
   |---|---|---|
   |Listener name |Enter the listener name. If left blank, it defaults to **Protocol\-port**, such as TCP\-80. |listener01 |
   |Listening protocol |Select the protocol type for NLB instance listener. [Prerequisite](https://docs.byteplus.com/en/docs/clb/NLB-Listener-overview#.55uR5ZCs5Y2P6K6u57G75Z6L) |TCP |
   |Listening port |Select the port type and type the port. The port value ranges from 1 to 65535. [Prerequisite](https://docs.byteplus.com/en/docs/clb/NLB-Listener-overview) |80 |
   |Timeout period |Set the timeout period. If no data is transferred over the connection within the timeout period, it will be automatically disabled. The value ranges from 10 to 900 seconds, with a default of 900 seconds. |900 seconds |

4. Click **Next**, then select the server group created above.

5. Click **Next** to confirm the configuration information.

6. Click **Migrate** to complete the action.

### Step 4: Configure security group and Network Access Control List

* **Security Groups and Network ACLs associated with the NLB instance**

   * Security Group configuration example:

      |Rule direction |Priority |Strategy |Protocol type |Port range |Source/destination address |Description |
      |---|---|---|---|---|---|---|
      |Inbound |1 |Allow |Listening protocol: TCP |Listening port: 80 |Client address: 0.0.0.0/0 |Allow inbound client traffic to the NLB |
      ||1 |Allow |ICMP |ALL |100.64.0.0/10 |Allow traffic to detect the availability of the NLB instance private IPv4 address |
      ||1 |Deny |TCP |80 |Access to the NLB's IP address is not allowed |Deny specified IP addresses from accessing the NLB |
      |Outbound |100 |Allow |ALL |ALL |0.0.0.0/0 |Allow\-all fallback policy |

   * Network ACL configuration example:

      |Rule direction |Priority |Strategy |Agreement |Source/destination address |Destination port |Description |
      |---|---|---|---|---|---|---|
      |Inbound |1 |Allow |Listening protocol (TCP) |0.0.0.0/0 |Listening port<br><br>(80) |Allow client access traffic |
      ||2<br><br> |<br>Allow<br><br><br><br><br> |Listening protocol and health check protocol<br><br>(All are TCP in this article) |Backend server private IP address |Backend server port and health check port (both 80 in this article) |Allow health check response traffic from backend servers to the NLB, allow client\-originated response traffic from backend servers to the NLB |
      ||3 |Allow |ICMP |100.64.0.0/10 |ALL |Allow traffic for system probes to detect the availability of the NLB private IPv4 address |
      |Outbound |1 |Allow |ALL |0.0.0.0/0 |ALL |Allow all IPv4 traffic |

* **Security Groups and Network ACLs associated with the backend servers**

   * Security Group configuration example:

      If [Passed backend security group](https://docs.byteplus.com/en/docs/clb/NLB-Allowing-backend-security-group) is enabled, backend security groups do not require configuration; if not enabled, backend security groups must be configured.

      |Rule direction |Priority |Strategy |Protocol type |Port range |Source |Description |
      |---|---|---|---|---|---|---|
      |Inbound |1 |Allow |Listening protocol and health check protocol<br><br>(All are TCP in this document) |Backend server port and health check port (both port 80) |CIDR block of the subnet where the NLB instance resides. |Allow both request forwarding traffic and health check traffic from NLB to backend servers |

   * Network ACL configuration example:

      |Rule direction |Priority |Strategy |Agreement |Source/destination address |Destination port |Description |
      |---|---|---|---|---|---|---|
      |Inbound<br><br> |1 |Allow<br><br> |Listening protocol and health check protocol<br><br>(All are TCP in this document) |Source address: CIDR block of the subnet where the NLB instance resides. |Backend server port and health check port<br><br>(both port 80) |Allow both request forwarding traffic and health check traffic from NLB to backend servers |
      |Outbound |1 |Allow |ALL |Destination: 0.0.0.0/0 |ALL |Allow all traffic |

   For more details, see [Configuring NLB security groups and Network ACLs](https://docs.byteplus.com/en/docs/clb/Configuring-security-group-and-Network-ACL-for-NLB) and [Configuring backend server security groups and Network ACLs](https://docs.byteplus.com/en/docs/clb/NLB-Configuring-backend-server-security-group-and-Network-ACL).

### **Step 5: Resolve custom domain names to NLB domain names**

BytePlus does not allow users to **Directly** use the default domain name provided by the NLB service for **Internet** access. If you need to provide services to the internet through an NLB instance, please use your own domain name and resolve it via CNAME to the NLB domain name. If you do not have your own domain name, please refer to [BytePlus Domain Names](https://docs.byteplus.com/en/docs/domain-names/introduction_en).

> Explanation

> This example uses configuring resolution records in BytePlus's DNS service. If you manage your business domain name on another platform, please configure resolution records on the corresponding platform.

1. Log in to the [DNS Console](https://console.byteplus.com/dns-suite/dns/publiczone/zones).

2. Refer to [Map Your Domain Name to a CDN CNAME](https://docs.byteplus.com/en/docs/byteplus-dns-suite/Map_Your_Domain_Name_to_a_CDN_CNAME) to resolve your own domain name to the NLB instance domain name and verify if the configuration takes effect. The parameter description is shown in the table below.

   |Parameter |Description |
   |---|---|
   |Domain name |Set it to the host record (domain prefix) of your own domain name. For example: `www.example.com`. |
   |Record type |Set to **CNAME**. |
   |Record value |Set to the domain name of the NLB instance, in this document as `nlb-2fe5af0pxlvy859gp68ag.cn-guangzhou.nlb.volces.com`. |
   |> **tip**<br><br><br>> For parameters not mentioned above, please keep the default values.<br> ||

## Verification

1. Open the browser on your local computer.

2. Input `http://your custom domain name`, if the application page deployed by the backend server is displayed, it indicates that your business has successfully configured the NLB.
