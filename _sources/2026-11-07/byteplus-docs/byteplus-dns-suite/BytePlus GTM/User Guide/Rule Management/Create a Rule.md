---
title: "Create a Rule"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/snlUdP"
---

This document introduces how to create a rule for a GTM instance in BytePlus GTM. You can configure the following failover settings in the rule:


* Create and configure a pool set

* Configure health check tasks


If the currently enabled policy is intelligent routing, BytePlus GTM automatically generates rules based on the traffic targets you add after the GTM instance is started. Therefore, if you do not need to customize rules, you can skip creating rules and directly start the GTM instance. If you need to customize rules, you can also create them under the intelligent policy. The rules you create have a higher priority than the system\-generated ones.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can create both IP and domain type addresses in one rule. However, in the same GTM instance, other rules will not be able to use the line configured by this rule.</div>


<span id="prerequisites"></span>
## Prerequisites

Before creating a rule, you must configure a GTM instance. See [Configure a GTM Instance](https://docs.byteplus.com/docs/byteplus-dns-suite/0_OA55).

<span id="steps"></span>
## Steps

Complete the following steps to create a rule.


1. On the [Instance management page](https://console.byteplus.com/dns-suite/gtm/instances), find your GTM instance. Click the domain name in the **Domain** column.

2. On the **Policy management** tab, click the **Configure** button for the policy you are currently setting up.

3. In the **Custom rules** tab, click **Add rule**.

4. On the **Create rule** page, in the **Basic information** tab, configure the basic information of the rule.

   **Basic information**

   
   |Parameter |Description |
   |---|---|
   |**Name** |The name of the rule. |
   |**Line** |The line used by the rule. The default line covers all lines. You need to configure at least one rule for the default line. Otherwise, users may receive a NXDOMAIN response. See [DNS Routing Policies](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-intelligent-dns-based-routing) to learn how to configure lines. |
   |**Weight** |The weight of the rule. You need to enable load balancing when [configuring a GTM instance](https://docs.byteplus.com/docs/byteplus-dns-suite/0_OA55). Otherwise, this parameter is invalid. Weight is a positive integer, and its value range can be found in [Editions](https://docs.byteplus.com/docs/byteplus-dns-suite/8cqTK1). |
   |**Enabled** |Whether the rule is enabled.<br><br><br>* **Enable**: The rule is enabled.<br><br>* **Disable**: The rule is disabled. |
   |**Pool set activation mode** |The activation mode of the pool set. Only one pool set can be activated within the same rule.<br><br><br>* **Automatic** (default): BytePlus GTM automatically sets the active pool set. The pool set with the highest priority that is available automatically becomes active. If all pool sets are unavailable, the one with the highest priority becomes active.<br><br>* **Manual**: BytePlus GTM ignores the priority and availability of the pool sets and you manually set the active pool set. If you set the **Pool set activation mode** to **Manual**, a **Set to active** button appears in the **Pool set** section. You can click this button to set a pool set to active. |
   

   **Pool set**

   
   |Parameter |Description |
   |---|---|
   |**Pool set availability threshold** |The minimum number of available addresses for a pool set to be considered available. For example, if you set this parameter to 1 and there is 1 or more available address, then the pool set is available. Otherwise, it is unavailable. The default value is 1. When health checks are not enabled, all pool sets are considered available by default. |
   |**Address type** |* **IPv4**: Pools in this pool set use IPv4 addresses.<br><br>* **IPv6**: Pools in this pool set use IPv6 addresses.<br><br>* **Domain**: Pools in this pool set use domain names. |
   |**Pool** |The pools included in the pool set. You need to add pools to the GTM instance. |
   |**Weight** |The weight of each pool. Only the ultimate edition supports this parameter. Weight is a positive integer, and its value range can be found in [Editions](https://docs.byteplus.com/docs/byteplus-dns-suite/8cqTK1). |
   |**Priority** |You can adjust the priority of the pool set by clicking the arrow buttons. The smaller the number, the higher the priority. |
   

   After completing the configuration, click **OK**.

5. On the **Add rule** page, select the **Health check** tab and configure the health check for the rule.

   
   |Parameter |Description |
   |---|---|
   |Enabled |Whether to enable health checks in this rule.<br><br><br>* **Enabled**: Health checks are enabled.<br><br>* **Disabled**: Health checks are disabled. |
   

   **Health check parameters**

   The health check parameters in this rule. If you select **Inherit instance configuration**, the health check parameters will inherit the settings you configured during configuring a GTM instance or updating a GTM instance.

   **Health check probe**

   The health check probes in this rule. If you select **Inherit instance configuration**, the health check parameters will inherit the settings you configured during configuring a GTM instance or updating a GTM instance.


After completing the configuration, click **OK**. You can see the added rule in the **rules** tab.

<span id="follow-up-steps"></span>
## Follow\-up steps

After creating a rule, you may:


* [Start the GTM instance](https://docs.byteplus.com/docs/byteplus-dns-suite/U5nvpy)

* [Update the rule](https://docs.byteplus.com/docs/byteplus-dns-suite/T849Eo)

* [Delete the rule](https://docs.byteplus.com/docs/byteplus-dns-suite/i1Y6S8)
