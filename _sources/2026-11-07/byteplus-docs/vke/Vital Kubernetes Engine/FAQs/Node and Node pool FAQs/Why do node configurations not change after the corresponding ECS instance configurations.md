---
title: "Why do node configurations not change after the corresponding ECS instance configurations are modified in the ECS console?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Why-are-changes-not-synchronized-to-a-node-after-I-modify-the-ECS-instance-configurations-of-the-nod"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description

The node resources of VKE correspond to the ECS resources of . After you directly modify the configurations of ECS instances, such as the instance type, billing mode, and security group in the ECS console, the configurations of the corresponding node resources in VKE do not change synchronously.

<span id=".6Kej5Yaz5pa55rOV"></span>
## Solution


1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. In the left navigation bar, click **Cluster**. On the page that appears, locate the target cluster and click its name.

3. In the left navigation bar of the cluster management page, click **Node**. Find the node whose configurations have been modified in the ECS console, and in the **Actions** column, click `...` \> **Remove**.

4. In the secondary confirmation dialog box, unselect **Synchronous destruction of free nodes**, and click **Remove**.

5. On the **Node** page, click **Add existing node** to add the node removed in the previous step to the cluster. For details, see [Adding existing nodes](https://docs.byteplus.com/en/docs/vke/Adding-existing-nodes).
