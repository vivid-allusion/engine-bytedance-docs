---
title: "Forwarding rule overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Forwarding-rule-Overview"
---

<span id="n8jVIzdN"></span>
## Introduction​

ALB distributes access traffic according to the forwarding rules you set based on different traffic characteristics.

You can configure multiple forwarding rules for a listener.

Basic edition ALB instances support forwarding rules based on domain names and paths. Standard edition ALB instances support forwarding rules based on domain names, paths, and HTTP headers, and also support composite forwarding conditions.

There are differences in the matching logic of forwarding rules between the Basic and Standard editions. For details, see description below.

<span id="c0fbdfd3"></span>
## Classification


|Classification |Explanation |Basic ALB instance |Standard ALB instance |
|---|---|---|---|
|Default forwarding rule |After you create a listener, the system automatically generates a default forwarding rule. Default forwarding rules cannot be deleted, but you can modify the default backend server group associated with the default forwarding rule.<br><br>If a request does not match any custom forwarding rule, ALB applies the default forwarding rule to the request.<br><br> |In the default forwarding rule, the value of the **Domain name** in the forwarding condition is `–`, which indicates any domain name. The value of the **path** is `/`, which indicates the root directory.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For Basic edition ALB instances, the default forwarding rule cannot be applied in the following scenario:</div><br><br><br><div data-tips="true" data-tips-type="default">When a request matches a specific domain name in a forwarding rule but does not match the path.</div><br> |In the default forwarding rule, the value of the forwarding condition is `–`, which indicates any request. |
|Custom forwarding rules |Besides the default forwarding rule, you can create custom forwarding rules based on your business requirements.<br><br><br>* Basic ALB instance: You can specify forwarding conditions and forwarding actions.<br><br>* Standard ALB instance: You can specify forwarding conditions, forwarding actions, and rule priority. | | |


<span id="83a4a6ca"></span>
## Composition of forwarding rules

A forwarding rule consists of a forwarding condition and a forwarding action. The forwarding condition is used to filter requests, and the forwarding action determines how the requests are forwarded.

The following table lists the forwarding conditions and forwarding actions supported by Basic edition ALB instances and Standard edition ALB instances.


|**Version** |**Forwarding condition** |**Forwarding action** |
|---|---|---|
|Basic edition |Based on domain name and path |Forward to, Redirect to |
|Standard edition |Based on Domain, Path, HTTP Headers, HTTP Request Methods, and Query Strings |Forward to, Redirect to, Rewrite, Rate limiting, Return fixed response |


<span id=".6L2s5Y-R6KeE5YiZ5Yy56YWN55qE5LyY5YWI57qn6K-05piO"></span>
## Forwarding rule match

<span id="DiYTMhUv"></span>
### Basic ALB instance

<span id=".6L2s5Y-R6KeE5YiZ5Yy56YWN55qE5LyY5YWI57qn"></span>
#### Domain name and path priority

There is no priority among forwarding rules for Basic edition ALB instances. When ALB receives a client request, it selects a forwarding rule based on the matching results of the domain name and path, and forwards the client request according to that rule. During domain name and path matching, ALB considers the priority of the domain name and path.


* **Domain name priority**

   If the client request's domain name matches multiple domain names in different forwarding rules, ALB determines the corresponding forwarding rule according to the domain name priority.

   
   |**Domain type** |**Example** |**Priority** |
   |---|---|---|
   |Exact domain name |www.example.com |Maximum |
   |Wildcard domain names starting with an Asterisk (\*) |\*.test.com |Second highest |
   |Wildcard domain names ending with an Asterisk (\*) |test.com.\* |Minimum |
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Wildcard domain name matching principle: A wildcard domain name only matches domain names at the same level. For example, \*.example.com matches www.example.com but not example.com.   </div>
   

* **Path priority**

   If the client request's path matches multiple paths in different forwarding rules, ALB selects the corresponding forwarding rule according to the path priority. Details are as follows:

   Paths defined using regular expressions have higher priority than exact paths.

   * If a request's path matches multiple paths defined using regular expressions, ALB selects one forwarding rule based on the configuration time of the corresponding forwarding rules. The rule configured earliest is prioritized.

   * If a request's path matches multiple paths, ALB selects one forwarding rule according to the longest prefix matching principle. The rule corresponding to the path with the longest prefix is prioritized. For example, the request path /abcde matches both /abc and /abcd, but ALB will select the forwarding rule corresponding to /abcd.


<span id=".5Yy56YWN5ZCO55qE6L2s5Y-R5pON5L2c"></span>
#### Forwarding rule matching process

When ALB receives a client request, it first performs domain name matching according to domain name priority:


* If a matching domain name exists, it continues to perform path matching according to path priority.

   * If a matching path exists, it forwards the request according to the forwarding rule corresponding to the matched domain name and path.

   * If no matching path exists, the request cannot be forwarded, and a 4xx status code is returned to the client.

* If no matching domain name exists, it attempts to match a forwarding rule with "path only, no domain name".

   * If there is a forwarding rule with "path only, no domain name," the process continues with path matching according to path priority.

      * If a matching path exists, the request is forwarded according to the forwarding rule corresponding to that path.

      * If no matching path exists, the request is forwarded according to the default forwarding rule.

   * If there is no forwarding rule with "path only, no domain name," the request is forwarded according to the default forwarding rule.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Note on "path only, no domain name": This refers to a forwarding rule configured with a non\-<code>/</code> path but no specific domain name.</div>


* <div data-tips="true" data-tips-type="tip">When no domain name is configured, the default value for the domain name, <code>-</code>, is used. In the flowchart above, the "domain name" referred to in the conditional statement "the domain name configured in the forwarding rule matches the request's domain name" means a specific domain name like <code>www.example.com</code>. The case where the domain name is <code>-</code> is not included.</div>



<span id="944a56e9"></span>
### Standard ALB instance

<span id="9bbf0f37"></span>
#### **Forwarding rule priority**

For Standard edition ALB instances, there is priority among forwarding rules under the same listener:


* The default forwarding rule has the lowest priority, and its priority cannot be adjusted.

* The priority of custom forwarding rules can be adjusted.

* A smaller priority number indicates a higher priority. In the forwarding rule list, a rule placed higher up has a higher priority.

* By default, a newly created forwarding rule has a higher priority than existing rules.


<span id="5763c6ac"></span>
#### **Forwarding rule matching process**

Upon receiving a client request, ALB performs matching sequentially according to the priority of the forwarding rules, from highest to lowest. When a request satisfies the forwarding conditions of a particular forwarding rule, ALB stops matching other rules and forwards the request according to this matched rule.

Different forwarding conditions within the same rule have an "AND" relationship. Different values within the same forwarding condition have an "OR" relationship. A request is considered to match a forwarding rule only when it satisfies all the forwarding conditions within that rule.

<span id="8b17724a"></span>
## Traffic distribution based on forwarding rules

When an ALB instance receives a client request, it distributes the traffic to server groups based on the forwarding rules.

Forwarding rules are divided into default and custom rules:


* A default forwarding rule can only be associated with one backend server group.

* A custom forwarding rule can be associated with multiple backend server groups. Furthermore, you can configure weights for server groups and enable session persistence between groups. ALB distributes traffic to the server groups according to your configuration.


<span id="4fae2ffb"></span>
### **Server group weight**

ALB can forward client traffic to the corresponding server groups proportionally based on the weight of each server group.

When you add multiple server groups to a custom forwarding rule, you can set a weight for each group. Weight range: 0\-100. When you add a new server group, its default weight is 100. When the weight is set to 0, it indicates that ALB will not forward client traffic to that server group.

Example:

If you add 4 server groups to a custom forwarding rule and set different weights for each server group. The proportion of client traffic received by the different server groups is shown in the table below.


|Server Group |Weight |Proportion of client traffic received by a server group |
|---|---|---|
|Server group A |40 |40/(40+20+20+20) × 100% = 40% |
|Server group B |20 |20/(40+20+20+20) × 100% = 20% |
|Server group C |20 |20/(40+20+20+20) × 100% = 20% |
|Server group D |20 |20/(40+20+20+20) × 100% = 20% |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Currently, ALB does not provide health check capabilities at the server group level. For example, when Server Group A has no servers added or all servers within the group have an abnormal health check status, 40% of the traffic will still be forwarded to Server Group A. In such cases, ALB will return a 502 or 503 status code.</div>


<span id="bb489866"></span>
### **Session persistence between server groups**

When you add multiple server groups to a custom forwarding rule, you can enable the "Inter\-Server Group Session Persistence" feature.


* After enabling this, ALB provides cookie\-based session persistence, which can forward requests from the same client to the same backend server group. Specifically, after the client's first request is forwarded to a server group, ALB embeds that server group's cookie information in the response. Subsequent client requests will carry this cookie. ALB recognizes the cookie information and forwards the request to the same previous server group.

* The priority of the "Inter\-Server Group Session Persistence" feature is higher than server group weight. When a client request carries cookie information, ALB forwards the request to the same previous server group and no longer distributes traffic based on server group weights.


<span id="2701ca61"></span>
### Traffic distribution process based on weight and session persistence

When you add multiple server groups to a custom forwarding rule, you can configure inter\-group session persistence to direct requests from the same client to the same server group. Additionally, you can configure session persistence for servers within a group to direct requests from the same client to the same server.

The flowchart below illustrates how ALB forwards client requests to server groups and servers within those groups based on the weight and session persistence configurations after receiving a client request.
