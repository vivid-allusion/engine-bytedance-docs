---
title: "回源 Host"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/origin-host_zh-cn"
---

本文档介绍如何配置 CDN 回源请求中携带的全局 Host 字段。

全局回源 Host 配置始终启用，无法关闭。您必须指定将加速域名或自定义域名用作全局回源 Host。在源站服务器上存在多个站点时，正确配置回源 Host 可确保 CDN 从目标站点获取资源。

<span id="配置优先级"></span>
## 配置优先级

CDN 支持以下两处回源 Host 配置：


* **全局回源 Host**：应用于分发策略中的所有源站。

* **源站回源 Host**：应用于特定源站。不同源站可以配置不同的回源 Host，其优先级高于全局回源 Host。默认值与全局回源 Host 相同。配置方法参见 [源站配置](https://docs.byteplus.com/en/docs/18/%E6%BA%90%E7%AB%99%E9%85%8D%E7%BD%AE.md)。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">对于 <strong>源站类型</strong> 为 <strong>对象存储源站</strong> 的源站，全局回源 Host 不生效。CDN 使用对象存储源站配置中的回源 Host 或为云厂商预设的 Host。</div>


<span id="操作步骤"></span>
## 操作步骤


1. 打开 **源站配置** 标签页。操作步骤参见 [域名配置](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-cn)。

2. 定位 **回源 Host**。

3. 选择全局回源 Host 的取值方式：

   * **加速域名**：使用当前加速域名作为回源 Host。

   * **自定义域名**：输入源站服务器上的实际站点域名。域名长度不能超过 1,024 个字符。

4. 配置完成后，在页面右下方点击 **保存**。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06f81d1711b244de9f789139d7366fbb~tplv-goo7wpa0wc-topic.webp) </span>

如果需要为特定源站配置不同的回源 Host，请在源站列表中编辑该源站，并在 **回源 Host** 中输入实际站点域名。
