---
title: "Best practices for configuring Bot protection policies to resist malicious Bot traffic"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/Configuring_bot_protection_policies_to_block_malicious_traffic"
---

Web application firewalls support defending against and detecting malicious Bot behaviors through automation, allowing you to improve rule effectiveness by confirming the results of automatic detections without needing to configure specific Bot detection characteristics. This article describes how to configure automated Bot protection policies to resist malicious Bot traffic.

<span id="3805d55c"></span>
## Background information

Bot traffic refers to automated program traffic that accesses web sites, apps, and API interfaces on the internet through tools, scripts, crawlers, or simulators, which is typically referred to as machine traffic. \nBot traffic can be both legitimate and malicious. Legitimate traffic includes normal traffic such as search engine, statistics, and advertising programs; while malicious traffic is involved in data scraping, abusing business interfaces, exploiting promotional activities, cheating with external tools, and leveraging vulnerabilities through means like utilizing IDC data center IPs, proxies, or rapid dialing IPs, resulting in risks and impacts such as information leakage, resource consumption, or financial losses.

<span id="821bad4d"></span>
## Notes

The Bot management feature is currently only available to premium version users and above.

<span id="6b194893"></span>
## Configure automatic discovery of Bot characteristics

Once the automatic discovery feature for Bot characteristics is enabled, the WAF will automatically analyze the values of identical fields across different source IPs in the traffic to detect automated attack behaviors.

<span id="cd624a7b"></span>
### Steps:


1. Log in to [the Web Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. Select the instance region in the top menu bar.

3. In the left navigation, select **Protection Policy \> Bot Management**.

4. Enable the statistical protection rule function for the domain to be protected.

   1. Select the domain to be protected.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Confirm that the protection mode of the current domain is <strong>Protection enabled</strong>. Otherwise, change the protection mode.      </div>
      

   2. Turn on the statistical protection rule switch.

5. Click **View**.

6. Click **Edit Features**.

7. Set features.

   1. Enable extraction function.

   2. Configure the statistical time, which defaults to 15 seconds.

   3. (Optional) Set custom fields and exception fields.

8. Click **Confirm**.


<span id="6f5884b0"></span>
### What to do next

WAF will automatically discover malicious Bot traffic and list the features presented. You can determine whether the request behavior is malicious Bot traffic based on the feature description and hit IP to improve the accuracy of automatic discovery.

<span id="74dd0b97"></span>
## Configure the Bot behavior map

The Bot behavior map refers to the WAF's intelligent tracking and analysis of discovered and confirmed API access behaviors and corresponding traffic based on the domain name dimension, providing a visual queue diagram. You can set the default disposal action for the queue, which performs observation, interception, JS challenge, or human verification actions for API request behaviors in the queue.

<span id="87f77895"></span>
### Steps


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. Select the instance region in the top menu bar.

3. In the left navigation, select **Protection Policy \> Bot Management**.

4. Enable the behavior map feature for the domain pending protection.

   1. Select the domain pending protection.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Confirm that the protection mode of the current domain is <strong>Protection enabled</strong>, otherwise, you need to change the protection mode.      </div>
      

   2. Turn on the behavior map switch.

5. Set the default action for the strategy to **JS challenge**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">JS challenge refers to verifying the client's JavaScript execution capability through the JS\-SDK; if the verification passes, the request traffic is directly allowed, otherwise the request is intercepted.   </div>
   

<span id="df5d25b7"></span>
### What to do next

Determine whether it is malicious Bot traffic based on the behavior map hits or the detected abnormal rules. Support modifying execution actions and interception time; you can also analyze the specific details based on the logs of the relevant requests.
