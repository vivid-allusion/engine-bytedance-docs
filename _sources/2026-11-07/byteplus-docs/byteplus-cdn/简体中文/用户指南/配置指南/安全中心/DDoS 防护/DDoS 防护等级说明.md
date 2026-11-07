---
title: "DDoS 防护等级说明"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DDos_protection_levels_cn"
---

BytePlus CDN 根据您使用的增值服务或套餐版本，提供不同等级的 DDoS 防护。

增值服务包括 CDN 高级 DDoS 防护、WAF 防护等。套餐包括 CDN\-Security\-Plan Standard Edition 和 CDN\-Security\-Plan Advanced Edition。

<span id="7c8edd49"></span>
## **网络层和传输层 DDoS 防护**


|**服务类型** |**防护能力** |**适用对象** |
|---|---|---|
|CDN 原生防护 |* 最小防护带宽：不承诺<br><br>* 最大防护带宽：10 Gbps（依据平台容量调整） |所有用户 |
|CDN 标准 DDoS 防护 |* 最小防护带宽：50 Gbps<br><br>* 最大防护带宽：依据平台容量调整 |* 订阅 CDN\-Security\-Plan Standard Edition 的用户<br><br>* 单独申请开启 CDN 标准 DDoS 防护的用户 |
|CDN 高级 DDoS 防护 |* 最小防护带宽：100 Gbps<br><br>* 最大防护带宽：Tbps 级（尽力防护） |* 订阅 CDN\-Security\-Plan Advanced Edition 的用户<br><br>* 单独采购 CDN 高级 DDoS 防护的用户 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>概念说明：</strong></div>



* <div data-tips="true" data-tips-type="tip"><strong>防护带宽</strong>：指在单次攻击事件中，CDN 平台能够处理的入向异常流量所消耗带宽的总和。您账号下所有域名的异常流量都会被计算在内。</div>


* <div data-tips="true" data-tips-type="tip"><strong>最小防护带宽</strong>：CDN 平台稳定提供的防护能力。</div>


* <div data-tips="true" data-tips-type="tip"><strong>最大防护带宽</strong>：CDN 平台通过动态调度可达到的最高防护能力。<strong>最大防护带宽为参考值。</strong></div>



<div data-tips="true" data-tips-type="tip"><strong>注意事项：</strong></div>



* <div data-tips="true" data-tips-type="tip">使用 CDN 高级 DDoS 防护时，请确保已为相关域名开启防护功能。相关操作，请参考<a href="https://docs.byteplus.com/en/docs/byteplus-cdn/Manage_protected_domains_cn#%E6%B7%BB%E5%8A%A0%E5%9F%9F%E5%90%8D">添加域名到高级 DDoS 防护实例</a>。</div>


* <div data-tips="true" data-tips-type="tip">当攻击流量超出 CDN 平台防护能力且可能影响平台稳定性时，将触发黑洞、域名下线、服务停用等保护机制。您的站点业务可能会因此中断。为降低影响，建议您：</div>


   * <div data-tips="true" data-tips-type="tip">提前订阅增值服务，提升安全防护等级。</div>


   * <div data-tips="true" data-tips-type="tip">在攻击停止后，<a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000735">提交工单</a>申请解除保护机制带来的限制。</div>



<span id="0bc0c4c2"></span>
## **应用层 DDoS 防护**


|**服务类型** |**防护能力** |**适用对象** |
|---|---|---|
|CDN 原生防护 |* 最小防护请求数：不承诺<br><br>* 最大防护请求数：10 万 QPS（依据平台容量调整） |所有用户 |
|搭配 Edge WAF 的应用层 DDoS 防护 |* 最小防护请求数：50 万 QPS<br><br>* 最大防护请求数：300 万 QPS（依据平台容量调整） |* 订阅 BytePlus Edge WAF 的用户<br><br>* 订阅 CDN\-Security\-Plan Standard Edition 的用户<br><br>* 订阅 CDN\-Security\-Plan Advanced Edition 的用户 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>概念说明：</strong></div>



* <div data-tips="true" data-tips-type="tip"><strong>防护请求数</strong>：指在单次攻击事件中，CDN 平台能够处理的异常请求总数。您账号下所有域名的异常请求都会被计算在内。</div>


* <div data-tips="true" data-tips-type="tip"><strong>最小防护请求数</strong>：CDN 平台稳定提供的防护能力。</div>


* <div data-tips="true" data-tips-type="tip"><strong>最大防护请求数</strong>：CDN 平台通过动态调度可达到的最高防护能力。<strong>最大防护请求数为参考值。</strong></div>



<div data-tips="true" data-tips-type="tip"><strong>注意事项：</strong></div>



* <div data-tips="true" data-tips-type="tip">使用搭配 Edge WAF 的应用层 DDoS 防护时，请确保已为相关域名开启防护功能，并按需配置安全策略。相关操作，请参考<a href="https://docs.byteplus.com/en/docs/waf/Adding_a_CDN_domain_name_to_a_WAF_instance">添加域名到 WAF 实例</a>和<a href="https://docs.byteplus.com/en/docs/waf/docs-configuring-rate-limit-policies">配置限流策略</a>。</div>


* <div data-tips="true" data-tips-type="tip">当攻击流量超出 CDN 平台防护能力且可能影响平台稳定性时，将触发沙箱处置、强制限流、域名下线、服务停用等保护机制。您的站点业务可能会因此中断。为降低影响，建议您：</div>


   * <div data-tips="true" data-tips-type="tip">提前订阅增值服务，提升安全防护等级。</div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000735">提交工单</a>申请解除保护机制带来的限制。</div>



<span id="7279419d"></span>
## 更多信息

<span id="51bd7ce6"></span>
### 标准 DDoS 防护和高级 DDoS 防护对比

针对网络层和传输层 DDoS 攻击，CDN 提供标准 DDoS 防护和高级 DDoS 防护。相比于标准 DDoS 防护，高级 DDoS 防护能够提供更高的 DDoS 防护能力。

下表列出了标准 DDoS 防护和高级 DDoS 防护的具体差异。


| |**标准** **DDoS** **防护** |**高级** **DDoS** **防护** |
|---|---|---|
|**服务范围** |* 服务对象：订阅 CDN\-Security\-Plan Standard Edition 的用户或单独申请开启 CDN 标准 DDoS 防护的用户<br><br>* 服务区域：全球（不包含中国内地） |* 服务对象：订阅 CDN\-Security\-Plan Advanced Edition 的用户或订阅高级 DDoS 防护的用户<br><br>* 服务区域：全球（不包含中国内地） |
|**订阅与计费** |如果您订阅了 CDN\-Security\-Plan Standard Edition 或单独申请开启了 CDN 标准 DDoS 防护，在您的域名接入 CDN 后，标准 DDoS 防护将自动开启。您无需额外配置和付费。 |* 订阅 CDN\-Security\-Plan Advanced Edition<br><br><br>系统会自动创建高级 DDoS 防护实例。无需单独支付高级 DDoS 防护的费用。<br><br><br>* 单独采购高级 DDoS 防护<br><br><br>您需要创建高级 DDoS 防护实例并支付使用费。高级 DDoS 防护的费用包括实例费用（预付费）、安全流量费用（后付费）和超出默认配额（50个）的域名的费用（预付费）。安全流量费按 CDN 传输给客户端的数据量计算。计费详情，请参考 [计费说明](https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-pricing)。 |
|**防护方式** |标准 DDoS 防护基于 CDN 分布式节点上的自建 DDoS 防护系统实现。该系统采用了基于快速数据路径（eXpress Data Path，简称 XDP） 技术的防护插件，能够处理高并发流量。 |CDN 拥有全球多区域分布的大容量清洗中心。清洗中心部署了专用的 DDoS 清洗引擎。<br><br>当 DDoS 攻击发生时，攻击流量经 Anycast IP 分散到清洗中心，由 DDoS 清洗引擎拦截。只有正常流量会被传输到 CDN。 |
|**防护能力** |标准 DDoS 防护提供以下防护能力：<br><br><br>* 防护常见量级的网络层和传输层 DDoS 攻击。 |高级 DDoS 防护提供以下防护能力：<br><br><br>* 防护大规模的网络层和传输层 DDoS 攻击。<br><br>* 提供 Tbps 级防护带宽资源。<br><br>* 提供专属的防护 IP 资源。<br><br>* 默认情况下，一个高级 DDoS 防护实例可以防护 50 个域名。如果您需要防护更多的域名，可以额外付费提升域名配额。 |
|**防护范围** |防护常见的攻击，包括 SYN Flood、ACK Flood、RST Flood、空连接攻击、TCP 畸形包攻击、LAND 攻击等 |防护常见的攻击，包括 SYN Flood、ACK Flood、RST Flood、RST/FIN Flood、SYN\-ACK Flood、UDP Flood、UDP 分片、UDP 反射、ICMP 分片、ICMP Flood、Ping of Death、Smurf、Teardrop、IP Options、LAND 攻击等 |
|**监控告警** |标准 DDoS 防护不支持攻击监控和告警功能。如果您的服务疑似因大规模网络攻击而被限制使用和禁用，请[提交工单](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000735)咨询。 |高级 DDoS 防护支持攻击监控和告警功能。您可以通过监控面板（Dashboard）来查看高级 DDoS 防护实例的实时监控数据。当攻击流量达到阈值后，系统会向您发送报警通知。更多信息，请参见[查看监控数据](https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-viewing-ddos-attack-protection-information)。 |


<span id="12536d10"></span>
### 使用高级 DDoS 防护时的注意事项

使用高级 DDoS 防护时，请您关注以下方面的注意事项：


* IPv6

   开启高级 DDoS 防护后，无需手动修改域名的 DNS 解析配置。但是，DNS 会停止将域名解析为 IPv6 地址（即使您在 CDN 的策略中启用了 IPv6），所有客户端流量会指向 IPv4 高防 IP 地址。

* 性能

   开启高级 DDoS 防护会带来一定的域名访问时延。客户端所在区域和网络环境会影响到时延大小。

* 服务区域

   * DDoS 功能的服务区域不包含中国内地：

      * 如果您为域名指定的加速区域为“全球”，仅在除中国内地以外的区域会启用清洗中心。即，只有来自这些区域的客户端流量会经过清洗中心。

      * 如果您为域名指定的加速区域为“中国内地”，则无法为该域名开启 DDoS 防护功能。

   * 为域名开启 DDoS 防护后，您将无法切换域名的加速区域。
