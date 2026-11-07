---
title: "Switch Policies for a GTM Instance"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/YCZRHw"
---

This document describes how to switch policies for your GTM instance.

<span id="operation-steps"></span>
## Steps

Follow the steps below to switch policies for your GTM instance.


1. On the [Instance management page](https://console.byteplus.com/dns-suite/gtm/instances), find your GTM instance. Click the domain name in the **Domain** column.

2. In the **Policy management** tab, select the policy that you want to switch to. Click **OK** in the pop\-up confirmation window.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you are switching from intelligent routing to basic routing, the default weight value for the address that does not have a set weight is 1.</div>


* <div data-tips="true" data-tips-type="tip">If you are switching from basic routing to intelligent routing, the default capacity value for the address that does not have a set capacity is 1000.</div>



<span id="follow-up-steps"></span>
## Follow\-up steps


* If you are switching from intelligent routing to basic routing, you will need to configure the basic routing policy as follows:

   * Decide whether to enable load balancing.

   * Create rules. See [Create a Rule](https://docs.byteplus.com/docs/byteplus-dns-suite/snlUdP).

* If you are switching from basic routing to intelligent routing, the default routing mode is performance\-prioritized. You need to select the routing mode and configure the policy:

   * Performance: Add traffic targets. See [Set Traffic Targets for Intelligent Policy](https://docs.byteplus.com/docs/byteplus-dns-suite/c7KpPz).

   * Capacity:

      * Add traffic targets. See [Set Traffic Targets for Intelligent Policy](https://docs.byteplus.com/docs/byteplus-dns-suite/c7KpPz).

      * Set capacity for the pool or target address.
