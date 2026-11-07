---
title: "Adding a hardware-based branch gateway"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-adding-a-branch-gateway-hardware-version-"
---

Through the configuration of branch gateways, you can enable on\-premises networks to be connected with SealSuite’s public cloud via nearby access points named POP nodes. This helps you integrate the networks of branch offices, headquarters, internet data centers, and cloud servers into a larger corporate network and optimize network interconnectivity later on. The branch gateways are divided into two categories: software\-based and hardware\-based branch gateways. This article introduces how to add hardware\-based branch gateways in the Admin Portal for enterprises that have purchased SealSuite's networking device named FLG.

<span id="8168e9fc"></span>
# Prerequisite

Prepare the FLG in the place where you want to set up branch gateways.

<span id="945b3bd3"></span>
# Step 1: Adding a hardware\-based branch gateway in the Admin Portal


1. Log in to the Admin Console.

2. In the left navigation bar, click **SD\-WAN** \> **Branch Gateway**.

3. In the upper right corner of the **Branch Gateway** page, select  **+ Add Branch** \> **Hardware**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a22aa7a6e19b4b329decc345c334f7d9~tplv-goo7wpa0wc-image.image) </span>

4. In the **Basic configuration** section of the **Add Branch Gateway** page, configure the branch gateway by using the following configuration items and click **Next Step**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e20f20852c0f441c8be0f40d196305b8~tplv-goo7wpa0wc-image.image) </span>

   The description of configuration items is as follows:

   
   |**Items** |**Description** |
   |---|---|
   |**Branch Name** |Enter a custom name for the branch gateway in Chinese and English. |
   |**Device Model** |Choose **FLG\-X1** or **FLG\-X2** based on the device model in use. |
   |**Branch Gateway Type** |Select the type of premises where you want to set up the branch gateway. Available options include: **Office Branch**, **Headquarter**, **Data Center**, **Public Cloud** and **Other**. |
   |**Source Network Address Translation (SNAT)**  |SNAT is used to hide internal network addresses and solve private network address conflicts.<br><br><br>* \*\*Enabled: \*\*When the current branch gateway's branch network segment conflicts with other branch network segments, it needs to be **enabled**. After enabling SNAT, SealSuite will automatically generate branch network segments for the branch gateway for network communication with SealSuite's public cloud.<br><br>* **Disabled:**  When SNAT is not enabled, you need to manually set the branch network segment for the branch gateway. After setting, SealSuite will automatically distribute the corresponding branch network segments of the branch gateway to each access point or the POP node to achieve network communication between the branch gateway and SealSuite public cloud. |
   

5. In the **Device Provisioning** section of the **Add Branch Gateway** page, configure your FLG by using the provided steps on the webpage.

   * For detailed information on the steps as shown in the **Device Preparation** section and the **Device Provision** section, refer to [step 2](https://arcosite.bytedance.net/sites/1673322421329/64b8d299f46a1b022f9c183b/editor/654c767a2e2b130300d851b3?docLang=en&bv=652fd8f3fb401502ea5effe0#4e45bfb9) below. Besides, you need to save the **Authentication** **URL**, **ID**, and **Secret**, which will be used to provision the device later on.

   * By default, the physical WAN port of the device is set to DHCP. If you want to access the Internet through a static IP, you can configure static IP addresses by clicking **Go to configuration** in the **Device Provision** section. For more information, please refer to[Managing devices and networks for hardware-based branch gateways](https://docs.byteplus.com/docs/sealsuite/docs-managing-devices-and-networks-for-branch-gateway-hardware-version).

   * After completing basic configurations, if you close the current webpage in the Admin Portal, you can find the newly added gateway which is not activated in the branch gateway list. By clicking on your target gateway and the **View Device Provisioning Info** link as shown in the screenshot below, you can retrieve information of the specified gateway, including the authentication **URL**, **ID**, and **Secret**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8af078cb78a046738d1094fac5d10b2a~tplv-goo7wpa0wc-image.image) </span>


<span id="4e45bfb9"></span>
# Step 2: Configuring the FLG in your target premises


1. Power up the FLG and plug in the network cable through the WAN port, ensuring the Internet connections are running smoothly.

2. Connect the LAN port of the device to a desktop computer by using network cables.

3. On the provisioned computer, access the gateway's console interface by using `192.168.168.1`, and log into the console with an Administrator account.

4. On the **WAN configuration** page of the console, configure the WAN ports by using the following configuration items as per your requirements.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a1bae90e7b13497097981992fd096728~tplv-goo7wpa0wc-image.image) </span>

   The description of configuration items is as follows:

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Connection Type** |Select **Static IP** or **DHCP** according to actual needs.<br><br><br>* If **Static IP** is selected, you need to configure the **IP address**, **Subnet Mask**, and **Default Gateway** of the WAN port accordingly. The IP address of the WAN port needs to be in the same network segment as the IP address of the opposite port connected to the WAN port.<br><br>* If **DHCP** is selected, it indicates that dynamically obtaining the IP address without manually configuring other parameters. |
   |**SNAT** |Choose whether to enable **SNAT**. After you enable this option, the IP addresses within a private network packet are automatically converted to public IP addresses, facilitating connections between a private network and the Internet. |
   

5. On the **Device Provision** page of the console, specify provisioning settings for the device and click **Finish**.

   * Authentication URL: Corresponds to the authentication URL of the specified hardware\-based branch gateway in the Admin Portal.

   * ID: Corresponds to the **ID** of the specified hardware\-based branch gateway in the Admin Portal.

   * Secret: Corresponds to the **Secret** of the specified hardware\-based branch gateway in the Admin Portal.

6. Ensure that the gateway is activated and provisioned, and the hardware\-based branch gateway that you created in the Admin Portal is bound to the psychical gateway device.

   You can view and manage hardware\-based branch gateways in the Admin Portal later.

7. (Optional) At the bottom of the left navigation bar, modify your password by clicking **Reset Password**.


<span id="f27ef1fd"></span>
# Related information


* After you deploy branch gateways for your enterprise's offices in different locations and ensure these branch gateways are operational, the networks of branch offices are automatically connected to nearby POP nodes, facilitating the setup of an integrated corporate network. After that, you can choose to enable the **Remote Working** capability under the networking module, allowing users to access the corporate network through the SealSuite client or Web browsers. For more information, please refer to [Enabling remote working on the cloud](https://docs.byteplus.com/docs/sealsuite/docs-enabling-telecommuting-on-the-cloud).

* In the regular server operation and maintenance processes, it is suggested to manage hardware\-based branch gateways through the Admin Portal by using the procedures provided in the following topics:

* [Managing devices and networks for hardware-based branch gateways](https://docs.byteplus.com/docs/sealsuite/docs-managing-devices-and-networks-for-branch-gateway-hardware-version)

* [Configuring branch gateway routing](https://docs.byteplus.com/docs/sealsuite/docs-configuring-branch-gateway-routing)

* [Viewing basic information and performance statistics of a branch gateway](https://docs.byteplus.com/docs/sealsuite/docs-e51gqmg9ny)

* [Editing or deleting a branch gateway](https://docs.byteplus.com/docs/sealsuite/docs-editing-or-deleting-a-branch-gateway)
