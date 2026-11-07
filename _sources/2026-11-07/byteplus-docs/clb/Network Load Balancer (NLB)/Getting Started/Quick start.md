---
title: "Quick start"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Quick-start"
---

This topic introduces data planning and resource preparation before configuring Network Load Balancer (NLB), as well as the configuration process.

## Data planning

### Region and AZ

Select the Region and availability zone based on the geographical location of the actual business.

* Region: It is recommended to select a region as close as possible to the geographical location of the client to reduce latency and improve download speed.

* Availability Zone: NLB supports active\-active deployment across multiple availability zones by default. Select two or more availability zones within the same region to deploy NLB and improve overall service availability.

### IP version

NLB supports instances with IPv4 and dual\-stack IP protocols. Choose according to the business requirements.

* When only IPv4 is involved, select the IPv4 type.

* When dealing with IPv6 services, regardless of whether IPv4 services are involved, always select Dual\-stack type.

### Plan network type

NLB supports two types: public and private network. See the table below for appropriate selection.

> **tip**

> IPv4 instances only require IPv4 network planning, while dual\-stack instances require both IPv4 and IPv6 network type planning.

|Network type ||Explanation |
|---|---|---|
|IPv4 Network Type |Internet |If you want IPv4 internet clients to access the NLB instance, it is recommended that you select the internet network.<br><br>At this point, you also need to confirm the creation type of Elastic IP (EIP):<br><br><br>* Newly purchased EIP: There is no need to apply for an EIP in advance; the system automatically synchronizes and applies for an EIP when creating an NLB instance. The default configuration of the EIP is as follows:<br><br>   * Bandwidth limit: 200Mbps<br><br>   * ISP: BGP (Multi\-ISP)<br><br>   * Billing method: Pay\-by\-data\-transfer<br><br>   * Security protection level: Default (basic protection)<br><br>* Using existing EIP: You need to plan the bandwidth cap and type information (including ISP, billing methods, and security protection type) in advance and apply for EIP. The type of all EIPs associated with a single NLB instance must be consistent. |
||Private |If you do not want IPv4 internet clients to access the NLB instance, it is recommended that you select the private network. |
|IPv6 network type |Internet |If you want IPv6 internet clients to access the NLB instance, we recommend selecting the internet type.<br><br>> **tip**<br><br><br>> Since creating dual\-stack instances of the IPv6 internet type is not supported directly, you need to convert the IPv6 network type to internet after the NLB instance is created.<br> |
||Private |If you do not want IPv6 Internet clients to access NLB instances, it is recommended to select the private network. |

### Plan protocol type

NLB supports TCP, UDP and TLS protocol listeners. Choose according to your scenario.

|Listening protocol |Explanation |Application scenarios |
|---|---|---|
|TCP |TCP is a connection\-oriented protocol that requires establishing a connection via three\-way handshake to ensure reliability before data transmission. Once data transfer is complete, the connection must be terminated. |Applicable to scenarios that prioritize reliability and data accuracy, such as file transfers, email communications, remote logins, and web applications. |
|UDP |UDP is a connectionless protocol that does not require establishing a connection. The sender can directly transmit the datagram to the receiver, and the receiver also does not need to send an acknowledge back to the sender. |Applicable to scenarios that require real\-time performance, such as voice and video chat, online gaming, and real\-time financial updates. |
|TLS |On the foundation of a TCP connection, TLS utilizes certificates and security policies to establish a secure connection between the client and the server, encrypting and authenticating data in transit. |Applicable for scenarios under the TCP protocol with very high security requirements, such as large\-scale TLS offloading scenarios. |

### Planning instance Identity and Access Management (IAM)

Traffic entering the NLB instance is restricted by the security group associated with the NLB instance and the network ACL associated with the subnet of the NLB instance. You need to see Configurating instance access control to plan the outbound and inbound direction rules of the security group and Network ACL, so as to allow Client access traffic and Traffic verifying the availability of the NLB private IP address.

## Resource preparation

### Prepare the private cloud network environment

Create a Virtual Private Cloud (VPC) that meets business needs to provide a private network environment for the NLB.

* See Creating an IPv4 VPC to create a private network that supports only IPv4.

* See Creating an IPv6 VPC to create a private network that supports both IPv4 and IPv6.

### Prepare backend servers

NLB supports three types of backend servers: Elastic Compute Service (ECS) instances, secondary network interfaces, and IP addresses. Please see the table below to select as needed.

|Backend server types |Application scenarios |Configuration actions |Access Control Policy Configuration Instructions |
|---|---|---|---|
|ECS instance |Used for adding backend servers within the same VPC to the NLB. |Create an ECS instance and deploy services for external access. For specific operations, see Purchasing an ECS and Setting up backend services. |Ensure that the security groups associated with the ECS instance and the Network ACL of the subnet to which the Cloud Service instance belongs have allowed Client access traffic and NLB health check traffic. For detailed configuration, please see Configuring Backend Server Access Control. |
|Secondary network interface (associated with an ECS instance) |Used to add backend servers within the same VPC to the NLB. By switching the associated ECS instance, you can flexibly adjust which servers receive and process NLB traffic. |Create a secondary network interface and mount it to an ECS instance. For detailed steps, see Creating a secondary network interface and Mounting a secondary network interface. |In addition to the access control policy configuration of the above ECS instance, routing also needs to be configured for the secondary network interface. For detailed configuration, please see Configuring Secondary Network Interface Routing. |
|IP Address |Mainly used to add backend servers across VPCs for NLB, and can also add backend servers within the same VPC. The address can be a private IP address of an ECS within this VPC or another VPC, or an IP address of a server in an on\-premises data center (IDC). |* When the IP address belongs to an ECS instance or secondary network interface within the VPC, see Buying ECS instance and Configuring secondary network interface to complete resource creation and obtain the resource's IP address.<br><br>* When the IP address belongs to an on\-premises IDC server, please obtain the server's IP address in advance. |* When the IP address belongs to an ECS instance or a secondary network interface within the VPC, ensure that the access control policies for the ECS instance or secondary network interface meet configuration requirements.<br><br>* When the IP address is from a server in an on\-premises IDC, ensure that the server's access control policy allows Client traffic and NLB health check traffic. For detailed configuration, please see Configuring backend server access control. |

## Configuration procedures

**IPv4 NLB**

1. Create an NLB instance: Create an IPv4\-type internet NLB instance.

2. Create a Server Group and Add backend servers: Create an IPv4\-type server group and add backend servers that provide actual services.

3. Add a listener: Add a listener to the NLB instance and associate it with the server group.

4. Configure the Security group and Network ACL: Allow the NLB traffic in the security group and Network ACL associated with the NLB instance and backend servers.

5. [Point own domain to NLB domain](https://docs.byteplus.com/en/docs/clb/Setting-up-an-IPv4-NLB#YAJjurNK): Configure a CNAME record to parse the actual business domain to the NLB domain.

6. Verification: Verify that the configured NLB can forward access requests to backend servers properly.

**IPv6 NLB**

1. Create an NLB instance: Create a private NLB instance with dual\-stack support.

2. CreateIPv4Server Group and Add backend servers: Create an IPv4\-type server group and add backend servers that provide actual services.

3. Add a listener: Add a listener to the NLB instance and associate it with the server group.

4. Activate IPv6 Internet bandwidth: If IPv6 Internet services are needed, change the NLB instance's IPv6 network type into internet.

5. Configure the Security group and Network ACL: Allow the NLB traffic in the security group and Network ACL associated with the NLB instance and backend servers.

6. [Resolve custom domain to NLB domain](https://docs.byteplus.com/en/docs/clb/Setting-up-an-IPv6-NLB#vaEfbm8a): Configure a CNAME record from the actual business domain to the NLB domain.

7. Verification: Verify that the configured NLB can forward access requests to backend servers properly.
