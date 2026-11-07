---
title: "Adding a RADIUS server"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-adding-a-radius-server"
---

Before building an enterprise Wi\-Fi or wired network, you need to first configure the RADIUS server to manage network access requests and user authentication.

<span id="df3240bb"></span>
# Prerequisite

You have one or more Linux servers, which are deployed with the SealSuite RADIUS components as the RADIUS servers. To understand the recommended deployment and requirements for the RADIUS server, please refer to [Wi-Fi management overview](https://docs.byteplus.com/docs/sealsuite/docs-wi-fi-management-overview).

<span id="7124ff50"></span>
# Procedure

The number of servers you can add depends on the number of RADIUS servers you selected during the SealSuite purchase. For instance, if you chose one RADIUS server, only one RADIUS server can be added.


1. Log in to the Admin Console.

2. In the left navigation bar, click **NAC** \> **Config**.

3. Under the **RADIUS server** tab of the **Configuration** page, click **Configure**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/80aa00170cee40f2af74bd1e2a6c4b8d~tplv-goo7wpa0wc-image.image) </span>

4. Under the **Basic Information** tab of the **Configure the RADIUS server** page, complete the configuration by referring to the table below and click **Next Step**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c8820006e1554aa599eb0999c31564b4~tplv-goo7wpa0wc-image.image) </span>

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**RADIUS name** |A custom name that identifies the current RADIUS server. |
   |**Internal IP** |The IP address that identifies the RADIUS server within the corporate intranet. |
   |**Employee Wi\-Fi authentication port** |The port used by the RADIUS server to authenticate client employee Wi\-Fi connections. The default port is 1812, and it supports customization. |
   |**Employee Wi\-Fi accounting port** |The port used by the RADIUS server to bill client employee Wi\-Fi connections. The default port is 1813, and it supports customization. |
   |**Wired network authentication port** |The port used by the RADIUS server to authenticate client employee wired network connections. The default port is 2812, and it supports customization. |
   |**Wired network accounting port** |The port used by the RADIUS server to bill client employee wired network connections. The default port is 2813, and it supports customization. |
   |**Guest Wi\-Fi authentication port** |The port used by the RADIUS server to authenticate client guest Wi\-Fi connections. The default port is 3812, and it supports customization. |
   |**Guest Wi\-Fi accounting port** |The port used by the RADIUS server to bill client guest Wi\-Fi connections. The default port is 3813, and it supports customization. |
   

5. Under the **Deploy** tab of the **Configure the RADIUS server** page, copy the commands and log in to the prepared Linux server and install the component. After installation is complete, return to the **Deploy** tab and click **Next Step**.

6. Under the **Connectivity Test** tab of the **Configure the RADIUS server** page, click **Start detection** to check if the RADIUS server and SealSuite service network are communicating properly. After connectivity is confirmed, click **Finish**.


<span id="3e4c51e5"></span>
# Next steps

After configuring the RADIUS server, you can proceed to configure wireless routers or switches to build an enterprise Wi\-Fi or wired network.


* Configure wireless routers to build an enterprise Wi\-Fi network. For specific procedure, please refer to [Adding a wireless router](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-wireless-router).

* Configure switches to build an enterprise wired network. For specific procedure, please refer to [Adding a switch](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-switch).


<span id="906b5545"></span>
# Related information

If needed, you can edit or delete the RADIUS server later on by referring to [Editing or deleting a RADIUS server](https://docs.byteplus.com/docs/sealsuite/docs-editing-or-deleting-a-radius-server).
