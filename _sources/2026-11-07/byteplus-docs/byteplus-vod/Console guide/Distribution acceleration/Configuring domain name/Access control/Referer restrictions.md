---
title: "Referer restrictions"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-referer-restrictions"
---

To prevent unauthorized hotlinking and control access to your video and image resources, you can configure Referer restrictions. This guide provides step\-by\-step instructions on how to set up an allowlist or blocklist for your **Playback**, **Image**, and **Custom\-origin** domain names within the BytePlus VOD console.

<span id="76863e44"></span>
## Introduction

Referer is a field in the HTTP request header that indicates which site page the request comes from. You can use the Referer field to identify the source of the request. For example, if you click on the `https://www.byteplus.com` link on the page `https://www.example.com/test.html`, the HTTP request header will contain `Referer: https://www.example.com/test.html`.

BytePlus VOD supports configuring the Referer allowlist and blocklist. After a user initiates a request for a resource, the request reaches the CDN node, which determines the source based on the Referer allowlist and blocklist you have configured. Requests that meet the rules can successfully access the resource, while requests that do not meet the rules fail to access the resource.

<span id="176c2ad9"></span>
### Empty Referer

When a request is not triggered by a user clicking on a link, but rather by the user entering a URL in the address bar or selecting a browser bookmark, the Referer field of that request is empty or the request header does not contain the Referer field. For example, if you directly enter `https://www.byteplus.com` in the browser's address bar to visit this website, the request header will not contain the Referer field.

<span id="07127eb6"></span>
## Configuring the Referer allowlist and blocklist


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a specific space.

2. Click **Distribution acceleration** \> **Domain names** on the left navigation bar.

3. Depending on the type of your domain name, click the **Playback domain name**, **Image domain name**, or **Custom\-origin domain name** tab.

4. Find the domain name you want to configure and click the **Configure** button in the **Action** column.

5. Click the **Access control** tab.

6. Click the **Modify** button at the bottom of the page.

7. Under **Referer allowlist and blocklist**, switch the **Status** toggle and configure the Referer restrictions:

   
   |**Configuration** |**Description** |
   |---|---|
   |Type |This configuration has the following options:<br><br><br>* **Allowlist**: You can configure an allowlist when you only want to allow requests from certain sites. If the user's request does not match the allowlist, the CDN node rejects the request and responds with a 403 status code.<br><br>* **Blocklist**: When you want to block requests from certain sites, you can configure a blocklist. If the user's request matches the blocklist, the CDN node rejects the request and responds with a 403 status code. |
   |Referers |Enter one or more list entries. List length cannot exceed 30,000 characters. You can enter one or more domain names (including subdomain names and wildcard domain names) and IP addresses (including IPv4 addresses, IPv6 addresses, and CIDR network segments). Multiple entries are separated with semicolons (;) or newlines. You can enter up to 1,000 entries. It should be noted that a second\-level domain name is a single domain name, not a wildcard domain. A wildcard domain does not include the second\-level domain itself. For example: \*`.test.com` does not contain the second\-level domain name `test.com`, but contains `www.test.com` and `a.a.test.com`. For details, see [Referer matching Logic](https://docs.byteplus.com/docs/byteplus-vod/docs-referer-restrictions#2c1dd336). |
   |Allowing empty Referer |Indicates whether to accept requests with no value in the Referer header or requests that do not contain the Referer header. |
   

8. Click **Save**.


<span id="2c1dd336"></span>
## Referer matching logic

After you configure the Referer blocklist or allowlist, BytePlus VOD will use Referer rules to match the Referer value in requests. The matching is case\-insensitive. If the Referer value meets all of the following conditions, the match is successful. Otherwise, the match fails.


* The host of the Referer header in the client request header must be an exact match with the Referer configuration.

* The Referer header in the client request header must comply with all of the following specifications:

   * The content of the field matches one of the following URL formats:

      * scheme://host:port/path

      * scheme://host:port/

      * scheme://host:port

      * scheme://host/path

      * scheme://host/

      * scheme://host

   * The scheme must be HTTP or HTTPS.

   * The port must be a number.

   * When the host is an IPv6 address, the address must be wrapped in `[]`.


<span id="c10d0bec"></span>
## Example

Here are some examples where the Referer does not comply with the specifications, resulting in mismatched results.


* Suppose the Referer rule is `www.example.com:8888`. If the Referer header in the request has the value `www.example.com:8888`, BytePlus VOD determines it as a mismatch because the value is not a valid URL (it lacks a scheme like http://).

* Suppose the Referer rule is `350e:b1:e401:4::1a`. If the Referer header has the value `http://350e:b1:e401:4::1a:8090/`, BytePlus VOD determines it as a mismatch because the IPv6 address in the URL is not enclosed in square brackets (`[]`).


<span id="3cc13ae3"></span>
## Response status code

If the result is a mismatch, BytePlus VOD returns the following status codes:


* For the allowlist:

   * If the value of the Referer header does not comply with the specifications, the status code is 403.

   * If the Referer configuration rule does not match, the status code is 403.

* For the blocklist:

   * If the value of the Referer header does not comply with the specifications, the status code is 200.

   * If the Referer configuration rule does not match, the status code is 200.
