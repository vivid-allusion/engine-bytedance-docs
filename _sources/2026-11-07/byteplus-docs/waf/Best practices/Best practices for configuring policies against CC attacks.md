---
title: "Best practices for configuring policies against CC attacks"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/Configuring_rate_limiting_policies_to_defense_against_L7_DDoS_attacks"
---

If your business is likely exposed to the risk of CC attacks, it is recommended to enhance protective effects by configuring Rate limiting strategies and Bot traffic protection. Prevent your server resources from being excessively occupied, ensuring that normal access to services is not affected.

<span id="6a98457a"></span>
## Explanation of CC attack methods

<span id="6a98457a"></span>
## Common CC attacks mainly include the following methods:


* **High\-frequency requests**: Attackers can control the frequency of requests, sending a large number of requests to the target website within a short period, such as hundreds or even thousands of requests per second. This type of request may involve frequent visits to the homepage or specific pages to maximize server resource consumption.

* **Multiple source IP addresses**: Attackers use multiple different IP addresses to launch attacks, bypassing the server's access control mechanisms, causing the request limit strategy for a single IP address to fail. Requests from multiple source IP addresses can make it harder for attackers to be tracked and identified, increasing the difficulty of defense.


<span id="72578e3a"></span>
## Configuring Rate limiting policies

WAF provides two modes: custom Rate limiting protection and intelligent Rate limiting protection. When both modes are enabled, the system first matches the custom protective rules. If the request does not hit the custom protective rules, it then matches the intelligent protective strategies.


* CC Custom Protection: Supports flexible customization of white traffic request characteristics based on business conditions. Requests can be restricted based on various HTTP request objects such as network access IP and Session, alleviating the impact of CC attacks on the server.

* CC Intelligent Protection (available only for the advanced version and above, and free for a limited time): WAF forms asset profiles through autonomous learning of business traffic baselines, outputs customized intelligent protection strategies for assets, and continuously analyzes traffic baselines to dynamically adjust protection strategies based on business conditions. After enabling the CC Intelligent Protection function, WAF will initiate business traffic baseline learning upon monitoring request traffic. The initial learning period is approximately 7 days, and after learning is completed, intelligent protection rules will be pushed and enabled, with rules continuously updated.


<span id="cf7ad027"></span>
### Configure Custom rate\-limiting policies

To configure a custom protection strategy that meets requirements and is effective, it is necessary to first analyze the business traffic situation. For example, set a CC rule to observe whether the number of requests from a single IP to the specified path exceeds the set threshold during the statistical period, and analyze the access logs to determine if attack requests were intercepted.

<span id="87ce9113"></span>
#### Notes

If there are IPs that have been clearly identified as potential false positives for the CC protection strategy, white\-listing can be performed through the **Allowlist** function of access control.

<span id="e25f0753"></span>
#### Scenario Description

When an IP accesses the login page `login.html` under the current domain more than 1000 times within 10 seconds, the request behavior of that IP will be recorded. \nThis scenario is only for reference as an example. In practical applications, you need to set the protection path and protection threshold based on your business needs, and choose appropriate handling actions to achieve protection.

<span id="16d625da"></span>
#### Steps


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. In the top menu bar, select the region of your instance.

3. In the left navigation select **Protection Policy \> Rate limiting**.

4. Turn on the Rate limiting function of the domain name to be protected.

   1. Select the domain name to be protected.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Confirm that the protection mode of the current domain is <strong>"Protection enabled"</strong>. Otherwise, you need to change the protection mode.      </div>
      

   2. Turn on the protection switch.

5. Click **Add** to configure relevant parameters.

   * Request path: fill in the most important and frequently visited paths under this domain, such as the website login page `/login.html`

   * Statistical object: Select **source IP**, which means to collect request data for different IPs by dimension of IP.

   * Duration of statistics: set according to traffic fluctuations. The greater the business fluctuations, the smaller the value set relatively. It is recommended to set it to 5\-10 seconds.

   * Threshold setting: Select **periodic cycle effectiveness**

      * Each object access threshold and request path threshold should remain consistent, both are set to 1000.

      * If the effective time needs to include 00:00, it is recommended to set two time periods, one before 00:00 and one after 00:00, to ensure complete data recording. For example, if you want to set the effective time from 19:00 to 05:00 the next day, you should set two periods of effective time: 19:00\-23:59 and 00:00\-04:59

   * Set the action: change to **Observe.** 

6. Click **OK**.


<span id="513643fc"></span>
#### What to do next

On the **log management** page, filter log data under the specified domain and path where the action taken is **pass** and **observe**. Determine whether there are false positives or missed requests.


* If the logs where the action taken is **allow** only contain normal business requests, and the logs where the action taken is **observe** only contain attack requests, it indicates that there are no false positives or missed requests. At this time, it is recommended to adjust the handling action to **block** for protection.

* If the logs where the action taken is **observe** contain normal business requests (i.e., false positives exist), it is recommended to adjust the threshold to a higher value and observe the protection effect.

* If the logs where the action taken is **allow** contain attack requests (i.e., missed requests exist), it is recommended to adjust the threshold to a lower value and observe the protection effect.


<span id="5bc2195b"></span>
### Configure intelligent rate\-limitig policies

WAF forms asset profiles through self\-learning of business traffic baselines, outputs customized intelligent protection strategies for assets, and continuously analyzes traffic baselines to dynamically adjust protection strategies based on business conditions.

<span id="7fc2785b"></span>
#### Steps


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. In the top menu bar, select the region of your instance.

3. In the left navigation select **Protection Policy \> Rate limiting**.

4. Turn on the CC access function of the domain name to be protected.

   1. Select the domain name to be protected.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Confirm that the protection mode of the current domain is <strong>Protection enabled</strong>. Otherwise, you need to change the protection mode.      </div>
      

   2. Turn on the intelligent CC protection switch.

   3. Set the mode to **Managed Mode \- Normal** and the action to **Intelligent Management**.


<span id="cb6b80e3"></span>
#### What to do next

Adjust the parameter settings according to the business status and protection effect.


* If your business is under attack, it is recommended to promptly change the mode to **Emergency Mode**.

* If the current intelligent protection effect cannot effectively block attacks, it is recommended to set the protection threshold range to **more stringent**.


<span id="bda6fe82"></span>
## Configure the Bot statistical protection policies

If you find that the attack source IP, User\-Agent, or request path meets fixed characteristics, these attack requests are likely initiated by automated tools. For such attack requests, you can create a new Bot statistical protection strategy. Bot statistical protection rules are used to count the number of times or the percentage of repeated IPs that meet the request characteristics within a specific time. When the statistical content reaches the set threshold, actions such as observation, interception, human verification, or other actions are executed on requests that meet the request characteristics.

<span id="20a1e214"></span>
### Notes

The Bot management function is currently only available for the Advanced version and above.

<span id="3e27cd35"></span>
### Scenario Description

Assuming a type of attack traffic has the following characteristics: the number of source IPs with the same User\-Agent within 30 seconds accounts for more than 15% of all source IPs. Now needs to set up a Bot statistical protection strategy for this attack behavior. Refer to the following steps.

<span id="83217609"></span>
### Steps


1. Log in to [The Web Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. In the top menu bar, select the region of your instance.

3. In the left navigation, select **Protection Strategy \> Bot Management**

4. Enable the statistical protection rule function for the domain to be protected.

   1. Select the domain to be protected.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Confirm that the protection mode of the current domain is <strong>Protection enabled</strong>. Otherwise, you need to change the protection mode.      </div>
      

   2. Confirm that the protection mode of the current domain is "Protection enabled". Otherwise, you need to change the protection mode.

   3. Enable the statistical protection rule switch.

5. Click **Add** to configure the relevant parameters.

   * Feature description: **Request path** is `/*`, or set the path to other frequently accessed and important paths.

   * Statistical object: **Custom header** is set to **User\-Agent**.

   * Statistical content: Duplicate ratio, within **15** seconds, the percentage of identical IPs among each object exceeds **10%** , and the number is greater than **20**.

   * Execute Action: Observe.

6. Click **OK**.


<span id="109636a7"></span>
### What to do next

On the **Log Management** page, filter the log data with the specified domain name and path, where the action is **Allow** and **Observe**. Determine whether there are false positives or missed requests.


* If the logs with the action as **Allow** only contain normal business requests, and the logs with the action as **Observe** only contain attack requests, it indicates that there are no false positives and no missed requests. At this time, it is recommended to adjust the action to intercept for protection.

* If the logs with the action as **Observe** contain normal business requests (i.e., there are false positives), it is recommended to adjust the threshold to a higher value and then observe the protection effect.

* If the logs with the action as **Allow** contain attack requests (i.e., there are missed requests), it is recommended to adjust the threshold to a lower value and then observe the protection effect.


<div style="text-align: center">
</div>
