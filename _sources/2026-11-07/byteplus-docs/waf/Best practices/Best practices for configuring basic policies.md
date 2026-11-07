---
title: "Best practices for configuring basic policies"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/Best_practices_for_API_protection_and_auto-discovery"
---

When first connecting to the Web Application Firewall, you need to understand the differences in protection strategies, configuration order, and configuration methods, among others. For example, you may not know which basic protection strategies should be configured for the newly integrated business, and how to configure these strategies to achieve optimal protection for your business. This article primarily introduces the basic configuration after the initial connection to the Web Application Firewall. You can determine based on specific scenarios whether relevant strategies need to be configured.

<span id="d95478a1"></span>
## Configure vulnerability protection policies

WAF provides a rule set for vulnerability protection management, supporting common public vulnerabilities and exposures (CVE) and [OWASP Top 10](https://owasp.org/www-project-top-ten/) vulnerabilities. It is divided into three types of protection: general detection, logical vulnerabilities, and Web backdoors, each corresponding to different vulnerability detection rules, as detailed below.


* General detection: detection and protection against common vulnerability attacks such as SQL injection, command injection, expression injection, XPath injection, LDAP injection, arbitrary file read/directory traversal, LFI, SSTI, SSRF, XSS, etc.

* Logical vulnerabilities: detection and interception of some middleware that has access control issues and form bypass vulnerabilities.

* Web backdoors: detection of web commands that exist in the form of web files such as asp, php, jsp, or cgi, to intercept web trojans. You can choose different protection levels to adapt to the protection needs of various attack scenarios. The stricter the protection level, the more complex the detection rules, covering a wider range of detection.


<span id="be76f4bc"></span>
### Steps


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. Select the instance region in the top menu bar.

3. In the left navigation, select **Protection Policy \> Vulnerability Protection**.

4. Enable the vulnerability protection feature for the domain to be protected.

   1. Select the domain to be protected.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Confirm that the protection mode of the current domain is "Protection enabled". Otherwise, you need to change the protection mode.      </div>
      

   2. Turn on the vulnerability protection switch; it will only take effect after being turned on.

   3. Select the protection mode as **Normal**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The normal mode includes common detection rules for certain types of attacks or rules with fewer false positives, including all rules classified as loose and normal. This is suitable for general protection scenarios.      </div>
      

   4. Set the protection action to **intercept**.

      All detected attack requests will be directly intercepted, and the request behavior will be reported to the attack log.


<span id="0a72027a"></span>
### Configuration results

After enabling vulnerability protection detection, the WAF will automatically detect requests that may pose vulnerability threats based on preset detection rules. For example, by identifying malicious SQL code in the requests to intercept SQL injection attacks; or by identifying malicious JavaScript code carried in the requests to intercept cross\-site scripting (XSS) attacks, etc. Details of the intercepted requests can be viewed in the attack details or log management page.

<span id="a994846e"></span>
## Configure rate limiting policies

The rate limiting policy can prevent excessive occupation of your server resources, ensuring that normal access services are not affected. The WAF provides two modes: custom and intelligent protection. When both are enabled, the system first matches custom protection rules, and then dynamically adjusts based on the intelligent protection policy.


* CC custom protection: Supports flexible customization of white traffic request characteristics based on business situations. Requests can be restricted based on various HTTP request objects such as network access IP and Session to mitigate the impact of CC attacks on the server.

* CC intelligent protection (currently free for a limited time and only available for the premium version and above): WAF forms an asset profile through autonomous business traffic baseline learning, providing customized intelligent protection strategies for assets, while continuously analyzing traffic baselines and dynamically adjusting protection strategies based on business circumstances. After enabling the CC intelligent protection feature, WAF will initiate business traffic baseline learning upon monitoring request traffic. The initial learning period is approximately 7 days, and after learning is completed, intelligent protection rules will be pushed and activated, with rules continuously updated.


<span id="7e5dc5f3"></span>
### Notes


* The CC intelligent protection feature is currently in a limited\-time free phase and is available only for the premium version and above.

* The order of effectiveness for the two protection modes: prioritize matching custom protection rules, and then dynamically adjust according to intelligent protection strategies.


<span id="d580a03d"></span>
### Configure custom rate\-limiting policies

Custom rate\-limiting policies are based on the request path and the number of visits of custom statistical objects within a certain time period to perform corresponding actions on access requests.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you cannot temporarily determine the threshold for the specific path's number of visits, you can first configure a CC protection policy that applies to all paths, setting the threshold slightly below the maximum QPS capacity of the origin site. Observe whether there are any signs of attacks or traffic surges.</div>


<span id="c1f9cabd"></span>
#### Steps


1. Log in to [the Web Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. Select the instance region in the top menu bar.

3. In the left navigation select **Protection Policy \> Rate limiting**.

4. Turn on the CC protection function of the domain name to be protected.

   1. Select the domain name to be protected.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Confirm that the protection mode of the current domain is "Protection enabled". Otherwise, you need to change the protection mode.      </div>
      

   2. Turn on the Rate limiting switch.

5. Click **Add** to configure the relevant parameters.

   * Request path: /\*

   * Statistical object: Source IP

   * Threshold setting: Effective permanently, each object accesses more than 1000 times, and the request path accesses more than 1000 times

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">It is recommended to set this count threshold slightly lower than the QPS capacity limit of the source station.      </div>
      

   * Execution action: Observe

   * Priority: P0

   * Regular switch: Enable


<span id="3a6aff2d"></span>
#### What to do next

Observe the protection overview data and traffic logs. If there are false positive events, it is recommended to increase the count threshold to allow legitimate traffic.

<span id="b6297f70"></span>
### Configure intelligent rate\-limiting policy

The initial learning period for CC intelligent protection policy is approximately 7 days. After completion, intelligent protection rules will be pushed and enabled, and rules will be continuously updated. Therefore, it is recommended to enable CC intelligent protection function as soon as possible after connecting to the WAF service, so the system can complete learning faster and provide intelligent protection.

<span id="c820a478"></span>
#### Steps


1. Log in to [ Web](https://console.byteplus.com/waf/dashboard) [Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. In the top menu bar, select the region of your instance.

3. In the left navigation select **Protection Policy CC**. **Protection**.

4. Turn on the CC access function of the domain name to be protected.

   1. Select the domain name to be protected.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Confirm that the protection mode of the current domain is "Protection enabled". Otherwise, you need to change the protection mode.      </div>
      

   2. Turn on the CC intelligent protection switch.

   3. Set the mode to **Managed Mode \- Normal**, with the action as **Intelligent Managed**.


<span id="095c4f92"></span>
#### What to do next

Adjust parameter settings based on business status and protection effectiveness.


* If your business is under attack, it is recommended to promptly switch the mode to **emergency mode**.

* If the current intelligent protection is not effectively blocking the attack, it is recommended to set the protection threshold range to **more stringent**.


<span id="5c38f6f0"></span>
## Configure Bot management policies

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When black and gray production confrontations are detected in business operations, or when facing crawling or malicious registration behaviors, it is necessary to enable this function. </div>


Bot management helps you monitor or limit the traffic of common automation tools, such as search engines, speed test tools, content aggregators, scanning tools, etc., and supports the use of hosted Bot management rules or custom Bot management rules. You can also configure frequency limiting and statistical protection rules to prevent malicious access behaviors that meet statistical characteristics. In the basic policy configuration, you can enable hosted Bot classification rules to execute actions and rule switches according to the system's default Bot types to control the traffic of different Bots.

<span id="5ZPLicBY"></span>
### Notes

The Bot management function is currently only available for premium versions and above.

<span id="435db707"></span>
### Steps


1. Log in to [Web](https://console.byteplus.com/waf/dashboard) [Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. In the top menu bar, select the region of your instance.

3. Select **Protection Policy＞Bot Management** in the left navigation.

4. Enable the managed Bot classification rules feature for the domain to be protected.

   1. Select the domain to be protected.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Confirm that the protection mode of the current domain is "Protection enabled". Otherwise, you need to change the protection mode.      </div>
      

   2. Turn on the managed Bot classification rules switch.

5. Enable all Bot detection rule switches and set the execution action to **Observe**.


<span id="2e6eed41"></span>
### What to do next

You can go to **Security Overview＞Attack Overview＞Bot Protection** to view attack detection data within specific events (attack sources and attacked domains) and determine if there are false positives. If the detection result meets expectations, it is recommended to change the action executed by the hosted Bot rule to **intercept** in order to block illegal requests.

<span id="8ee84e2f"></span>
## Configure API protection policies

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When there is a need to manage, monitor, and protect all APIs on the website, this rule can be utilized for overall management and protection of the website's APIs. API protection policies enable the WAF to inspect API request traffic based on predetermined API formats and parameters. This allows it to filter and block unauthorized API requests that meet certain rules. You can manually set protection policies for specific API endpoints and request methods, or automatically record APIs using the API auto\-discovery function.</div>


<span id="5adbbdcf"></span>
### Notes

The API auto\-discovery function is currently in a limited time free phase and is only open to enterprise versions and above.

<span id="dd9fcfa4"></span>
### Steps


1. Log into [Web Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. Select the region of your instance in the top menu bar.

3. In the left navigation, select **Protection Policies \> API Protection**.

4. Enable auto\-discovery function.

   1. Select the domain to be protected.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Confirm that the protection mode of the current domain is "Protection enabled". Otherwise, the protection mode needs to be changed.      </div>
      

   2. Activate the API protection switch.

   3. Set unregistered API execution action as **Do not check**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Unregistered APIs are API requests that have neither been added manually nor included in the API automatic discovery list. After configuration, the traffic of these requests will be directly permitted, and the request behavior will be reported to the access log.      </div>
      

   4. Set AI protection (auto discovery) as **enabled**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Once enabled, if the WAF detects an API request that poses risks, it will automatically generate an API rule with the execution action of "Monitoring", and the status of this rule will be "Discovered".      </div>
      

<span id="30ce5a4c"></span>
## Configure log parameters

The platform supports collecting web attack and access log data for defense resources already added to the WAF, and provides retrieval analysis, monitoring alerts, data visualization and other functions based on BytePlus log services, helping you quickly understand the status of web request operations and defense effectiveness, so you can deal with anomalies promptly.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">It is recommended to add all protected domain names to the log collection scope to avoid exposing domain names to attack risks due to incomplete log data collection.</div>



1. Log in to [the Web Application Firewall Console](https://console.byteplus.com/waf/region:waf+cn-gaofang-nt3/purchase-guide).

2. Select the instance region in the top menu bar.

3. Select **Log Management** from the left navigation to enter the log management page.

4. Click **Log Settings** in the top right corner of the page to enter the log parameter settings page.

5. Configure or confirm the log parameters.

   1. Enable log capacity alarms; the alarm threshold and interval can remain at their default values.

      When usage reaches the set value, the platform will push alarm notifications.

   2. It is recommended to set the storage duration to 180 days.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">To meet security compliance requirements, it is recommended to set the log storage duration to 180 days.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">When the log storage duration exceeds 180 days, the log service will clean up historical data in chronological order.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If your log capacity runs out more than 180 days ago, you will not be able to continue storing logs.      </div>
      

   3. In the domain collection range list, check **all domains**.

6. Click **OK**.


<span id="6af48b7f"></span>
## Configure other policies

Other types of protection strategies, such as access control, geographical access control, etc., can be configured as needed. For details, please refer to [protection strategy types](https://docs.byteplus.com/en/docs/6511/1130952).
