---
title: "HSTS 设置"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-hsts_1-cn"
---

本文档介绍如何在 BytePlus CDN 中对域名启用 HSTS。

<span id="hsts-概述"></span>
## HSTS 概述

HSTS 的全称是 HTTP Strict Transport Security，是一种网络安全的策略机制。HSTS 的目的是保护用户在访问 HTTPS 站点的期间免受降级攻击和 cookie 劫持。 在您对站点启用 HSTS 后，站点的响应中会包含 `Strict-Transport-Security` 响应头。`Strict-Transport-Security` 响应头告知浏览器其向站点发送的每个请求都必须使用 HTTPS 协议。

`Strict-Transport-Security` 响应头还包含两个参数。关于这两个参数的描述，参见 [配置说明](https://docs.byteplus.com/en/docs/18/6975#%E9%85%8D%E7%BD%AE%E8%AF%B4%E6%98%8E)。

<span id="hsts-与-http-重定向到-https-配置"></span>
## HSTS 与 "HTTP 重定向到 HTTPS" 配置

CDN 提供的 "协议重定向" 功能中，有一个 "HTTP 重定向到 HTTPS" 的配置（以下简称 "HTTP 重定向"）。该配置的作用是 CDN 将收到 HTTP 请求重定向到 HTTPS 请求。

在进一步阐述 HSTS 之前，有必要先解释 HSTS 与 "HTTP 重定向" 的区别。

HTTP 是一个不安全的协议。当用户在浏览器中指定 HTTP 协议向一个站点发送请求时，该请求可能会被劫持并重定向到恶意站点。为了避免 HTTP 请求访问域名，CDN 提供了以下两个配置：


* HTTP 重定向：在启用 "协议重定向" 后，您需要设置 **策略** 为 **将 HTTP 重定向到 HTTPS**。

* HSTS。


<span id="http-重定向的局限"></span>
### HTTP 重定向的局限

在您配置了 HTTP 重定向后，如果浏览器向 CDN 发送了一个 HTTP 请求，CDN 会返回 301 或者 302 响应状态码通知浏览器将 HTTP 请求跳转到 HTTPS 请求。关于更多 HTTP 重定向的信息，参见 [协议重定向](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-protocol-redirect_1-cn)。

但是，即使您配置了 HTTP 重定向，用户依然可以在浏览器中指定 HTTP 协议向 CDN 发送 HTTP 请求。虽然会被跳转到 HTTPS 请求，这些 HTTP 请求在到达 CDN 前依然有被劫持的风险。

<span id="hsts-的优势"></span>
### HSTS 的优势

相比 HTTP 重定向，HSTS 提供了一个更安全的方案。在您为域名启用 HSTS 后，CDN 的响应中会包含 `Strict-Transport-Security` 响应头。如果浏览器成功使用 HTTPS 协议对 CDN 发送过一次请求，浏览器就会缓存该响应头。假设之后用户再次在浏览器中指定 HTTP 协议访问 CDN。在发送请求前，浏览器会将 HTTP 转换成 HTTPS。由于转换过程在浏览器侧发生，就能极大降低浏览器向 CDN 发送的 HTTP 请求的数量。同时，也降低了 HTTP 请求被劫持的风险。

<span id="hsts-响应头起作用的前提条件"></span>
#### HSTS 响应头起作用的前提条件

虽然 HSTS 方案更安全，但是要使浏览器遵循 `Strict-Transport-Security` 响应头将 HTTP 转换成 HTTPS，以下条件必须满足：


* 浏览器已缓存了 `Strict-Transport-Security` 响应头。

* 已缓存的响应头未过期。关于 `Strict-Transport-Security` 响应头的缓存有效时间，参见 [配置说明](https://docs.byteplus.com/en/docs/18/6975#%E9%85%8D%E7%BD%AE%E8%AF%B4%E6%98%8E)。


在域名启用了 HSTS 后，CDN 在响应任何请求时都会返回 `Strict-Transport-Security` 响应头。但要使浏览器缓存该响应头，浏览器必须成功使用 HTTPS 协议向 CDN 发送过一次请求。因此，在您启用 HSTS 时，推荐您也启用协议重定向并设置 **策略** 为 **将 HTTP 重定向到 HTTPS**。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">当您在 CDN 控制台中启用 HSTS 时，CDN 会提示您是否需要启用 HTTP 重定向配置。参见 <a href="https://docs.byteplus.com/en/docs/18/6975#%E6%93%8D%E4%BD%9C%E6%AD%A5%E9%AA%A4">操作步骤</a>。</div>


<span id="浏览器与-cdn-的交互过程"></span>
#### 浏览器与 CDN 的交互过程

在您启用了 HSTS 与 HTTP 重定向后，如果用户使用浏览器向 CDN 发送了一个 HTTP 请求，浏览器与 CDN 的交互过程如下：


1. 浏览器检查是否存在已缓存的 `Strict-Transport-Security` 响应头。

2. 由于浏览器缓存中不存在该响应头，浏览器向 CDN 发送该 HTTP 请求。

3. CDN 收到该请求后，由于 HTTP 重定向的配置，CDN 的响应状态码是 301 或 302。同时，由于 HSTS 的配置，响应中包含了 `Strict-Transport-Security` 响应头。此时，由于还未成功使用 HTTPS 协议向 CDN 发送过一次请求，浏览器不缓存该响应头。

4. 由于 301 或 302 响应状态码，浏览器向 CDN 发送 HTTPS 请求。在响应中，CDN 同样包含了 `Strict-Transport-Security` 响应头。假设该响应头的有效时间是 10 分钟，并且该 HTTPS 请求成功获取了请求的文件。

5. 由于 HTTPS 请求成功，浏览器对 `Strict-Transport-Security` 响应头进行缓存。


在 10 分钟内，假设该用户使用浏览器再次向 CDN 发送 HTTP 请求。此时，浏览器与 CDN 的交互过程如下：


1. 浏览器检查是否存在已缓存的 `Strict-Transport-Security` 响应头。

2. 由于浏览器缓存中存在该响应头，浏览器检查该响应头是否已过期。

3. 由于该响应头未过期，浏览器就将 HTTP 转换为 HTTPS 并向 CDN 发送该请求。


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">如果缓存的 <code>Strict-Transport-Security</code> 响应头已过期，当该用户向 CDN 发送 HTTP 请求时，会重复 "浏览器与 CDN 的交互过程" 中描述的步骤。</div>


* <div data-tips="true" data-tips-type="warning">需要注意的是，即使您已启用了 HSTS 与 HTTP 重定向，CDN 收到的 HTTP 请求是无法杜绝的。因为在以下任意情况下，浏览器不会将 HTTP 转换成 HTTPS：</div>


   * <div data-tips="true" data-tips-type="warning">浏览器缓存中不存在 <code>Strict-Transport-Security</code> 响应头。</div>


   * <div data-tips="true" data-tips-type="warning">浏览器缓存中的 <code>Strict-Transport-Security</code> 响应头已过期。</div>



<span id="前提条件"></span>
### 前提条件

要开启该配置，域名必须已经开启了 HTTPS 加密服务。

<span id="操作步骤"></span>
## 操作步骤


1. 打开 **HSTS 设置** 配置页面。操作步骤参见 [域名配置](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-cn)。

2. 设置 **状态** 为 **开启**。

   如果此时您还未启用协议重定向，或者您已经启用了协议重定向但是 **策略** 不是 **将 HTTP 重定向到 HTTPS**，CDN 会询问您是否要配置HTTP 重定向。其原因参见 "HSTS 响应头起作用的前提条件"。

   * 如果您点击 **确认**，CDN 会配置 HTTP 重定向。在您点击 **确认** 前，请充分评估 HTTP 重定向这个设置对您业务的影响。

   * 如果您点击 **忽略**，CDN 会保留当前协议重定向的设置。

3. 参照以下配置说明。

4. 配置完成后，点击 **保存**。


<span id="配置说明"></span>
### 配置说明


|**配置** |**说明** |
|---|---|
|缓存过期时间 |表示 `Strict-Transport-Security` 响应头在客户端浏览器中的缓存过期时间。该配置对应`Strict-Transport-Security` 响应头的 `max-age` 参数。在发送一个 HTTP 请求前，浏览器会检查其缓存的 `Strict-Transport-Security` 响应头是否已经过期。如果该响应头已过期，浏览器不会将 HTTP 转换成 HTTPS。<br><br>&nbsp;<br><br>您最长可以设置的时间是 31,536,000 秒，表示 365 天。如果您设置过期时间为 `0`，其效果等同于禁用 HSTS。<br><br>&nbsp;<br><br>需要留意的是，对于浏览器收到的每个响应，如果响应中包含 `Strict-Transport-Security` 响应头，浏览器会使用收到的响应头的过期时间来替换缓存的响应头的过期时间。 |
|子域名 |表示 HSTS 配置是否应用于子域名站点。该配置有以下选项：<br><br><br>* **不使用**：表示 HSTS 配置不应用于子域名站点。<br><br>* **应用**：表示 HSTS 配置应用于子域名站点。此时，响应头会包含 `includeSubDomains` 参数。<br><br><br><div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div><br><br><br><div data-tips="true" data-tips-type="danger">如果您设置 <strong>子域名</strong> 为 <strong>包含</strong>，CDN 返回的响应头是告知浏览器向所有子域名发送的请求也必须使用 HTTPS 协议。此时，请确保子域名站点必须是可以使用 HTTPS 协议访问的。并且，子域名也要有一个类似配置将子域名的 HTTP 请求重定向到 HTTPS 请求。</div><br> |


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a2bd9f1d4ceb4a9ea1d3f8968574e125~tplv-goo7wpa0wc-topic.webp) </span>

**举例**


* 例子 1：您指定过期时间是 6 秒并且包含子域名。此时，CDN 实际返回的响应头如下：

   * `Strict-Transport-Security: max-age=6;includeSubDomains`

* 例子 2：您指定过期时间是 1 天并且不包含子域名。此时，CDN 实际返回的响应头如下：

   * `Strict-Transport-Security: max-age=86400`


<span id="更多信息"></span>
## 更多信息

<span id="如何在浏览器中管理-hsts-配置"></span>
### 如何在浏览器中管理 HSTS 配置

下面以 Google Chrome 和 Microsoft Edge 为例，阐述如何在浏览器中管理 HSTS 配置。

在 Chrome 或 Edge 中，访问以下 URL：


* `chrome://net-internals/#hsts`


在打开的页面中，您可以：


* 将一个域名添加到浏览器的 HSTS 缓存中。

* 从浏览器的 HSTS 缓存中删除指定的域名。

* 查询一个域名是否存在于浏览器的 HSTS 缓存中。

   * 如果该域名不存在，查询结果是 `Not found`。

   * 如果该域名存在，查询结果会展示该域名的 HSTS 配置信息。在配置信息中，`dynamic_sts_observed` 表示浏览器缓存该域名的时间，时间格式是 Unix 时间戳。`dynamic_sts_expiry` 表示该域名在 HSTS 缓存中的过期时间。


在您查询一个域名时，结果数据可能会有 1 分钟的延时。

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bceca7d3f4666d763c878521f8ae8164.png) </span>
