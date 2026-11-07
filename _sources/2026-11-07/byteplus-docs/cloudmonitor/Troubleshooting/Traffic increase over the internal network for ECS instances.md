---
title: "Traffic increase over the internal network for ECS instances"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Traffic_increase_in_the_internal_network_of_an_ECS_instance"
---

<span id="2592b2fc"></span>
## **Issue description**

On the **Cloud Service Monitor** page, select the cloud product **ECS**. After you click the name of the target instance, you see that the inbound and outbound traffic rate over the internal network and the received and sent packet rate for the ECS instance have increased on the **basic monitoring or Operating system monitoring** tab.

<span id="5Vye8ZiH"></span>
## **Cause analysis**


* When other ECS instances transmit data to a specific ECS instance, the traffic over the internal network for the target ECS instance increases.

* If no ECS instances transmit data to the ECS instance, but the traffic over the internal network is increased, the ECS instance may be infected with viruses, which causes the ECS instance to send a large number of outbound packets.


<span id="SHetBm4n"></span>
## **Solution**


* If the ECS instance is deployed on Linux, perform the following operations:

   1. Log in to the ECS instance, run the command `yum install nethogs` to download and install NetHogs.

   2. Run the command `nethogs eth0` to view the processes occupying internal bandwidth.

      <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/27efb051dc2345b8a85ed67c400e7173.png) </span>

* If the ECS instance is deployed on Windows, perform the following operations:

   1. Log in to the ECS instance, right\-click the taskbar, and then select **Task Manager**.

   2. On the **Process** tab of the **Task Manager** dialog box, view the internal bandwidth usage of processes.
