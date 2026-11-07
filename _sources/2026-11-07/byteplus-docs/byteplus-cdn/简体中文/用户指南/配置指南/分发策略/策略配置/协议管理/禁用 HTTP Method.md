---
title: "禁用 HTTP Method"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-disallowed-http-method-cn"
---

本文档介绍了如何在 BytePlus CDN 中指定不支持的请求方法。

<span id="关于-http-请求方法"></span>
## 关于 HTTP 请求方法

HTTP 请求方法指定了资源请求的方式。不同的请求方法有特定的使用场景。默认情况下，CDN 允许用户使用以下请求方法访问域名。


* GET

* POST

* HEAD

* DELETE

* PUT

* PATCH

* CONNECT

* OPTIONS


您可以根据需求配置 CDN 所不支持的 HTTP 请求方法。 如果一个用户请求使用了不支持的 HTTP 请求方法，CDN 会拒绝该请求并返回 405 响应状态码。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">GET 和 POST 是用户访问 CDN 时普遍使用的请求方法，我们不建议您禁用。</div>


* <div data-tips="true" data-tips-type="tip">在 CDN 向对象存储源站发送回源请求时，回源请求使用的方法与用户请求相同。默认情况下，CDN 支持用户请求使用的请求方法有 DELETE、GET、HEAD、POST、PUT、PATCH、CONNECT、OPTIONS。如果您不希望使用特定请求方法的回源请求访问您的源站，例如您不希望使用 DELETE 方法的请求删除源站上文件，建议您执行以下所有操作：</div>


   * <div data-tips="true" data-tips-type="tip">对于您提供的 AK/SK 所对应的云厂商账号，在云厂商处设置权限，禁止该账号在您的对象存储源站上执行特定的操作。</div>


   * <div data-tips="true" data-tips-type="tip">在 "禁用 HTTP 方法" 设置中，指定 CDN 不支持用户请求使用的请求方法。</div>



<span id="操作步骤"></span>
## 操作步骤


1. 打开 **禁用 HTTP Method** 配置页面。操作步骤参见 [域名配置](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-cn)。

2. 设置 **状态** 为 **开启**。

3. 勾选那些不支持的 HTTP 请求方法，然后点击 **保存**。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_20cb6ede5f2d7ede323a4ad5fc0d06fd.png) </span>
