---
title: "View Health Check Task Sets and Tasks"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/_q5mIh"
---

This document describes how to view the health check task set of a GTM instance in BytePlus GTM.

<span id="how-byteplus-gtm-manages-health-checks"></span>
## How BytePlus GTM manages health checks

In BytePlus GTM, you can configure health check parameters for policies or rules:


* The health check parameters you configure in a policy apply to all rules under that policy.

* The health check parameters you configure in a rule only apply to the current rule. A rule can inherit the health check parameters configured in the policy or use custom health check parameters configured in the rule.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Under the intelligent routing policy, BytePlus GTM automatically generates a rule named <strong>System\-generated rule</strong>. You cannot change the health check parameters of the automatically generated rule. The automatically generated rule inherits the health check parameters of the policy and automatically selects appropriate health check probes based on the geographical location/ISP of the addresses in the traffic targets.   </div>
   

BytePlus GTM performs health checks on the addresses in the rules according to the health check parameters actually used by the rules.

<span id="health-check-parameters"></span>
### Health check parameters

Health check parameters include **Interval**, **Protocol**, **Advanced configuration**, and **Health check probes**. Health check probes are nodes distributed across various regions worldwide. These probes simulate real users sending requests to the address to perform health checks. Generally, the IP addresses of health check probes are in the same geographical location or belong to the same ISP as the IP addresses of users accessing the address.

<span id="health-check-tasks-and-health-check-task-sets"></span>
### Health check tasks and health check task sets

Health checks on addresses are implemented through one or more health check tasks. BytePlus GTM creates health check tasks based on the health check parameters of the rules and the addresses under the rules. Each health check task corresponds to one health check probe, one address, and a set of health check parameters.


* BytePlus GTM assigns a health check probe to each health check task from the **Health check probes** in the health check parameters actually used by the rule.

* BytePlus GTM assigns addresses to health check tasks based on the addresses in the rule.

* The health check probes perform health checks on the addresses according to the health check parameters.


After a health check task starts running, the health check probe periodically performs health checks on the address according to the configurations such as **Interval**, **Protocol**, **Advanced configuration** in the health check parameters of the rule.

BytePlus GTM automatically groups health check tasks with the same address and health check parameters into the same **Health check task set**. Within a health check task set, different health check tasks are assigned to different health check probes. You can view the health check results of an address based on multiple health check probes in a health check task set.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If multiple health check tasks have the same <strong>Interval</strong>, <strong>Protocol</strong>, <strong>Advanced configuration</strong>, and <strong>Health check probes</strong> in their health check parameters, then these health check tasks are considered to have the same health check parameters.</div>


<div data-tips="true" data-tips-type="tip">The <strong>Health check probes</strong> in the health check parameters of different health check tasks are considered the same if any of the following conditions are met:</div>



* <div data-tips="true" data-tips-type="tip">The <strong>Health check probes</strong> all inherit the policy\-level health check configuration.</div>


* <div data-tips="true" data-tips-type="tip">The <strong>Health check probes</strong> all use the <strong>Recommended</strong> method in rules with the same line.</div>


* <div data-tips="true" data-tips-type="tip">The <strong>Health check probes</strong> all use custom configuration, and the custom health check probes are exactly the same.</div>



BytePlus GTM assigns a task set ID to each health check task set. This ID is unique within the same BytePlus account.

<span id="how-byteplus-gtm-creates-health-check-tasks-and-groups-them-into-health-check-task-sets"></span>
### How BytePlus GTM creates health check tasks and groups them into health check task sets

BytePlus GTM performs health checks on addresses periodically through one or more health check probes. Based on the health check results, the address will be determined as available or unavailable.

For example, in a GTM instance with 3 rules: Rule A, Rule B, and Rule C:


* Rule A includes addresses `1.1.1.1` and `2.2.2.2`; Rule B includes addresses `2.2.2.2` and `3.3.3.3`; Rule C includes addresses `3.3.3.3` and `1.1.1.1`;

* Rule A and Rule B have different health check parameters: Rule A's **Interval** in the health check parameters is 15s; Rule B's **Interval** in the health check parameters is 60s.

* Rule B and Rule C have the same health check parameters.

* Rule A, Rule B, and Rule C each have only one health check probe: Probe A, Probe B, and Probe C, respectively.


Therefore, BytePlus GTM will create the following health check task sets and health check tasks:


|Health check task set |Health check task |Address |Health check parameters |Health check probe |
|---|---|---|---|---|
|Task Set 1 |Task 1 |`1.1.1.1` |Health check parameters from Rule A |Probe A |
|Task Set 2 |Task 2 |`2.2.2.2` |Health check parameters from Rule A |Probe A |
|Task Set 3 |Task 3 |`2.2.2.2` |Health check parameters from Rule B |Probe B |
|Task Set 4 |Task 4 |`3.3.3.3` |Health check parameters from Rule B |Probe B |
|Task Set 4 |Task 5 |`3.3.3.3` |Health check parameters from Rule C |Probe C |
|Task Set 5 |Task 6 |`1.1.1.1` |Health check parameters from Rule C |Probe C |


Since Task 4 and Task 5 have the same address and health check parameters, they will be grouped into the same health check task set.

<span id="how-byteplus-gtm-determines-if-an-address-is-unavailable"></span>
### How BytePlus GTM determines if an address is unavailable

BytePlus GTM determines whether an address is unavailable based on the number of consecutive health check failures for that address. You can set the threshold for the number of consecutive health check failures for a single address to be considered unavailable in the **Advanced configuration \> Address unavailability threshold** section of the health check parameters. For example, if you set this parameter to 3, an address will be considered unavailable if it fails 3 consecutive health checks.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In a health check task, the health check probe sends health check requests to the address periodically according to the <strong>Interval</strong>. Within a health check cycle, if more than 50% of the health check probes return abnormal results, this health check is considered a failure.</div>


An address may correspond to multiple health check tasks. Health check probes for different health check tasks may belong to different lines. As long as an address is unhealthy in any line's health check result, the status of that address will be determined as unavailable.

<span id="view-health-check-task-sets"></span>
## View health check task sets

<span id="view-health-check-task-sets-under-your-byteplus-account"></span>
### View health check task sets under your BytePlus account

Follow these steps to view the health check task sets under your BytePlus account.


1. Open the [Health check](https://console.byteplus.com/dns-suite/gtm/health) page of BytePlus GTM.

2. On the **Health check** page, you can view all health check task sets under your account, as well as information such as the GTM instance to which the health check task set belongs, the task set status, etc.

   * If you need to view the detailed information of a health check task set, refer to [View detailed information of a health check task set](https://docs.byteplus.com/en/docs/36/20753#detailed).

   * If you need to view data analysis for one or more health check task sets, refer to [View data analysis for one or more health check task sets](https://docs.byteplus.com/en/docs/36/20753#analysis).


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_ed0140b52f183943adf4eabfdfb020f2.png) </span>

<span id="view-health-check-task-sets-under-a-gtm-instance"></span>
### View health check task sets under a GTM instance

Follow these steps to view the health check task sets of your GTM instance.


1. On the [Instance Management](https://console.byteplus.com/dns-suite/gtm/instances) page of BytePlus GTM, find your GTM instance. Click the domain name in the **Domain name** column.

2. Select the **Health check tasks** tab. You can view the current health check task sets and their running status on the **Task list** tab.

   * If you need to view the detailed information of a health check task set, refer to [View detailed information of a health check task set](https://docs.byteplus.com/en/docs/36/20753#detailed).

   * If you need to view data analysis for one or more health check task sets, refer to [View data analysis for one or more health check task sets](https://docs.byteplus.com/en/docs/36/20753#analysis).


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_0e0b7c1e5f6c7b4c9734e79c84d74aa7.png) </span>

&nbsp;

<span id="view-detailed-information-of-a-health-check-task-set"></span>
### View detailed information of a health check task set

If you need to view the detailed information of a specific health check task set, you can click the task set ID in the **Task set ID** column when viewing health check task sets.

The detailed information of a task set includes:


* **Basic information**: Basic information of the health check task set, including task set ID, status, health check parameters, and number of nodes (i.e., number of health check probes).

* **Statistics**: Includes statistics for the following metrics:

   * Health Check Status: The health status of the address.

   * Average Latency: The average of all health check latencies in the task set within the specified time granularity range. For different health check protocols, the definition of health check latency is as follows:

      * Ping: The time from when the health check probe sends an ICMP request to when it receives a complete ICMP response.

      * TCP: The time from when the health check probe starts TCP connection establishment to when it receives a complete TCP response.

      * HTTP/HTTPS: The time from when the health check probe sends an HTTP/HTTPS request to when it receives a complete HTTP/HTTPS response.

   * Average Availability: The proportion of time the address is in a healthy state within the specified time granularity range.

* **Details**: Detailed data for each health check, including:

   * Probe IP: The IP address of the health check probe.

   * Health check time: The time when the health check was initiated.

   * Country/Region/Province, City, ISP: Line information of the health check probe.

   * Detailed data of health check results: For example, for Ping type health checks, the detailed data of health check results includes packet loss rate, Ping latency, and the detailed Ping command used for the health check.


&nbsp;

<span id="view-data-analysis-for-one-or-more-health-check-task-sets"></span>
### View data analysis for one or more health check task sets

If you need to view data analysis for one or more health check task sets, you can click **Analyze** in the **Actions** column when viewing health check task sets.

On the **Analytics** page, you can select one or more addresses in the **Address list**, and then view the data analysis of the health check task sets corresponding to your selected addresses. You can view analysis data for the following metrics:


* Average latency: The average of all health check latencies in the task sets corresponding to your selected address(es) within the specified time granularity range. For different health check protocols, the definition of health check latency is as follows:

   * Ping: The time from when the health check probe sends an ICMP request to when it receives a response from the address.

   * TCP: The time from when the health check probe starts TCP connection establishment to when it receives a response from the address.

   * HTTP/HTTPS: The time from when the health check probe sends an HTTP/HTTPS request to when it receives a complete HTTP/HTTPS response.

* Average availability rate: The proportion of time the address is in a healthy state within the specified time granularity range.


<span id="frequently-asked-questions"></span>
## Frequently asked questions

<span id="in-what-situations-can-health-check-task-sets-be-reused"></span>
### In what situations can health check task sets be reused?

The same health check task set can be reused in the following situations:


* Reuse between different rules within a GTM instance. A GTM instance can contain multiple rules. Health check task sets can be reused among multiple rules under a GTM instance. These rules have the same health check parameters and addresses.

* Reuse between different GTM instances under the same BytePlus account. A BytePlus account can contain multiple GTM instances. Health check task sets can be reused among multiple rules under different GTM instances. These rules have the same health check parameters and addresses.


<span id="how-are-tasks-in-health-check-task-sets-that-belong-to-multiple-gtm-instances-simultaneously-billed"></span>
### How are tasks in health check task sets that belong to multiple GTM instances simultaneously billed?

The number of health check tasks corresponding to a BytePlus account equals the sum of the number of health check tasks corresponding to all GTM instances under that BytePlus account. The billing generated by the number of tasks contained in health check task sets that belong to multiple GTM instances simultaneously will be randomly added to any one of the GTM instances under that BytePlus account.

Therefore, if your BytePlus account has health check task sets that belong to multiple GTM instances simultaneously, you can understand which GTM instance the billing generated by the number of tasks contained in that task set has been added to by checking the overall cost of the BytePlus account.

<span id="how-does-byteplus-gtm-calculate-the-number-of-health-check-tasks"></span>
### How does BytePlus GTM calculate the number of health check tasks?

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">BytePlus GTM bills based on the number of health check tasks. Refer to <a href="https://docs.byteplus.com/docs/byteplus-dns-suite/R4Anoj">Billing</a>.</div>


In a health check task set, each health check probe (node) corresponds to one health check task. For example, if a health check task set contains 3 health check probes (nodes), then this health check task set contains 3 health check tasks.

The number of health check tasks corresponding to a GTM instance equals the sum of the number of health check tasks corresponding to all rules under that GTM instance. For example, if a GTM instance contains two health check task sets, one health check task set contains 3 health check tasks, and the other health check task set contains 6 health check tasks, then this GTM instance contains a total of 9 health check tasks.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the GTM instance's policy is an intelligent routing policy, then the name of the rule automatically generated by the system to which the health check task set belongs is <strong>System\-generated rule</strong>.</div>


<span id="if-health-checks-for-a-policy-or-rule-are-turned-off-and-you-later-turn-them-back-on-will-the-historical-status-in-the-relevant-health-check-tasks-be-preserved"></span>
### If health checks for a policy or rule are turned off and you later turn them back on, will the historical status in the relevant health check tasks be preserved?

If health checks for a policy or rule are turned off, the historical status of the relevant health check tasks will not be preserved. For example, before turning off health checks, a policy had a related health check task. In the health check parameters of this health check task, the value of **Address unavailability threshold** was 3, indicating that the threshold for the number of health check failures for a single address to be determined as unavailable was 3.

If you turn off health checks for the policy or rule when an address has failed two consecutive health checks, BytePlus GTM will not save the status of this address being determined as unavailable for two consecutive times after you later turn on health checks for the policy or rule. After health checks are restarted, BytePlus GTM will re\-determine address faults. The address will only be determined as unavailable when it fails three consecutive health checks afterwards.
