---
title: "Creating IPv4/IPv6 dual-stack clusters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Deploying-an-IPv4_IPv6-dual-stack-cluster-using-VKE"
---

VKE provides support for IPv6 networks by using the IPv4/IPv6 dual\-stack solution, which enables you to use IPv6 addresses in Kubernetes clusters. This topic describes how to create an IPv4/IPv6 dual\-stack cluster.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta \- apply for trial</strong></a>]: The IPv4/IPv6 dual\-stack cluster feature is currently in beta stage. To use this feature, submit an application.</div>


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

With the development of the Internet, IPv4 addresses have gradually become exhausted. As the next\-generation Internet protocol, IPv6 offers a larger address space and enhanced security. To meet your requirements for IPv6, dual\-stack transition is the optimal solution.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The IPv4/IPv6 dual\-stack feature is currently in beta for all related services, such as VPC (required), CLB (required), ALB, and VCI. Make sure that IPv4/IPv6 allowlist permissions have been granted for all dependent resources to the current account in your scenario. If usage permissions on dependent resources are not granted, submit an application or contact your designated service contacts.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits


* Only the clusters running on Kubernetes v1.24.10\-vke.6 or later support the IPv4/IPv6 dual\-stack feature.

* Only the clusters using the VPC\-CNI container network model support the IPv4/IPv6 dual\-stack feature.

* In an IPv4/IPv6 dual\-stack cluster, only the nodes with IPv6 addresses can be added. Similarly, only these nodes can be included in the node pools you created.

* VPC and CLB mentioned in the prerequisites are strong dependencies for creating a dual\-stack cluster. Make sure that usage permissions on these resources are granted. Grant usage permissions on other resources based on your business requirements.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Yib5bu6LWlwdjQtaXB2Ni3lj4zmoIjnp4HmnInnvZHnu5zlj4rlrZDnvZE="></span>
### Step 1: Create an IPv4/IPv6 dual\-stack VPC and subnet

After you have completed the preceding preparations, perform the following steps to create an IPv4/IPv6 dual\-stack VPC and subnet for creating a dual\-stack cluster.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information about IPv6 VPCs, see <a href="https://docs.byteplus.com/en/docs/vpc/Building-an-IPv6-VPC">Creating IPv6 VPCs</a>.</div>



1. Log in to [VPC console](https://console.byteplus.com/vpc).

2. In the left navigation bar of the VPC console, click **VPC**.

3. On the VPC page, click **Create VPC** in the upper\-left corner. On the page that appears, specify related parameters.   

   * In the **CIDR block** section, select the **IPv6 CIDR** parameter to enable the IPv6 feature for this VPC.

   * In the **Subnet** section, configure the **IPv6 CIDR** blocks for different subnets.

5. Click **Confirm**.


<span id=".5q2l6aqk5LqM77ya5Yib5bu6LWlwdjQtaXB2Ni3lj4zmoIjpm4bnvqQ="></span>
### Step 2: Create an IPv4/IPv6 dual\-stack cluster

After the IPv4/IPv6 dual\-stack VPC and subnet are created, perform the following steps to create an IPv4/IPv6 dual\-stack cluster.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click **Create cluster** in the upper\-left corner.

4. In the **Create cluster** dialog box, go to the **Custom managed clusters** section and click **Create now**.

5. On the **Create cluster** page, follow the wizard to configure the cluster.   

   * Select **IPv6 dual stack** for the **IP version** parameter.

   * Select a VPC with IPv4/IPv6 dual\-stack enabled for the **VPC** parameter.

   * Select subnets with IPv4/IPv6 dual\-stack enabled for the **Pod subnets** parameter.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This scenario provides IPv6\-related configuration details. For other parameters, see <a href="https://docs.byteplus.com/en/docs/vke/Creating-a-cluster">Creating managed clusters</a>.   </div>
   

6. Complete other cluster parameter configurations and create the cluster.


<span id="rm94OUpi"></span>
### Step 3: (Optional) Enable IPv6 public bandwidth

After an IPv4/IPv6 dual\-stack cluster is created, both the nodes and pods within the cluster will be assigned IPv6 addresses from the VPC. However, these addresses can only be used for private network access. If nodes or pods need to access the Internet via IPv6, you need to enable the IPv6 Internet bandwidth feature for the corresponding network interface in the IPv6 gateway instance.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Please ensure that your private networks and subnets are bound to an IPv6 gateway. For details, see <a href="https://docs.byteplus.com/en/docs/IPv6/Enable_IPv6_for_private_networks">Enabling IPv6 for VPCs</a>. If you cannot access the IPv6 gateway console, please contact your account manager.</div>


* <div data-tips="true" data-tips-type="warning">This part describes how to enable the IPv6 Internet bandwidth feature for cluster nodes, enabling them to access the public network via IPv6 addresses. To configure the IPv6 Internet bandwidth feature for pods, see <a href="https://docs.byteplus.com/en/docs/vke/Configuring_IPv6_public_bandwidth_for_pods">Configure IPv6 Internet bandwidth for pods</a>.</div>


1. Log in to the [IPv6 Gateway](https://console.byteplus.com/eip/ipv6s) console.

2. Click the IPv6 gateway name corresponding to the private network to enter the gateway details page.

3. Select the **IPv6 Internet bandwidth** tab and use the IPv6 address of the node to search.

4. Click **Enable Internet bandwidth** in the **Actions** column for the target IPv6 address. This enables the Internet bandwidth feature for the IPv6 address, allowing it to access the public network. For configuration details, see [Enabling IPv6 Internet bandwidth](https://docs.byteplus.com/en/docs/IPv6/Enable_IPv6_internet_bandwidth).


<span id="xzqdJLOQ"></span>
## Validating results

<span id="EigLgplV"></span>
### Viewing cluster information

‌Cluster creation typically takes 15\-20 minutes. Please wait patiently or check the cluster list for real\-time status updates.

<span id="obeUOpCD"></span>
### Validating IPv6 Internet access 


1. Use **ECS Terminal** to log in to the node. For details, see [ECS Terminal](https://docs.byteplus.com/en/docs/vke/Managing-nodes#ecs-terminal).

2. Execute the following command to validate connectivity.

   ```Bash
   ping6 ipv6.baidu.com
   ```
   

   The information below is what will be printed on the screen.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7e3ee2f8e902daef887a3c218a27a387.png) </span>
