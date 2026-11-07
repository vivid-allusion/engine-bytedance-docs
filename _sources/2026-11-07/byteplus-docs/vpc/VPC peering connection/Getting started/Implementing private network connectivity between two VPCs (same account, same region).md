---
title: "Implementing private network connectivity between two VPCs (same account, same region)"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Implementing-private-nnetwork-connectivity-same-account-same-region"
---

This topic explains how to use Peering Connection to establish private network connectivity between same account, same region Virtual Private Cloud (VPC) instances.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b8cd579ece06651cafd05d97878349cc.png) </span>

<span id="J8EpePFB"></span>
## Preparations

For demonstration purposes, this topic uses the scenario shown in the diagram above. Before you begin, complete the following preparatory steps:


1. Register account A and complete real name verification.

2. Recharge account.

3. In China (Beijing) region, [Create 2 VPCs with their subnets](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) and [Create 2 ECSs](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances). The required information is as follows:

   * VPC\-A (172.16.0.0/16), subnet\-A (172.16.1.0/24), ECS\-A (172.16.1.11).

   * VPC\-B (192.168.0.0/16), subnet\-B (192.168.1.0/24), ECS\-B (192.168.1.22).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The CIDR blocks of the two VPCs to be interconnected must not overlap.</div>


<span id="GBdwsFGQ"></span>
## Procedures

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The following text only describes the required parameters and their values; for other parameters not mentioned, please keep the default configuration.</div>


<span id="xmPDwJ2R"></span>
### Step 1: Create peering connection


1. Log in to the [Peering Connection console](https://console.byteplus.com/vpc/region:vpc+cn-beijing/peerConnection).

2. In the top menu bar, select the target region and project.

3. Click **Create peering connection**.

4. Configure parameters based on the table below.

   
   |Parameters |Notes |Sample value |
   |---|---|---|
   |Name |Enter the name of peering connection instance. |Peering Connection\-X |
   |Requester VPC instance |Select the requester VPC. |VPC\-A |
   |Acceptor account type |Select the acceptor account type. This topic selects **Same account**. |Same account |
   |Acceptor region type |Select the acceptor region type. This topic selects **Same region**. |Same region |
   |Acceptor VPC instance |Select the acceptor VPC. |VPC\-B |
   

5. Click **Create** to complete the action.


<span id="pMqFoqSD"></span>
### Step 2: Receive peering connection

Peering connection is accepted by default within the same account.

<span id="D0H0vasS"></span>
### Step 3: Configure requester VPC routing, security group, and network ACL

 **(1) Configure requester VPC route**


   1. Click **Configure route** under the **Requester column** of the target peering connection.

   2. Configure parameters based on the table below.

      
      |Parameters |Notes |Sample value |
      |---|---|---|
      |Route entry name |Enter the name of the requester route entry. |Requester route |
      |Requester route table |Select the requester route table. |VPC\-A route table |
      |Destination CIDR |Set the destination CIDR block for traffic routing. This topic selects CIDR block of VPC\-B. |192.168.0.0/16 |
      |Next Hop |The name of the peering connection is fixed. |Peering Connection\-X |
      

   3. Click **Save** to complete configuration.


 **(2) Configure security group and network ACL**


For the requester VPC, the security groups associated with the ECS instances and the network ACLs associated with the subnets that need to communicate with the acceptor VPC are as follows:

   * Security Group configuration example:

      1. Log in to the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance).

      2. Click the ECS name to enter the details page.

      3. On the Security Group tab, click **Configure**.

      4. On the **Inbound rule** or **Outbound rule** tab. Click **Add rule**, then configure the security group rules as shown in the example below.

         
         |Rule direction |Priority |Policy |Protocol type |Destination port |Source/destination address |Description |
         |---|---|---|---|---|---|---|
         |Inbound |100 |Allow |ALL |ALL |Source address: 192.168.1.0/24 |Allow access traffic from VPC\-B to enter VPC\-A |
         |Outbound |100 |Allow |ALL |ALL |Destination address: 192.168.1.0/24 |Allow access traffic from VPC\-B to exit VPC\-A |
         

      5. Click **Add** to complete the action.

   * Network ACL configuration example:

      1. Log in to the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance).

      2. Click the ECS name to enter the details page.

      3. Click the subnet name to enter the details page.

      4. Click the network ACL name to enter the details page.

      5. On the inbound rule or outbound rule tab, click **Edit inbound rule** or **Edit outbound rule**. Configure the network ACL rules as shown in the example below.

         
         |Direction |Priority |Policy |Protocol type |Destination port |Source/destination address | |
         |---|---|---|---|---|---|---|
         |Inbound |Set priority (e.g. 1) |Allow |ALL |ALL |Source address: 192.168.1.0/24 |Allow traffic from VPC\-B to enter VPC\-A |
         |Outbound |Set priority (e.g. 1) |Allow |ALL |ALL |Destination address: 192.168.1.0/24 |Allow traffic destined for VPC\-B to exit VPC\-A |
         

      6. Click **Save** to complete the action.


<span id="htMvr91k"></span>
### Step 4: Configure acceptor VPC routing, security group, and network ACL

 **(1) Configure acceptor VPC route**


   1. Click **Configure route** under the **Acceptor** column of the target peering connection.

   2. Configure parameters based on the table below.

      
      |Parameters |Notes |Sample value |
      |---|---|---|
      |Route entry name |Enter the name of the acceptor route entry. |Requester route |
      |Acceptor route table |Select the acceptor route table. |VPC\-A route table |
      |Destination CIDR |Set the destination CIDR block for traffic routing. This topic selects CIDR block of VPC\-A. |172.16.0.0/16 |
      |Next Hop |The name of the peering connection is fixed. |Peering Connection\-X |
      

   3. Click **Save** to complete configuration.


 **(2) Configure security group and network ACL**


Security groups and network ACLs of resources in the acceptor VPC that need to communicate with the requester VPC:

   * Security Group configuration example:Security Group

      1. Log in to the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance).

      2. Click the ECS name to enter the details page.

      3. On the Security Group tab, click **Configure**.

      4. On the **Inbound rule** or **Outbound rule** tab. Click **Add rule**, then configure the security group rules as shown in the example below.

         
         |Rule direction |Priority |Policy |Protocol type |Destination port |Source/destination address |Description |
         |---|---|---|---|---|---|---|
         |Inbound |100 |Allow |ALL |ALL |Source address: 172.16.0.0/16 |Allow access traffic from VPC\-A to enter VPC\-B |
         |Outbound |100 |Allow |ALL |ALL |Destination address: 172.16.0.0/16 |Allow access traffic from VPC\-A to exit VPC\-B |
         

      5. Click **Add** to complete the action.

   * Network ACL configuration example:

      1. Log in to the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance).

      2. Click the ECS name to enter the details page.

      3. Click the subnet name to enter the details page.

      4. Click the network ACL name to enter the details page.

      5. On the inbound rule or outbound rule tab, click **Edit inbound rule** or **Edit outbound rule**. Configure the network ACL rules as shown in the example below.

         
         |Direction |Priority |Policy |Protocol type |Destination port |Source/destination address |Description |
         |---|---|---|---|---|---|---|
         |Inbound |Set priority (e.g. 1) |Allow |ALL |ALL |Source address: 192.168.0.0/16 |Allow traffic from VPC\-A to enter VPC\-B |
         |Outbound |Set priority (e.g. 1) |Allow |ALL |ALL |Destination address: 192.168.0.0/16 |Allow traffic destined for VPC\-A to exit VPC\-B |
         

      6. Click **Save** to complete the action.


<span id="zg3sXPy2"></span>
## Verify


1. Remotely log in to ECS\-A.

2. In the command line, run `ping <IP address of ECS-B, for example 192.168.1.22 in this topic>` to test network connectivity.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_177a7daa6fc6a6a2276e68b3e28111d7.png) </span>

3. Similarly, verify that ECS\-B can access ECS\-A.
