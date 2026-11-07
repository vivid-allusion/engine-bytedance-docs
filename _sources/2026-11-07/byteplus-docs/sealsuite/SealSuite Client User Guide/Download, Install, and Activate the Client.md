---
title: "Download, Install, and Activate the Client"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/download-install-and-activate-the-client"
---

This document guides you through downloading, installing, activating, and switching enterprise environments in the SealSuite client.

<span id="44a01ec9"></span>
# Download the Client

You can obtain the installation package in either of the following ways based on your enterprise administrator’s requirements.

<span id="ccc85a1c"></span>
## Method 1: Download from the Portal Page

This method applies to users who need to view account status or change the initial password.


1. **Access the portal**: Open a browser and enter the portal domain provided by your enterprise in the address bar.

2. **Verify your identity**: Enter your registered phone number or email address, and enter the initial password.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/39179f93d607443aac0b4625c62ca5fc~tplv-goo7wpa0wc-image.image" width="400px" />   </div>
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If secondary verification is enabled, enter the phone or email verification code you received. If you are prompted to enter a <strong>Dynamic Password</strong>, view it on the mobile client where you have logged in to SealSuite, or contact the administrator to obtain a backup dynamic password.   </div>
   

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e272db9d0a264d12bdc6374acf3ca714~tplv-goo7wpa0wc-image.image" width="500px" /></div>



3. **Change the initial password**: The first time you log in, we recommend changing the password as prompted. You can also change it after entering the portal by choosing **Toolbox** \> **Security**.

4. **Download the client**:

   1. In **Toolbox** on the portal page, click the **Download client** icon.

   2. On the client download page, select the installation package that matches your operating system. **Note**: Record the **Enterprise identification Code** displayed on this page. You need it for subsequent activation.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50ddb7757d7849979e020340510b941f~tplv-goo7wpa0wc-image.image) </span>


<span id="bc986d49"></span>
## Method 2: Download from a Self\-service Link

If the administrator directly provides a self\-service installation link, visit the link and select the client for your operating system to download it.

<span id="2a22282d"></span>
# Install the Client

<span id="fa0a2f82"></span>
## Windows and macOS Devices


1. Double\-click the downloaded installation package, such as an `.exe`, `.pkg`, or `.dmg` file.

2. Follow the installation wizard to complete the installation.


<div style="text-align: center">
macOS</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed2bc7fba9c44bb886bd0a2717b84242~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
Windows</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70290902a52c4676a50712ffa4c7cc07~tplv-goo7wpa0wc-image.image) </span>

<span id="576a247e"></span>
## Linux Devices

SealSuite supports multiple Linux distributions. We recommend confirming system version compatibility before installation.

<span id="9e4046a0"></span>
### Compatibility


|Distribution |Recommended Version |
|---|---|
|Ubuntu |18.04 or later |
|Debian |10 |
|CentOS |8 |
|Deepin |20.2.1 |
|Manjaro |22.0.5 |


<span id="4983b358"></span>
### Installation Commands

Run the following commands based on your package manager. **Note**: Replace `{actual version}` in the commands with the actual file name of the downloaded file.


* **DEB package (Ubuntu / Debian / Deepin)** 

   * First\-time installation with automatic dependency resolution:`sudo apt install -y ./SealSuite_Linux_{actual version}.deb`

   * Overwrite update:`sudo dpkg -i SealSuite_Linux_{actual version}.deb`

   * Uninstall:`sudo apt autoremove -y vecorplink`

* **RPM package (CentOS)** 

   * First\-time installation with automatic dependency resolution:`sudo rpm -ivh --nodeps --force SealSuite_Linux_{actual version}.rpm`

   * Overwrite update:`sudo rpm -ivh --replacepkgs --nodeps SealSuite_Linux_{actual version}.rpm`

   * Uninstall:`sudo rpm -e veCorpLink`

* **Tar.gz package (Manjaro / general)** 

   1. Extract the package:`tar -zxvf SealSuite_Linux_{actual version}.tar.gz`

   2. Go to the extracted directory and install:`sudo make install && sudo make postinst`

   3. Uninstall: Go to the original installation directory and run: `sudo make uninstall`


<span id="5102fc92"></span>
### Install Wi\-Fi Connection Dependencies (Optional)

To use "one\-click Wi\-Fi connection" in SealSuite, make sure the related components are installed on your system.


* **Ubuntu/Debian:**  `sudo apt install dnsmasq-base network-manager libxtst6 libnss3 auditd libnss3-tools`

* **Fedora/CentOS:**  `sudo dnf install dnsmasq NetworkManager nss-tools`


<span id="d6cf4937"></span>
# Activate and Log In to the Client

After installation, you must verify the enterprise identification code before entering the login page.


1. **Start the client**: Open the SealSuite desktop client.

2. **Verify and activate**:

   * **Automatic verification**: The client usually attempts to automatically fill in and verify the enterprise identification code.

   * **Manual verification**: If the enterprise identification code is not automatically filled in, enter the enterprise identification code obtained from the download portal or provided by the administrator, and click **Verify activation**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/245b9e5fb9cd4f17be04b1a8becf3714~tplv-goo7wpa0wc-image.image" width="500px" /></div>



3. **Confirm information**: In the pop\-up window, confirm that the enterprise information is correct and click **Confirm.** 


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36ea578c10aa4601af05e05f1462d681~tplv-goo7wpa0wc-image.image" width="500px" /></div>



4. **Log in to your account**: After successful activation, enter your account and password, and secondary verification code if required, to log in.


<span id="28a6888d"></span>
# Advanced Operations: Manage Enterprise identification codes

<span id="afff124b"></span>
## Switch the Enterprise

If your enterprise environment changes, or you need to log in to another enterprise instance, perform the following steps:


1. **Log out of the current account**: If you have logged in, click Client **Settings** and select **Log out**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2598270c2ea4f33ad09a620dcba20ad~tplv-goo7wpa0wc-image.image" width="500px" /></div>



2. **Start switching**: On the login page or initial page, click **Switch Enterprise**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/952aad05fc6c456c948cfa004d8ae869~tplv-goo7wpa0wc-image.image" width="500px" /></div>



3. **Confirm clearing**: In the risk warning dialog box, click **Confirm**. This operation resets the current activation status.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/25fbcba9850f47b2b2fe6c1c87589ee4~tplv-goo7wpa0wc-image.image" width="500px" /></div>



4. **Reactivate**: Enter the new enterprise identification code and complete verification.
