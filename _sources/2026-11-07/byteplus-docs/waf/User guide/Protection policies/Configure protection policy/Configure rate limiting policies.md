---
title: "Configure rate limiting policies"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/docs-configuring-rate-limit-policies"
---

The rate limiting policy can prevent your server resources from being excessively occupied and ensure that normal access services are not affected. WAF offers two modes of protection: customized and intelligent. When both modes are enabled, the system first matches the customized protection rules, then dynamically adjusts based on the intelligent protection policy.

<span id="b98b8fec"></span>
## Background information


* Customized protection: supports flexible customization of white traffic request characteristics based on business circumstances. Requests can be restricted according to various HTTP request objects such as network access IP and Session to mitigate the impact of CC attacks on the server.

* Intelligent protection (available only for the advanced version and above): WAF learns the baseline of independent business traffic to form asset profiles, providing customized intelligent protection strategies for assets while continuously analyzing the traffic baseline to dynamically adjust protection strategies based on business circumstances. After enabling the intelligent protection feature, WAF will start learning the business traffic baseline upon monitoring request traffic. The initial learning cycle lasts approximately 7 days. Upon completion, intelligent protection rules will be pushed and enabled, with continuous updates to the rules.


<span id="53772fd7"></span>
## Caution


* The intelligent protection feature is currently only available to premium versions and above. Once enabled, corresponding feature activation fees, QPS package additional fees, and elastic QPS additional fees must be paid.

* The sequence of effectiveness for the two protection modes: prioritize matching custom protection rules, then dynamically adjust according to the intelligent protection strategy.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Requirements

You have connected the website that needs to be protected to the WAF instance. For relevant association operations, please refer to [Comparison of website association methods](https://docs.byteplus.com/en/docs/6511/935148).

<span id="3dc1727c"></span>
## Add a custom rate limiting rule

The custom rate limiting rule executes corresponding actions on access requests based on the request path and the number of visits to the custom statistical object within a certain period.

<span id="4adb8b35"></span>
### Procedure


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. Select the instance region in the top menu bar.

3. In the left navigation, select **Protection Policy \> Rate limiting**.

4. Turn on the Rate limiting function of the domain name to be protected.

   1. Select the domain name that needs to add a policy.

   2. (Optional) Confirm that the protection mode of the current domain is "Protection enabled". Otherwise, click **Change protection mode** to modify it.

   3. Turn on the policy enable switch.

5. Click **Add Rule** to configure the rate limiting rule parameters.

   
   |**Parameter** |**Description** |Example |
   |---|---|---|
   |Rule name |Protection rule name.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Start with a letter or digit.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Allowed characters include letters, digits, periods (.), underscores (_), and hyphens (\-).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The length must be between 1 and 128 characters.</div><br> |Rate limiting |
   |Request characteristics |||
   |Request path |Please fill in the path of the website that needs protection, which can be a specific page path or all paths under the entire website.<br><br><br>* **Match specific path**: A specific page path, for example, to intercept access to `test.com/test.html`, just fill in the path information after the domain name `/test.html`.<br><br>* **Match all paths under the directory**: Use`*`It can match all paths, and`*`must be at the end of the path.<br><br>   * To match all paths under the entire website, fill in `/*`.<br><br>   * To match all paths under a certain directory, use it under the corresponding directory path.`*`That's it. For example, `/test/*` indicates matching all paths under the `/test/` directory.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><code>/test/*/abc.html</code> and <code>/test/*</code> both indicate matching all paths under the <code>/test/</code> directory.   </div><br>    |/test.html |
   |Advanced conditions |* Set other matching fields, logical operators, and matching content. For a description of matching fields and logical operators, please refer to [Advanced Condition Configuration Instructions](https://docs.byteplus.com/en/docs/6511/1356289).<br><br>* The **request path** and **advanced conditions** have an `AND` relationship, meaning that the rule can only be triggered when both the request path and advanced conditions are met.<br><br>* To configure **multiple request path matches**: if you need the rule to apply to multiple request paths, first set the main request path to all paths under the directory, then add conditions for matching fields as the request path. For example, to configure `/test/123.html` and `/test/abc.jpg`, you can refer to the following operations:<br><br>   1. Set the **request path** to `/test/*`.<br><br>   2. Add 2 conditions:<br><br>      * Condition 1: `Request path` equals `/test/123.html`<br><br>      * Condition 2: `Request path` equals `/test/abc.jpg`<br><br>   3. The relationship between the two conditions is set to `OR`. |`Request protocol` `Equal to` `HTTP` |
   |Statistical conditions |||
   |Statistical object |Select the statistics object that needs to be matched by the rule and fill in the configuration information. Support custom header, custom cookie, custom parameters and source IP four types.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To use fields in cookies as statistical objects, you need to select <code>custom cookies</code> and configure field information. It is not supported to use the entire cookie as a statistical object.</div><br><br><br><br>* Custom header: Fill in the header, the first letter of each word needs to be capitalized, such as `User-Agent`, `Cookie`, `X-Forwarded-For`.<br><br>* Custom cookies: support filling in English, numbers, underscore “_” and hyphen “\-”.<br><br>* Custom parameters: Support filling in English, numbers, underscore “_” and hyphen “\-”.<br><br>* Source IP: A single access IP is used as a statistical object. |Custom Header: User\-Agent |
   |Statistical time |The statistical time period in which the request occurred. |60 |
   |Threshold setting |Thresholds include the number of requests per object over the duration of the count, as well as the number of requests per path. When the number of times the statistical object initiates a request and the total number of request path accesses exceeds the set threshold, the system processes the request of the statistical object according to a preset execution action. You can set the effective period to be permanent or to be a cyclical period.<br><br><br>* Permanent effectiveness: Continuous statistics of access times throughout the day.<br><br>* Cyclical effectiveness: Set the time period during which it is effective, such as from 8 AM to 8 PM on every working day, counting access times, and not counting during other times. |* Cyclic effective: Monday, Tuesday, Wednesday, Thursday, Friday<br><br>* During the effective time `08:00-11:59`, if each object is accessed more than `200` times, and the request path is accessed more than `10000` times<br><br>* During the effective time `18:00-11:59`, if each object is accessed more than `1000` times, and the request path is accessed more than `10000` times |
   |Execute action |||
   |Action |* Observe: Allow the traffic to pass through, but record the behavior in the attack log.<br><br>* Intercept: Intercept the request traffic and report the request behavior to the attack log. If a custom interception response page is configured, WAF will return the configured interception response page information to the client side.<br><br>* Speed limit: Limit the access rate to this request.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For example, set a limit where, within a statistical time of 60 seconds, the maximum number of access times per source IP is 1000 times, and when the total access times reach 10000 times, the speed limit action is executed. Therefore, if a certain source IP reaches 1000 accesses and the total access times for that path reach 10000 times within 60 seconds, all subsequent requests will be intercepted.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To avoid affecting your business, please set the speed limit conditions carefully.   </div><br>   <br><br>* Man\-machine verification: Man\-machine verification is carried out through the verification code. If the verification is passed, it will be released to prevent false sealing.<br><br>* JS challenge: Verify the client JavaScript execution capability through the JS\-SDK. If the verification is passed, it will be released within a specified time. |Block |
   |Time limit |The effective duration of the execution action. Needs to be set when the execution action is interception, human verification, or JS challenge. |180 |
   |Effective configuration |||
   |Priority |The priority of rule matching, P0 has the highest priority and P9 has the lowest priority. The priority of Rate limiting rules under the same request feature cannot be repeated. |P0 |
   |Regular switch |Turn on or off the current rule, which is enabled by default. |Keep it enabled |
   

6. Click **OK** to complete the rule configuration.


<span id="ed8e48d6"></span>
### Configuration result

After the rule is added, you can view the configuration information of the rules in the list, and perform operations such as adjusting rule priority and quick addition.

<span id="df5a234c"></span>
#### Rule effect logic

After configuring the CC rule, when a request occurs, the WAF will match the rule according to the following logic.


1. The access request matches the access path first.

   In the path matching principle, follow the exact matching and longest matching principles, that is, when the access path is requested to match the exact path and the wildcard path at the same time, the exact path will be hit first. For example: there are both `/test/test.html` and `/test/*` path matching rules, priority matching `/test/test.html` related rule settings.

2. For the request to hit the configuration path, and then match its request characteristics.

3. Finally matching statistical characteristics, the request to hit the rule will perform pre\-configured disposal action.


<span id="c5e89b7a"></span>
#### Rule group hierarchy


* First\-level rule group: Rate limiting rules are grouped according to request paths, that is, rules with the same request path belong to the same first\-level rule group.

* Second\-level rule group: Within the same first\-level rule group, second\-level rule groups are distinguished according to advanced conditions of request characteristics. That is, rate limiting rules with the same request path and request characteristics belong to the same second\-level rule group. Within the same second\-level rule group, the priority of the rules cannot be duplicated.


<span id="e3b4abe8"></span>
#### Adjusting priorities

You can adjust the effective priority of rules by dragging the order adjustment icon.


* Drag the position shown in the figure to adjust the priority of the second\-level rule group under the same request path condition. The priority of rules configured with advanced conditions is always higher than that of rules without advanced conditions (i.e., request feature as `All`).

* You can adjust the priority of a single rule within the secondary rule group by dragging the position shown in the figure below②.


<span id="d8e7f59a"></span>
#### Quickly add rules


* Click the position shown in the figure below③ to quickly add rules that satisfy the same request path. You can customize other parameters aside from the request path.

* Click the position shown in the figure below④ to quickly add rules that satisfy the same request features (i.e., both request path and advanced condition configurations are the same). You can customize other parameters aside from the request features.


<span id="fa3f92fb"></span>
### Configuration guidelines

Assuming your expected scenario is as follows: for the path under the domain name `/test.html`, when the same source IP accesses the path more than 500 times within 60 seconds and the total number of visits to the path exceeds 600 times, the interception action is performed, and the access is restricted for 60 seconds; when the access exceeds 50 times within 60 seconds and the total number of visits to the path exceeds 60 times, the alarm action is performed. You need to configure two CC protection rules based on the access path, the reference configuration is as follows.


| |Rule number one |Rule two |
|---|---|---|
|Rule name |Custom |Custom |
|Request path |`/test.html` |`/test.html` |
|Statistical object |Source IP |Source IP |
|Threshold setting |Each object is accessed more than 500 times, and the path access is requested more than 600 times. |Each object is accessed more than 50 times, and the path access is requested more than 60 times. |
|Statistical time |60 seconds |60 seconds |
|Action |Intercept |Warning |
|Time limit |60 seconds |\- |
|Priority |P0 |P1 |


<span id="6b90d7cf"></span>
## Enable intelligent rate\-limiting policy

Intelligent rate\-limiting refers to the WAF forming asset profiles through autonomous baseline learning of business traffic, outputting customized smart protection strategies for assets, while continuously analyzing traffic baselines and dynamically adjusting protection strategies based on business conditions.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Intelligent rate\-limiting policy is currently only available for the premium version and above, and requires payment for the corresponding feature activation fee, QPS package additional fee, and elastic QPS additional fee. For detailed billing information, please refer to <a href="https://docs.byteplus.com/en/docs/6511/182848#e87b876e">Additional functions</a>.</div>


<span id="696ff26e"></span>
### The steps are as follows:


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. Select the instance region in the top menu bar.

3. In the left navigation, select **Protection Policy \> Rate limiting**.

4. Enable intelligent rate\-limiting policy protection for the domain to be protected.

   1. Select the domain for which to add the policy.

   2. (Optional) Confirm that the current domain's protection mode is "Enable Protection"; otherwise, you need to click **Change Protection Mode** to modify it.

   3. Turn on the policy switch.


<span id="b02f07e4"></span>
### Enable description

The system will update the asset profile every 2 hours after enabling the intelligent protection feature and detecting traffic, and push intelligent protection rules at 10 AM on T+7 days.

<span id="3ec98694"></span>
#### Protection mode


* Managed mode: After setting different levels of strictness, the system will automatically push the corresponding range of intelligent protection rules based on the business baseline learning results.

* Emergency mode: The system will automatically issue intelligent protection rules based on the business baseline learning results to quickly mitigate source site anomalies, suitable for business requiring rapid response and a higher level of protection. However, this mode has the risk of false positives, meaning that your normal business access may be intercepted, so it is recommended to set an appropriate protection threshold range.


<span id="52e89d77"></span>
#### Actions


* Intelligent management: Automatically recommend disposal actions based on learning results.

* Observation only: Only observe corresponding requests, and will not restrict.
