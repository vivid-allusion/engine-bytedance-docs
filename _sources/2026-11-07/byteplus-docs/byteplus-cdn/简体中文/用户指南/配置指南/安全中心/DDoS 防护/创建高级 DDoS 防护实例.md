---
title: "创建高级 DDoS 防护实例"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/Create_an_Advanced_DDoS_Protection_instance_cn"
---

本文档介绍如何在 BytePlus CDN 管理控制台的 **DDoS** **防护** 页面创建高级 DDoS 防护实例。

创建高级 DDoS 防护实例后，您的 BytePlus 账号即订阅并激活了高级 DDoS 防护服务。

<span id="背景信息"></span>
## 背景信息

针对网络层和传输层 DDoS 攻击，CDN 提供标准 DDoS 防护和高级 DDoS 防护。如需使用高级 DDoS 防护，您需要订阅 CDN\-Security\-Plan Advanced Edition 或者创建高级 DDoS 防护实例。

关于标准 DDoS 防护和高级 DDoS 防护的更多说明，请参考 [标准 DDoS 防护和高级 DDoS 防护对比](https://docs.byteplus.com/en/docs/byteplus-cdn/DDos_protection_levels_cn#%E6%A0%87%E5%87%86-ddos-%E9%98%B2%E6%8A%A4%E5%92%8C%E9%AB%98%E7%BA%A7-ddos-%E9%98%B2%E6%8A%A4%E5%AF%B9%E6%AF%94)。

<span id="使用限制"></span>
## 使用限制


* 当前，如需使用高级 DDoS 防护功能，请[提交工单](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000735)进行申请。

* 一个 BytePlus 账号下，只能创建一个高级 DDoS 防护实例。


<span id="注意事项"></span>
## 注意事项


* 当您为域名开启高级 DDoS 防护且订阅方案非 CDN\-Security\-Plan Advanced Edition 时，将会产生安全流量费用。安全流量的费用按 CDN 传输给客户端的数据量计算。计费详情，请参考 [计费说明](https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-pricing)。

* 为域名开启高级 DDoS 防护后，您无需修改域名的 DNS 解析配置。但是，DNS 会停止将域名解析为 IPv6 地址（即使您在 CDN 的策略中启用了 IPv6）。所有流量会指向 IPv4 高防 IP 地址。

* 开启高级 DDoS 防护会带来一定的域名访问时延。客户端所在区域和网络环境会影响到时延大小。


更多信息，请参考[使用高级 DDoS 防护时的注意事项](https://docs.byteplus.com/en/docs/byteplus-cdn/DDos_protection_levels_cn#%E4%BD%BF%E7%94%A8%E9%AB%98%E7%BA%A7-ddos-%E9%98%B2%E6%8A%A4%E6%97%B6%E7%9A%84%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9)。

<span id="操作步骤"></span>
## 操作步骤


1. 登录 [BytePlus CDN 管理控制台](https://console.byteplus.com/cdn)。

2. 在左侧导航栏，选择 **安全中心** \> **DDoS** **防护**。

3. 在 **DDoS** **防护** 页面的 **实例管理** 区域，单击 **订阅实例**。

4. 在 **创建CDN高级DDoS防护实例** 页面，配置以下参数：

   * **防护域名数量**：设置需要被防护的域名的数量。域名数量不小于 50 且须为 5 的倍数。

      默认情况下，一个高级 DDoS 防护实例最多可以防护 50 个域名。如果有更多的域名需要防护，您需要额外付费。计费说明，请参见[计费详情](https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-pricing)。

   * **订阅时长**：指定订阅时长。

      该页面上的其他参数的值由系统指定，无法手动修改。对这些参数的说明如下：

   * **地区**：高级 DDoS 防护提供服务的区域。当前，高级 DDoS 防护只能在除中国内地以外的区域使用。

   * **配置模式**：高级 DDoS 防护的配置模式。CDN 服务下的高级 DDoS 防护功能的配置模式为 **CDN联动**。

   * **预留资源**：预留的专用 IP 地址。当您订阅高级 DDoS 防护后，CDN 会为您分配一个专属的防护 IP 地址。

   * **防护能力**：高级 DDoS 防护提供的防护能力。固定值为 **全力防护**。**全力防护** 意味着清洗中心的最大防护容量都会被用来防护 DDoS 攻击。

   * **数据传输费用**：安全流量的费用。安全流量的费用按 CDN 传输给客户端的数据量计算。

5. 确认配置无误后，勾选 **我已阅读并同意服务条款、服务等级协议、客户协议**，然后单击 **创建**。

6. 按页面提示完成支付。创建完成的实例会显示在 **DDoS 防护** 页面的实例列表中。


<span id="后续操作"></span>
## 后续操作


1. [添加域名](https://docs.byteplus.com/en/docs/byteplus-cdn/Manage_protected_domains_cn#%E6%B7%BB%E5%8A%A0%E5%9F%9F%E5%90%8D)：创建高级 DDoS 防护实例后，您需要手动添加需要防护的域名。

2. （可选）[查看监控数据](https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-viewing-ddos-attack-protection-information)：您可以通过 Dashboard 查看 DDoS 防护数据如攻击流量、攻击次数、回源流量、出站流量、攻击事件等。
