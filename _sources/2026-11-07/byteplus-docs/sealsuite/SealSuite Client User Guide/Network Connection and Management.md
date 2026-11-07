---
title: "Network Connection and Management"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/network-connection-and-management"
---

<span id="79688dc7"></span>
## VPN Connection

<span id="db071603"></span>
### One\-click Connection

Click the switch on the **VPN Connectivity** card on the **Overview** page to turn VPN on or off. After VPN is connected, SealSuite displays the connection time, current VPN mode, and current server node.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="warning">If your organization enables multi\-factor authentication for VPN connections, follow the on\-screen instructions to verify your identity when connecting. You can connect to the VPN after verification succeeds. Your administrator configures the available authentication methods.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3647ca3ccaf84b3d8a725b66ad6cc708~tplv-goo7wpa0wc-image.image) </span>

<span id="7eab09c5"></span>
### Switch the Network Mode

Go to the **Network** page and click **Split mode** or **Full mode** to switch the current network mode.


* **Split mode**: This mode is generally recommended. In this mode, only office\-related network traffic is routed through VPN.

* **Full mode**: This mode is recommended for insecure networks. In this mode, all network traffic is routed through VPN.


<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/mfa-en-20260928/en-network-2-redacted.png) </span>

<span id="a6734541"></span>
### Switch the Server Node

If the latency of the current server node is high, click the icon on the right side of the current **server** to switch the server node.

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/mfa-en-20260928/en-network-3-redacted.png) </span>

<span id="95310601"></span>
## Wi\-Fi Connection

After the desktop client identifies the employee SSID, SealSuite displays a real\-time notification indicating that Wi\-Fi is available. Click **Connect** to quickly go to the network connection page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d19e39059a04a45aabc64bf412efb48~tplv-goo7wpa0wc-image.image) </span>

If you do not use the quick redirect, you can also click **Network** \> **Wi\-Fi** \> **Connect** to connect to Wi\-Fi with one click.

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/mfa-en-20260928/en-network-5-redacted.png) </span>

You can also use the account and password displayed on the **Wi\-Fi** page to connect to Wi\-Fi. Enter them in the **Account Name** and **Password** fields in the PC network connection window. The following figure uses a Mac device as an example.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1466f4b454884fc9b6baf19ec1ce27bc~tplv-goo7wpa0wc-image.image) </span>

If the enterprise administrator has enabled the feature to **hide Employee Wi\-Fi and wired network passwords** in the Admin Console, the Employee Wi\-Fi password is hidden in the client. Contact the administrator if you need the password.

<span id="10f485f4"></span>
## Wired Network Connection

The SealSuite desktop client supports wired network connections through the dedicated company network port.

<span id="f60e42fe"></span>
### macOS

<span id="295caced"></span>
#### Scenario 1: Password Visible

After the computer is connected to a wired network port, go to **Network** \> **Wired** in the SealSuite desktop client to view the account and password. Enter the account and password in the system pop\-up window to complete the wired network connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/64bd9dcb472243dcabe24c11d8a764a2~tplv-goo7wpa0wc-image.image) </span>

For macOS, after the computer is connected to a wired network port, enter the SealSuite wired network account and password in the system pop\-up window. If the pop\-up is closed accidentally, unplug the network cable and plug it back into the computer to display the pop\-up again.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/98197ab393c74f0d828cba6d768e711f~tplv-goo7wpa0wc-image.image) </span>

<span id="e74b906f"></span>
#### Scenario 2: Password Hidden

For macOS, if the wired network password is not displayed in the client, follow the prompts to complete the connection. After the configuration is complete, you do not need to repeatedly enter the account and password for authentication each time you connect the network cable.


1. Click **Check the connection method.** 

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b935e52aade241b088bcc926e7d48b60~tplv-goo7wpa0wc-image.image) </span>

2. On the guide page, click the button to download the profile for macOS.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/500dff386eac4ad6b787f022dc3e8757~tplv-goo7wpa0wc-image.image) </span>

3. When the **Profile Downloaded** message appears, click **OK**. Open **System Settings** and search for profiles to locate **Device Management**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b13c999cca54c7c8a34fde1338d0c44~tplv-goo7wpa0wc-image.image) </span>


4. In **Device Management**, double\-click the downloaded **802.1x Wired** profile, then click **Install**.


<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/mfa-en-20260928/en-network-12-redacted.png) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb737dd64a4a411d87d864004136ad6c~tplv-goo7wpa0wc-image.image) </span>


5. After installation, verify that the file status is **Installed**. Then unplug and reconnect the network cable. The macOS system automatically authenticates the network.


<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/mfa-en-20260928/en-network-14-redacted.png) </span>

<span id="6392be8c"></span>
#### Notes

In **System Settings** \> **Network**, you can view the 802.1X configuration for the wired interface. If you click **Connect** here, a prompt appears asking you to enter the 802.1X account and password, and automatic authentication is not performed.

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/mfa-en-20260928/en-network-15-redacted.png) </span>

**Enable automatic connection** must be enabled here. It is enabled by default.

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/mfa-en-20260928/en-network-16-redacted.png) </span>

After the password is reset, you need to generate and install a new profile.

<span id="364a1403"></span>
### Windows

On Windows, connect your computer to a wired network port, go to **Network** \> **Wired**, and click **Connect**. SealSuite authenticates automatically. You do not need to enter credentials in a system dialog. To reconnect later, click **Connect** again. A "Wired network configuration successful" prompt confirms that you are connected.

If a Windows system pop\-up window appears, click **Cancel** or close it. This does not affect the normal use of wired network configuration in SealSuite. If the network disconnects during use, click **Connect** again to reconnect.

<span id="205d281a"></span>
## Guest Wi\-Fi

The desktop client supports Guest Wi\-Fi. Click **Overview** \> **Toolbox** \> **Guest Wi\-Fi** to apply for Guest Wi\-Fi.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/901728faf6cb402c9be50d2c772dba36~tplv-goo7wpa0wc-image.image) </span>

On the **Guest Wi\-Fi** page, click **Apply for guest Wi\-Fi**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94953edd22db4b2bb203323a1b3afca8~tplv-goo7wpa0wc-image.image) </span>

Enter the guest’s phone number and visit time, and select SMS or QR code as the network access method. The guest account is valid only within the validity period. After the validity period expires, you need to apply for guest Wi\-Fi again.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb3b5a2aeef74df39d30653a81b24a54~tplv-goo7wpa0wc-image.image) </span>
