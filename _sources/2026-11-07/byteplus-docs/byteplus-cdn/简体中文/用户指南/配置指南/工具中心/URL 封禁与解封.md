---
title: "URL 封禁与解封"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/url-block_zh-cn"
---

BytePlus 内容分发网络（CDN）提供 **URL 封禁与解封**功能，允许您指定并阻断外部对加速域名下某些 URL 的访问，或对已封禁的 URL 恢复访问。该功能可帮助您快速响应安全事件，或根据业务需求灵活管理内容的访问权限。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如果用户尝试访问一个被封禁的 URL，CDN 会响应 <code>403</code> 状态码，且响应头中会包含 <code>Byte-Error-Code: 007</code>。</div>


<span id="3a02ed17"></span>
## 功能概述

通过 BytePlus CDN 控制台的 **URL 封禁与解封** 页面，您可以执行以下操作：


* **封禁 URL**：主动阻止外部对特定 URL 的访问。

* **解封 URL**：对已封禁的 URL 恢复正常访问。

* **查看操作记录**：查询历史的封禁与解封操作状态及执行结果。


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">您无法直接对泛域名下的文件和目录执行封禁和解封操作。如需操作，请参见 <a href="https://docs.byteplus.com/docs/byteplus-cdn/purge-prefetch-faq_zh-cn#881a5fbc">如何对泛域名下的文件和目录执行刷新、预热、URL 封禁与解封操作</a>。</div>


<span id="00f7e570"></span>
## 封禁 URL

如果您不希望用户访问域名下的某些特定文件，可通过该页面指定需要封禁的 URL。当用户请求匹配了封禁 URL 时，CDN 将拒绝该请求。


* **操作额度**：主账号每日最多可封禁 3,000 个 URL。

* **提交要求**：

   * 必须以 `http://` 或 `https://` 开头。

   * 单次任务最多可包含 100 个 URL。

* **提交方式**：

   1. **手动输入**：直接在文本框中每行输入一个需要封禁的 URL。

   2. **上传文件**：上传包含需封禁 URL 的 `.txt` 文件（每行一个 URL）。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f671e79e43f04fb39412b7471be3885f~tplv-goo7wpa0wc-image.image) </span>

<span id="99a4a985"></span>
## 解封 URL

用于解除之前被拦截的 URL，恢复用户的正常访问。


* **操作额度**：主账号每日最多可解封 3,000 个 URL。

* **提交要求**：同封禁要求，需包含 `http/https` 前缀，单次任务最多 100 个 URL。

* **提交方式**：支持**手动输入**和**上传文件**。


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>平台违规封禁的 URL 不支持自助解封</strong> 如果您的业务涉及中国大陆地区，您通过 CDN 分发的内容必须符合中国大陆的相关法律法规（如《网络安全法》、《互联网信息服务管理办法》等）。对于因内容违规被 BytePlus 主动封禁的 URL，您无法通过本页面进行自助解封，此类任务将会提示<strong>解封失败</strong>。如需解封，请 <a href="https://console.byteplus.com/ticket/createTicketV2/">提交工单</a> 申请。</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/af138f0280da4b3cabba21cad54049e8~tplv-goo7wpa0wc-image.image) </span>

<span id="aded05e7"></span>
## 查看操作记录

在“URL 封禁与解封”页面的 **操作记录** 标签页，您可以追踪各个 URL 封禁与解封任务的执行结果。

系统支持查询过去 **92 天内** 的记录。您可以通过以下条件进行精准过滤：


* **操作时间**：自定义过去 92 天内的时间段（默认值为“今天”）。

* **任务类型**：URL封禁 / URL解封。

* **任务状态**：完成 / 执行中 / 执行失败（默认包含所有状态）。

* **封禁原因**：URL 被封禁的原因。

* **URL**：精确查询某个具体 URL 的执行情况。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">系统仅保留 92 天内的可查询记录。对于 92 天前被封禁的 URL，您只能通过其返回的 <code>403</code> 状态码及 <code>Byte-Error-Code: 007</code> 响应头来判断是否处于封禁状态。</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21a6516cc3a3476fbefa1d2c2269817a~tplv-goo7wpa0wc-image.image) </span>
