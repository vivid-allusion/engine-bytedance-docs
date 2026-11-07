---
title: "Forwarding rule description"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Configuring-a-forwarding-rule-01"
---

<span id="VLXY2QPM"></span>
## Introduction​

Forwarding rules are used to direct requests for specified domain names and URLs to designated backend server groups.

You can configure multiple forwarding rules for one Layer 7 listener.

<span id="VzprpvmQ"></span>
## Classification


|Category |Explanation |
|---|---|
|Default forwarding rule |After successfully creating the Layer 7 listener, the system automatically creates forwarding rules. The default forwarding rule has an empty domain name and a URL of `/`, indicating that requests from any domain name and URL can be forwarded to the specified backend server group. |
|Custom forwarding rules |Custom forwarding rule: Forwarding rule added manually for Layer 7 listeners according to business needs. Custom forwarding rules can forward or redirect access requests matching domains and URLs. |


<span id=".6L2s5Y-R6KeE5YiZ6YWN572u6K-05piO"></span>
## Domain name and URL


* **Domain name**

   Domain name supports two configuration modes: precise domain name and wildcard domain name.

   * Exact domain name: An exact domain name that complies with domain name specifications. For example www.test.com

   * Wildcard domain: Use wildcard \* to replace one or more characters, \* is only supported at the beginning or end of a domain name, it can only appear once per domain name, and can only be placed around . Allowed placement before or after the <a i=3\>.</a\>

      * Allowed formats: `*.test.com`, `www.test.*`

      * Disallowed formats: www.\*.com, \*.test.\*, \*.\*.com, \*aaa.com

* **URL**

   URL paths start with `/`, e.g., `/`, `/abc/read`. If not configured, the default is `/`.

   You can configure the domain name only, URL only, or both domain name and URL according to your business needs.

   * If only the domain name is configured, the URL defaults to `/`, meaning it forwards requests matching any URL under that domain name. For example, if the domain name is configured as `www.test.com`, requests to `www.test.com/lb/` or `www.test.com/lb/create` will both match this forwarding rule.

   * If only the URL is configured, the domain name defaults to empty, meaning it forwards requests matching that URL on any domain. For example, if the URL is set to `/lb`, requests to `www.test.com/lb` or `www.test.cn/lb` will both match this forwarding rule.

   * If both the domain name and URL are configured, it forwards requests that match both the specified domain name and URL.


<span id=".6L2s5Y-R6KeE5YiZ5Yy56YWN6K-05piO"></span>
## Matching description


* **Matching process**

   When the Layer 7 listener receives a request, it forwards the request to the corresponding backend server group by matching the domain name and URL based on the forwarding rule configuration. The matching process is as follows:

   If the received request contains a domain name, domain matching is performed in the priority order of exact domain name \> wildcard domain starting with  **`*`**  \> wildcard domain ending with  **`*`** 

   * If a matching domain name exists, continue matching the URL according to the longest match principle.

      * If a matching URL exists, forward the request to the backend server group of the corresponding rule.

      * If there is no matching URL, forward the request to the backend server group of the default forwarding rule.

   * If no matching domain name exists, continue matching forwarding rules with "no domain name, URL path only" based on the longest match principle.

      * If a matching URL exists, forward the request to the backend server group of the corresponding rule.

      * If there is no matching URL or no forwarding rule with "no domain name, URL path only," forward the request to the backend server group of the default forwarding rule.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Domain matching for forwarding rules is case\-insensitive, while URL matching is case\-sensitive. When configuring forwarding rules for a Layer 7 listener, configure the URLs with the correct case according to the actual URLs.   </div>
   

* **Matching examples**

   For example, a Layer 7 listener has the following forwarding rules configured in sequence:

   
   |Domain name |URL |Forwarding action |
   |---|---|---|
   |\- |/ |Forward to default backend server group RS0 |
   |\- |/lb |Forward to RS1 |
   |\- |/abc/create |Forward to RS2 |
   |www.test.com |/ |Forward to RS3 |
   |\*.test.com |/lb/create |Forward to RS4 |
   |example.test.\* |/lb/create |Forward to RS5 |
   

   The matching rules for the following requests are as follows:

   
   |Request |Match backend server group |Explanation |
   |---|---|---|
   |www.test.com/ |RS3 |Exact domain name and URL match, forward to RS3. |
   |www.test.com/lb |RS3 |Exact domain match. URL matches based on the longest match rule and forwards to RS3. |
   |example.test.com/lb/create |RS4 |Wildcard domain match \*.test.com, exact URL match, forward to RS4. |
   |example.test.com/lb/create/abc |RS4 |Wildcard domain matching \*.test.com, URL matched by longest match principle, forwarding to RS4. |
   |clb.test.com/abc |\- |Wildcard domain match \*.test.com, URL not matched, return 404 error (because requested URL is not the root directory). |
   |clb.test.com/ |\- |wildcard domain matching \*.test.com returns error 403 if the URL is not matched (because the request URL is the root directory). |
   |www.test.cn/lb |RS1 |No domain matched. Fully matched URL with no domain forwarding rule, forward to RS1. |
   |test.com/abc/create/lb |RS2 |No domain name matched. According to the longest match principle, match the URL of the no domain forwarding rule and forward it to RS2. |
   |www.b.com/ab |RS0 |No matching domain or URL found, forwarding to the default backend server group RS0. |
