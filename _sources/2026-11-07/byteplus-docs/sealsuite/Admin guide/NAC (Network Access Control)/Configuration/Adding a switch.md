---
title: "Adding a switch"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-adding-a-switch"
---

To build a wired network for your enterprise, you need to add a switch after adding the RADIUS server. This article will guide you through the process of adding a switch.

<span id="1becacd2"></span>
# Prerequisite

The RADIUS server has been added. For more information, please refer to [Adding a wireless router](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-wireless-router).

<span id="e9ea0709"></span>
# Procedure


1. Log in to the Admin Console.

2. In the left navigation bar, click **NAC** \> **Config**.

3. Under the **Network Device** tab, click **Network** **Switch**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fcac1f0791774e598e785426512c09a3~tplv-goo7wpa0wc-image.image) </span>

4. In the **Add Wired switch** dialog box, complete configurations by referring to the table below and click **Finish**.

   If you need to add multiple switches, you can click **Add new** after completing the current configuration.

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Device Name** |Enter a customized name to identify the switch. |
   |**Brand** |Select the brand of the switch. |
   |**IP address** |Enter the source IP address of the wireless router. The following IP address formats are supported. Fill in according to the actual device.<br><br><br>* IP address, such as 10.10.0.0<br><br>* IP address range, such as 10.10.0.0 \- 10.10.0.5<br><br>* CIDR |
   |**MAC Address** |Enter the MAC address of the switch. |
   |**CoA port** |CoA allows you to modify employees' permissions or re\-authenticate them using RADIUS after their successful authentication. This configuration should be consistent with the CoA port of the wired switch. The default value is 3799. |
   


<span id="1c5bee17"></span>
# Related information


* You can configure employee network accounts and permissions to ensure the secure use of the wired network. For more information, please refer to [Managing staff Wi-Fi](https://docs.byteplus.com/docs/sealsuite/docs-managing-staff-wi-fi).

* You can set up dumb terminals to access the wired networks. For more information, please refer to [Managing dumb terminals](https://docs.byteplus.com/docs/sealsuite/docs-managing-dumb-terminals).

* You can edit or delete routers. For more information, please refer to [Editing or deleting routers and switches](https://docs.byteplus.com/docs/sealsuite/docs-editing-or-deleting-routers-and-switches).
