---
title: "Priority of bot management policies"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/Priority_of_bot_management_policies"
---

The bot management feature is designed to provide you with capabilities for precise identification and control of automated traffic. It can effectively handle access from various automated tools, such as search engines, monitoring probes, content aggregators, and malicious scanners.

WAF provides a multi\-layered bot protection system, which mainly includes:


* **Managed rules**: A built\-in, continuously updated set of rules used to identify known and common bot behaviors.

* **Custom rules**: You can create highly customized Bot protection strategies based on your business requirements. There are three main types:

   * **Custom bot classification**: Identify and categorize bots with specific characteristics.

   * **Rate limiting**: Rate control based on access frequency is the core method for addressing behaviors such as repeated interface calls.

   * **Statistical protection**: This feature identifies distributed and group\-based attack behaviors based on statistical characteristics such as IP aggregation.

* **API behavior analysis**: By intelligently learning from discovered APIs, generates a behavior map to help you identify and manage risky APIs.


This document focuses on explaining the matching logic and priority order of various **custom Bot rules** to help you build precise and efficient Bot protection strategies.

<span id="c5dd789a"></span>
## Custom Bot categories

This feature is used to identify and categorize specific bots. The WAF matches custom bot rules sequentially in the order of **protected domain** \> **request characteristics**.

The following are the description and internal priority order for each configuration module:

<span id="4bd800d3"></span>
### Protected domain name

Specify the domains to be protected; both exact domains and wildcard domains can be selected and added.


* Priority: exact domain name \> wildcard domain name

* Example:

   Suppose you have two rules:

   * **Rule A:**  The protected domain name is `www.example.com` (exact domain name)

   * **Rule B:**  The protected domain name is `*.example.com` (wildcard domain)

      When a request to `www.example.com` arrives, the WAF will **match rule A first**. An attempt will be made to match rule B only if the subsequent conditions of rule A, such as path or advanced conditions, are not met.


<span id="a444ceee"></span>
### Request features

Used to restrict the characteristic conditions of a Bot, such as request protocol, request method, request header, request parameters, request body, Cookie, User\-Agent, and so on. There is no priority among different request characteristics.

<span id="deba42f8"></span>
### Creation time

If two rules have the same protected domain name and request characteristics but different actions, priority is determined by the order in which the rules are created. Rules created earlier have higher priority; that is, rules with smaller rule IDs have higher priority than those with larger rule IDs.

<span id="a610f814"></span>
## Rate limiting

Bot frequency limiting rules are used to limit the rate of traffic access under specific conditions. During the statistical period, after both each statistical object's access count and the total access count reach the specified threshold, actions such as rate limiting, blocking, or other measures are applied to requests with certain characteristics.

WAF matches frequency limiting rules progressively in the order of **protected domain name \> request path \> request characteristic \> statistical condition**. The more specific the rule definition, the higher its relative priority. Support manual adjustment of the priority of rules corresponding to different request characteristics and statistical conditions.

<span id="509f477e"></span>
### Protected domain name

Specify the domains that need protection. You can add either exact domains or wildcard domains.


* Priority: exact domain names \> wildcard domain names

* Example:

   Suppose you have two rules:

   * **Rule A:**  The protected domain name is `www.example.com` (exact domain name)

   * **Rule B:**  The protected domain name is `*.example.com` (wildcard domain)

      When a request to `www.example.com` arrives, the WAF will **match rule A first**. Only when the subsequent conditions of rule A, such as path or advanced conditions, are not satisfied, will an attempt be made to match rule B.


<span id="0935d81c"></span>
### Request path

Specify the target URL path; supports entering an exact path or using wildcards.`*`Matches any path. WAF groups different protection rules under the same domain according to the request path. That is, rate limiting rules with the same request path belong to the same first\-level rule group.


* Priority: exact path \> wildcard path

* Example:

   For the domain `www.example.com`, you have configured two rules:

   * **Rule A:**  Request path is `/login.php` (exact path)

   * **Rule B:**  The request path is `/login/*` (wildcard path)

      When a request to `www.example.com/login.php` arrives, the WAF will **match Rule A first**. Only if the subsequent conditions for rule A are not met will the system continue to attempt to match rule B.


<span id="840cedf6"></span>
### Request features

Used to set more granular matching criteria, such as request protocol, request method, request headers, request parameters, request body, request cookie, request User\-Agent, and more. You can set multiple rules based on different request characteristics. Within the same primary rule group, WAF distinguishes secondary rule groups based on request characteristics. That is, rules that have the same request path and request characteristics belong to the same secondary rule group.


* **Priority**

   * **Rules configured with specific features \> rules without configured features (ALL)** : The system will prioritize matching rules that have explicit request features configured.

   * **Support manual adjustment**: You can drag feature rule groups to adjust their detection order. The higher a group is in the order, the higher its priority. By default, rule groups created earlier have higher priority.

* **Example**

   Taking the above diagram as an example, for the path /freq_bot, the request feature groups you set, from top to bottom, are as follows:

   
   |Request features |Rule name |
   |---|---|
   |`Request method` `Equal to` `POST` |freq1 |
   |`Client IP` `Include` `Location XX` |freq2 |
   |`ALL` |freq |
   

   * At this time, the default priority order from highest to lowest is: freq1 \> freq2 \> freq

   * If you manually drag the `feature group containing the client IP address with location XX` to the top of the list, then the priority order from highest to lowest is: freq2 \> freq1 \> freq


<span id="0164bb59"></span>
### Statistical criteria

This metric is used to measure the access frequency and concurrency of the statistical object in order to determine whether a protective action should be triggered. Priority explanation as follows


* **Support manual adjustment**: Within the same request feature group, you can add multiple rules with different statistical conditions. There is also a priority among these rules. You can adjust the order by dragging, which determines which rule is judged first. By default, rules created earlier have higher priority.

* **Priority number**: The system assigns a priority number (ranging from P0 to P9) to each statistical condition rule. Each number must be unique and is used to precisely control the order.


<span id="ca77bb31"></span>
## Statistical protection

Bot statistical protection rules are used to count the number of repeated IPs or the proportion of repeated IPs among entities being monitored that match specific request characteristics within a specified period. When the count or proportion reaches the set threshold, actions such as observation, interception, human\-machine verification, or other measures are performed on requests matching these characteristics.

WAF matches protection rules hierarchically in the order of **protected domain name \> request path \> request feature \> statistical criteria**. The more specific the rule, the higher its relative priority. Supports manual adjustment of the priority of rules that correspond to different request characteristics and statistical conditions.

<span id="d9bfd71d"></span>
### Protected domain name

Specify the domains that require protection. You can choose to add either exact domains or wildcard domains.


* Priority: exact domain name \> wildcard domain name

* Example:

   Suppose you have two rules:

   * **Rule A:**  The protected domain name is `www.example.com` (exact domain name)

   * **Rule B:**  The protected domain is `*.example.com` (wildcard domain)

      When a request to `www.example.com` arrives, the WAF will **prioritize matching Rule A**. Rule B will only be matched if the subsequent conditions of Rule A, such as path or advanced conditions, are not met.


<span id="7f9216db"></span>
### Request path

Specify the URL path for the access target. You can enter an exact path or use wildcards.`*`Match any path. WAF groups different protection rules under the same domain according to the request path, meaning that frequency limiting rules with the same request path belong to the same primary rule group.


* Priority: exact path \> wildcard path

* Example:

   For the domain `www.example.com`, you have configured two rules:

   * **Rule A:**  The request path is `/login.php` (exact path)

   * **Rule B:**  Request path is `/login/*` (wildcard path)

      When a request to `www.example.com/login.php` arrives, the WAF will **match rule A first**. Rule B will only be attempted if the subsequent conditions of rule A are not met.


<span id="21e3fb93"></span>
### Request features

Used to set more granular matching criteria, such as request protocol, request method, request headers, request parameters, request body, request cookies, request User\-Agent, and more. You can set multiple rules based on different request characteristics. Within the same primary rule group, WAF distinguishes secondary rule groups based on request characteristics. That is, rules with the same request path and request characteristics belong to the same secondary rule group.


* **Priority**

   * **Rules configured with specific characteristics \> rules without specific characteristics (ALL)** : The system will prioritize matching rules that specify explicit request characteristics.

   * **Support manual adjustment**: You can manually drag to adjust the detection order of feature rule groups. Groups placed earlier in the order have higher priority. By default, rule groups created earlier have higher priority.

* **Example**

   Taking the above diagram as an example, for the path /api/v1/query, the request feature groups you have configured (from top to bottom) are:

   
   |Request features |Rule name |
   |---|---|
   |`Client IP` `Equal to` `1.1.1.1` |sta1、sta3 |
   |`Request protocol` `Equal to` `HTTP` |sta2 |
   |`ALL` |sta |
   

   * At this time, the default priority order from highest to lowest is as follows: sta1 \> sta3 \> sta2 \> sta.

   * If the feature group containing `request protocol equals HTTP` is manually dragged to the top of the list, the priority order from highest to lowest will be: sta2 \> sta1 \> sta3 \> sta


<span id="f11fbc6c"></span>
### Statistical criteria

To measure the access frequency and concurrency of statistical objects in order to determine whether to trigger a protective action. Priority explanation


* **Support manual adjustment**: In the same request feature group, you can add multiple rules with different statistical conditions. There is also a priority order among these rules. You can adjust the order by dragging, which determines which rule is evaluated first. By default, rules created earlier have higher priority.

* **Priority number**: The system assigns a unique priority number (ranging from P0 to P9) to each statistical condition rule, ensuring that numbers are not duplicated and enabling precise control over their order.


<span id="9531425f"></span>
## Summary

To facilitate your quick understanding and reference, we have summarized the priority logic of different custom Bot rules as follows:


|Rule data type |Core functionality |Priority determination logic |
|---|---|---|
|**Custom Bot categories** |Identify and mark specific bots |First, match the domain name. Then, match by creation time according to the rules, with items created earlier being matched first. |
|**Rate limiting** |Implement rate control based on access frequency |`Domain name` \> `Path` \> `Feature` \> `Statistical condition` The more specific a rule is, the higher its priority relative to other rules. The priority can be manually adjusted. |
|**Statistical protection** |Implement protection based on IP clustering |`Domain name` \> `Path` \> `Feature` \> `Statistical conditions`. The more specific a rule is, the relatively higher its priority; the priority can be adjusted manually. |
