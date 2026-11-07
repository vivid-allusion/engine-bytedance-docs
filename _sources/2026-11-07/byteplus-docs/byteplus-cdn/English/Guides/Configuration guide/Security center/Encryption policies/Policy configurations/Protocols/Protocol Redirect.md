---
title: "Protocol Redirect"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-protocol-redirect_1"
---

To enforce a specific request protocol for your domain, such as redirecting all HTTP traffic to HTTPS for enhanced security, you can use the Protocol Redirection feature in BytePlus CDN. This guide provides instructions on how to configure redirect policies and select the appropriate HTTP status code (301, 302, 307, etc.) for your needs.

<span id="prerequisites"></span>
### Prerequisites


1. Open the **Protocol Redirect** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Configure the settings as described in the table below.

3. After completing the configuration, click **Save**.



|**Configuration** |**Description** |
|---|---|
|Policy |Specifies the redirect policy.<br><br><br>* **No Redirect**: The user's request protocol is not redirected.<br><br>* **Redirect HTTP to HTTPS**: Redirects HTTP requests to HTTPS.<br><br>* **Redirect HTTPS to HTTP**: Redirects HTTPS requests to HTTP. |
|Redirect Code |Specifies the HTTP status code that the CDN returns to perform the redirection. This configuration appears when the **Policy** is **Redirect HTTP to HTTPS** or **Redirect HTTPS to HTTP**.<br><br>&nbsp;<br><br>The available options for this configuration are **301**, **302**, **303**, **307**, **308**.<br><br>&nbsp;<br><br>Please note that:<br><br><br>* For 301 and 302, if the original request method is not GET, the method used by the client when sending a request to the new URL may change to GET.<br><br>* For 303, the method used for the new request is GET.<br><br>* For 307 and 308, the method for the new request is the same as the original request. |


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_42aed8fa7419ff5197198159125e7398.png) </span>
