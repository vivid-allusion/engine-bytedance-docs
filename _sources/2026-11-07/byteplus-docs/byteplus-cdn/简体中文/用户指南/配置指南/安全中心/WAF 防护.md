---
title: "WAF 防护"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-web-application-firewall-waf--cn"
---

<span id="功能介绍"></span>
## 功能介绍

BytePlus CDN 集成了 BytePlus Web 应用防火墙（WAF）的安全防护能力，为接入域名提供针对应用层攻击的防护能力。CDN 通过在内容分发链路中嵌入 WAF 防护模块，实现对访问请求的过滤与控制。

在您为接入 CDN 的域名启用 WAF 防护功能后，所有针对该域名发起的 HTTP 和 HTTPS 访问请求都会经过 WAF 防护模块的处理。具体流程如下：


1. **请求路由**：客户端发起的访问请求到达 CDN 边缘节点后，首先经过 CDN 分发策略中的请求控制规则处理。然后，通过的请求会被转发到 WAF 防护模块进行安全检测。

2. **WAF检测**：WAF 防护模块依据预设的防护规则对请求进行深度分析，然后根据分析结果对请求进行处理。防护规则包括访问控制、CC 攻击防护、漏洞防护、Bot 管理和API 防护规则等。

   * **合法请求处理**：经 WAF 防护模块判定为合法的请求将被放行，继续在 CDN 中进行处理。CDN 会根据缓存策略判断是否直接从边缘节点的缓存中获取内容，或向源站请求内容。

   * **非法请求处理**：经 WAF 防护模块判定为非法的请求将被阻断或被记录在攻击日志中。请求被阻断时，系统支持向客户端返回自定义响应页面，同时生成详细的攻击日志。攻击日志包含被攻击域名、发起攻击的 IP 地址、攻击发生时间等信息，便于后续安全审计与溯源分析。


通过将 WAF 防护功能深度集成于 CDN 架构中，CDN 在保障内容分发效率的前提下，实现对 Web 应用的实时安全防护。

<span id="应用场景"></span>
## 应用场景

WAF 防护功能主要用于以下场景：访问控制、CC 攻击防护、漏洞防护、Bot 管理和 API 防护。

<span id="访问控制"></span>
### 访问控制

访问控制规则能够实现对 HTTP 请求的精准识别和控制。您可以配置自定义规则，基于访问源和 HTTP 请求特征来允许或阻止特定请求。

访问源可以是 IP 地址、IP 地址段或者地理位置。HTTP 请求特征包含请求路径、请求 URI、请求协议、请求方法、请求参数、请求头、自定义 Header、自定义 Cookie 等。

<span id="cc-攻击防护"></span>
### CC 攻击防护

CC 攻击（Challenge Collapsar） 是一种针对 Web 应用服务器的七层 DDoS 攻击。攻击者通过发送大量看似合法的 HTTP 请求来消耗目标服务器的资源，最终导致服务器无法正常响应合法用户的请求。

您可以自定义 CC 防护规则。系统根据您配置的 HTTP 请求特征和统计条件，对检测到的 CC 攻击执行相应动作，从而实现精准的流量阻塞或限制。

<span id="漏洞防护"></span>
### 漏洞防护

内置的防护规则为您的 Web 应用提供全方位保护，有效防御针对常见漏洞（包括 CVE 披露漏洞和 OWASP TOP 10 漏洞）的 Web 攻击威胁。

防护规则类型覆盖 SQL 注入、命令注入、服务端请求伪造（SSRF）、跨站脚本攻击（XSS）、XML 实体注入（XXE）、文件目录遍历、LDAP 注入、XPath 注入、服务端模版注入（SSTI）、表达式注入等。

<span id="bot-管理"></span>
### Bot 管理

Bot 管理规则能够有效阻止来自外部 Bot 的恶意请求和行为，确保只有合法请求正常转发。托管 Bot 管理规则对常见 Bot 进行分类并按照默认设置执行相应动作。

您也可以根据业务需求自定义 Bot 管理规则，基于 HTTP 请求特征实现精细化 Bot 管理。

<span id="api-防护"></span>
### API 防护

API 防护规则能够根据配置的 API 路径、请求方法和参数来检查 API 请求，对符合指定特征的 API 请求执行拦截或观察动作。

API 防护能够利用智能检测和学习能力来识别存在风险的 API 请求行为，并将相关 API 记录到自动添加的 API 防护规则中。您也可以手动创建 API 防护规则。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">更详细的防护能力说明和规则配置指引，请参考 <a href="https://docs.byteplus.com/en/docs/waf/docs-what-is-byteplus-web-application-firewall">BytePlus WAF 文档</a>。</div>


<span id="使用流程"></span>
## 使用流程

<span id="配置-waf-防护"></span>
### 配置 WAF 防护

如需使用 WAF 防护功能防护您的域名，您需要执行以下操作：


1. [创建 WAF 实例](https://docs.byteplus.com/en/docs/waf/docs-system-management)。

2. [将域名添加到 WAF 实例](https://docs.byteplus.com/en/docs/waf/Adding_a_CDN_domain_name_to_a_WAF_instance)。

3. [配置防护规则](https://docs.byteplus.com/en/docs/waf/docs-introduction-to-custom-waf-rules)。


<span id="查看接入域名的-waf-防护状态"></span>
### 查看接入域名的 WAF 防护状态

在 CDN 控制台的 [WAF 防护](https://console.byteplus.com/cdn/cdn-bp/security/waf-protection)页面，您可以查看已接入到 CDN 的域名是否开启了 WAF 防护。
