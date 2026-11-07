---
title: "Disabled HTTP Methods"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-disallowed-http-method"
---

To enhance security and control access to your resources, you can specify which HTTP request methods are not supported by your BytePlus CDN domain. This guide shows you how to configure this feature. Once configured, any request using a disabled method will be rejected with a 405 status code.

<span id="about-http-request-methods"></span>
## About HTTP Request Methods

HTTP request methods determine how a resource is requested. Different methods are used for specific scenarios. By default, the CDN allows users to access your domain name using the following request methods:


* GET

* POST

* HEAD

* DELETE

* PUT

* PATCH

* CONNECT

* OPTIONS


You can configure unsupported HTTP request methods based on your needs. If a user request uses an unsupported HTTP method, the CDN will reject the request and return a 405 response status code.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">GET and POST are the most commonly used methods when users access the CDN, and we do not recommend disabling them.</div>


* <div data-tips="true" data-tips-type="tip">When the CDN forwards a request to an object storage origin, it uses the same HTTP method as the original user request. To prevent requests with certain methods from reaching your origin (for example, to block DELETE requests from deleting files), we recommend taking both of the following actions:</div>


      * <div data-tips="true" data-tips-type="tip">In your cloud provider's console, configure permissions for the account associated with your AK/SK to deny specific operations on your object storage origin.</div>


      * <div data-tips="true" data-tips-type="tip">In the "Disable HTTP Methods" settings of CDN, specify the request methods that CDN does not support for user requests.</div>



<span id="steps"></span>
## Steps


1. Open the **Disabled HTTP Methods** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set **Status** to **Enabled**.

3. Select the HTTP methods to disable, and then click **Save**.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_ca783ea7067b48099017020db3024fe6.png) </span>
