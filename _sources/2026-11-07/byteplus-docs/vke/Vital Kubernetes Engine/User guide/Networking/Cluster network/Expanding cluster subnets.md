---
title: "Expanding cluster subnets"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Expanding-cluster-subnets"
---

When you create a cluster, you need to select a virtual private network (VPC) and subnets for the cluster, such as the node network and the Pod network. As the cluster is used and expanded, IP addresses may be insufficient in the cluster subnets. This topic describes how to expand the subnets of a cluster by using a secondary CIDR block.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

After the VPC and subnets of a cluster are created, you cannot modify the CIDR blocks of the networks. When IP addresses in the VPC of the cluster are insufficient or the CIDR block needs to be modified, you can only create a larger VPC to address the issue. In this case, the configured network features need to be configured again, and ECS instances need to be migrated between VPCs, which is costly.

Vital Kubernetes Engine (VKE) clusters allow you to use secondary CIDR blocks in VPCs. You can add a new secondary CIDR block to the original CIDR block and use the primary or secondary CIDR block to expand the subnets of a cluster.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits


* The secondary CIDR block must be in the same CIDR block as the primary CIDR block of the target VPC. For example, if the primary CIDR block of the target VPC belongs to 192.168.0.0/16\-/24, the secondary CIDR block must also belong to 192.168.0.0/16\-/24, and cannot belong to 10.0.0.0/8\-/24 or 172.16.0.0/12\-/24.

* If the primary CIDR block of the target VPC is already the largest CIDR block, such as 192.168.0.0/16, you cannot add a secondary CIDR block.

* The secondary CIDR block cannot overlap with other CIDR blocks of the target VPC.

* After a secondary CIDR block is added, it cannot be modified.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more details about secondary CIDR blocks, see <a href="https://docs.byteplus.com/en/docs/vpc/Managing-secondary-CIDR-blocks">Adding or deleting a secondary CIDR</a>.</div>


<span id=".5q2l6aqk5LiA77ya5Yib5bu66L6F5YqpLWNpZHI="></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Yib5bu66L6F5YqpLWNpZHI="></span>
### Step 1: Create a secondary CIDR block


1. Log in to the [VPC console](https://console.byteplus.com/vpc).

2. In the left navigation bar, click **VPC**.

3. In the VPC list on the right, find the target VPC and click **Add Secondary CIDR Block** in the **Actions** column.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fa7b6bd554e2168def95741da83a4ef6.png) </span>

4. Configure the secondary CIDR block.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d7f7e41195c458f228c8a8a9569bf985.png) </span>

5. Click **Add** to complete the configuration.


<span id="euCNaTph"></span>
### Step 2: Create a subnet


1. In the left navigation bar, click **Subnet**.

2. Click **Create Subnet** to create subnets in different availability zones by using the secondary CIDR block.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9d13fb98ba372dd4bf6429bd9f0656d1.png) </span>


<span id="UZm6rmr1"></span>
### Step 3: Use the secondary CIDR block to expand cluster subnets

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>



* <div data-tips="true" data-tips-type="warning">When you expand the subnet, the selected secondary CIDR block must not overlap with the Service CIDR block.</div>


* <div data-tips="true" data-tips-type="warning">Expanding cluster subnets with a secondary CIDR block may restart kube\-apiserver. We recommend that you perform the expansion during off\-peak hours.</div>



<span id=".5omp5bGV6IqC54K55a2Q572R"></span>
#### Expanding the node subnet

You can directly use a secondary CIDR block when you create or update a node pool to expand the node network. This topic uses the creation of a node pool as an example.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. On the page that appears, click the name of the target cluster.

3. In the left navigation bar of the cluster management page, click **Nodes \> Node pool**.

4. Click **Create node pool**, configure the new node pool, and then select the created secondary CIDR block to expand the node subnet. For configuration details, see [Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d09e18e5cfada2942198211082e9f504.png) </span>


<span id=".5omp5bGVLXBvZC3lrZDnvZE="></span>
#### Expanding the pod subnet


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. Click the name of the target cluster, and in the left navigation bar, click **Overview**.

4. On the **Overview** tab, find **Cluster network configuration**, click **Add** under **Pod subnets**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c90cbf921b3e17e7e75fb05ab1360112.png) </span>

1. In the panel that appears, select the secondary CIDR block and click **Confirm ** to expand the pod subnet.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a156433fdea8c77f3aa21ce81696f46c.png) </span>


<span id="snLW8hkn"></span>
### Step 4: Check security groups

Normal communication between nodes and pods in the cluster is always important. After you expand the cluster subnet using a secondary CIDR block, we recommend that you check the security groups of the cluster to verify that the security groups allow traffic from the secondary CIDR block. The following content provides an example configuration. In your scenario, replace the source addresses and port numbers with your desired ones.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">In addition to the security group of the VKE cluster, you also need to confirm that the security groups of other services (for example, the vePFS service) accessed by the cluster allow the secondary CIDR.</div>



1. Log in to the [VPC console](https://console.byteplus.com/vpc).

2. In the left navigation bar, click **Security Group**. On the Security Group page, find the target security group.

3. Click the security group name to enter the details page. Click the **Access rules** tab, and on the **Inbound rule** sub\-tab, confirm that the security group allows traffic from the newly added secondary CIDR block.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c33b823a5085b44bb4146e8f5c6e39a1.png) </span>

4. If traffic from the CIDR block is not allowed, click **Add rule** to add an inbound rule for the CIDR block. For configuration details, see [Adding rules to a security group](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules).


&nbsp;
