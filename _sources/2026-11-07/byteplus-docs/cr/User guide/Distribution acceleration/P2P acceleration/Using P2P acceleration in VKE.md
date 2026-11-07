---
title: "Using P2P acceleration in VKE"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/use-p2p-acceleration-in-vke"
---

P2P (Peer\-to\-Peer) acceleration allows cluster nodes to reuse data already downloaded by other nodes when pulling images, which reduces redundant download traffic from CR and reduces image pull time for large\-scale workloads. This topic describes how to activate or disable P2P acceleration and change the VPC to which it applies.

> **tip**

> This operation applies only to Standard Edition instances.

## Background information

Following the P2P (Peer\-to\-Peer) architecture upgrade, the P2P acceleration entries in CR have been adjusted. Entries for different scenarios are as follows:

|**Action** |**Entry** |**Description** |
|---|---|---|
|[Activate the new P2P acceleration](https://docs.byteplus.com/en/docs/cr/use-p2p-acceleration-in-vke?lang=en#w6LPJAlT) |VKE console |The new P2P acceleration is uniformly activated and configured on the VKE side. |
|[Disable the legacy P2P acceleration](https://docs.byteplus.com/en/docs/cr/use-p2p-acceleration-in-vke?lang=en#d2nMQ53r) |CR console |Applies only to instances for which P2P acceleration has already been activated in CR. |
|[Modify the VPC access scope for legacy P2P acceleration](https://docs.byteplus.com/en/docs/cr/use-p2p-acceleration-in-vke?lang=en#7kyu6Izl) |CR console |Applies only to instances for which P2P acceleration has already been activated in CR. |

## Prerequisites

* A Vital Kubernetes Engine (VKE) cluster has been created. For detailed operations, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* You have created a Standard Edition instance. For instructions, see [Creating Standard instances](https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance) **.**

* You have created a VPC to define the accessible scope for P2P acceleration. For details, see [Creating VPCs](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

   > **warning**

   > All nodes in the VKE cluster that use P2P acceleration must be located within the accessible VPC configured for P2P acceleration.

## Procedure

### Activate the new P2P acceleration

To enable P2P acceleration for the first time, go to the ** Image acceleration** module in the VKE console to complete the configuration and improve the image pull speed of your workloads. For detailed steps, see[ Configuring P2P acceleration](https://docs.byteplus.com/en/docs/vke/P2P-acceleration-solution?lang=en).

### **Disable the legacy P2P acceleration**

> **warning**

> Disabling P2P acceleration affects VKE clusters with this feature in use. The p2p\-accelerator add\-on in VKE clusters will no longer function and needs to be uninstalled manually. For instructions on uninstalling p2p\-accelerator, see [Uninstalling add\-ons](https://docs.byteplus.com/en/docs/vke/Uninstalling-an-add-on).

1. Log in to the [CR console](https://console.byteplus.com/cr) **.**

2. Select the target region in the top navigation bar.

3. In the left navigation bar, click **Instance list**. Then, on the **Instance list ** page, find the Standard Edition instance for which you want to enable P2P acceleration and click **Enter instance**.

4. On the Standard Edition instance details page, select **Distribution acceleration** \> **P2P acceleration** in the left navigation bar.

5. Click **Disable ** to the right of P2P **acceleration**, enter the name of the current Standard Edition instance, and then click **Confirm** to disable the P2P acceleration feature for this instance.

### Modify the VPC scope for **legacy P2P acceleration**

> **warning**

> Modifying the P2P acceleration VPC scope affects which VKE clusters can access and use this P2P acceleration feature. Confirm before proceeding.

1. Log in to the [CR console](https://console.byteplus.com/cr) **.**

2. Select the target region in the top navigation bar.

3. In the left navigation bar, click **Instance list**. Then, on the ** Instance list ** page, find the Standard Edition instance for which you want to disable P2P acceleration and click **Enter instance**.

4. On the Standard Edition instance details page, select **Distribution acceleration** \> **P2P acceleration** in the left navigation bar.

5. Click **Modify VPC range** to change the VPC(s) in which the P2P acceleration feature is available for the current Standard Edition instance.
