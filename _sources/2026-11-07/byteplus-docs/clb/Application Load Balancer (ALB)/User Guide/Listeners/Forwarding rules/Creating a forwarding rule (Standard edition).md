---
title: "Creating a forwarding rule (Standard edition)"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Creating-a-forwarding-rule_Standard-edition"
---

This topic describes how to create forwarding rules for Standard Edition ALB instances in the console.

<span id="6222f5d8"></span>
## Components

A forwarding rule consists of a forwarding condition and a forwarding action.


|Components |Notes |
|---|---|
|Forwarding condition |**The forwarding condition is used to filter requests. A forwarding rule can contain one or more forwarding conditions.** <br><br><br>* The types of forwarding conditions supported by the Standard ALB instance include Domain name, URL path, HTTP header, HTTP request method, query string, Cookie, and SourceIP.<br><br>* Configuration: Different types of forwarding conditions can be configured individually or in combination.<br><br>   * When multiple forwarding conditions are configured together, the relationship between them is AND. Example: If you configure both a domain name and a URL path in a single rule, a request is considered a match only if it matches both the specified domain name and URL path.<br><br>   * Multiple values are allowed for the same forwarding condition, and the relationship between these values is OR. Example: If you configure multiple values for the Domain Name condition, the condition is satisfied if the request's domain name matches any one of those values. |
|Forwarding action<br><br> |**The forwarding action determines how a request is forwarded.** <br><br><br>* Standard edition ALB instances support the following forwarding actions: Forward to, Redirect to, Rewrite, Rate Limit, Return Fixed Response, Cross\-domain, and Write Header.<br><br>* Rate limiting and Rewrite must be used together with either Forward to or Redirect to.<br><br>* Rate limiting, Rewrite, and Forward to can also be used together. When multiple forwarding actions are configured in combination, the relationship between them is AND. |


<span id="79AWUFYj"></span>
## Matching

Upon receiving a client request, ALB performs matching sequentially according to the priority of the forwarding rules, from highest to lowest.


* Priority exists among forwarding rules under the same listener:

   * The default forwarding rule has the lowest priority, and its priority cannot be adjusted.

   * The priority of custom forwarding rules can be adjusted.

   * A smaller priority number indicates a higher priority. In the forwarding rule list, a rule placed higher up has a higher priority.

   * By default, a newly created forwarding rule has a higher priority than existing rules.

* How to adjust custom forwarding rule priority:

   * Method 1: Enter a value. Click **Set priority**, enter the target value, then click **Save**. The system will automatically adjust the rule's position.

   * Method 2: Drag and drop. Hover the mouse over the settings icon in the upper right corner of the rule card, then drag the card to the target position. In the dialog box, confirm the prompt, then click **Save**.


For details on the forwarding rule matching process, see [Forwarding rule matching (Standard edition)](https://docs.byteplus.com/en/docs/clb/Forwarding-rule-Overview).

<span id="1fb64e34"></span>
## **Prerequisites**


* ALB instance has been created. For ALB instance creation, see [Creating an instance](https://docs.byteplus.com/docs/clb/Creating-an-instance).

* Listener has been created. For listener creation, see [Creating a listener](https://docs.byteplus.com/docs/clb/Creating-a-listener).

* Server group has been created and backend servers have been added. For server group creation and backend server management, see [Creating and managing a server group](https://docs.byteplus.com/docs/clb/Managing-server-groups).


<span id="a7578097"></span>
## Use limits


* Except for the default forwarding rule, each instance can create up to 100 forwarding rules.

* Each forwarding rule must satisfy the following constraints:

   * The number of forwarding conditions must be between 1 and 10 (inclusive).

   * Only one of the three forwarding actions \- Forward to, Redirect to, or Return fixed response \- can be configured, and this action must be placed at the end of the action list.

   * The rate\-limiting action must be placed at the top of the forwarding action list.

   * Rate limiting and Rewrite must be used together with either Forward to or Redirect to. Cross\-origin and Write Header must be used together with Forward to, Redirect to, or Return fixed response.

* The order of forwarding actions can be adjusted using the up (↑) and down (↓) arrows on the page.


<span id="QbSSwdxh"></span>
## Procedures


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. On the **Instance management** page, find the ALB instance to configure, then under the **Actions** in the column, click **Listener**.

3. On the **Listener information** tab, find the listener to configure and under **Actions** in the column, then click **Edit forwarding rules**.

4. On the **Forwarding rules** tab, click **Add forwarding rules**.

5. On the **Add forwarding rules** page, configure the related parameters according to the instructions below.

   1. **Configure forwarding conditions**

      
      |Parameters |Notes |
      |---|---|
      |Domain |Specify one or more domain names. When you specify multiple domain names, the relationship between these domain names is OR.<br><br><br>* Domain name is case\-insensitive. The specified domain must comply with the following specifications:<br><br>   * Only allow English letters, numbers, and the following special characters: `.- _ *`.<br><br>   * Must contain at least one half\-width period (.), but cannot begin or end with a half\-width period (.).<br><br>* Supports 1 to 128 characters.<br><br>* A domain name can be an exact domain name or a wildcard domain name:<br><br>   * Exact domain: Must comply with domain name specifications.<br><br>   * Wildcard domain<br><br>      * An asterisk (\*) can represent one or more characters.<br><br>      * The asterisk (\*) must be at the beginning or the end of the domain name.<br><br>      * A domain name can contain at most one asterisk (\*).<br><br>      * Characters other than a period (.) are not allowed immediately before or after the asterisk (\*).<br><br>   * Example:<br><br>      * Valid domain examples: `www.test.com`, `*.com`, `www.test.*`.<br><br>      * Invalid domain examples: `*aaa.com`, `www.*.com`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">A wildcard domain name only matches domain names at the same level. For example, \*.example.com matches www.example.com but not example.com.</div><br> |
      |URL path |Specify one or more paths. When you specify multiple paths, the relationship between these paths is OR.<br><br><br>* Path length supports 0 to 128 characters.<br><br>* Supports exact paths and regular expressions:<br><br>   * Exact path<br><br>      * Format:<br><br>         * The value must start with a forward slash (/).<br><br>         * Only letters, numbers, and the following special characters are permitted: `- _ / .% ?# * & ＝`.<br><br>         * Consecutive forward slashes are not allowed.<br><br>         * By default, exact matching is used. The asterisk (\*) and question mark (?) can also be used as wildcards.<br><br>      * Examples:<br><br>         * Exact match: If the path is configured as `/api/v1/users`, a request to `/api/v1/users` will match successfully.<br><br>         * Prefix match: If the path is configured as `/api/*`, requests to `/api/v1/users` and `/api/v2` will both match successfully.<br><br>   * Regular expression<br><br>      * Format:<br><br>         * The value must start with a tilde (~), and the tilde can only appear once at the beginning.<br><br>         * Only letters, numbers, and the following special characters are allowed: `.- _ / ＝ ?~ ^ * $ : ( ) [ ] + \|`.<br><br>         * `~` at the beginning indicates case\-sensitive matching. `~*` at the beginning indicates case\-insensitive matching.<br><br>      * Example: ~^/api/v[0\-9]+/users/.\*$ |
      |HTTP header |Set HTTP headers. HTTP header is expressed in the form of **key\-value pairs**. Each key can correspond to multiple values, and the relationship between these values is OR. Within the same forwarding rule, key must be unique. If you need to add multiple HTTP headers, click **Add forwarding condition**.<br><br><br>* Requirements for the entered key:<br><br>   * Only English letters, numbers, hyphens (\-), and underscores (_) are allowed.<br><br>   * Cannot be Cookie or Host.<br><br>   * Supports 1 to 40 characters.<br><br>* Requirements for the entered value:<br><br>   * Can contain printable ASCII characters.<br><br>   * Cannot start or end with a space.<br><br>   * Supports 1 to 128 characters. |
      |HTTP request method |Select one or more HTTP request methods. When you select multiple request methods, the relationship between these methods is OR.<br><br>The following request methods are supported: HEAD, GET, POST, OPTIONS, PUT, PATCH, DELETE. |
      |Query string |Set query string. The query string is expressed in the form of key\-value pairs. Within the same forwarding condition, the relationship between multiple key\-value pairs is OR. Across different forwarding conditions, the relationship between key\-value pairs is AND. Within the same forwarding rule, key\-value pairs must be unique.<br><br><br>* Requirements for the entered key:<br><br>   * Allowed characters: lowercase English letters, numbers, and printable special characters except `#[]{}\\|<>&"`.<br><br>   * Cannot contain spaces.<br><br>   * Supports 1 to 100 characters.<br><br>* Requirements for the entered value:<br><br>   * Allowed characters: lowercase English letters, numbers, and printable special characters except `#[]{}\\|<>&"`.<br><br>   * Cannot contain spaces.<br><br>   * Supports 1 to 128 characters. |
      |Cookie |Add one or more cookies.<br><br><br>* The cookie key must comply with the following specifications:<br><br>   * The key for the cookie cannot be empty.<br><br>   * Supports 1 to 100 characters.<br><br>   * Supports visible characters, the wildcard asterisk (\*), and the half\-width question mark (?). If letters are used, they must be lowercase.<br><br>   * Does not support spaces and `;#[]{\\|<>&"`.<br><br>   * Cannot consist entirely of `*` and `?`.<br><br>* The cookie value must comply with the following specifications:<br><br>   * Cookie value cannot be empty.<br><br>   * Supports 1 to 100 characters.<br><br>   * Supports visible characters, the wildcard asterisk (\*), and the half\-width question mark (?). If letters are used, they must be lowercase.<br><br>   * Does not support spaces and `;#[]{\\|<>&"`.<br><br>   * Cannot consist entirely of `*` and `?`.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This feature is currently in Beta stage. For trial requests, please contact your account manager.</div><br> |
      |SourceIP |Only requests that match the SourceIP condition will be forwarded.<br><br><br>* Only supports entering IPv4 addresses/IPv4 address ranges, and the IP address must include a mask.<br><br>* Does not support address ranges of the 0.0.0.0/x type, where x is any number.<br><br>* If a forwarding condition includes SourceIP, only requests whose source matches the specified IP address or CIDR block will match this rule.<br><br>* A single rule supports a maximum of 5 values for the SourceIP condition type.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This feature is currently in Beta stage. For trial requests, please contact your account manager.</div><br> |
      

   2. **Configure forwarding actions**

      * **Forward** ** to**

         The ALB forwards the request to the server group you specify.

         
         |Parameters |Notes |
         |---|---|
         |Server group |Select the server group to which requests are forwarded.<br><br><br>* You can only select server groups that are in the same VPC as the current ALB instance.<br><br>* When a request meets the specified forwarding condition(s), it will be forwarded to the server group.<br><br>* In a single custom forwarding rule, you can add up to 5 server groups.<br><br>* When multiple server groups are added, you can set a weight for each server group individually. The default weight for a server group is 100. You can modify the weight to any value from 0 to 100. When a server group's weight is set to 0, it indicates that the ALB will not forward client traffic to that server group. For more information, see [Server group weight](https://docs.byteplus.com/docs/clb/Forwarding-rule-Overview). |
         |Session persistence among server groups |Enable session persistence among server groups.<br><br><br>* This parameter is only displayed when you have configured multiple server groups.<br><br>* Session persistence between server groups is disabled by default. After enabling this feature, you need to set a timeout period. The valid range for the timeout is 1 to 86400 (seconds), with a default value of 1000. Unit: Second.<br><br><br>For more information, see [Session persistence between server groups](https://docs.byteplus.com/docs/clb/Forwarding-rule-Overview). |
         

      * **Redirect** ** to**

         The ALB redirects the request. For example, redirect an HTTP request to an HTTPS request, or redirect requests from the original domain to a new domain.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">To redirect all requests of a listener, configure the forwarding rules as follows: leave the domain field empty, set the path to ~/, and select Redirect as the forwarding action.         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">When configuring redirect parameters, modify at least one of the following parameters to avoid redirect loops: <strong>Protocol</strong>, <strong>Domain</strong>, <strong>Port</strong>, or <strong>URL</strong>. When the request protocol differs from the redirect protocol, ensure the correct port is configured and update relevant server settings to avoid redirection failure.         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">If the value of the <code>Content-Length</code> header in the request exceeds the maximum request body size (<code>client_max_body_size</code>) set on the listener, the ALB will directly return a 413 status code to the client and will not execute the redirection action. For information on how to adjust the maximum request body size on a listener, see <a href="https://docs.byteplus.com/docs/clb/Custom-configurations">Custom configuration</a>.         </div>
         

         
         |Parameters |Notes |
         |---|---|
         |Agreement |Select the protocol for redirection. The protocol can be HTTPS or HTTP.<br><br>When a request meets the specified forwarding condition(s), it will be redirected. |
         |Domain |Specify the domain name to which the request is redirected.<br><br><br>* If you do not specify a domain name, the redirected domain name will be the same as the request's domain name.<br><br>* Domains must comply with the following specifications:<br><br>   * Only English letters, numbers, half\-width periods (.), and hyphens (\-) are allowed.<br><br>   * Must contain at least one half\-width period (.), but cannot begin or end with a half\-width period (.).<br><br>   * Neither the beginning nor the end of each level of a domain name can be a hyphen (\-).<br><br>   * A maximum of 128 characters is allowed.<br><br>   * Must be an exact domain name that complies with domain name specifications, e.g., `www.test.com`. |
         |Port |Specify the port to which the request is redirected. Port range: 1 to 65535.<br><br>If you do not specify a port, the redirected port will be the same as the request port. |
         |URI |Specify the path to which the request is redirected.<br><br><br>* If you do not specify a path, the redirected path will be the same as the request path.<br><br>* The path must comply with the following specifications:<br><br>   * Must start with a forward slash (/).<br><br>   * A maximum of 128 characters is allowed.<br><br>   * Only English letters, numbers, and the following special characters are allowed: `- _ / .% ?# &＝`. Consecutive forward slashes are not allowed.<br><br>* Supports exact paths and regular expressions:<br><br>   * Exact path<br><br>      * Format:<br><br>         * Must start with a forward slash (/).<br><br>         * Only letters, numbers, and the following special characters are permitted: `- _ / .% ?# * & ＝`. Consecutive forward slashes are not allowed.<br><br>         * By default, exact matching is used. The asterisk (\*) and question mark (?) can also be used as wildcards.<br><br>         * A maximum of 128 characters is allowed.<br><br>      * Examples:<br><br>         * Exact match: If the path is configured as `/api/v1/users`, a request to `/api/v1/users` will match successfully.<br><br>         * Prefix match: If the path is configured as `/api/*`, requests to `/api/v1/users` and `/api/v2` will both match successfully.<br><br>   * Regular expression<br><br>      * Format:<br><br>         * The value must start with a tilde (~), and the tilde can only appear once at the beginning.<br><br>         * Only letters, numbers, and the following special characters are allowed: `.- _ / ＝ ?~ ^ * $ : ( ) [ ] + \|`.<br><br>         * `~` at the beginning indicates case\-sensitive matching. `~*` at the beginning indicates case\-insensitive matching.<br><br>      * Example: ~^/api/v[0\-9]+/users/.\*$<br><br>      * If you use parentheses `( )` in the path specified in the forwarding condition to create capture groups, you can use placeholders like `${1}`, `${2}`, `${3}`, etc., in the path specified in the forwarding action. These placeholders correspond sequentially to the capture groups (${1} for the first group, ${2} for the second, and so on). When processing the request, ALB replaces these placeholders with the path fragments matched by the corresponding capture groups. Example: Suppose the path in the forwarding condition is `/volc/(.*)/(.*)/aaa`, and the path in the forwarding action is `/${1}/${2}`. If the request path is `/volc/ccc/bbb/aaa`, ALB will replace ${1} with ccc and ${2} with bbb. The final redirect path is `/ccc/bbb`. |
         |Query |Specify the query string of the redirect target URL, which is the part after the ? in the URL, e.g., `xxx=xxx`. Example: `city=beijing` in `www.test.com/test/?city=beijing`.<br><br><br>* If no query string is specified, the redirect automatically uses the query string from the original request.<br><br>* Custom query strings must meet the following specifications:<br><br>   * Maximum length: 128 characters;<br><br>   * They must not contain spaces or any of the characters `#[]{}\\|<>"`;<br><br>   * Only lowercase English letters are allowed. |
         |Status code |Select a status code to indicate the redirection response status.<br><br>The default status code is 301, indicating that the requested resource has been permanently moved to a new location. ALB supports status codes 301, 302, 307, and 308. |
         

      * **Rewrite**

         The ALB rewrites the request path or domain name and then forwards the request to backend servers using the new path or domain.

         
         |Parameters |Notes |
         |---|---|
         |Path |Specify the new path. When a request meets the specified forwarding condition(s), it will be forwarded to the new path. The path must comply with the following specifications:<br><br><br>* The path length cannot exceed 128 characters.<br><br>* The path must start with a forward slash (/).<br><br>* The path can only include English letters, numbers, and the following special characters: `- _ / .% ?# &＝`. Consecutive forward slashes are not allowed.<br><br>* If you use parentheses `( )` in the path specified in the forwarding condition to create capture groups, you can use placeholders like `${1}`, `${2}`, `${3}`, etc., in the path specified in the forwarding action. These placeholders correspond sequentially to the capture groups (${1} for the first group, ${2} for the second, and so on). When processing the request, ALB replaces these placeholders with the path fragments matched by the corresponding capture groups. Example: Suppose the path in the forwarding condition is `/volc/(.*)/(.*)/aaa`, and the path in the forwarding action is `/${1}/${2}`. If the request path is `/volc/ccc/bbb/aaa`, ALB will replace ${1} with ccc and ${2} with bbb. The final forwarding path is `/ccc/bbb`. |
         |Domain |Specify the new domain name. When a request meets the specified forwarding condition(s), it will be forwarded to the new domain name. Domains must comply with the following specifications:<br><br><br>* If left blank, it defaults to being consistent with the original request's domain name.<br><br>* The hostname must be 3 to 128 characters in length, and supports lowercase letters (a–z), numbers, hyphens (\-), periods (.), as well as wildcard asterisks (\*), equals signs (=), tildes (~), underscores (_), plus signs (+), backslashes (\), carets (^), exclamation marks (!), dollar signs ($), ampersands (&), vertical bars (\|), parentheses (()), square brackets ([]), and question marks (?).<br><br>* A hostname must contain at least one period (.), which cannot appear at the beginning or end.<br><br>* The rightmost domain label can only contain letters and the wildcard asterisk (\*); it cannot contain digits or hyphens (\-). The leftmost domain label is allowed to be an asterisk (\*).<br><br>* A hyphen (\-) cannot appear at the beginning or end of any domain tag. The wildcard asterisk (\*) and question mark (?) can appear anywhere in a domain label. |
         

      * **Rate limiting**

         When the number of requests exceeds the configured QPS, the ALB will reject requests that exceed the limit.

         
         |Parameters |Notes |
         |---|---|
         |QPS |Configure QPS.<br><br><br>* When the number of client requests exceeds the configured QPS, ALB will reject the exceeding requests and return a 503 status code to the client.<br><br>* The rate limiting feature is disabled by default. After enabling this feature, you need to enter the QPS value. Value range: 100\-150000. |
         

      * **Return fixed response**

         The ALB directly returns your custom response to the client and does not forward the client request to the backend server.

         
         |Parameters |Notes |
         |---|---|
         |HTTP response code |Set the HTTP response status code. Allowed response status codes include 2xx, 4xx, and 5xx. The x can be any number from 0 to 9. |
         |Response body type |Set the response body type. The response returned by ALB to the client will include the Content\-Type header.<br><br>Allowed response body types include: text/plain, text/css, text/html, application/javascript, and application/json. |
         |Response body |Optional. Configure the response body. Maximum of 1024 characters is supported. |
         

      * **Cross\-domain**

         Cross\-domain refers to any difference in the protocol, domain, or port between the client's request and the address of the page returned by the server.

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">This feature is currently in Beta stage. For trial requests, please contact your account manager.         </div>
         

         
         |Parameters |Notes |
         |---|---|
         |Allowed sources |Set the site allowed to access server resources via browser.<br><br><br>* Supports configuring the wildcard "\*", and allows multiple values separated by commas, up to 32 values.<br><br>* Each value must start with http:// or https://, followed by a domain name or a single\-level wildcard domain (\*.test.abc.example.com).<br><br>* Each value supports setting a port, with a port range of 1 to 65535. |
         |Allowed methods |Select the allowed HTTP method for cross\-origin access.<br><br><br>* Supports GET, POST, PUT, DELETE, HEAD, OPTIONS, and PATCH.<br><br>* Multiple selections are supported. |
         |Allowed request headers |Allowed headers for cross\-origin requests (excluding default browser headers)<br><br><br>* Can be configured with the wildcard "\*", and allows multiple values separated by commas, up to 32 values.<br><br>* Each value only allows uppercase and lowercase letters, numbers, and hyphens "\-" and underscores "_" that are not at the beginning or end, with a maximum length of 32 characters. |
         |Allowed response headers |Response headers allowed to be accessed by browsers and JavaScript scripts<br><br><br>* Can be configured with the wildcard "\*", and allows multiple values separated by commas, up to 32 values.<br><br>* Each value only allows uppercase and lowercase letters, numbers, and hyphens "\-" and underscores "_" that are not at the beginning or end, with a maximum length of 32 characters. |
         |Allow credentials |Allow credentials for cross\-origin requests<br><br><br>* Allow<br><br>* Deny |
         |Browser cache duration |Set the browser cache duration. Value range: \-1 to 172,800 seconds. |
         

      * **Write Header**

         Add a `key: value` pair to the request header, which will be sent to the backend server along with the request.

         
         |Parameters |Notes |
         |---|---|
         |Key |Enter the header field name.<br><br><br>* The length must be 1 to 40 characters, and supports uppercase and lowercase letters (a–z), numbers, underscores (_), and hyphens (\-).<br><br>* Field names must be unique.<br><br>* Regardless of case, the following header names are not supported: x\-real\-ip, x\-forwarded\-for, x\-forwarded\-proto, x\-alb\-waf\-requestid, x\-alb\-waf\-real\-port, upgrade, connection, x\-vport, x\-vip, x\-clb\-cluster, x\-toutiao\-lb\-ip, x\-vni, content\-length, transfer\-encoding, keep\-alive, host, cookie, authority. |
         |Value type |Header field content type. Valid values:<br><br><br>* Custom: You define the custom header field content.<br><br>* System defined: The system defines the header field content. |
         |Value |Enter the header field content.<br><br><br>* When Value Type is set to System\-defined, the system automatically writes content to the header. The available options are as follows:<br><br>   * $remote_addr (client IP address)<br><br>   * $remote_port (client port)<br><br>   * $Scheme (request protocol)<br><br>   * $load_balancer_id (ALB instance ID)<br><br>   * $Vport (listening port)<br><br>   * $endpoint_id (endpoint ID)<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">$endpoint_id parameter is in invite\-only beta. For trial requests, please contact your account manager.   </div><br>   <br><br>* When Value Type is set to Custom, you can define the header content yourself, subject to the following specifications:<br><br>   * Length limit: 1\-128 characters.<br><br>   * Supports wildcard asterisks (\*), question marks (?), and printable ASCII characters with code values in the range `ch >= 32 && ch < 127`. The characters `$` and `"` are not supported.<br><br>   * No leading or trailing spaces.<br><br>   * Must not end with `\`. |
         

   3. **Other parameters**

      
      |Parameters |Notes |
      |---|---|
      |Description |Enter the description of the forwarding rules. The description must comply with the following specifications:<br><br><br>* Cannot exceed 255 characters.<br><br>* Must start with an English letter or a Chinese character.<br><br>* Can only contain English letters, Chinese characters, numbers, spaces, and the following special characters: `,._=-，。`. |
      

6. Click **Associate/Disassociate** to complete the action.


&nbsp;

&nbsp;

&nbsp;
