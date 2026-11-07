---
title: "Adding a wireless router"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-adding-a-wireless-router"
---

To build an enterprise Wi\-Fi network, including staff and guest Wi\-Fi, you need to add a wireless router after adding the RADIUS server. This article provides instructions on how to add a wireless router.

<span id="2eb37e0f"></span>
# Prerequisite

The RADIUS server has been added. For more information, please refer to [Adding a RADIUS server](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-radius-server).

<span id="f7babae4"></span>
# Procedure


1. Log in to the Admin Console.

2. In the left navigation bar, click **NAC** \> **Config**.

3. Under the **Network Device** tab, click **Wireless controller**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c1cf2e59aa4249ca983fb6c86aa4f62e~tplv-goo7wpa0wc-image.image) </span>

4. In the **Add Wireless controller** dialog box, complete configurations by referring to the table below and click **Finish**.

   If you need to add multiple wireless routers, you can click **Add new** after completing the current configuration.

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Device Name** |Customize a name to identify the wireless router. |
   |**Brand** |Select the brand of the router. If your target brand is not available in the drop\-down list, add it in the input field. |
   |**IP address** |Enter the source IP address of the wireless router. The following IP address formats are supported to avoid configuring multiple device templates. Please fill in according to the actual device.<br><br><br>* IP Address, such as 10.10.0.0.<br><br>* IP Address Range, such as 10.10.0.0 \- 10.10.0.5.<br><br>* CIDR. |
   |**MAC Address** |Enter the MAC address of the wireless router. |
   |**Opening ability** |Select **Staff Wi\-Fi** or **Guest Wi\-Fi**, supporting multiple selections.<br><br><br>* **Staff Wi\-Fi**: Allows employees to connect to the enterprise Wi\-Fi. After selecting this, you need to configure the **CoA port** in the **More** settings.<br><br>* **Guest Wi\-Fi**: Allows guests to connect to the enterprise Wi\-Fi. After selecting this, you need to configure the **Visitor authentication information receiving address** and configure guest authentication related information in the **Custom Attributes** settings. |
   |**Visitor authentication information receiving address** |This address is required only when **Guest Wi\-Fi** is enabled. It is the address provided by the wireless router for external portal authentication, and the external portal service uses this address to submit guest usernames and passwords. |
   |**Custom Attributes** |* **CoA Port**: After the employee has been successfully authenticated and connects to the network, you can modify the online employee's network access rights or perform re\-authentication through the RADIUS server. This configuration needs to be consistent with the CoA port of the wireless router, which is 3799 by default.<br><br>* **Visitor Authentication Protocol Type**: Only needs to be configured when **Guest Wi\-Fi** is enabled, supports selecting **Portal** or **PEAP** authentication.<br><br>   * **Portal**: The client will support selecting account password or employee scanning code for guest authentication. This authentication method also requires configuring the following information:<br><br>      * **Visitor Authentication User Name Field**: The username field used by the wireless router, and field value may vary across different device manufacturers.<br><br>      * **Visitor Authentication Password Field**: The password field used by the wireless router, and field value may vary across different device manufacturers.<br><br>      * **Enter Custom JSON**: When guest authentication requires additional fields, you need to input customized data through custom JSON\-based format to meet requirements of different device brands.<br><br>      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If the corresponding wireless router needs to configure a guest portal server to achieve Portal authentication, please refer to <a href="https://docs.byteplus.com/docs/sealsuite/docs-managing-guest-portal-server">Managing guest portal server</a>.      </div><br>      <br><br>   * **PEAP**: The client only supports guest access through account password authentication. With PEAP chosen, you cannot deactivate accounts in the Application List of Guest Wi\-Fi. |
   


<span id="edd60196"></span>
# Next step

After adding a wireless router, you need to set the SSID for the enterprise Wi\-Fi. The SSID is the name of the enterprise Wi\-Fi displayed on devices. Employees or guests can access the corporate intranet by using the designated Wi\-Fi SSID. For more information, please refer to [Setting up Wi-Fi SSID](https://docs.byteplus.com/docs/sealsuite/docs-setting-up-wi-fi-ssid).

<span id="677da5e3"></span>
# Related information

If needed, you can edit or delete the RADIUS server later on by referring to [Editing or deleting routers and switches](https://docs.byteplus.com/docs/sealsuite/docs-editing-or-deleting-routers-and-switches).
