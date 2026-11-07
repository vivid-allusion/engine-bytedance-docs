---
title: "How do I manually enable Public NAT for Internet endpoint for a cluster?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How-do-I-manually-enable-internet-facing-access-for-a-cluster"
---

Vital Kubernetes Engine (VKE) clusters allow you to access the public network by using Internet NAT Gateways in Virtual Private Clouds (VPC). To enable public access, you can enable or disable Public NAT for Internet endpoint when you create a cluster. You can also manually configure Internet NAT Gateways and SNAT rules for existing clusters for which Public NAT for Internet endpoint is not enabled. This topic describes how to manually enable Public NAT for internet endpoint for a cluster.

<span id="WAK4l3Ty"></span>
## Background information

VKE clusters allow you to access the public network by using Internet NAT Gateways in VPC in the following scenarios.


* Automatically create an Internet NAT Gateway: You can enable the **Public NAT for internet endpoint** feature when you create a cluster. The system will automatically create an Internet NAT Gateway in the VPC where the cluster is located and configure the corresponding SNAT rules. After the cluster is created, you can use the Internet NAT Gateway to access the public network. For specific configuration methods, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* Manually create an Internet NAT Gateway: If you do not enable the **Public NAT for internet endpoint** feature when you create a cluster, or need to use a custom Internet NAT Gateway to achieve public access for the cluster, you can manually create an Internet NAT Gateway and configure the corresponding SNAT rules after the cluster is created to achieve more flexible public access.


The following figure shows the basic principle of public access of a VKE cluster.

<span id="hz9ZQ7IR"></span>
## Prerequisites


* A cluster has been created, and **Public NAT for internet endpoint** is not enabled during cluster creation or is manually disabled.

* An EIP has been applied. For details, see [Applying for EIP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP).


<span id="GXl0c6Ey"></span>
## Procedure

<span id="JH9ipLMO"></span>
### Step 1: Create an Internet NAT Gateway


1. Log in to the [Internet NAT Gateway console](https://console.byteplus.com/nat).

2. Click **Create NAT Gateway** to create an Internet NAT Gateway for the cluster.   

   * Select the VPC where the VKE cluster is located for the **VPC** parameter.

   * In the **EIP Access Rule Configuration** section, select **Manual configuration** for the Configuration method parameter.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For more configuration details, see <a href="https://docs.byteplus.com/en/docs/natgateway/Creating-an-Internet-NAT-gateway">Creating Internet NAT Gateway</a>.   </div>
   

3. Click **Confirm order** to complete the configuration.


<span id="76DpyJX3"></span>
### Step 2: Configure an EIP


1. Find the target gateway in the gateway list, and click **Configure EIP** in the **Actions** column.

2. Click **Associate EIP**, and select an EIP in the panel that appears.

3. Click **Confirm**.


<span id="marpr4jH"></span>
### Step 3: Configure an SNAT rule


1. Find the target gateway in the gateway list, and click **Configure SNAT rule** in the **Actions** column.

2. Click **Create SNAT rule** to configure an SNAT rule for the NAT Gateway.

   * Select **VPC** or **Subnet** for the **Granularity** parameter. Configure the VPC where the cluster is located, or the subnet that needs to access the public network for the cluster.

   * Select the EIP bound to the NAT Gateway for the **EIP address** parameter.

3. Click **Confirm**.


<span id="ToxGagQ1"></span>
## Validating results

After you create an Internet NAT Gateway in the VPC where the cluster resides, bind an EIP, and configure an SNAT policy, the nodes and pods in the cluster can access the public network through this gateway. You can perform the following steps to check whether the feature takes effect:


1. Log in to the [VKE console](https://console.byteplus.com/vke). In the left navigation bar, click **Cluster**.

2. Click the name of the target cluster. In the left navigation bar of the cluster management page, click **Nodes** \> **Node**.

3. Click `...` \> **ECS terminal** in the Actions column of the target node to connect to the node console by using ECS Terminal.

4. Run the ping command to check whether the node can access the public network as expected.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6e11cd1f9357c685f6bb08a5edbc8813.png) </span>


&nbsp;
