---
title: "Create a VKE private resource pool"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Create_a_VKE_private_build_resource_pool"
---

The private resource pool is a custom resource pool built by the user. When the public resource pool does not meet requirements, users can create and use a private resource pool for pipeline build activities. This article introduces how to create a VKE private resource pool.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

CP supports connecting to the private resource pool (private build cluster) via the Agent method to run pipeline tasks. This method does not require exposing the cluster's API Server public network address, providing enhanced security. The VKE cluster to be imported must meet the following conditions:


* The VKE cluster has opened the public network, AND Inbound supports the public network. Outbound does not require public network access and can be adjusted according to actual business needs.

   * For instructions on turning on public network access, see [How to manually enable cluster public network access?](https://docs.byteplus.com/en/docs/vke/How-do-I-manually-enable-internet-facing-access-for-a-cluster).

   * For a description of public network Inbound and Outbound access rule settings, see [Cluster access rules](https://docs.byteplus.com/en/docs/vke/Cluster-access-rules).

* Each cluster can only be connected once. If abnormal connection occurs, please delete and reconnect.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A VKE cluster has been created. For details, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* Only part of the Kubernetes versions of the VKE cluster support this feature. The specific version number is subject to the Console. To upgrade the cluster Kubernetes version, see [Upgrade cluster](https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [CP Console ](https://console.byteplus.com/cp).

2. In the left navigation bar, click **Resource management \> ** **Deployment resource pool ** .

3. Click **Create private resource pool**.

4. On the **Create private resource pool** page, configure the private resource pool information as required.

   
   |Parameter |Description |
   |---|---|
   |Name |Customize the private resource pool name. |
   |Description |Enter a description for this custom resource pool, within 100 characters. Optional. |
   |Sharing scope |Control workspace permissions for the private resource pool.<br><br><br>* All workspaces: All workspaces can use this private resource pool.<br><br>* Specify workspace (recommended): Only specified workspaces can use this private resource pool. |
   |Connection Type |Select **VKE**. |
   |Region |Select the scope of the region where the resources are located. |
   |cluster |Select a created Vital Kubernetes Engine cluster. |
   |TOS cache |Select whether to turn on TOS cache. After turning it on, select a created TOS bucket and enter the corresponding address. The default path is `/cp-{cluster uuid}/cache`, for example, `/cp-7cf837a0-565b-11f0-9d82-d558f8d9*****/cache`. |
   

6. Click **Confirm** to complete the creation of the private resource pool.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

After Agent deployment is complete, you can use the Agent to consume pipeline tasks. On the **Create/Edit pipeline \> Basic information** page, in the build resource pool area, select your private resource pool.
