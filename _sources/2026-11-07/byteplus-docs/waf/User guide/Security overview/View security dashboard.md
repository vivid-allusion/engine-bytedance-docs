---
title: "View security dashboard"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/docs-security-overview"
---

The Security Panorama and Overview displays the business information of the websites accessed by users, including overview information, business information, and attack information, presented through multidimensional data indicators, helping users quickly understand the security status of the website.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Requirements

You have added the website that needs to be protected to the WAF instance.

<span id=".5p-l55yL57u05bqm"></span>
## View instructions


* Domain dimension: The Security Panorama and Overview page allows you to select the domain you wish to view, including all domains and single domains that have been accessed. By default, all domain data is displayed.

* Time dimension: The Security Panorama and Overview page allows you to choose the time range you wish to view, including 1 hour, 24 hours, 7 days, 30 days, and a custom time range. By default, data from the past 24 hours is displayed.

* The chart dimension: Supports zooming in on a single chart for separately filtering domains and time ranges.


<span id=".5a6J5YWo5qaC6KeI"></span>
## Overview data


* When you filter the domain range to **all domains**, the overview module displays aggregated information for all domains.

* When you filter the domain range to **single domain**, the overview graph shows the access method, return source type, and origin information for that domain. For example, the domain shown in the image below is accessed via CNAME and has an internal return source; you can view the VPC ID and IP address.


The table below explains the parameters of the overview module.


|Parameter |Description |
|---|---|
|**Number of protected websites** |Display the number of protected websites based on the selected domain name range. Click to jump to view the list of websites added to the WAF instance. |
|**Number of protected attacks** |Display the cumulative number of requests triggering WAF rules based on the selected domain range and time range. |
|**Number of intercepted IPs** |According to the selected domain name range and time range, display the number of attack source IPs that were intercepted after triggering the WAF rules. |
|**Peak request rate (all/back\-end)**  |According to the selected domain name range and time range, display the peak request rate of data points, including both all requests and back\-end requests dimensions. |
|**Peak request count (total/origin)**  |According to the selected domain name range and time range, display the peak number of requests, including both all requests and back\-end requests dimensions. |


<span id="a5f50779"></span>
## Chart data

<span id=".5Lia5Yqh5qaC6KeI"></span>
### Business overview

The business overview displays detailed business information for the websites that the user has accessed, allowing you to refer to different charts to understand the operating status of the website within the selected time frame.


* **Request rate**: displayed as the cumulative value within the corresponding time granularity and domain range.

   * **All** refers to all requests from the client to WAF.

   * **Attacks** refer to requests that trigger WAF protection policies.

   * **Backsource** refers to requests that are allowed by the WAF to reach the origin server.

* **Request count**: displays the cumulative value based on the corresponding time granularity and domain range.

   * **All** refers to all requests from the client to the WAF.

   * **Attack** refers to requests that triggered WAF policies.

   * **Backsource** refers to requests that are allowed by the WAF to reach the origin server.

* **Response count**: refers to responses returned from the origin server to the WAF, displayed as cumulative values based on the corresponding time granularity and domain range.


<span id="02d40305"></span>
### Attack overview

The attack overview displays statistical information about attacks on the website connected by users, showing you the attacks suffered by the protected website. The attack overview is a centralized display of different types and events of attacks, helping you horizontally compare the differences between different attack events to adjust your protection strategies and provide more effective protection for the website.


* **Request trend chart**: displays the trend of the number of different requests as cumulative values based on the corresponding time granularity and domain range.

   * **All** refers to all requests from the client to the WAF.

   * **Attack** refers to requests that trigger WAF protection policies.

   * Support for viewing requests of different attack types separately, including vulnerability attacks, blocklist, CC attacks, bots, API parameter anomalies, API routing anomalies, etc.

* **QPS trend chart**: Displays the QPS trend of different requests based on the cumulative value within the corresponding time granularity and domain name range.

   * **All** refers to all requests from the client to WAF.

   * **Attack** refers to requests that trigger WAF protection policies.

   * Support for viewing requests of different attack types separately, including vulnerability attacks, blocklist, CC attacks, bots, API parameter anomalies, API routing anomalies, etc.

* **Attack type distribution**: Displays the proportion of each attack type based on the selected domain name range and time range according to the number of attacks.

* **Top 5 attack source IPs**: Displays the IP information of the top 5 attack sources based on the number of attacks, as well as the corresponding number of attacks and their proportions, according to the selected domain name range and time range.

* **Top 5 attack source User\-Agents**: Displays the User\-Agent information of the top 5 attack sources based on the number of attacks, as well as the corresponding number of attacks and their proportions, according to the selected domain name range and time range.

* **Top 5 attacked domains**: Displays the information of the top 5 attacked domains based on the number of attacks, as well as the corresponding number of attacks and their proportions, according to the selected domain name range and time range.

* **Top 5 attack source areas**: Displays the top 5 attack source areas according to the selected domain range and time range, sorted by the number of attacks. Supports viewing the distribution separately for the global or mainland China.


<span id=".6K6_6Zeu566h5o6n"></span>
### Access Control


* **Request Trend Chart**: Displays the distribution of requests triggering access control policies within the corresponding time granularity and domain range based on cumulative values. Supports switching between request count trend and QPS trend.

   * **All** refers to all requests from the client to the WAF.

   * **Attack** refers to requests that trigger the WAF access control policy.

   * **Observe** refers to requests that execute the “observe” action after triggering the access control policy.

   * **Intercept** refers to requests that execute the “intercept” action after triggering the access control policy.

* **Attack Type Distribution**: Displays the proportion of various attack types that trigger access control policies according to the selected domain range and time range, including blocklist and geographical restrictions, based on the number of attack requests.

* **Top 5 attack sources**: Based on the selected domain range and time range, it shows the top 5 sources with the highest number of triggered access control policies, including attack source IP, matched rules, attack count, and attack proportion.

   * The matched rules display the top 3 rule IDs that have triggered the most.

   * Clicking on the corresponding IP will take you to the log management page to view the log information for that IP.

   * Clicking on the corresponding matched rule ID will take you to the rules list to view or modify the rule details.

* **Top 5 attacked domains**: Based on the selected domain range and time range, it shows the top 5 attacked domains with the highest number of triggered access control policies, along with the corresponding attack counts and proportions.

* **Top 5 attack source regions**: Based on the selected domain range and time range, it shows the top 5 attack source regions with the highest number of triggered access control policies. Supports viewing the distribution situation of either globally or within mainland China.


<span id=".Q0PpmLLmiqQ="></span>
### Rate limiting


* **Request trend chart**: Shows the distribution of requests triggering the Rate limiting policy based on cumulative values within the corresponding time granularity and domain range. Supports switching to view the trend of request counts and QPS trends.

   * **All** refers to all requests from the client to the WAF.

   * **Attack** refers to requests that trigger WAF access control policies.

   * **Observation** refers to requests that execute the "observe" action after triggering access control policies.

   * **Interception** refers to requests that execute the "intercept" action after triggering access control policies.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The request count corresponding to the <strong>intercept</strong> action includes scenarios of custom interception, rate limiting interception, and verification failure interception.   </div>
   

* **Distribution of disposal actions**: Based on the selected domain range and time range, it shows the proportion of various disposal actions that trigger the Rate limiting policies by the number of triggers, including alerts, rate limiting, verification, and custom interception.

* **Top 5 attack sources**: Based on the selected domain range and time range, it displays the top 5 attack source information with the most triggers of the Rate limiting policies, hit rules (showing the top 3 by the number of triggers), number of attacks, and attack proportion.

   * Supports viewing lists counted by different attack sources, including IP, custom Header, custom Cookie, and custom parameters.

   * Hit rules display the top 3 rule IDs that triggered the most rules.

   * Clicking on the corresponding IP will take you to the log management page to view the log information of that IP.

   * Click on the corresponding matched rule ID to go to the rule list to view or modify the rule details.

* **Top 5 attacked domains**: Display the top 5 attacked domains that triggered the Rate limiting策略 the most times based on the selected domain range and time range, as well as the corresponding attack counts and proportions.

* **Top 5 attack source areas**: Display the top 5 attack source areas that triggered the Rate limiting策略 the most times based on the selected domain range and time range, as well as the corresponding attack counts and proportions. Supports viewing the distribution situation for both globally and within mainland China.

* **Top 5 triggered rules**: Display the top 5 custom Rate limiting rules that triggered the Rate limiting策略 the most times based on the selected domain range and time range, as well as the corresponding attack counts and proportions.


<span id=".5ryP5rSe6Ziy5oqk"></span>
### Vulnerability protection


* **Request trend chart**: Display the distribution of requests that triggered the vulnerability protection策略 based on the cumulative value within the corresponding time granularity and domain range. Supports switching to view the trend of request counts and QPS trends.

   * **All** refers to all requests from the client to the WAF.

   * **Attacks** refer to requests that triggered the WAF access control策略.

   * **Observation** refers to requests that execute the "observe" action after triggering access control policies.

   * **Interception** refers to requests that execute the "intercept" action after triggering access control policies.

* **Attack type distribution**: displays the proportion of each attack type triggering vulnerability protection policies based on the selected domain and time range according to the number of attack requests.

* **Top 5 attack sources**: displays the top 5 sources that triggered the vulnerability protection policies most frequently, including attack source IP, matched rules (displaying the top 3 by trigger count), number of attacks, and attack proportion based on the selected domain and time range.

   * Matched rules display the top 3 rule IDs that have been triggered most frequently.

   * Clicking the corresponding IP will take you to the log management page to view the log information for that IP.

   * Clicking the corresponding matched rule ID will take you to the rule list to view or modify the rule details.

* **Top 5 attacked domains**: displays the top 5 attacked domains that triggered the vulnerability protection policies most frequently, along with the corresponding number of attacks and proportions based on the selected domain and time range.

* **Top 5 attack source regions**: displays the top 5 attack source regions that triggered vulnerability protection policies most frequently based on the selected domain and time range. Supports viewing distribution separately for global or mainland China.


<span id=".QVBJ6Ziy5oqk"></span>
### API protection


* **Request trend chart**: Displays the distribution of requests that triggered the API protection policy based on the cumulative values within the corresponding time granularity and domain range. Supports switching between viewing request count trends and QPS trends.

   * **All** refers to all requests from the client to WAF.

   * **Attack** refers to requests that triggered the WAF access control policy.

   * **Observation** refers to requests that executed the "observe" action after triggering the access control policy.

   * **Interception** refers to requests that executed the "intercept" action after triggering the access control policy.

* **Attack type distribution**: Displays the proportion of each attack type that triggered the API protection policy based on the selected domain range and time range, categorized by the number of attack requests.

* **Top 5 attack sources**: Displays the top 5 sources that triggered the API protection policy the most based on the selected domain range and time range, including attack source IP, hit rules (top 3 displayed by the number of triggers), attack count, and attack proportion.

   * The hit rules display the top 3 rules that were triggered the most. Attacks triggered by custom API protection rules will display the rule ID. API access without custom protection rules will perform routing checks, and abnormal access will be displayed as "Routing Exception."

   * Clicking on the corresponding IP will take you to the log management page to view the log information for that IP.

   * Clicking on the corresponding matched rule ID will take you to the rule list to view or modify rule details.

* **Top 5 attacked domains**: Based on the selected domain range and time range, it displays the top 5 attacked domains that triggered the API protection policy the most, along with the corresponding attack counts and proportions.

* **Top 5 attack source regions**: Based on the selected domain range and time range, it displays the top 5 attack source regions that triggered the vulnerability protection policy the most. Supports viewing the distribution situation globally or specifically for mainland China.

* **Attack requests**: Based on the selected domain range and time range, it displays a list of access control related attack events, including the attacked domain, attack IP, attack path, risk level, attack type, execution action, and attack time.

   * Supports searching by attack path or attack IP.

   * Supports filtering by attacked domain, risk level, and execution action.

   * Click **details** to view attack event log information.


<span id=".Qm906Ziy5oqk"></span>
### Bot protection


* **Request trend chart**: displays the distribution of requests triggering Bot protection strategies within the cumulative values of the corresponding time granularity and domain range. Supports switching between request count trends and QPS trends.

   * **All** refers to all requests from the client to the WAF.

   * **Attacks** refer to requests triggering the WAF access control strategy.

   * **Observations** refer to requests that execute the "observe" action after triggering the access control strategy.

   * **Interceptions** refer to requests that execute the "intercept" action after triggering the access control strategy.

* **Attack type distribution**: shows the proportion of each attack type that triggered Bot protection strategies according to the selected domain range and time range, based on the number of attack requests.

* **Top 5 attack sources**: displays the top 5 sources with the most occurrences of requests triggering Bot protection strategies according to the selected domain range and time range, including attack source IP, hit rules, number of attacks, and attack ratio.

   * Display the top 3 rules that triggered the hit rule. Display rule ID for custom Bot protection rules, and Bot name for built\-in Bot rules.

   * Click on the corresponding IP to go to the log management page to view the log information for that IP.

   * Click on the corresponding rule ID to go to the rule list to view or modify the rule details.

* **Top 5 attacked domains**: Display the top 5 attacked domains based on the selected domain range and time range, along with the number of attacks and proportion.

* **Top 5 attack source areas**: Display the top 5 attack source areas based on the selected domain range and time range. Support viewing the distribution separately for global or mainland China.

* **Attack requests**: Display a list of attack events related to access control according to the selected domain range and time range, including attacked domains, attack IPs, attack paths, risk levels, attack types, executed actions, hit rules, and attack times.

   * Support searching by attack path or attack IP.

   * Support filtering by attacked domain, risk level, and executed action.

   * Click **Details** to view the attack event log information.
