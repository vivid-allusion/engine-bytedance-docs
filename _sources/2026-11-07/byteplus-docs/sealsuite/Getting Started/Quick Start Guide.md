---
title: "Quick Start Guide"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/quickstart"
---

<span id="6ed61c4f"></span>
# Introduction

To quickly set up a test environment for SealSuite, this guide provides step\-by\-step instructions for the most common initial configurations. By following this guide, you will configure core functionalities including user and department creation, VPN access, endpoint security policies (DLP, Watermark, Device Baseline), and network settings for Wi\-Fi and SD\-WAN, enabling you to begin testing immediately. The guide assumes that you have basic knowledge of Linux operating systems.

After completing each basic configuration session, you can start testing the SealSuite functions accordingly. During the testing process, if you encounter any issues, you can refer to the official SealSuite documentation for clarification. If you need further assistance, please contact the SealSuite support team.

<span id="8de47c2c"></span>
# Prerequisite


1. Login to the SealSuite admin portal. (SaaS or On\-prem version)


Admin Reference Guide: https://www.sealsuite.com/docs/admin\-manual/


2. SealSuite Client installed into the testing PC.


(Configuration changes might take up to 10 mins to reach to your client side)

Latest Client Download Link: https://www.sealsuite.com/download/


3. Get your testing tenant ID ready to login to the client.


<span id="b794cfae"></span>
## Topology for the VPN/Radius nodes mentioned in this guide

Both VPN and Radius Server will need to reach SealSuite Server via port 49900 to pull the latest configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0d8ebb0f392443da091214a34ec4b0b~tplv-goo7wpa0wc-image.image" width="2204px" /></div>


<span id="79bdf875"></span>
# Create Users & Departments

You can add users manually for testing:


1. In the SealSuite Admin Console: Identity \- Users & Department click Add Member


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa0e382ba89d40c9a4f6510adea011fb~tplv-goo7wpa0wc-image.image" width="2810px" /></div>



2. Enter a name, phone number or email address, assign a role (optional), and click Confirm.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1bb62e5900dd40fd86537d6a279d92b2~tplv-goo7wpa0wc-image.image" width="1556px" /></div>



3. Get the initial password from the admin portal and login to the SealSuite Client.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f6d497f9ef7a460f9a5252b5841e7e73~tplv-goo7wpa0wc-image.image" width="1888px" /></div>


<span id="06f0281e"></span>
# VPN Configuration


1. Preparation:

   * The configured VPN ports must be reachable from both SealSuite Server and SealSuite Client.

   * Prepare a Linux server for VPN server node installation. Refer to the deployment guide for the VPN Server specs.

2. Go to "VPN Management" \- "VPN Gateway", click "Add VPN Gateway" in the upper right corner, and follow the steps to configure and deploy the node.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ca587988e5d4d9e92be3f5bf42e8e28~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0eab66a9ce334f488afee784c8c0cd69~tplv-goo7wpa0wc-image.image) </span>


3. In "VPN Management" \- "Access Control Rules", select "Default Open" mode and configure relevant resources and policies if required.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/66252b082858471ab0a2f6d00f5a9524~tplv-goo7wpa0wc-image.image" width="2850px" /></div>



4. Open SealSuite Client and try to connect to the VPN nodes you have created.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/66a9f13875d8423ba04c0b5d16ecc359~tplv-goo7wpa0wc-image.image" width="778px" /></div>



5. Once the VPN is connected, try to ping/telnet some known internal resources to confirm the connectivity.


Your device should now have the same network access as the VPN server.

<span id="e211e145"></span>
## Two different modes:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/46022aae41fc48c0989576bd8725f968~tplv-goo7wpa0wc-image.image" width="1498px" /></div>


**Full Tunnel Mode:** 


* All device traffic will be routed through the VPN tunnel.

* This ensures that all data remains encrypted for optimal security.

* Please note that this mode might potentially increase the load on VPN gateways.


**Split Tunnel Mode:**  (This can be configured in VPN \-\> Advanced Settings)


* Only traffic to the configured sites will be routed through the VPN tunnel

* Only the configured site\-related data will be encrypted.

* It saves network bandwidth, reduces the load on VPN gateways, and enhances the overall network experience for users.


<span id="ee37d1bc"></span>
# Endpoint Security Configuration

<span id="caac0914"></span>
## DLP


1. Security \- DLP \- Policy Management, click "New Policy", select "Audit Policy" and then click "create a rule"


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4298dac344a142c59897d13f71dd218c~tplv-goo7wpa0wc-image.image" width="2834px" /></div>



2. Follow these steps to complete the policy configuration:

   1. Add policy name.

   2. Select a strategy priority (e.g., 100).

   3. Click "Detect Outgoing Method" to view detailed content, expand and select the apps and websites for which you want to monitor outgoing data.

   4. Click "Add Sensitive Data" \- search and select "Certificate related documents".

   5. Select the user scope (Apply to the test user).

   6. Click Confirm to save this rule.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/865fbab4f8594d5db2b1216192fe2560~tplv-goo7wpa0wc-image.image" width="2832px" /></div>



3. Log in to the machine with the SealSuite Client, and try to upload a certificate file using one of the defined apps or websites.


<span id="12c9c212"></span>
## Watermark


1. Log in to the Admin portal, go to Security \- DLP \- Watermark \- Policy Management, click "New Policy" on the upper right corner and fill in the policy content.

   1. Enter a policy name.

   2. Select a strategy priority (e.g., 100).

   3. Select watermark type \- Visible watermark.

   4. Preview and adjust the watermark opacity, font, rotation angle and content.

   5. Choose the scope and click "Add".


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67c51c627a724cdf91de0281f50c4be6~tplv-goo7wpa0wc-image.image" width="1000px" /></div>



2. Log in to the SealSuite client to check the configured watermarks on the client and web pages.


<span id="9b6f95b5"></span>
## Device Baseline


1. Device Baseline \- Scanning Configuration \- Process Scanning Items \- Add Process Group, define your own process here. (You might wish to refer to this detailed guide: https://docs.byteplus.com/en/docs/sealsuite/docs\-configure\-detection\-items)

   1. e.g. You can define [Beijing Volcengine Technology Co., Ltd.] as the Digital Signature and [corplink\-service.exe] for the Process Name.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ebc5339336e04132b1ad63b9da1b09cc~tplv-goo7wpa0wc-image.image" width="2472px" /></div>



2. Device \- Device Control \- Device Baseline \- Policy Management, Click "New Policy"


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf0f00fa96d34c7a9a2f0d31444f3e78~tplv-goo7wpa0wc-image.image" width="2420px" /></div>



3. Select the baseline content to be tested as below:

   1. Application Security Scanning \- configure [WeChat] as mandatory app, and [QQ] as the non\-compliant app. (you can define your own mandatory app under Device Baseline \- Scanning Configuration \- Application Scanning Items \- Add New Application)

   2. Process Security Scanning \- configure [corplink\-service.exe] that you just created as the Required process group

   3. Select "Scan on Triggers", check [Login] [Open SealSuite].

   4. Choose the scope and click "Confirm"


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c02e96a1cdf64c97af70fde0d13ebfd7~tplv-goo7wpa0wc-image.image" width="2830px" /></div>



4. Log in to SealSuite Client and trigger the scan.


<span id="879695b6"></span>
# Client Configuration


1. Settings \- General Settings \- Client Settings.

2. Enable both Prevent User Logouts and Application anti\-uninstall.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fcccd1c6f794ae1bd25a67a4dfe4618~tplv-goo7wpa0wc-image.image" width="2450px" /></div>



3. Ensure the scope includes the test user/machine

4. Log in to SealSuite Client and wait for 10 minutes

5. Try to log out SealSuite Client.

6. Try to uninstall SealSuite Client.


<span id="d9104616"></span>
# Wi\-Fi Configuration


1. Network \- Wi\-Fi Management \- Staff Network, click "Start Configuration" and select the authentication protocol 802.1X.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27bcdb3493b141e3a715b48aa708404e~tplv-goo7wpa0wc-image.image" width="2436px" /></div>



2. Deploy and configure the Radius Server.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71f919f842014969a715c0e2db87db65~tplv-goo7wpa0wc-image.image" width="2042px" /></div>



3. Add an AC/AP or switch, and use 0.0.0.0 and 00:00:00:00:00:00 as the wildcard IP and MAC address, respectively.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ba6c0741977a4af28337a0dc570c9f32~tplv-goo7wpa0wc-image.image" width="1042px" /></div>



4. Setting up Wi\-Fi SSID. (This must be the same SSID that is set up on your AC/AP).

5. Set up the AP/AC to point authentication to the deployed Radius Server via port 1812 and accounting to port 1813.

6. Go to "Wi\-Fi Management" \- "Staff Network" \- "Authorization", create a rule to allow all employees access this SSID.

   1. If you don't have any VLAN setup on your SSID, you can just key in any integer value for Tunnel\-Pvt\-Group\-ID.

   2. Select the Scope and click "Save"


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3dca41c964db4393889be18e85c3cb58~tplv-goo7wpa0wc-image.image" width="2320px" /></div>


<span id="4540f991"></span>
# SD\-WAN Configuration


1. SD\-WAN \> Branch Gateway, Click "Add Branch", and select "software".

2. Enter the "Branch Name" and select the "Branch Gateway Type".

3. Choose "Not Applicable" for SNAT and set up the "Branch Network Segment" for your IP resources that you want to access.

4. Set up a DNS proxy if you need to point to your own DNS, or it will use our SealSuite central DNS.

5. Click "Next Step".


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d09c4a83ead345d78a7e61945ff66b05~tplv-goo7wpa0wc-image.image" width="1944px" /></div>



6. Follow the steps to copy and paste the commands to deploy the server.

   1. Replace the vcpe package with our latest stable version: [https://cdn.isealsuite.com/component/vcpe/feilian_vcpe_v2.2.16_b1307_13d04e.tar.gz](https://cdn.isealsuite.com/component/vcpe/feilian_vcpe_v2.2.16_b1307_13d04e.tar.gz)

7. Click "Next Step" to perform the Connectivity test.

8. Navigate to VPN \> VPN Gateway, click the "Cloud VPN" and change the status to "Online"

9. You can now log in to your client and connect to this "Cloud VPN" for testing the SD\-WAN functions.
