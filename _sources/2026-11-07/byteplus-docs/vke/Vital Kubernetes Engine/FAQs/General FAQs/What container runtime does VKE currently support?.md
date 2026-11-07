---
title: "What container runtime does VKE currently support?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/What-container-runtimes-does-VKE-currently-support"
---

VKE currently supports only the containerd runtime.

As VKE's Kubernetes versions evolve, the containerd runtime version on nodes will also change. You can perform the following steps to view the runtime:


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Find the target cluster and click its name.

3. In the left navigation bar of the cluster management page, click **Node**. On the page that appears, find a node and click the node name.

4. On the **Overview** tab of the **Node details page**, view the **Container runtime** in the **Kubernetes information** section.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_eaaaf5accd5fb9a7d240b1455f00111b.png) </span>
