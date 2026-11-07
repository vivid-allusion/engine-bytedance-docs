---
title: "Create forwarding rules (Basic edition)"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Creating-a-forwarding-rule"
---

This article introduces how to create forwarding rules for Basic edition ALB instances in the console.

<span id="378d6b8c"></span>
## Background

A forwarding rule consists of forwarding conditions and forwarding actions. Forwarding conditions filter requests, and forwarding actions determine how requests are forwarded.

<span id="7f85b907"></span>
### Forwarding conditions

The types of forwarding conditions supported by Basic edition ALB instances include “domain name” and “path.”

**Domain name** defaults to`-`, indicating any domain name. **Path** defaults to`/`, represents the root directory. If you do not configure a domain name or path, the system applies these default values automatically.

According to business needs, you can configure only the domain name, only the path, or both domain name and path in a forwarding rule:


* Configure only the domain name: any request matching this domain name will match this forwarding rule. For example, if you configure the domain name as `www.test.com`, then requests to `www.test.com/lb/` or `www.test.com/lb/create` will match this forwarding rule.

* Configure only the path: any request matching this path will match this forwarding rule. For example, if you configure the path as `/lb`, then requests to `www.test.com/lb` or `www.test.cn/lb` will match this forwarding rule.

* Configure both domain name and path: only requests matching both the domain name and path will match this forwarding rule. For example, if you configure the domain name as `www.test.com` and the path as `/lb`, only requests to `www.test.com/lb` will match this forwarding rule.


<span id="2acb4ed3"></span>
### Forwarding action

The forwarding actions supported by the Basic edition ALB instance include "Forward to" and "Redirect to".

<span id="e2354612"></span>
## **Before you begin**


* Created ALB instance. For details, see [Create an instance](https://docs.byteplus.com/docs/clb/Creating-an-instance).

* Created listener. For details, see [Create listener](https://docs.byteplus.com/docs/clb/Creating-a-listener).

* Created server group and added backend servers. For details, see [Create and manage server group](https://docs.byteplus.com/docs/clb/Managing-server-groups).


<span id="538c8fe8"></span>
## Limits


* Each instance can have up to 50 forwarding rules in addition to default forwarding rules.

* Only one forwarding action can be configured per forwarding rule.

* At least one of domain name or path must be filled in.

* The rate limiting feature must be used together with the "Forward to" forwarding action.


<span id="19f5db85"></span>
## **Procedure**


1. Log in to the [Application Load Balancer console](https://console.byteplus.com/alb).

2. On the **Instance management** page, find the ALB instance to be configured, and click **Configure listener** in the **Actions** column.

3. On the **Listener** tab, find the listener to be configured, and click **Edit forwarding rules** in the **Actions** column.

4. On the **Forwarding rules** tab, click **Add forwarding rules**.

5. On the **Add forwarding rules** page, configure the parameters according to the instructions below, then click **Confirm**.


<span id="149af1ba"></span>
### **Forwarding condition**


|**Configuration Item** |**Description** |
|---|---|
|Domain name |Specify a domain name. The default value of **domain name** is`-`, representing any domain name. Once the forwarding rule is created, the domain name cannot be modified.<br><br>Domain names are case\-insensitive. The specified domain name must meet the following requirements:<br><br><br>* Only English letters, numbers, and the following special characters are allowed: `.` `- _ *`。<br><br>* It must contain at least one half\-width period (.) and cannot start or end with a half\-width period (.).<br><br>* A maximum of 128 characters is allowed.<br><br><br>The domain name can be an exact domain or a wildcard domain:<br><br><br>* Exact domain: must comply with domain name specifications.<br><br>* wildcard domain<br><br>   * The asterisk (\*) can replace one or more characters.<br><br>   * The asterisk (\*) must be at the beginning or end of the domain name.<br><br>   * Only one asterisk (\*) is allowed per domain name.<br><br>   * No characters other than the half\-width period (.) are allowed before or after the asterisk (\*).<br><br>* Examples:<br><br>   * Valid domain examples: `www.test.com`, `*.com`, `www.test.*`.<br><br>   * Invalid domain examples: `*aaa.com`, `www.*.com`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">wildcard domains only match domain names at the same level. For example, \*.example.com can match www.example.com but cannot match example.com.</div><br> |
|Path |Specify a path. The default value of the **path** is`/`, which represents the root directory. After creating the forwarding rule, the path cannot be modified.<br><br>The path length must not exceed 128 characters.<br><br>ALB allows you to specify an exact path or use a regular expression to specify the path.<br><br><br>* Exact path<br><br>   * Input specification:<br><br>      * The value must start with a forward slash (/).<br><br>      * Only letters, numbers, and the following special characters are allowed: `- _ / .` `% ?` `# &＝`。 Forward slashes (/) cannot be consecutive.<br><br>   * Example value: /api/v1/users<br><br>* regular expression<br><br>   * Input specification:<br><br>      * The value must start with a tilde (~), and the tilde (~) can only appear once.<br><br>      * Only letters, numbers, and the following special characters are allowed: `.` `- _ / ＝ ?` `~ ^ * $ : ( ) [ ] + \|`。<br><br>      * `~`Starting character indicates case sensitivity. `~*` starting character indicates case insensitivity.<br><br>   * Example value: ~^/api/v[0\-9]+/users/.\*$<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To specify the path using a regular expression, please <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000645">submit a ticket</a> or contact customer service support.</div><br> |


<span id="7b6ec339"></span>
### **Forwarding action**


* #### Forward to    <span id=".6L2s5Y-R6Iez"></span>


The ALB forwards requests to the server group you specify.


|**Configuration Item** |**Description** |
|---|---|
|Server group |Specify the server group to which the request is forwarded. You can only attach server groups that are under the same VPC as the current ALB instance. When a request matches the specified domain name and path, it will be forwarded to this server group. |



* #### Redirect to    <span id=".6YeN5a6a5ZCR6Iez"></span>


ALB redirects requests. For example, ALB can redirect HTTP requests to HTTPS to enhance security; it can also redirect requests from old domains to new domains to accommodate domain changes.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When configuring redirect parameters, modify at least one of the following to avoid redirect loops: <strong>Agreement</strong>, <strong>domain name</strong>, <strong>Port</strong>, and <strong>URI</strong>. If the request protocol differs from the redirect protocol, ensure the port is set correctly and related server settings are updated to prevent redirect failures.</div>


* <div data-tips="true" data-tips-type="tip">If the <code>Content-Length</code> header in the request exceeds the maximum request body size set in the listener (<code>client_max_body_size</code>), ALB returns a 413 status code directly to the client without performing the redirect. For instructions on adjusting the listener's request body size limit, refer to <a href="https://docs.byteplus.com/docs/clb/Custom-configurations">custom configuration</a>.</div>




|**Configuration Item** |**Description** |
|---|---|
|Agreement |Select the protocol used for redirection. The protocol can be HTTPS or HTTP.<br><br>Requests will be redirected when they meet the specified forwarding conditions. |
|Domain name |Specify the domain name to which the request is redirected.<br><br>If you do not specify a domain name, the redirected domain will be the same as the requested domain.<br><br>The specified domain name must meet the following requirements:<br><br><br>* Only English letters, numbers, half\-width periods (.), and hyphens (\-) are allowed.<br><br>* It must contain at least one half\-width period (.), but cannot start or end with a half\-width period (.).<br><br>* Each level of the domain cannot start or end with a hyphen (\-).<br><br>* A maximum of 128 characters is allowed.<br><br>* It must be an exact domain name that complies with domain name standards, e.g., `www.test.com`. |
|Port |Specify the Port to which the request is redirected. The Port range is 1 to 65535.<br><br>If you do not specify a Port, the redirected Port will be the same as the request Port. |
|URI |Specify the path to which the request is redirected.<br><br>If you do not specify a path, the redirected path will be the same as the request path.<br><br>The specified path must meet the following requirements:<br><br><br>* Must start with a forward slash (/).<br><br>* Allow up to 128 characters.<br><br>* Allow only English letters, numbers, and the following special characters: `- _ / .` `% ?` `# &＝`。 Forward slashes (/) cannot be used consecutively. |
|Status code |Select the status code to indicate the redirect response status.<br><br>The default status code is 301, indicating the requested resource has permanently moved to a new location. ALB supports status codes 301, 302, 307, and 308. |


<span id="2fab1a7b"></span>
### Other parameters


|**Configuration Item** |**Description** |
|---|---|
|Rate limiting |Optional. Configure QPS. When client requests exceed the configured QPS, ALB discards the excess requests and returns a 503 status code to the client.<br><br>The rate limiting feature is disabled by default. After enabling this feature, enter the QPS value. Value range: 100–150000.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you need to use the rate limiting feature, please <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000645">submit a ticket</a> or contact customer service support.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The rate limiting feature must be used together with the "Forward to" forwarding action.</div><br> |
|Description |Optional. Enter a description for the forwarding rule.<br><br>The entered description must meet the following requirements:<br><br><br>* Must not exceed 255 characters.<br><br>* Must start with an English letter or a Chinese character.<br><br>* Can only contain English letters, Chinese characters, numbers, spaces, and the following special characters: `,._=-，。`. |
