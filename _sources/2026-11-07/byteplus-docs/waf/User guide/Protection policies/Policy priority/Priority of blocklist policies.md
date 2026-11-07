---
title: "Priority of blocklist policies"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/Priority_of_blocklist_policies"
---

Blocklist policies are used to block known malicious access and support configuration based on multi\-dimensional criteria, including IP address, IP range, geographic location, access path, and request protocol. Due to the large number of configuration parameters and the priority relationships between rules, it is recommended that you carefully read this document before making any configurations to understand the execution order of the rules.

<span id="7eb66485"></span>
## Rule composition

Each access denial rule consists of the following elements, and the protection action is triggered only when all elements match:


* **Protected domain name (see figure 1 below)** : Specifies the domain name to be protected. Supports selecting and adding exact domain names, wildcard domain names, or custom domain name groups.

* **Access source (see ② in the figure below)** : This refers to the IP address from which access originates and supports the following configuration methods:

   * Manually enter a single IP, multiple IPs, or an IP range

   * Select configured IP address group

   * Select specific geographic locations

* **Access features**:

   * **Access path (Figure 3 below)** : The URL path of the target; supports entering an exact path or using wildcards`*`Match any path.

   * **Advanced conditions (see ④ in the figure below)** : Other matching conditions, including request protocol, request method, request headers, request parameters, request body, request cookies, request user agent, and more.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">A single advanced condition in a rule has only one configuration method for its matching value; therefore, advanced conditions will temporarily not be included in the scope of discussion below.      </div>
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9481aed50e861eb1d3e1ad847dcf613c.png) </span>


<span id="74b07d57"></span>
## Matching priority

After a blocklist rule is created, WAF will match rules in the order of **protected domain**, **access characteristic**, and **access source**. Internal priorities of each element are as follows:

<span id="3d61d8ae"></span>
### Protected domain name


* **Priority**: **Exact domain name** \> **Wildcard domain name**

* **Matching example**: Create two access denial rules, each using `www.example.com` and `*.example.com` respectively as a protected domain name.`A`And`B`。 When the WAF detects a request to access `www.example.com`, rule matching is prioritized.`A`。 To`A`If other matching conditions are not met, then match the rule.`B`。


<span id="87857fb0"></span>
### Access characteristics (access path)


* **Priority**: **Exact path** \> **Wildcard path**

* **Matching example**: Create two access denial rules whose protected domain is `www.example.com` and whose access paths are `/path/to/resource` and `/path/*`, respectively.`A`and`B`When the WAF detects a request to `www.example.com` with the target path `/path/to/resource`, the rule is matched first.`A`。 To`A`If other matching conditions are not met, apply the rule again.`B`。


<span id="c5146826"></span>
### Access source


* **Priority**: **Exact IP** \> **IP address range (CIDR)**  \> **IP address group** \> **IP list** \> **Geolocation** \> \* **(All IPs)** .

* **Matching example**: Create 6 access denial rules`A`、`B`、`C`、`D`、`E`、`F`All protected domain names are `www.example.com`, and all access paths are `/path/to/resource`. Differences in access sources

   * Rule`A`The source of access is a manually entered, precise IP address`1.1.1.1`;

   * Rule`B`The access source is a manually entered CIDR`1.1.1.0/24`;

   * Rule`C`The access source is IP address group A (which includes `1.1.1.1`, `1.1.1.2`, `1.1.1.3`)

   * Rule`D`The access source is a manually entered list of IP addresses `1.1.1.1`, `1.1.1.2`, `1.1.1.3`.

   * Rule`E`The source of access is the associated geographic locations: `Anhui` and `Afghanistan` (assuming `1.1.1.1` is located in Anhui).

   * Rule`F`Access source`*`(all IPs).


When the WAF detects a request to `www.example.com` with the target path `/path/to/resource` and the source IP `1.1.1.1`, the rule takes precedence.`A`。 To`A`Other matching conditions are not satisfied; match the rule.`B`; if`B`If the other conditions are also not met, the rule applies.`C`and so on.

<span id="ccc34ad6"></span>
## Configuration example

Below is a more complex scenario used as an example to illustrate the request matching process.

<span id="011345e0"></span>
### **Business requirements**

Monitor the following specific access requests:


* Protected domain name: `test.volc001.com`

* Access path: `/test/abc`

* Access source: `1.1.1.1`


<span id="cb95243e"></span>
### **Solution**

This requirement can be fulfilled through various combinations of rules. When the impact on other access traffic is not taken into account, the system supports 24 different rule configuration options. The specific configurations are shown in the following table. When multiple rules are present, WAF matches each rule one by one in the order shown in the diagram, from left to right and from top to bottom, and performs the corresponding protection actions.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To prevent erroneous Blockion from affecting normal business operations, it is recommended to configure rules according to the principle of minimal Blockion.</div>



|Rule |Protected domain name |Access path |Source IP |Perform action |
|---|---|---|---|---|
|1 |test.volc001.com |/test/abc |1.1.1.1 |Observe |
|2 |||1.1.1.1/24 |Block |
|3 |||IP address group containing 1.1.1.1 |Observe |
|4 |||1.1.1.1，1.1.1.2，... |Block |
|5 |||1.1.1.1 Region |Observe |
|6 |||\*(all IP addresses)\* |Block |
|7 ||/test/\* |1.1.1.1 |Observe |
|8 |||1.1.1.1/24 |Block |
|9 |||IP address group containing 1.1.1.1 |Observe |
|10 |||1.1.1.1，1.1.1.2，... |Block |
|11 |||1.1.1.1 Location |Observe |
|12 |||\*(all IPs) |Block |
|13 |\*.volc001.com |/test/abc |1.1.1.1 |Observe |
|14 |||1.1.1.1/24 |Block |
|15 |||IP address group containing 1.1.1.1 |Observe |
|16 |||1.1.1.1，1.1.1.2，... |Block |
|17 |||1.1.1.1 Region |Observe |
|18 |||\*(all IPs)\* |Block |
|19 ||/test/\* |1.1.1.1 |Observe |
|20 |||1.1.1.1/24 |Block |
|21 |||IP address group containing 1.1.1.1 |Observe |
|22 |||1.1.1.1，1.1.1.2，... |Block |
|23 |||1.1.1.1 Location |Observe |
|24 |||\*(All IPs) |Block |


<span id="c313c7f3"></span>
### **Effect validation**

The following are the results for several typical request scenarios:


* Target request

   * `curl http://test.volc001.com/test/abc -H "Client-Ip: 1.1.1.1"`

   * Matching rule: 1

   * Action: Observe

* Requests for different paths

   * `curl http://test.volc001.com/test/new -H "Client-Ip: 1.1.1.2"`

   * Matching rules: 8

   * Action: Block

* Cross\-domain requests

   * `curl http://newdomain.volc001.com/test/abc -H "Client-Ip: 1.1.1.1"`

   * Matching rule: 13

   * Action: Observe

* Requests for different domain names and paths

   * `curl http://newdomain.volc001.com/test/new -H "Client-Ip: 1.1.1.2"`

   * Matching rule: 20

   * Action: Block
