---
title: "Managing devices and networks for hardware-based branch gateways"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-managing-devices-and-networks-for-branch-gateway-hardware-version"
---

In the Admin Portal, you can utilize the device management and network configuration capabilities of the hardware\-based branch gateways. This helps you manage the configurations of hardware\-based branch gateways in remote locations. This article introduces how to manage the hardware\-based branch gateways in the Admin Portal.

<span id="ff394741"></span>
# Managing SealSuite's FLG Access Gateway

<span id="6a9c5dc3"></span>
## Prerequisite

Hardware\-based branch gateways have been added in the Admin Portal and the corresponding FLGs have been properly provisioned. For more information, please refer to [Adding a hardware-based branch gateway](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-branch-gateway-hardware-version-).

<span id="ea4fcb93"></span>
## Procedure


1. Log in to the Admin Console.

2. In the left navigation bar, click **SD\-WAN** \> **Branch Gateway**.

3. Locate the specific hardware\-based branch gateway, and click on the branch gateway card to enter the details page.

4. On the **Device Management** tab of the details page, you can perform the following actions:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2e796774fd8d4d58a51e90241c9001db~tplv-goo7wpa0wc-image.image) </span>

   
   |**Configuration Items** |**Description** |
   |---|---|
   |**Authorize Device** |After authorization, the device's manufacturer (SealSuite) can debug the device remotely. You can cancel the authorization according to the actual situation. |
   |**Unbind** |Dissociate the FLG device from its corresponding branch gateway in the Admin Portal.<br><br><br>* After unbinding the FLG device, if you want to re\-establish the association, you must complete the provisioning of the device again.<br><br>* After the disassociation, all data displayed on the details page, including the existing static IP addresses and the relevant configurations will be erased. |
   |**Restart the device** |Remotely restart the FLG. When you start the rebooting process, the device is not available for use until the rebooting process is completed. |
   |**Static Route** |Remotely manage static route configurations for the current FLG. You can modify the configurations of the static routes based on your requirements.<br><br><br>* Add a single static route: Click  **+ Add Route** on the right side of the page, and add a static route in the pop\-up dialog box.<br><br>* Add static routes in batch: Click  **↓ Import** on the right side of the page, and download a form template on the **Batch Route Import by Excel** page. After filling in static routing information in the downloaded template, you need to upload the form on the **Batch Route Import by Excel** page, and click **Start**.<br><br><br>The description of static route parameters is as follows:<br><br><br>* **Target** (**IP** column field in the Excel template): Specify the IP address of your target network segment in CIDR format.<br><br>* **Next Hop** (**Next Hop** Column Field in the Excel template): Specify the next hop IP address.<br><br>* **Active Now** (**Active Now** column fields in the Excel template): Set whether static routing configuration takes effect immediately.<br><br><br>After adding static routes, you can **edit**, **enable** or **delete** specific static routes. |
   


<span id="30a7d3ad"></span>
# Managing network configurations of FLG


1. Log in to the Admin Console.

2. In the left navigation bar, click **SD\-WAN** \> **Branch Gateway**.

3. Locate the specific hardware\-based branch gateway, and click on the branch gateway card to enter the details page.

4. On the **Network Configuration** tab of the details page, remotely configure the WAN and LAN Interfaces of the specified FLG.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fff20409af5844a0ba9b83a44a6f8ed6~tplv-goo7wpa0wc-image.image) </span>

   * At the top of the tab, you can view the current network connection status. You need to ensure that the device is connected to the Internet.

   * For detailed information on how to configure WAN interfaces and LAN interfaces, please refer to [WAN configuration](https://arcosite.bytedance.net/sites/1673322421329/64b8d299f46a1b022f9c183b/editor/654df735b6df2802f6d8c355?docLang=en&bv=652fd8f3fb401502ea5effe0#c286cb0d) and [LAN configuration](https://arcosite.bytedance.net/sites/1673322421329/64b8d299f46a1b022f9c183b/editor/654df735b6df2802f6d8c355?docLang=en&bv=652fd8f3fb401502ea5effe0#d0ba3d29).


<span id="c286cb0d"></span>
## WAN **configuration**

You can choose to configure WAN interfaces using either the **WAN1 configuration** tab or **WAN2 configuration** tab. Configuration items under these tabs are the same. The description of configuration items is as follows:


|**Configuration Items** |**Description** |
|---|---|
|**Connection Type** |You can select **static IP** or **DHCP**.<br><br><br>* If **static IP** is selected, you need to configure the corresponding **IP address**, **Subnet Mask**, and **Default Gateway**.<br><br>* If **DHCP** is selected, it indicates that IP addresses will be dynamically allocated to the requesting devices, without the need to manually add configuration information for each device. |
|**Effective Rule** |* If **Effective after start** is selected, you need to restart FLG to take effect the current configuration.<br><br>* If **Effective now** is selected, the configuration will take effect immediately within the device. |
|**SNAT** |After you enable this option, the source IP addresses within a private network packet are automatically converted to public IP addresses, facilitating connections between a private network and the Internet. |


<span id="d0ba3d29"></span>
## **LAN configuration**

On the **LAN configuration** tab, you can configure the default logical interface or use the following steps to add a logical interface:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When adding a logical interface, you need to ensure that the FLG is running smoothly.</div>



1. Click  **+**  **Add VLAN**.

2. On the **Add Logical LAN Interface** page, specify the following configuration items, and click **Confirm** or **Add new**.

   
   |**Configuration Items** |**Description** |
   |---|---|
   |**Logical Interface Name** |Enter a name to identify the logical interface. You can only enter 14 characters. |
   |**VLAN ID** |Specify the VLAN ID assigned to a physical interface, which ranges from 0~4095. If the ID is set to a value other than 0, you need to configure the VLAN settings on the corresponding network device. |
   |**IP Address** |Specify an IP address for the logical interface by using the IP address of the DHCP server's default gateway. You need to fill in a valid IP address in CIDR format, which belongs to the same network segment as the DHCP server. |
   |**DHCP** |If DHCP is enabled, the local client will dynamically obtain IP addresses through the DHCP protocol, which helps improve IP address usage and avoid address conflicts. After enabling this option, you need to configure the following parameters:<br><br><br>* **DHCP Starting IP Address**, **DHCP Last IP Address**: \*\*\*\* The starting IP address and the last IP address are used to specify the IP address range that will be available for allocation by the DHCP server. The starting IP address refers to the first IP address assigned by the DHCP server.<br><br>* **DHCP Lease Time**: \*\*\*\* The validity period of the IP addresses assigned by the DHCP server.<br><br>* Configure the **DNS server (primary)**  and **DNS server (backup)**  for DHCP. |
   |**Associate Physical LAN Interface** |Associate physical LAN interfaces with the current logical interface. When associating the interfaces, you need to pay attention to the following rules:<br><br><br>* A logical LAN Interface can be associated with multiple physical LAN Interfaces.<br><br>* The same physical LAN Interface and the same VLAN ID can only be associated with one logical LAN Interface. |
   

3. (Optional) In the interface list, you can edit, enable, disable, or delete the existing logical interfaces.
