---
title: "Managing virtual nodes"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Managing_virtual_nodes"
---

This topic describes how to manage virtual nodes by using the VKE console.

<span id="mfmk9hur"></span>
## Prerequisites


* The vci\-virtual\-kubelet add\-on has been installed in the VKE cluster. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.dmNpLXZpcnR1YWwta3ViZWxldC3nu4Tku7Y=).

* A subnet for the corresponding availability zone has been created within the VPC to which the VKE cluster belongs. For details, see [Creating subnets](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).


<span id="PgSD7yo1"></span>
## Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster.

4. In the left navigation bar, select **Nodes** \> **Virtual node**.

5. On the **Virtual node** page, configure and manage virtual nodes, and create a global VCI configuration.


<span id="RUGBAn90"></span>
### Configuring virtual nodes

To use VCI Pods in a specific availability zone, configure VCI Pod subnets in that availability zone. The system will automatically create virtual nodes in the corresponding availability zone based on the specified subnets.


1. On the **Virtual node** page, click **Configure virtual node**. Alternatively, in the availability zone list, find the availability zone in which you want to configure virtual nodes and then click **Configure virtual node** in the **Actions** column.

2. On the **Configure virtual node** page, configure VCI Pod subnets for virtual nodes in the target availability zone, or update the existing VCI Pod subnets.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">You can delete a specified VCI pod subnet only when it is not used by any VCI pod.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_aa4e68c3b075b21f21aa65442d4ba4ff.png) </span>

3. After the configuration is complete, click **Confirm** to save the configuration. The system will automatically create virtual nodes within the corresponding availability zone based on the specified VCI Pod subnets.


<span id="ZbGhBsBm"></span>
### Creating a global VCI configuration

A global VCI configuration can be created by using vci\-profile. vci\-profile is the configuration file for VCI. It allows you to define unified and globally fixed configurations for VCI resource usage at the cluster or namespace level. For a detailed description, see [Using VCI by configuring vci-profile](https://docs.byteplus.com/en/docs/vke/Using-VCI-by-configuring-vci-profile).

<span id="8ZLyOQQt"></span>
### Other operations

You can perform other operations on virtual nodes, such as cordoning, label management, taint management, and diagnosis. Find the target virtual node in the virtual node list and in the **Actions** column, click the ... icon to perform the corresponding operation. For a detailed description, see [Managing nodes](https://docs.byteplus.com/en/docs/vke/Managing-nodes).
