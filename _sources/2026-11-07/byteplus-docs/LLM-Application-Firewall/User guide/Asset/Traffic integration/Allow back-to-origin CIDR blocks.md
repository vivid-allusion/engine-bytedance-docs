---
title: "Allow back-to-origin CIDR blocks"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Allow_back-to-origin_CIDR_blocks"
---

To prevent your origin server's security policies from mistakenly blocking traffic from the LLM Application Firewall after integration, you must add the firewall's back\-to\-origin IP addresses to your server's allowlist. This guide explains why this is necessary due to centralized traffic flow and provides step\-by\-step instructions on how to find and configure the correct IP addresses to ensure your service runs smoothly.

<span id="75a17298"></span>
## Background information


* Before integration

   Before you integrate the LLM Application Firewall, traffic to your application is typically distributed, and no single IP address is overloaded with requests. If your origin server uses a firewall or security software, this normal traffic is not blocked or throttled.

* After integration

   After you integrate the LLM Application Firewall, all requests are routed to your origin server from the firewall's back\-to\-origin IP addresses. Because these back\-to\-origin IP addresses are fixed and limited in number, the request volume from each IP increases. If your origin server uses a firewall or security software, it might identify the concentrated traffic from the LLM Application Firewall's IP addresses as an attack, causing legitimate requests to be blocked or throttled.


<span id="a510b255"></span>
## Steps

When you integrate a domain and submit the configuration parameters, the LLM Application Firewall displays its back\-to\-origin IP addresses. This section explains how to view the back\-to\-origin IP address range on the asset management page.


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/).

2. Select the region of the instance in the top bar.

3. Select **Asset management** from the left navigation.

4. Click **Advanced filter**, then set the access method to **Traffic integration**.

5. Click the corresponding domain name in the list to view domain name details.

6. On the **Basic Information** page, obtain the back\-to\-origin CIDR blocks.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/3bb62f44aa314dff82a2cd62d8f5dcf1) </span>

7. In the security software on your origin server, add all the back\-to\-origin IP addresses shown in the diagram to the allowlist.


<span id="4d225ffb"></span>
## What to do next

After adding the back\-to\-origin IP addresses to your allowlist, verify that the forwarding rules have taken effect to ensure that traffic is correctly routed through the LLM Application Firewall. For more details, see [Verify forwarding configuration](https://docs.byteplus.com/docs/LLM-Application-Firewall/Verify_forwarding_configuration).
