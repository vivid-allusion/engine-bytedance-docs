---
title: "Introduction to custom WAF policies"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/docs-introduction-to-custom-waf-rules"
---

BytePlus Web Application Firewall (WAF) includes a predefined set of rules and provides defense against various web attacks such as SQL injection, XSS attacks, and website Trojans. You can also make custom rules for specific needs. These rules have a name and conditions to match. Based on the matching criteria, these custom rules can allow, block, or log requested traffic. You can also enable or disable individual rules as needed. The protection policies can be set to change all the rule statuses.

<span id="19ae3078"></span>
## Restrictions

Before configuring custom policies, you may need to understand the limitations on forwarding capability and rule\-matching priority.

<span id="14d08663"></span>
### Forwarding capability

Websites added from BytePlus CDN may send requests to WAF for detection based on CDN capabilities and settings. However, some types of requests may not be forwarded to WAF due to CDN limitations. This could make certain WAF protection rules ineffective for those requests.

As an example, requests using the TRACE method cannot be sent to WAF for detection. This means that WAF protection rules related to the TRACE request method would not be effective for such requests.

<span id="7caab27d"></span>
### Rule\-matching priority

The WAF can provide protection for both an exact domain and its corresponding wildcard domains at the same time. In such cases, the rules applied to the exact domain are given priority.

To provide a clearer example, let's consider the exact domain `a.test.com` and the wildcard domain `*.test.com`.


* If you set rules for both `a.test.com` and `*.test.com`, the rules for `a.test.com` will be effective for that specific domain, while the rules of `*.test.com` will be enforced on its subdomains (for example, `b.test.com`, `c.test.com`), excluding `a.test.com`.

* If you remove all rules for `*.test.com`, the rules for `a.test.com` will still apply to it.

* If you remove all rules for `a.test.com`, the rules for `*.test.com` will be applied to `a.test.com` and its subdomains.


<span id="33eb1798"></span>
## Action description

The action for a rule decides how to route a request when a WAF rule is triggered. There are three types of actions possible when a request matches a custom rule.


* **Allow**: WAF will forward the incoming requests to the origin server, and log the requests in the access log.

* **Observe**: WAF will forward the incoming requests to the origin server, but record the requests in the attack log.

* **Block**: WAF will block the incoming request to prevent it from reaching the origin server, and provide the client with a custom response page (if configured). The requests will be recorded in the attack log.


<span id="21c323a3"></span>
## Advanced settings

You can define more specific matching conditions for a rule by configuring advanced settings. The parameters below need to be set when adding matching conditions.


* **Logical operation**: This refers to the logical relationship between different conditions for combination.

   * **AND**: This implies that the rule is triggered only when all conditions are matched.

   * **OR**: This implies that the rule is triggered when any of the conditions are matched.

* **Match variable**: This is a field used to identify and match specific patterns or conditions in incoming requests. It can include elements such as the request method, request path, or request header.

* **Custom object**: Custom objects refer to specific settings for match variables.

* Typically, once a match variable is chosen, the corresponding custom object will be auto\-populated. For instance, if the match variable is set to **Request protocol**, the custom object **request.schema** will be automatically set.

* However, if a custom match variable, such as **Custom** **cookies** is selected, it is necessary to manually assign a specific value to the custom object.

* **Operator**: This is a symbol that signifies a specific mathematical or logical operation or process. It can include operations such as greater than, less than, or equal to.

* **Match value**: This refers to the specific value used to determine whether a condition is met. The format of this value depends on its corresponding operator.


<span id="48910777"></span>
## Policy types

The following introduces the types of policy protection provided by WAF, and you can view the specific configuration steps of the policy by clicking the corresponding document link.

<span id="a884b663"></span>
### Access control

Access control policies help you control who can access your website. You can allow or block requests from specific IP addresses or locations (like countries or regions). If you want to deliver more information to the client when requests are blocked by WAF, you can customize a response page with a response code and content.

For more details, see [Configuring access control policies](https://docs.byteplus.com/docs/waf/docs-configuring-access-control-policies).

<span id="28629a17"></span>
### Rate limiting

A rate limiting rule helps manage high traffic by limiting the number of requests to a specific path within a certain timeframe. This prevents excessive requests from overwhelming the server.

For more details, see [Configuring rate limiting policies](https://docs.byteplus.com/docs/waf/docs-configuring-rate-limit-policies).

<span id="39fba2bd"></span>
### Vulnerability protection

WAF has built\-in rules to protect against common web attacks. Different protection levels cover different types of attacks. Higher levels have more complex rules. You can customize allowlists to exclude specific requests or match variables from the vulnerability protection policies.

For more details, see [Configuring vulnerability protection policies](https://docs.byteplus.com/docs/waf/docs-configuring-vulnerability-protection-policies).

<span id="aa5a8560"></span>
### API protection

API protection policies examine incoming API traffic based on the defined API structure and parameters. You can add API rules manually or upload them as JSON files.

For more details, see [Configuring API protection policies](https://docs.byteplus.com/docs/waf/docs-configuring-api-protection-policies).

<span id="c422f834"></span>
### Bot management

Enabling or disabling bots helps prevent unwanted requests and malicious actions from certain bots, while allowing legitimate traffic to pass through. You can choose to use predefined bot rules or create your own custom bot management rules with specific matching conditions.

For more details, see [Configuring bot management policies](https://docs.byteplus.com/docs/waf/docs-configuring-bot-management-policies).
