---
title: "HTTPS 配置"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-https-zh-CN"
---

你可以将 SSL/TLS 证书绑定到你的域名，并启用 HTTPS，以提升直播过程中的安全性。

<span id="d1bc3916"></span>
# 适用对象


* 拉流域名

* 推流域名


<span id="47193979"></span>
# 概述

**HTTPS**

HTTPS（HyperText Transfer Protocol Secure）是一种用于计算机网络中安全通信的传输协议。它在 HTTP 基础上增加了 SSL/TLS 协议，通过数字证书和加密算法等技术，确保数据在传输过程中的安全性和完整性。


* **保障数据安全**：通过将 SSL/TLS 证书绑定到域名并启用 HTTPS，直播过程中传输的数据会被加密，防止数据被窃取或篡改，从而保护用户的隐私和安全。

* **提升用户信任**：使用 HTTPS 可以增强用户对你的直播平台的信任，提升用户满意度和忠诚度。

* **符合法律法规要求**：在某些场景下，使用 HTTPS 是法律要求，例如金融和电商行业。


**HTTP/2**

HTTP/2 是 HTTP 超文本传输协议的最新版本，于 2015 年 5 月正式发布。该版本在 HTTP/1.x 的基础上进行了升级，提供了二进制分帧层、头部压缩、多路复用和服务器推送等增强功能。虽然 HTTP/2 并不强制网站使用 HTTPS，但主流浏览器对 HTTP/2 的兼容性依赖于 SSL/TLS 的实现。目前，使用 HTTP/2 的网站通常也需要启用 HTTPS。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">HTTP/2 仅适用于拉流域名。</div>


**TLS 版本**

TLS 协议的不同版本在兼容性和安全性方面存在差异。旧版本兼容性更好但安全性较低，最新版本安全性更高但可能存在兼容性问题。大多数现代浏览器现已支持 TLS 1.3。

当你通过浏览器访问已开启 HTTPS 加速的域名时，缓存节点会选择与浏览器 TLS 版本和加速域名配置都匹配的最高 TLS 版本。如果缓存节点无法找到兼容的 TLS 版本，则 TLS 握手会失败，无法建立连接。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">设置 TLS 版本仅适用于拉流域名。</div>


<span id="8658adf5"></span>
# 前提条件


* 已添加域名

* SSL/TLS 证书。更多信息，请参见[管理 SSL/TLS 证书](https://docs.byteplus.com/docs/byteplus-media-live/docs-managing-certificates)。


<span id="5f81b8bf"></span>
# 操作流程


1. 登录 [BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

2. 在左侧导航栏，选择 **设置** \> **域名**。

3. 在出现的 **域名** 页面，找到你要配置的域名，在 **操作**列点击 **设置**。

4. 在打开的页面，点击 **HTTPS** 标签页。

5. 点击 **编辑**，位于 **HTTPS** 开关右侧。

6. 在 **编辑 HTTPS 信息**对话框中，**HTTPS** 开关默认已开启。选择你要使用的 SSL/TLS 证书。你还可以：

   * 为当前域名启用 **HTTP/2**。

   * 设置 **TLS 版本范围**。

7. 点击 **确认**。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">只有当你的域名被添加到证书的 <strong>Subject Alternative Name（SAN）</strong>字段时，你的 SSL/TLS 证书才会显示在 <strong>证书</strong>列表中。</div>


* <div data-tips="true" data-tips-type="tip">HTTPS 配置大约需要 10 分钟生效。如果配置未生效，请联系技术支持寻求帮助。</div>
