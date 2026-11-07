---
title: "Priority of global policies"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/Priority_of_global_policies"
---

This article mainly introduces the global rule matching priority mechanism of the BytePlus Web Application Firewall. Through explanations of fundamental principles, illustrative examples, and best practices, it helps you gain a deeper understanding of how WAF works, master rule configuration methods, and enhance security protection. To configure multiple protection rules that may conflict, or to troubleshoot the reasons why specific requests are unexpectedly blocked or allowed, it is essential to understand the rule matching priority.

<span id="ca290803"></span>
## Basic logic

WAF adopts a **multi\-layered priority mechanism** and performs layer\-by\-layer inspection and processing of HTTP requests according to the predefined rule matching sequence.

<span id="4c0b83a7"></span>
### Matching principles


* **Priority order**: WAF performs detection sequentially according to the priority of protection rules, with higher\-priority rules being matched and executed first.

* **Allowlist privilege**: The allowlist has the highest priority. Once a request matches the allowlist rule, the system will allow the request directly and will not perform any further checks.

* **Short\-circuit processing**: The system determines whether to continue subsequent detection based on the type of rule action.

   * When a termination\-type action is triggered (rate limiting, blocking, JS challenge, CAPTCHA, or proof of work), the short\-circuit mechanism will be activated, terminating subsequent detection.

   * When a request matches a non\-terminal action (allow or observe), it will continue to flow to lower\-priority rules for further inspection.

* **Order of matching within a rule**: Multiple matching conditions within a single rule are executed in order of priority: domain name \> path \> advanced conditions (including request method, request protocol, User\-Agent, Referer, and more).


<span id="6c239d4b"></span>
### Policy classification

BytePlus WAF divides protection policies into the following categories, and each category differs in configuration complexity and impact on performance:


|Policy type |Main features |Configuration complexity |Performance impact |
|---|---|---|---|
|**Access control** |IP allowlist/blocklist management |Simple |Low |
|**Geographic location access control** |Manage access sources by region |Simple |Low |
|**Vulnerability protection** |Web vulnerability detection and protection |Medium |Medium |
|**API protection** |Api security management |Simple |Medium |
|**Bot management** |Automation tools identification and protection |Complexity |High |
|**Rate limiting** |Rate limiting and Layer 7 DDoS protection |Medium |Medium |
|**Sensitive information leak** |Response content filtering |Medium |Low |
|**web tamper protection** |Page cache protection |Simple |Low |


<span id="f77d3385"></span>
### Data type of matching condition

Note: ✅ indicates support for configuring matching conditions for this data type, while \- indicates no support.


|Primary policy |Secondary rules |Protected domain name |Access path |Advanced conditions |Frequency threshold |
|---|---|---|---|---|---|
|Access control |allowlist |✅ |✅ |✅ |*  |
|Access control |blocklist |✅ |✅ |✅ |*  |
|Geolocation access control |*  |✅ |*  |*  |*  |
|Customize the intercept response |*  |✅ |✅ |✅ |*  |
|Rate limiting |Custom |✅ |✅ |✅ |✅ |
|Vulnerability protection |Managed vulnerability protection rules |✅ |*  |*  |*  |
|Vulnerability protection |Request allowlist |✅ |*  |✅ |*  |
|Vulnerability protection |Field highlighting |✅ |*  |*  |*  |
|Vulnerability protection |Directory traversal |✅ |*  |*  |✅ |
|Vulnerability protection |High\-frequency scanning |✅ |*  |*  |✅ |
|API protection |Default route (API execution actions that have not been registered) |✅ |*  |*  |*  |
|API protection |Manually add |✅ |✅ |*  |*  |
|API protection |Automatic discovery |✅ |*  |*  |*  |
|Bot management |Bot custom categories |✅ |*  |✅ |*  |
|Bot management |Bot hosting categories |✅ |*  |*  |*  |
|Bot management |Bot rate limiting |✅ |✅ |✅ |✅ |
|Bot management |Statistical bot protection |✅ |✅ |✅ |✅ |
|Bot management |Bot's dynamic token |✅ |✅ |*  |*  |
|Bot management |Behavior map |✅ |*  |*  |*  |
|Data leak prevention |*  |✅ |✅ |✅ |*  |
|Web tamper\-proofing |*  |✅ |✅ |*  |*  |


<span id="5fb64970"></span>
### Priority order

Perform matching for the corresponding rules in sequence. If a rule is matched and its action is of a terminating type, stop the checking process and handle the corresponding request according to the specified action.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following policies do not inspect request content and therefore do not participate in priority sorting for now:</div>



* <div data-tips="true" data-tips-type="tip">Custom interception response (configure custom response codes and response content to return to the client, providing specific feedback when interception rules are triggered).</div>


* <div data-tips="true" data-tips-type="tip">Prevent sensitive information leakage (identify sensitive information in responses and prevent disclosure of private information).</div>


* <div data-tips="true" data-tips-type="tip">Web tamper protection strategy (returns cached pages to prevent illegal tampering with the website under protection, ensuring the integrity and security of the website).</div>




|Priority |Primary policy |Secondary rules |
|---|---|---|
|1 |Access control |Allowlist |
|2 |Access control |Blocklist |
|3 |Rate limiting |Custom rate limiting rules |
|4 |Rate limiting |Intelligent protection (BytePlus only) |
|5 |Geo\-based access control |*  |
|6 |Bot management |Custom category |
|7 |Bot management |Managed categories |
|8 |Bot management |Rate limiting |
|9 |Bot management |Statistical protection |
|10 |Bot management |Behavior map |
|11 |Bot management |Dynamic token |
|12 |API protection |Unregistered API actions |
|13 |API protection |Manually add |
|14 |API protection |Automatic discovery |
|15 |Vulnerability protection |Request allowlist |
|16 |Vulnerability protection |Match variable allowlist |
|17 |Vulnerability protection |Vulnerability hosting rules |
|18 |Vulnerability protection |High\-frequency scanning |
|19 |Vulnerability protection |Directory traversal |


<span id="0e43e964"></span>
## Example

In the following, we use a request that meets multiple protection rules simultaneously as an example to explain in detail to you the corresponding rule matching logic and order.

<span id="dd16b15a"></span>
### Protection rules details

Suppose the following protection rules are configured in the WAF console:


|Priority |Rule type |Rule content |Perform action |
|---|---|---|---|
|1 |Access control\-allowlist |* Rule name: Internal network IP list<br><br>* Protected domain: example.com<br><br>* Access source: 192.168.1.100<br><br>* Access path: /admin.html |Release |
|2 |Access control \- blocklist |* Rule name: Denylist of IP addresses<br><br>* Protected domain name: example.com<br><br>* Source IP: 185.220.1.1<br><br>* Access path: /admin.html |Observation |
|16 |Vulnerability protection \- field allowlisting |* Allowlist the refer field<br><br>* Protected domain name: example.com<br><br>* Allowlist region: Request header<br><br>* Allowlist field: Referer |Allowlisted fields skip vulnerability checks |
|17 |Vulnerability protection \- managed protection rules |* Protection level: normal |Intercept |


<span id="6247f99f"></span>
### HTTP request

To fully demonstrate the WAF rule matching priority mechanism, we construct a real HTTP request containing multiple attack characteristics:

```HTTP
POST /api/user/login HTTP/1.1
Host: example.com
X-Forwarded-For: 185.220.1.1
X-Real-IP: 185.220.1.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Content-Length: 59
Cookie: sessionid=abc123
Referer: http://malicious-scanner.com/scan
Connection: keep-alive

username=admin' OR '1'='1'--&password=123456&remember=true
```


<span id="03a70c0d"></span>
### Analysis of attack characteristics


|Attack type |Specific features |Location |Corresponding detection rules |
|---|---|---|---|
|**Malicious IP** |`185.220.1.1` |X\-Real\-IP |Access control \- blocklist |
|**Suspicious sources** |`malicious-scanner.com` |Referer |Vulnerability protection \- field allowlisting |
|**SQL injection** |`username=admin' OR '1'='1'--&password=123456&remember=true` |POST Body |Vulnerability protection \- vulnerability management |


<span id="ada5c197"></span>
### Actual rule matching process

When this malicious request reaches the WAF, the following checks are performed in order of priority:


|Order |Rule |Detection content |Rule configuration |Matching results |Next step |
|---|---|---|---|---|---|
|1 |Allowlist |Is the request source 185.220.1.1 in the allowlist? |192.168.1.100 |Mismatch |Continue detection |
|2 |Blocklist |Is the request source 185.220.1.1 in the blocklist? |185.220.1.1 |Match |Perform actions of the non\-terminating type (observation), continue monitoring |
|3 |Allowlist rules for vulnerability protection fields |The referer field of the request header |Add the referer field in the request header to the allowlist |Match |The content of the Referer field is exempted; detection will continue. |
|4 |Managed vulnerability protection rules |Is there a risk of vulnerability attacks in the request content? |Enable managed rules for vulnerability protection and set the protection level to normal |Matching (<br><br>`username=admin' OR '1'='1'--&password=123456&remember=true` poses a risk of SQL injection) |When the action is executed as a terminating (interception) action, subsequent checks are stopped. |


<span id="7e1a1ee4"></span>
## Best practices

The following are some practical recommendations for WAF rule configuration and troubleshooting to help you make effective use of the WAF rule matching priority mechanism and enhance protection and system performance.

<span id="1bf41bae"></span>
### Rule configuration recommendations


|Configuration approach |Typical scenarios |Important notes |
|---|---|---|
|**Trust first** |internal IP address, monitoring interface, and special fields |Avoid unintended blocking of critical business operations |
|**Access control** |API management, malicious IP blocking |Balance security and usability |
|**Behavior detection** |Scan protection, rate limiting |Set reasonable thresholds and time windows |
|**Intelligent protection** |Bot detection, behavior analysis |Focus on false positive rate and user experience |
|**Content inspection** |Vulnerability protection, information leakage |Update the rule library regularly |


<span id="52cefce9"></span>
### Performance optimization policies

WAF performance optimization is the key to ensuring business availability. The following are specific optimization policies:


* **Allowlist prioritization**: Quick pass for trusted traffic

* **Exact match**: Avoid overly broad matching criteria

* **Reasonable thresholds**: Set appropriate thresholds for rate limiting and statistical protection

* **Rule simplification**: Regularly clean up invalid and duplicate rules

* **Simplicity first, complexity later**: Place complex conditions after and simple conditions before


<span id="cc7734af"></span>
## FAQs and solutions


|Problem data type |Symptom description |Possible causes |Solution |
|---|---|---|---|
|**False positive interception** |Normal request intercepted |Overly strict rules, IP false positive |Add allowlist, adjust rule parameters |
|**Missed detection** |Attack requests were not intercepted |Incomplete rule coverage and priority issues |Improve the rule library, adjust priorities |
|**Business continuity issues** |Response latency increases |Too many rules, complex matching |Optimize rules, enable short\-circuit mechanism |
