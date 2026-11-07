---
title: "Adding a CDN domain name to a WAF instance"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/Adding_a_CDN_domain_name_to_a_WAF_instance"
---

If your domain is integrated with BytePlus CDN service, CDN servers, rather than the origin servers process user requests directly. The WAF instance provides near\-source protection at CDN edge nodes, inspecting traffic flowing through CDN to ensure your business security. This document describes how to add a domain connected to BytePlus CDN to a WAF instance for protection.

<span id="7e6686fc"></span>
## How CDN works

The main principle of how CDN works is to add a new layer of network architecture to the existing network. It distributes the content from the origin server to different network nodes, enabling users to obtain the required content nearby, thus improving the speed at which users access websites. If the file requested by a user is not cached by the CDN, the CDN will first request the file from the origin server. After receiving the file from the origin server, the CDN will cache it. Subsequently, if subsequent requests for this file are received, the CDN will not request the file from the origin server again, but directly return the cached file to the user. This reduces the traffic on the origin server, thereby lowering the bandwidth costs for server hosting and the probability of server failures.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/560cce23e52e4f499c87b89c82b66873~tplv-goo7wpa0wc-image.image) </span>

<span id="0442ad26"></span>
## Associate WAF and CDN for protection

The association of WAF and CDN refers to integrating a domain name that has been added to CDN with WAF. When traffic flows through CDN, it will also go through the WAF inspection. This approach can not only improve the access speed but also conduct in\-depth inspection and cleaning of the traffic. WAF will block or allow requests according to the detection rules you configure.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67af50e938d34fd1ac874ac8b9c151b9~tplv-goo7wpa0wc-image.image) </span>

<span id="95cc5631"></span>
## Prerequisites


* You have already created a Cloud WAF instance. For more details, see [Creating a cloud WAF instance to protect your domain names](https://docs.byteplus.com/docs/waf/Creating_a_Cloud_WAF_instance).

* The domain name requiring protection has been added to BytePlus CDN. For details, see [Adding a domain name](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-add-your-domain-name).


<span id="d926ed60"></span>
## Procedure


1. Log in to the [BytePlus Web Application Firewall Console](https://console.byteplus.com/waf).

2. In the top menu bar, select **Edge(CDN**), the region where your WAF instance is located.

3. On the left\-side navigation pane, select **Website settings**, and then click **Add website**.

4. Select the domain name you want to add.

   The list automatically displays the domain names that have been added to the CDN service under the current account.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/11b67df11c294183872e986fb3b3e683~tplv-goo7wpa0wc-image.image) </span>

5. Set related parameters.

   * **Keep consistent with other products**: \*\*\*\* Project management is a resource management method provided by BytePlus to help keep resources independent and maintain data security. The default is to associate the project authorized by the current account, and it cannot be modified.

      * The main account can view all projects. After switching the project at the top of the console to **All Resources**, you can adjust the project settings.

      * If you select **Keep consistent with other products**, these domain names will be synchronized when other resources in the same project change (for example, transferred out of the project or policy permissions change).

   * **Log collection**: To ensure complete log data collection, we recommend that you enable the log service for the added domain name.

   * **Log all headers**:

      * If disabled, only common header fields will be logged.

      * If enabled, all header fields in the traffic will be logged, which may significantly increase the usage of log storage.

6. Click **OK**.

   After the domain name is added, you can view the domain name information on the **Website settings** page.


<span id="8c2f742c"></span>
## What to do next

Set up protection policies for accessed domains to achieve security protection that meets actual business scenarios.
