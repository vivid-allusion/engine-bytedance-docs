---
title: "DDoS 防护概述"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DDos_protection_overview_cn"
---

<span id="什么是-ddos-攻击？"></span>
## 什么是 DDoS 攻击？

分布式拒绝服务攻击（Distributed Denial of Service，简称 DDoS）是一种类型的网络攻击。攻击者利用多台受感染的设备如计算机等同时向目标服务器发送大量数据包或请求。这些 DDoS 攻击会迅速耗尽目标服务器的带宽、CPU 和内存等资源，导致目标服务器无法处理正常流量或响应正常请求。

DDoS 攻击通常发生在 OSI 模型的网络层（三层）、传输层（四层）和应用层（七层）：


* 网络层攻击

   攻击者利用大量伪造的 IP 地址向目标服务器发送大量数据包，导致目标服务器的网络带宽被耗尽，无法处理正常的网络流量。

* 传输层攻击

   攻击者利用大量伪造的 IP 地址向目标服务器发送大量 TCP 或 UDP 连接请求，消耗目标服务器的连接资源，导致服务器无法处理正常的连接请求。

* 应用层攻击

   攻击者利用大量伪造的请求，向目标服务器发送大量 HTTP 请求，消耗目标服务器的资源如 CPU 和内存等，导致服务器无法响应正常请求。


DDoS 攻击可能导致业务中断，带来严重的经济损失。游戏、电商、金融等行业的互联网应用和网络基础设施是 DDoS 攻击的主要目标。

<span id="byteplus-cdn-提供的-ddos-防护"></span>
## BytePlus CDN 提供的 DDoS 防护

BytePlus CDN （后文简称 CDN） 通过 DDoS 防护和 WAF 防护功能，提供完善的 DDoS 攻击防护。DDoS 防护功能能够拦截网络层和传输层的 DDoS 攻击。WAF 防护功能能够拦截应用层的 DDoS 攻击。通过这些防护措施，CDN 能够帮助您有效降低 DDoS 攻击带来的风险，保障您的源站安全和业务稳定。

<span id="网络层和传输层-ddos-防护"></span>
### 网络层和传输层 DDoS 防护

当您使用 CDN 服务来分发 Web 内容时，您的源站被隐藏在 CDN 服务后，避免遭受直接的攻击。

然而，攻击者仍可能向您的域名或域名所关联的 CDN 服务 IP 地址发起攻击。当您的域名引发大规模针对服务 IP 地址的 DDoS 攻击时，受影响的 IP 地址可能会被禁用并造成暂时的服务中断。在该情形下，您的业务可能也会受到影响。

针对向 IP 地址发起的网络层和传输层 DDoS 攻击，CDN 提供两种级别的安全防护服务：


* 标准 DDoS 防护：基于 CDN 边缘节点上的自建 DDoS 防护系统实现对 DDoS 攻击的防护。标准 DDoS 防护提供基础的 DDoS 防护能力，能够防护常见量级的 DDoS 攻击。

* 高级 DDoS 防护：基于全球多地域分布的大容量清洗中心，提供针对大规模 DDoS 攻击的防护能力。如果标准 DDoS 防护提供的防护能力不能满足您的业务正常运行需求，您可以订阅高级 DDoS 防护。


关于标准 DDoS 防护和高级 DDoS 防护的更多介绍，请参见 [标准 DDoS 防护和高级 DDoS 防护对比](https://docs.byteplus.com/en/docs/byteplus-cdn/DDos_protection_levels_cn#%E6%A0%87%E5%87%86-ddos-%E9%98%B2%E6%8A%A4%E5%92%8C%E9%AB%98%E7%BA%A7-ddos-%E9%98%B2%E6%8A%A4%E5%AF%B9%E6%AF%94)。

<span id="应用层-ddos-防护"></span>
### 应用层 DDoS 防护

向域名发起的应用层 DDoS 攻击有以下特点：攻击流量往往难以与正常的客户端访问流量区分。因此，攻击流量可能会到达源站，对源站安全造成严重威胁。此外，还可能会造成高额的 CDN 账单。

为应对这种攻击威胁，CDN 的 WAF 防护功能提供了应用层 DDoS 防护能力。您可以利用系统预设防护策略和自定义防护策略来识别和过滤攻击流量。

关于 WAF 防护功能的详细介绍，请参见 [WAF 防护](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-web-application-firewall-waf--cn)。

&nbsp;
