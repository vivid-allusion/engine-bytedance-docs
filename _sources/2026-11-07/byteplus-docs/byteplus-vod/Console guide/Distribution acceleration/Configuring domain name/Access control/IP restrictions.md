---
title: "IP restrictions"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-ip-restrictions"
---

To control access and enhance the security of your VOD content, you can configure IP restrictions in the BytePlus VOD console. This guide provides step\-by\-step instructions for setting up IP allowlists and blocklists for your **Playback**, **Image**, and **Custom\-origin domain names**.

<span id="操作步骤"></span>
## Configuring the IP allowlist and blocklist


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a specific space.

2. Click **Distribution acceleration** \> **Domain names** on the left navigation bar.

3. Depending on the type of your domain name, click the **Playback domain name**, **Image domain name**, or **Custom\-origin domain name** tab.

4. Find the domain name you want to configure and click the **Configure** button in the **Action** column.

5. Click the **Access control** tab.

6. Click the **Modify** button at the bottom of the page.

7. Under **IP allowlist and blocklist**, switch the **Status** toggle and configure the IP restrictions:

   
   |**Configuration** |**Description** |
   |---|---|
   |Type |This configuration has the following options:<br><br><br>* **Allowlist**: Specifies from which IP addresses requests are allowed to access your site. Allowlists can be configured when you only want to allow requests from certain IPs.<br><br>* **Blocklist**: Specifies from which IP addresses requests are not allowed to access your site. blocklists can be configured when you only want to block requests from certain IPs.<br><br><br>If the source IP of a request matches the blocklist or does not match the allowlist, CDN will reject the request and return a 403 response status code. |
   |IP |Enter one or more IP addresses or CIDR network segments. IP addresses and network segments can be in IPv4 and IPv6 formats. You can enter up to 1,000 IP addresses and network segments. Each IP address and network segment needs to be entered on a separate line. The configuration cannot exceed 30,000 characters in length. |
   

8. Click **Save**.


<span id="配置示例"></span>
## Configuration example

<span id="白名单配置"></span>
### **Allowlist**


* IP Addresses:

   192.168.3.0/24

   2001: db8::

* Purpose: Allows requests only from IP addresses in the range of 192.168.3.1 \- 192.168.3.254 and from 2001:db8::.


<span id="黑名单配置"></span>
### **Blocklist**


* IP Address: 2001:db8::/126

* Purpose: Blocks requests from IP addresses in the range 2001:0db8:: \- 2001:0db8::0003.
