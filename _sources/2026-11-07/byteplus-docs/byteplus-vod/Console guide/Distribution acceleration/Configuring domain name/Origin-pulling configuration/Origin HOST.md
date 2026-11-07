---
title: "Origin HOST"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-origin-host"
---

To direct origin\-pull requests to a specific site hosted on your origin server, especially when a single server hosts multiple sites, you can configure the origin HOST. This guide provides step\-by\-step instructions on how to set the origin HOST for a custom\-origin domain name in the BytePlus VOD console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Configuring the origin HOST applies to <strong>Custom\-origin domain name</strong>.</div>


<span id="bf2a2730"></span>
## Introduction

Origin HOST refers to the value of the HOST header in origin\-fetch requests. It specifies a specific site hosted on a given IP address, to which requests are redirected. For example, if you set the server host as "img.example.com" on the origin server "origin.example.com", the cache server will retrieve the requested content from "img.example.com/byteplus.png" when a user accesses "https://www.example.com/byteplus.png".

Note that the priority of this configuration is lower than that of the origin HOST configured in the origin server. Additionally, this configuration does not take effect for TOS origin servers. In such cases, the origin HOST for this type of origin will be forcefully set as `"{bucket}.{TOSDomain}"`.

<span id="操作步骤"></span>
## Configuring origin HOST


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a specific space.

2. Click **Distribution acceleration \> Domain names** on the left navigation bar.

3. Depending on the type of your domain name, click the **Custom\-origin domain name** tab.

4. Find the domain name you want to configure and click the **Configure** button in the **Action** column.

5. Click the **Origin\-pulling configuration** tab.

6. Click the **Modify** button at the bottom of the page.

7. Under **Origin HOST**, switch the **Status** toggle and configure the origin HOST.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/757beb309f784bdfb404963aec828fe2~tplv-goo7wpa0wc-image.image) </span>

   
   |**Configuration** |**Description** |
   |---|---|
   |Status |Disabled by default. Once enabled, you can configure the **Type** and **Domain name**. |
   |Type |Select the domain name type. The available options are:<br><br><br>* **Accelerated domain name**: Refers to the domain that users access and you want BytePlus VOD to accelerate. For example, when a user accesses `https://www.example.com/byteplus.png`, `www.example.com` is the accelerated domain name. If you set **Type** as **Accelerated domain name**, the origin HOST will be configured the same as the accelerated domain name.<br><br>* **Origin domain name**: Refers to the domain name of your origin server, to which the CDN sends requests for fetching content. If you set **Type** as **Origin domain name**, the origin HOST will be configured the same as the origin server's domain name.<br><br>* **Custom domain name**: Specify a custom domain name as the origin HOST. If your origin server is associated with multiple domain names, it is important to specify a specific domain name. Failure to do so may result in the origin fetch process failing.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the <strong>Origin type</strong> is set to <strong>Origin IP</strong>, the <strong>Origin domain name</strong> option is unavailable. You need to change the <strong>Origin</strong> <strong>type</strong> to <strong>Origin domain name</strong> first.</div><br> |
   |Domain name |* When the type is set to **Accelerated domain name**, you can select from your existing domains.<br><br>* When the type is set to **Custom domain name**, you can input a domain name. You must follow the following rules:<br><br>   * The domain name must be exact, such as `example.byte-test.com`. By default, wildcard domain names, such as `*.test.com`, are not supported.<br><br>      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">To add a wildcard domain name, please <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to our technical team for application.      </div><br>      <br><br>   * Capital letters are not supported.<br><br>   * Duplicate domain names are not supported. |
   

8. Click **Save**.
