---
title: "Adding and configuring domain name"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-domain-name-configuring"
---

To accelerate video content delivery for your website, you need to add and configure a domain name in the BytePlus VOD console. This guide provides step\-by\-step instructions on adding your domain, configuring CNAME records, and setting up advanced options for playback, images, or custom origins.

<span id="def487a4"></span>
## Domain name types

BytePlus VOD supports three types of domain names:


* **Playback domain name**: This type of domain name is used to generate the playback address for audio, video, and subtitle files. It retrieves the content from the BytePlus VOD origin server.

* **Image domain name**: This type of domain name is used to generate the addresses for cover images, cover candidates, and snapshots. It retrieves the content from the BytePlus VOD origin server.

* **Custom\-origin domain name**: This type of domain name retrieves content from third\-party origin servers, rather than the BytePlus VOD origin servers. This feature is useful in flexible business scenarios where content needs to be fetched from different sources.


<span id="14c0eb71"></span>
## Prerequisites


* Ensure that you have enabled the BytePlus VOD service.

* Prepare a valid domain name.


<span id="a5a5289c"></span>
## Procedure

<span id="60b20c02"></span>
### Step 1: Add a domain name

In the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/), add a domain name based on your business needs. For detailed steps and parameters, refer to [Adding domain name](https://docs.byteplus.com/en/docs/byteplus-vod/docs-domain-name-management).

<span id="a99dc70e"></span>
### Step 2: Add a CNAME record

After you add a domain name in the BytePlus VOD console, a BytePlus VOD domain name will be automatically assigned to your domain name, and you can find it in the **CNAME** column in the domain name list. You must add a CNAME record for your domain name to point to the assigned BytePlus VOD domain name in the console of your domain service provider. For details, see [Adding CNAME record](https://docs.byteplus.com/en/docs/byteplus-vod/docs-configuring-cname). After the configuration takes effect, a green check mark icon is displayed in the **CNAME** column in the domain name list.

<span id="c95e5400"></span>
### Step 3: Enable VOD scheduling

Enable VOD scheduling to retrieve video playback URLs through the BytePlus VOD service for the domain. Follow these steps:


1. Log in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and navigate to your space.

2. Click **Distribution acceleration** \> **Domain names** on the left navigation bar.

3. Select the domain name type by clicking the tabs.

4. Under the relevant tab (**Play domain name**, **Custom\-origin domain name**, or **Image domain name**), find your domain name and enable the **VOD scheduling** switch.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5458e2e6b2640c18af5cf8e4ee9cce6~tplv-goo7wpa0wc-image.image) </span>


<span id="f1e38b93"></span>
### Step 4: Configure the SSL certificate

By default, the domain names you add to the BytePlus VOD console use the HTTP protocol. If you want to use HTTPS for encrypted data transmission, you must configure SSL certificates for domain names. You can upload your SSL certificate to [BytePlus Certificate Center](https://www.byteplus.com/en/product/certificate-center) and then configure it in the VOD console. For detailed instructions, see [Configuring SSL certificate](https://docs.byteplus.com/en/docs/byteplus-vod/docs-configuring-ssl-certificates).

<span id="24c81486"></span>
### Step 5: Configure the domain name

BytePlus VOD offers options for access control, origin configuration, protocol settings, cache configuration, and more. Each acceleration domain type supports different configuration options outlined in the table below.


|Domain name type |Configuration option ||
|---|---|---|
|Playback domain name |Access control |* [Referer restrictions](https://docs.byteplus.com/docs/byteplus-vod/docs-referer-restrictions)<br><br>* [IP restrictions](https://docs.byteplus.com/docs/byteplus-vod/docs-ip-restrictions)<br><br>* [Anti-hotlinking with timestamp](https://docs.byteplus.com/docs/byteplus-vod/docs-timestamp-)<br><br>* [URL signing overview](https://docs.byteplus.com/docs/byteplus-vod/docs-url-authentication-overview)<br><br>* [UA restrictions](https://docs.byteplus.com/docs/byteplus-vod/docs-ua-restrictions)<br><br>* [Origin restrictions](https://docs.byteplus.com/docs/byteplus-vod/docs-origin-restrictions)<br><br>* [Remote authentication](https://docs.byteplus.com/docs/byteplus-vod/docs-remote-authentication) |
||Origin\-pulling configuration |* [Redirect follow](https://docs.byteplus.com/docs/byteplus-vod/docs-redirect-follow) |
||HTTP configuration |* [HTTP/2](https://docs.byteplus.com/docs/byteplus-vod/docs-http-2)<br><br>* [Protocol redirect](https://docs.byteplus.com/docs/byteplus-vod/docs-force-redirect)<br><br>* [Supported TLS versions](https://docs.byteplus.com/docs/byteplus-vod/docs-supported-tls-versions) |
||Advanced configuration |* [HTTP response headers](https://docs.byteplus.com/docs/byteplus-vod/docs-http-response-headers)<br><br>* [Video seeking](https://docs.byteplus.com/docs/byteplus-vod/docs-video-seeking) |
|Custom\-origin domain name |Access control |* [Referer restrictions](https://docs.byteplus.com/docs/byteplus-vod/docs-referer-restrictions)<br><br>* [IP restrictions](https://docs.byteplus.com/docs/byteplus-vod/docs-ip-restrictions)<br><br>* [URL signing overview](https://docs.byteplus.com/docs/byteplus-vod/docs-url-authentication-overview)<br><br>* [UA restrictions](https://docs.byteplus.com/docs/byteplus-vod/docs-ua-restrictions)<br><br>* [Origin restrictions](https://docs.byteplus.com/docs/byteplus-vod/docs-origin-restrictions)<br><br>* [Remote authentication](https://docs.byteplus.com/docs/byteplus-vod/docs-remote-authentication)<br><br>* [Geographic restrictions](https://docs.byteplus.com/docs/byteplus-vod/docs-geographic-restrictions)<br><br>* [Disallowed HTTP methods](https://docs.byteplus.com/docs/byteplus-vod/docs-disallowed-http-methods)<br><br>* [Data rate throttling (request-based)](https://docs.byteplus.com/docs/byteplus-vod/docs-data-rate-throttling) |
||Origin\-pulling configuration |* [Redirect follow](https://docs.byteplus.com/docs/byteplus-vod/docs-redirect-follow)<br><br>* [Origin HOST](https://docs.byteplus.com/docs/byteplus-vod/docs-origin-host)<br><br>* [Origin protocol](https://docs.byteplus.com/docs/byteplus-vod/docs-origin-protocol)<br><br>* [Origin SNI](https://docs.byteplus.com/docs/byteplus-vod/docs-origin-sni)<br><br>* [Origin request timeout](https://docs.byteplus.com/docs/byteplus-vod/docs-origin-request-time-out)<br><br>* [HTTP request headers](https://docs.byteplus.com/docs/byteplus-vod/docs-http-request-headers)<br><br>* [Query parameters](https://docs.byteplus.com/docs/byteplus-vod/docs-query-parameters) |
||HTTP configuration |* [HTTP/2](https://docs.byteplus.com/docs/byteplus-vod/docs-http-2)<br><br>* [Protocol redirect](https://docs.byteplus.com/docs/byteplus-vod/docs-force-redirect)<br><br>* [Supported TLS versions](https://docs.byteplus.com/docs/byteplus-vod/docs-supported-tls-versions)<br><br>* [HSTS](https://docs.byteplus.com/docs/byteplus-vod/docs-hsts) |
||Caching configuration |* [Cache key](https://docs.byteplus.com/docs/byteplus-vod/docs-cache-key)<br><br>* [Caching rules](https://docs.byteplus.com/docs/byteplus-vod/docs-caching-rule)<br><br>* [Caching status code](https://docs.byteplus.com/docs/byteplus-vod/docs-caching-by-status-code) |
||Advanced configuration |* [HTTP response headers](https://docs.byteplus.com/docs/byteplus-vod/docs-http-response-headers)<br><br>* [Smart compression](https://docs.byteplus.com/docs/byteplus-vod/docs-smart-compression)<br><br>* [Video seeking](https://docs.byteplus.com/docs/byteplus-vod/docs-video-seeking) |
|Image domain name |Access control |* [Referer restrictions](https://docs.byteplus.com/docs/byteplus-vod/docs-referer-restrictions)<br><br>* [IP restrictions](https://docs.byteplus.com/docs/byteplus-vod/docs-ip-restrictions)<br><br>* [URL signing overview](https://docs.byteplus.com/docs/byteplus-vod/docs-url-authentication-overview)<br><br>* [UA restrictions](https://docs.byteplus.com/docs/byteplus-vod/docs-ua-restrictions)<br><br>* [Origin restrictions](https://docs.byteplus.com/docs/byteplus-vod/docs-origin-restrictions) |
||Origin\-pulling configuration |* [Redirect follow](https://docs.byteplus.com/docs/byteplus-vod/docs-redirect-follow) |
||HTTP configuration |* [HTTP/2](https://docs.byteplus.com/docs/byteplus-vod/docs-http-2)<br><br>* [Protocol redirect](https://docs.byteplus.com/docs/byteplus-vod/docs-force-redirect)<br><br>* [Supported TLS versions](https://docs.byteplus.com/docs/byteplus-vod/docs-supported-tls-versions) |
||Advanced configuration |* [HTTP response headers](https://docs.byteplus.com/docs/byteplus-vod/docs-http-response-headers)<br><br>* [Video seeking](https://docs.byteplus.com/docs/byteplus-vod/docs-video-seeking) |
