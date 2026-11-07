---
title: "What is BytePlus Web Application Firewall"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/docs-what-is-byteplus-web-application-firewall"
---

BytePlus Web Application Firewall (WAF) provides a complete protection solution for your web applications on BytePlus CDN. WAF detects and filters HTTP/HTTPS request traffic to ensure that each request to the origin server is valid and secure, and invalid or malicious requests are logged or blocked. By preventing malicious attacks, WAF ensures data security while retaining high\-availability for your web applications.

<span id="0a394d77"></span>
## Overview

WAF uses your existing network infrastructure. Simply add your websites to the WAF instance and set up protection rules for safeguarding your web applications from common web threats. After accessing the WAF service, the CDN HTTP/HTTPS traffic is directed to the WAF cluster for real\-time detection and filtering before reaching the origin server.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f26af8409754c9b810a206b5f54aa1c~tplv-goo7wpa0wc-image.image) </span>

<span id="4f6b0edf"></span>
## Key features

Web Application Firewall (WAF) is an out\-of\-the\-box security solution for websites and APIs offering protection against web attacks such as vulnerability exploits, API attacks, layer 7 DDoS attacks, malicious crawlers, etc. It provides rule settings for the following strategies.

<span id="c919808b"></span>
### Access control

WAF access control allows HTTP traffic to be accurately identified and controlled based on custom rules. You can configure detection rules to allow or block traffic from specific IPs or counties/regions. WAF also supports the combination of multiple matching conditions and logical operations based on custom HTTP parameters such as headers, methods, and paths.

<span id="335f5e5b"></span>
### Rate limiting

Rate limiting employs distributed intelligent algorithms that analyze and calculate requests, blocking or limiting traffic when there is a match to the specified rules. You can set rate limiting rules for different objects, including headers, cookies, custom parameters, or IPs.

<span id="84b0f6f1"></span>
### Vulnerability protection

Vulnerability protection utilizes intelligent policies and customized rules to defend against web threats such as vulnerability exploits, SQL injections, XSS attacks, and website Trojans.

<span id="7f84d91f"></span>
### API protection

WAF provides intelligent API protection policies for traffic in\-depth inspection, and logs or blocks request traffic according to your restriction policies.

<span id="06620f8d"></span>
### Bot Management

By enabling or disabling bots, undesired requests and malicious behaviors from external bots can be blocked, while valid traffic is forwarded. You can use the preset bot rules or customize your own bot management rules as needed.

<span id="d52de8bb"></span>
## Why BytePlus WAF?

<span id="ac5a8984"></span>
### Convenient and efficient configuration

Our solution offers a quick and easy security setup without changing your current deployment architecture. Numerous scheduling algorithms ensure effective management and distribution of traffic.

<span id="bf139a3d"></span>
### Advanced custom access control

WAF presents an advanced access control capability system for users in a comprehensive way. It comes with robust rule configuration allowing for highly granular countermeasures, providing matching logic and detection capabilities for different request characteristics.

<span id="a3c5acbf"></span>
### Visualized security status

WAF provides a visualization of the overall security of your website applications. It collects, analyzes, and summarizes data on all the access traffic and presents views by events, durations, traffic, rules, etc.

<span id="32e4ea4a"></span>
## Applicable scenarios

<span id="0490e867"></span>
### Protecting against layer 7 DDoS attacks

Layer 7 DDoS attacks, also known as application layer attacks, target the top layer in the OSI model where web requests like HTTP GET and HTTP POST occur. These attacks are malicious and consume significant server and network resources, resulting in the inability to provide services to normal users. With configured rules for objects, WAF can accurately identify and mitigate these layer 7 DDoS attacks and maintain the stability of your website communications.

<span id="e9ef7e98"></span>
### Anti\-automation

Automated attacks are executed by malicious actors who leverage automated software or bots to scan, probe, and exploit target systems. These attacks can be highly efficient and scalable, allowing attackers to target multiple systems simultaneously or repeatedly. These attacks are designed to exploit vulnerabilities or weaknesses in computer systems or networks with the goal of gaining unauthorized access, causing damage, or extracting sensitive information. WAF provides anti\-automation protection to safeguard against data scraping and ultimately prevents potential business losses.

<span id="f844dbef"></span>
### Preventing malicious competition attacks

Malicious competitors can use automated tools to target and attack competitors' websites to weaken their business. Attackers may employ tactics such as malicious registration, fake reviews and ratings, and coupon fraud. WAF can enforce rate limiting rules, employ bot detection mechanisms, detect common vulnerabilities, and monitor and log suspicious requests, enabling your business to escape unfair competition and reduce the potential business losses caused by malicious attacks.
