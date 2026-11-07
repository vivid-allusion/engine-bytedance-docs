---
title: "Configuring client"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Configuring-the-client"
---

This topic introduces how to configure common SSL\-VPN clients (Linux, Windows, Mac, iOS).

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Download the SSL client certificate: **certs_vsc\-2feuoxsyxxxxxybovbq.zip**. For procedure, see [Creating and downloading an SSL client certificate](https://docs.byteplus.com/en/docs/vpn/Creating-and-downloading-an-SSL-client-certificate).

<span id=".5pON5L2c6K-05piO"></span>
## Instructions


* This documentation uses OpenVPN Connect for Windows, Mac, and iOS client connection configurations. If you use Pritunl to connect, first [modify the SSL client certificate](https://docs.byteplus.com/en/docs/vpn/modify-the-ssl-client-certificate).

* Currently, only iOS clients logged in with foreign Apple IDs can download OpenVPN Connect.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


<Tabs>
<Tab zoneid="Lr3lnFxOau" title="Linux client">
<TabTitle>Linux client</TabTitle>

1. Open the command line window on the Linux client.

2. Run the following command to install the OpenVPN client.

   * CentOS

      ```Plain Text
      sudo yum update
      sudo yum install epel-release
      sudo yum install openvpn
      ```
      

   * Ubuntu

      ```Plain Text
      sudo apt-get update
      sudo apt-get install -y openvpn
      ```
      

3. Upload the SSL client certificate to the Linux client’s `/etc/openvpn/conf/` directory. For data upload methods, see [Local data upload overview](https://docs.byteplus.com/en/docs/ecs/Local-data-uploading-overview).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the Linux client does not have the <code>/etc/openvpn/conf/</code> directory, you can create it manually.   </div>
   

4. Use the command `unzip certs_vsc-2feuoxsyxxxxxybovbq.zip` to unzip the certs_vsc\-2feuoxsyxxxxxybovbq.zip file in the current `/etc/openvpn/conf/` directory.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In practice, replace <code>certs_vsc-2feuoxsyxxxxxybovbq.zip</code> in the command with the actual client certificate archive name obtained.   </div>
   

5. Run the following command to start the remote SSL VPN connection.

   ```Plain Text
   openvpn --config /etc/openvpn/conf/config.ovpn --daemon
   ```
   


<span id=".V2luZG93c-WuouaIt-errw=="></span>
### 


</Tab>
<Tab zoneid="hqQZkH7wtB" title="Windows client">
<TabTitle>Windows client</TabTitle>

1. Upload the SSL client certificate to the Windows client. For data upload methods, see [Local data upload overview](https://docs.byteplus.com/en/docs/ecs/Local-data-uploading-overview).

2. Use any decompression tool to unzip the client certificate package certs_vsc\-2feuoxsyxxxxxybovbq.zip, and place the extracted files in the specified location. Here, the demonstration places the extracted files on the desktop.

3. Open the Windows client browser. Enter `https://openvpn.net/client/` in the address bar to visit the OpenVPN official website. Then click the **Download OpenVPN Connect for Windows** button to download and install OpenVPN Connect.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the Windows version is Win10 or above, please follow the steps below:   </div>
   

   1. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Install the latest version of OpenVPN. Download link: <a href="https://openvpn.net/community-downloads/">https://openvpn.net/community\-downloads/</a>.   </div>
   

   2. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Manually add a configuration entry in the client certificate configuration file: <code>windows-driver wintun</code>.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b1ecd7d78108e836d816f4a26293d327.png) </span>

4. After installing OpenVPN Connect, double\-click to open it, select **Import Profile** from the upper left menu, then click the **FILE** tab.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a4fcd1fcf2c4b8878b8f269971dbabc8.png) </span>

5. Drag the `.ovpn` file from the extracted client certificate files on the desktop into the **FILE** tab.

6. Click the **CONNECT** button in the lower right corner to start the remote SSL VPN connection.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_39fcf6035a9096cc8e4a1d0c0717d185.png) </span>


</Tab>
<Tab zoneid="tTlY1fk0yc" title="Mac client">
<TabTitle>Mac client</TabTitle>

1. Upload the SSL client certificate to the Mac client. For methods, see [Local data upload overview](https://docs.byteplus.com/en/docs/ecs/Local-data-uploading-overview).

2. Use any extraction tool to unzip the client certificate package certs_vsc\-2feuoxsyxxxxxybovbq.zip, and place the extracted files in the designated location. This example places the files on the desktop.

3. Open the Mac client browser and enter `https://openvpn.net/client/` in the address bar to go to the OpenVPN official website. Click the **Download OpenVPN Connect for Mac** button to download and install **OpenVPN Connect**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b2060838bd5fd852e2c3571241c8a1f4.png) </span>

4. After installing OpenVPN Connect, double\-click to open it, select **Import Profile** from the upper left menu, then click the **FILE** tab.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cc23160d94cbc9ff9280c465923f4102.png) </span>

5. Drag the `.ovpn` file from the extracted client certificate files on the desktop into the **FILE** tab.

6. Click the **CONNECT** button in the lower right corner to start the remote SSL VPN connection.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_49ef3b42ccb40db3866a54b7f6cc9b64.png) </span>





</Tab>
<Tab zoneid="DZYUs06IAe" title="iOS client">
<TabTitle>iOS client</TabTitle>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The OpenVPN Connect used in this example can currently only be downloaded by iOS clients logged in with foreign Apple IDs.</div>



1. Process the client certificate file.

   * If you use the certs_vsc\-2fen9va5qgpxxxxxx67cjgq.ovpn file, proceed to the next step directly.

   * If you use the certs_vsc\-2feuoxsyxxxxxybovbq.zip file, first extract the client certificate archive using any decompression tool, then merge the extracted certificate files into one. For details, see [merging certificate files](https://docs.byteplus.com/en/docs/vpn/Merging-client-certificates).

2. Upload the merged file to the iOS client via cable or other methods.

3. In the iOS client's App Store, search for **OpenVPN Connect**, then download the app to the iOS client.

4. Open **OpenVPN Connect**, then select **Import Profile \> FILE**.

5. Upload the merged file from step 2 to **FILE**, then click the **CONNECT** button to initiate the remote SSL VPN connection.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_49ef3b42ccb40db3866a54b7f6cc9b64.png) </span>


</Tab>
</Tabs>


<span id=".5ZCO572u5pON5L2c"></span>
## What to do next

[Test connectivity](https://docs.byteplus.com/en/docs/vpn/Testing-connectivity1)
