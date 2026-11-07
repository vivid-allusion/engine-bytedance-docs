---
title: "FAQ about BytePlus Web Application Firewall"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/FAQ-about-web-application-firewall"
---

This section details the frequently asked questions about BytePlus Web Application Firewall.

<span id="9082619d"></span>
## How is the WAF instance billed?

You are charged monthly for the WAF security functions and rules we provide (subscription fee) and the requests we process (request processing fee) during every service cycle, both of which are billed hourly. For more details, see [Billing model and pricing details](https://docs.byteplus.com/en/docs/waf/docs-billing-model-and-pricing-details).

<span id="abf341d7"></span>
## Why are some types of requests undetectable?

Websites added from BytePlus CDN may send requests to WAF for detection based on CDN capabilities and settings. However, some types of requests may not be forwarded to WAF due to CDN limitations. This could make certain WAF protection rules ineffective for those requests.

As an example, requests using the TRACE method cannot be sent to WAF for detection. This means that WAF protection rules related to the TRACE request method would not be effective for such requests.

<span id="7ee2920c"></span>
## How do the rules take effect if both exact domain names and wildcard domain names are under protection?

The WAF can provide protection for both an exact domain and its corresponding wildcard domains at the same time. In such cases, the rules applied to the exact domain are given priority.

To provide a clearer example, let's consider the exact domain `a.test.com` and the wildcard domain `*.test.com`.


* If you set rules for both `a.test.com` and `*.test.com`, the rules for `a.test.com` will be effective for that specific domain, while the rules of `*.test.com` will be enforced on its subdomains (for example, `b.test.com`, `c.test.com`), excluding `a.test.com`.

* If you remove all rules for `*.test.com`, the rules for `a.test.com` will still apply to it.

* If you remove all rules for `a.test.com`, the rules for `*.test.com` will be applied to `a.test.com` and its subdomains.


<span id="4a6b5c3f"></span>
## What is the difference between different vulnerability protection levels?

Web Application Firewall (WAF) offers three tiers of managed protection, each encompassing a distinct set of rules. Additionally, you have the flexibility to enable or disable the specific vulnerability protection rules under **Custom** mode.


* Managed protection: When you select a managed protection level, all the pre\-configured protection rules within that level will be automatically enabled. Of the three available levels, **Strict** contains the most rules, while **Loose** contains the fewest.

   * **Strict**: This level comprises detection rules for complex attack requests, encompassing an extensive range of vulnerability protection rules. These include the rules categorized under **Normal** and **Loose** levels.

   * **Normal**: This level indicates the common detection of specific types of attacks, focusing on rules that yield fewer false positives, including those set at **Loose** protection level. By default, the protection level is set to **Normal**.

   * **Loose**: It is applicable for requests that exhibit clear attack patterns, or in situations where the aim is to minimize the occurrence of false positives.

* Custom protection: It supports customization of the activation or deactivation of specific rules within the current scope of built\-in vulnerability detection rules.


<span id="b226e896"></span>
## How to obtain the IP address of WAF when verifying whether the forwarding is effective?


1. Log in to the [BytePlus Web Application Firewall Console](https://console.byteplus.com/waf).

2. In the top menu bar, select **Asia Pacific (Johor)** , \*\*\*\* the region where your cloud WAF instance is located.

3. On the left\-side navigation pane, select **Website settings**.

4. Click the domain name to view details.

5. Copy the **CNAME value**.

6. Run the local terminal command program and execute `ping <CNAME value>`.

   The following takes Mac OS as an example for illustration.

   * ①: The copied WAF CNAME value.

   * ②: The WAF IP address.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c0acfc5d14d4608af9f4ad6d45709be~tplv-goo7wpa0wc-image.image) </span>
