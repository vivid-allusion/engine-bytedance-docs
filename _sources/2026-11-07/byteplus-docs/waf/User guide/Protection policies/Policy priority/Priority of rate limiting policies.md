---
title: "Priority of rate limiting policies"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/Priority_of_rate_limiting_policies"
---

Rate limiting targets high concurrency and high\-frequency access at the application layer by matching paths and request characteristics, controlling statistical objects and time window thresholds, and performing actions such as observe, block, rate limiting, Captcha, or JS challenge when thresholds are reached. The purpose of this document is to help you clearly understand how a web application firewall determines which rate limiting rule takes effect first when multiple rate limiting rules coexist.

<span id="9766e10b"></span>
## Match order

WAF matches rate limiting rules sequentially in the order of **protected domain name** \> **request path** \> **request characteristic** \> **statistical condition**. Only when the conditions at the current level are successfully matched will the rules at the next level be matched.

The following are the descriptions and internal priority order for each configuration module:

<span id="bf055a6c"></span>
## Protected domain name

Specify the domains to be protected. You can select and add exact domains or wildcard domains.

<span id="9dc90a31"></span>
### Priority

Exact domain \> wildcard domain

<span id="429b2d12"></span>
### Example

Suppose you have two rules:


* **Rule A:**  The protected domain name is `www.example.com` (exact match domain name)

* **Rule B:**  The protected domain name is `*.example.com` (wildcard domain)


When a request to `www.example.com` arrives, the WAF will **prioritize matching rule A**. Rule B will only be matched when the subsequent conditions of rule A (such as path or feature) are not met.

<span id="ec3c742b"></span>
## Request path

Specify the URL path of the access target; you can enter an exact path or use wildcards.`*`Match any path. WAF groups different rate limiting rules under the same domain by request path, meaning that rate limiting rules with the same request path belong to the same primary rule group.

<span id="d00b3162"></span>
### Priority

Exact path \> wildcard path

<span id="a7bb658c"></span>
### Example

For the domain `www.example.com`, you have configured two rules:


* **Rule A:**  The request path is `/login.php` (exact path)

* **Rule B:**  The request path is `/login/*` (wildcard path)


When a request to `www.example.com/login.php` arrives, the WAF will **match rule A first**. Rule B will only be matched if the subsequent conditions of rule A are not met.

<span id="a98247fe"></span>
## Request features

Used to set more granular matching criteria, for example, request protocol, request method, request headers, request parameters, request body, request cookies, request User\-Agent, and more. You can set multiple rules based on different request characteristics. Within the same primary rule group, WAF distinguishes secondary rule groups based on request characteristics. That is, CC rules with the same request path and request characteristics belong to the same secondary rule group.

<span id="dae1bb17"></span>
### Priority


* **Rules configured with specific features \> Rules not configured with specific features (ALL)** : The system will prioritize matching rules that specify explicit request features.

* **Support manual adjustment**: You can drag and drop to manually adjust the detection order of feature rule groups. Groups placed earlier in the order have higher priority. By default, rule groups created earlier have higher priority.


<span id="fc3b6766"></span>
### **Example**

Taking the above diagram as an example, for the path /path/to/resource, the request feature groups you configured, listed from top to bottom, are as follows:


|Request features |Rule name |
|---|---|
|`Request protocol` `Equal to` `HTTP` |cc1 |
|`Client IP` `Equal to` `1.1.1.1` and `request method` `Equal to` `POST` |cc2 |
|`Client IP` `Equal to` `1.1.1.1` |cc3 |
|`ALL` |cc |



* At this time, the default priority order from highest to lowest is: cc1 \> cc2 \> c3 \> cc

* To set the priority order from highest to lowest as cc3 \> cc1 \> cc2 \> cc, manually drag the feature group containing `client IP equals 1.1.1.1` to the top of the list.


<span id="409f1629"></span>
## Statistical criteria

Specify the statistical object, statistical duration, and threshold to measure the access frequency and concurrency of the statistical object, in order to determine whether to trigger a protective action. Priority explanation as follows:


* **Support manual adjustment**: Within the same request feature group, you can add multiple rules with different statistical conditions. There is also a priority among these rules. You can adjust the order by dragging, which determines which rule is evaluated first. By default, rules created earlier have higher priority.

* **Priority number**: The system assigns a unique priority number (ranging from P0 to P9) to each statistical condition rule. The numbers cannot be duplicated and are used to precisely control their order.


<span id="f1189259"></span>
## Summary

For your quick understanding and reference, the entire matching logic is summarized in the following table:


|Matching level |Match content |Internal priority rules |
|---|---|---|
|**Level 1** |**Protected domain name** |Exact domain \> wildcard domain |
|**Level 2** |**Request path** |Exact path \> wildcard path |
|**Level 3** |**Request features** |Specific features \> Unconfigured features (ALL); items at the same level can be manually reordered |
|**Level 4** |**Statistical criteria** |Multiple entries can be configured under the same feature, and their order can be manually adjusted. |
