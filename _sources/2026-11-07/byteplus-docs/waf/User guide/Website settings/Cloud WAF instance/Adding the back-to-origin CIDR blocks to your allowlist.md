---
title: "Adding the back-to-origin CIDR blocks to your allowlist"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/Modifying_the_DNS_record"
---

After your business is integrated with WAF, all requests are forwarded to the origin server through the back\-to\-origin CIDR blocks of WAF. This will increase the number of requests on each back\-to\-origin IP address, which may easily trigger false positives or rate limiting policies. Consequently, it is essential to allow access from the back\-to\-origin CIDR blocks of WAF.

<span id="d62e6974"></span>
## Background information


* **Before integrating your domain names with WAF**

   Before integrated with WAF, your business requests are relatively scattered under normal circumstances, and no IP address will be overloaded with requests. If a firewall is configured or security software is installed on the origin server, these normal requests will not be blocked or rate\-limited.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/81e8da63b95747bca6485ae19f85466f~tplv-goo7wpa0wc-image.image) </span>


* **After integrating your domain names with WAF**

   After your domain name is added to WAF, all your business requests will be returned to your origin server through the back\-to\-origin IP addresses of WAF. Since the back\-to\-origin IP addresses of WAF are fixed and limited, the number of requests on each IP address will increase. If the origin server has a firewall or security software installed, the WAF's back\-to\-origin IP addresses may be identified as attack sources, triggering security policies and causing back\-to\-origin requests to be mistakenly blocked or rate\-limited.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9eacf4dd2bc946b5b0c961882a80d233~tplv-goo7wpa0wc-image.image) </span>

<span id="a78e868d"></span>
## Prerequisites

You have added the domain name to be protected to the Cloud WAF instance. For related operations, see [Adding a domain name to a Cloud WAF instance](https://docs.byteplus.com/docs/waf/Allowing_back-to-origin_CIDR_blocks).

<span id="143ccac3"></span>
## Procedure


1. Log in to the [BytePlus Web Application Firewall Console](https://console.byteplus.com/waf).

2. In the top menu bar, select **Asia Pacific (Johor)** , \*\*\*\* the region where your cloud WAF instance is located.

3. On the left\-side navigation pane, select **Website settings**.

4. Click the domain name to view details.

5. Copy the back\-to\-origin CIDR blocks.

6. Proceed to the origin server's firewall, access control list (ACL), or any other security software, and add the back\-to\-origin CIDR blocks to the allowlist.


<span id="2d265847"></span>
## What to do next

After allowing the back\-to\-origin CIDR blocks, you need to verify if the forwarding rule has taken effect and ensure that traffic can be forwarded normally through WAF. For more details, see [Verifying the configurations of your domain name](https://docs.byteplus.com/docs/waf/Verifying_website_settings).
