---
title: "Modify DNS resolution"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Modify_DNS_resolution"
---

After domain configuration is complete, you need to resolve the domain to the CNAME address provided by the LLM Application Firewall. This will route the traffic of the protected service to the LLM Application Firewall instance for protection.

<span id="4a0d9371"></span>
## Prerequisites

You have verified that the LLM Application Firewall configuration is valid, and forwarding is now functioning normally. For related operations, refer to [Verify forwarding configuration](https://docs.byteplus.com/docs/LLM-Application-Firewall/Verify_forwarding_configuration).

<span id="3d0af1dd"></span>
## Steps


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/).

2. In the top bar, select the instance's region.

3. Select **Asset management** in the left navigation.

4. Click **Advanced filter**, and select **Traffic integration** as the access method.

5. Click the corresponding domain name in the list to view domain name details.

6. On the **Basic information** page, obtain the CNAME value.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/f9389da7111c464398d18f916e135ba5) </span>

7. Go to your domain's DNS provider and add a CNAME record that points the protected domain to the CNAME of the LLM Application Firewall.

8. Enter the protected domain name in a browser to verify that it is accessible.
