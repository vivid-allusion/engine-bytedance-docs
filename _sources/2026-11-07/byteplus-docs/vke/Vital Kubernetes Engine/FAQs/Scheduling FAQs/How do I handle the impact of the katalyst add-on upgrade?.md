---
title: "How do I handle the impact of the katalyst add-on upgrade?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Handling_the_impact_after_Katalyst_add-on_upgrade"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description

When you use the katalyst add\-on in a cluster that runs on Kubernetes v1.24 or v1.26 and upgrade the add\-on version from v0.3.5\-vke.5 to v0.5.x or later, you need to update the configurations of custom kubelet parameters. Otherwise, you may encounter the TopologyAffinityError issue when creating pods.

<span id=".5aSE55CG5pa55rOV"></span>
## Solution

After you upgrade the katalyst add\-on from v0.3.5\-vke.5 to v0.5.x or later, you need to set the custom `topology-manager-policy` field of the kubelet parameter for the node pool associated with the add\-on to `none`, and synchronize the update to existing nodes. You can perform the following steps:


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. On the left navigation bar, select **Cluster**, and click the name of the target cluster.

3. In the left navigation bar of the cluster management page, click **Nodes** \> **Node pool**.

4. On the **Node pool** page, find the node pool where the katalyst add\-on is deployed and click the node pool name to go to the details page.

   For the node pool associated with the katalyst add\-on, you can see the `vke.node.katalyst.deploy:true` node label in the More configurations section on its details page.

5. On the node pool details page, click the **Kubelet configs** tab, and click **Edit**.

6. Set the `topology-manager-policy` field to `none` and save the configuration.

7. On the **Kubelet configs** tab, click **Existing node config synchronization** to synchronize custom kubelet parameter configurations for existing nodes.
