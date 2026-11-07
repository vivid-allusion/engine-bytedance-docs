---
title: "WAF protection"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-web-application-firewall-waf-"
---

<span id="feature-introduction"></span>
## Feature introduction

BytePlus CDN integrates BytePlus Web Application Firewall (WAF) security capabilities to protect domains against application layer attacks. By embedding the WAF protection module into the content delivery process, CDN effectively filters and controls incoming access requests.

After you enable WAF protection for a domain connected to CDN, all HTTP and HTTPS requests to that domain undergo processing by the WAF protection module. The process works as follows:


1. **Request routing**: When client requests arrive at CDN edge nodes, they are first processed by access management rules specified in CDN's delivery policies. Then, the requests that pass this processing are forwarded to the WAF protection module for security inspection.

2. **Security inspection**: The WAF protection module conducts in\-depth analysis of each request based on predefined protection rules and processes them according to the analysis results. These protection rules include access control, CC attack protection, vulnerability protection, Bot management, and API protection rules.

   * **Processing of legitimate requests**: Requests identified as legitimate by the WAF protection module proceed through the CDN system. CDN then determines whether to serve content directly from the corresponding edge node's cache or fetch the content from the origin server based on caching rules.

   * **Processing of malicious requests**: Requests identified as malicious are either blocked or logged in attack records. For blocked requests, the system can return a customized response page to clients while generating detailed attack logs. An attack log includes information such as the targeted domain name, the attacker's IP address, and the attack time, facilitating security audits and analysis.


By integrating WAF protection, CDN delivers real\-time security for web applications while maintaining optimal content delivery performance.

<span id="application-scenarios"></span>
## Application scenarios

The WAF protection feature addresses various security scenarios, including access control, CC attack protection, vulnerability protection, Bot management, and API protection.

<span id="access-control"></span>
### Access control

Access control rules provide precise identification and management of HTTP requests. You can create custom rules to allow or block specific requests based on their sources and characteristics.

Access sources may include IP addresses, IP address ranges, or geographic locations. HTTP request characteristics cover request paths, URIs, protocols, methods, parameters, standard headers, custom headers, cookies, and more.

<span id="cc-attack-protection"></span>
### CC attack protection

Challenge Collapsar (CC) attacks are Layer 7 DDoS attacks targeting web application servers. Attackers overwhelm target servers by flooding them with seemingly legitimate HTTP requests, ultimately preventing normal service to legitimate users.

You can create custom CC protection rules that execute specific actions based on your configured HTTP request characteristics and statistical thresholds, enabling precise traffic blocking or rate limiting.

<span id="vulnerability-protection"></span>
### Vulnerability protection

The built\-in protection rules offer comprehensive security for your web applications, effectively defending against attacks that exploit common vulnerabilities including CVE\-identified vulnerabilities and vulnerabilities categorized in the OWASP Top 10.

Protection rules cover numerous attack methods including SQL injection, command injection, Server\-Side Request Forgery (SSRF), Cross\-Site Scripting (XSS), XML External Entity (XXE) injection, directory traversal, Lightweight Directory Access Protocol（LDAP）injection, XPath injection, Server\-Side Template Injection (SSTI), and expression injection.

<span id="bot-management"></span>
### Bot management

Bot management rules effectively block malicious requests and behaviors from external bots, ensuring that only legitimate requests reach your applications. Managed bot rules automatically categorize common bots and apply appropriate actions based on default configurations.

You can also create custom bot management rules tailored to your business requirements, implementing granular control based on specific HTTP request characteristics.

<span id="api-protection"></span>
### API protection

API protection rules examine API requests according to configured request paths, methods, and parameters, and then apply "Block" or "Observe" actions to requests matching specified request characteristics.

The system leverages intelligent detection and learning capabilities to identify risky API request behaviors and record relevant APIs in automatically added API protection rules. You can also manually create custom API protection rules.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For detailed information about protection capabilities and rule configuration guidelines, see the <a href="https://docs.byteplus.com/en/docs/waf/docs-what-is-byteplus-web-application-firewall">BytePlus WAF documentation</a>.</div>


<span id="usage-process"></span>
## Usage process

<span id="configure-waf-protection"></span>
### Configure WAF protection

To implement WAF protection for your domain, complete the following steps:


1. [Create a WAF instance](https://docs.byteplus.com/en/docs/waf/docs-system-management).

2. [Add your domain to the WAF instance](https://docs.byteplus.com/en/docs/waf/Adding_a_CDN_domain_name_to_a_WAF_instance).

3. [Configure protection rules](https://docs.byteplus.com/en/docs/waf/docs-introduction-to-custom-waf-rules).


<span id="view-waf-protection-status"></span>
### View WAF protection status

You can visit the [WAF protection](https://console.byteplus.com/cdn/cdn-bp/security/waf-protection) page in the CDN console to check the WAF protection status for your domains connected to CDN.
