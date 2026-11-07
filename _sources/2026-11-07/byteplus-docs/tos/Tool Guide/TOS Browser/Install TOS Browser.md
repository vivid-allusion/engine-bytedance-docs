---
title: "Install TOS Browser"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Install-tos-browser"
---

This article describes the download links and the steps to install and upgrade TOS Browser.

<span id=".5LiL6L295Zyw5Z2A"></span>
## Download links


|**Operating system** |**Operating system requirements** |**Download link for installation package** |
|---|---|---|
|Windows |* Windows 7 Pro SP1 64\-bit<br><br>* Windows 10 Pro 64\-bit<br><br>* Windows Server 2016 standard 64\-bit |[TOS Browser-win64](https://tos-tools.tos-ap-southeast-1.bytepluses.com/windows/TOS_Browser_BytePlus_Public-win32-x64.exe) |
|macOS |* Mac OS X10.13.3 (distinguishes between Intel and Apple Silicon)<br><br>* Mac OS X10.15.7 (distinguishing between Intel and Apple Silicon)<br><br><br>&nbsp;<br><br>The macOS system cannot open unverified developer apps by default. If the installation of TOS Browser prompts that the developer cannot be verified, you need to modify the system settings. For details, see [When installing TOS Browser on a macOS system, it prompts that the developer cannot be verified](https://docs.byteplus.com/en/docs/tos/Tools#64c5af56). |[TOS Browser-darwin-intel](https://tos-tools.tos-ap-southeast-1.bytepluses.com/darwin/TOS_Browser_BytePlus_Public-darwin-x64.dmg)<br><br>[TOS Browser-darwin-arm64](https://tos-tools.tos-ap-southeast-1.bytepluses.com/darwin/TOS_Browser_BytePlus_Public-darwin-arm64.dmg) |
|Linux |Ubuntu 18.04 |The Linux version of TOS Browser is in beta testing. Contact your account manager if you want to use it. |


<span id=".5pu05paw5pel5b-X"></span>
## Release notes


|**Version number** |**Version type** |**Release date** |**Update instructions** |
|---|---|---|---|
|1.11.4 |Latest version |2025\-11\-24 |* Optimize copy operations to improve copy speed.<br><br>* Optimize move operations by enabling the RenameObject feature: once enabled, the system prioritizes invoking the RenameObject interface to perform moves, significantly boosting move performance. For details, see [Enabling RenameObject](https://docs.byteplus.com/docs/tos/Use-renameobject).<br><br>* Supports switching the TOS Browser UI language. For details, see [Switch Session and Language](https://docs.byteplus.com/docs/tos/Log-in-to-tos-browser).<br><br>* Supports accessing object storage via an HTTP proxy. For details, see [Use HTTP Proxy](https://docs.byteplus.com/docs/tos/Log-in-to-tos-browser). |
|1.11.2 |Historical version |2025\-09\-03 |Optimize version stability. |
|1.9.0 |Historical version |2024\-10\-25 |First release. Support for creating buckets, uploading files, and other functions. For a list of supported features, see [Overview](https://docs.byteplus.com/docs/tos/Overview3). |


<span id=".5a6J6KOFLXRvcy1icm93c2Vy"></span>
## Install TOS Browser


1. Download the corresponding installation package based on your operating system.

2. Double\-click the installation package and follow the prompts to install.


<span id=".5Y2H57qnLXRvcy1icm93c2Vy"></span>
## Upgrade TOS Browser

On the TOS Browser login page, the system automatically checks for the latest version. If a new version is available, it will prompt you to update.

You can also manually check for updates and upgrade TOS Browser by following these steps:


1. [Log in to TOS Browser](https://docs.byteplus.com/docs/tos/Log-in-to-tos-browser).

2. Click the circular button in the upper\-right corner.

3. In the pop\-up dialog, upgrade to the corresponding version.

   * **Install the latest version**: click **Check for updates**, then after the installation package downloads, click **Restart to upgrade.** 

   * **Automatic update installation**: after selecting **Install updates automatically**, TOS Browser will automatically install the latest version when you next restart the app.
