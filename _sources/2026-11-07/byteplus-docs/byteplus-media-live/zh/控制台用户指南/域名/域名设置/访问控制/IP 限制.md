---
title: "IP 限制"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-ip-blocklist-and-allowlist-zh-CN"
---

为提升流媒体服务的安全性，您可以配置 IP 黑名单或白名单。本主题提供有关如何为推流和拉流域名限制或授予访问权限的分步说明，确保只有合法用户能够访问您的内容。


* 被添加到黑名单的 IP 地址无法访问该域名。

* 如果配置了白名单，只有列表中的 IP 地址可以访问该域名。

* 这些列表支持 IPv4 地址和 IP 网络段。


<span id="b3e4fbb7"></span>
# 适用范围


* 推流域名

* 拉流域名


<span id="ed9f0df7"></span>
# 前提条件

您已添加域名。更多信息，请参见[添加域名](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain-zh-CN)。

<span id="26c3b955"></span>
# 操作步骤


1. 登录[BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

2. 在左侧导航栏，点击**域名**。

3. 找到您要查看的域名，在**操作**列点击**设置**。

4. 点击**访问控制**标签页。

5. 在**IP 限制**开关右侧，点击**编辑**。

6. 在弹出的**编辑 IP 黑名单和白名单**对话框中，配置以下参数。

   * **列表类型**：选择**黑名单**或**白名单**。这两个选项互斥。如果选择**黑名单**，黑名单中的 IP 地址无法访问该域名。如果选择**白名单**，只有白名单中的 IP 地址可以访问该域名。

   * **规则**：输入规则所需的 IPv4 地址或 IP 网络段。最多可配置 100 条规则。如需配置超过 100 条规则，请[联系技术支持](https://console.byteplus.com/workorder/create)申请提升限制。

7. 点击**确认**。
