---
title: "Enabling or disabling health check convergence routing for a VPN attachment"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Enabling-or-disabling-health-check-convergence-routing-for-a-VPN-attachment"
---

<span id="hiOQohiC"></span>
## Scenarios

Health Check Convergence Routing supports updating the effective status of static routes in the TR route table automatically based on the health check status of IPsec\-VPN connections, delivering higher business reliability and stability.


* When multiple source/destination IP pairs are configured for health checks on an IPsec\-VPN connection, the **failure** of any single pair will cause the system to deactivate all routes in the TR route table that use this VPN attachment as their next hop. The status of these routes becomes **Not effective**.

* When multiple source/destination IP pairs are configured for health checks on an IPsec\-VPN connection, the system will reactivate all affected routes in the TR route table. This only happens when the health checks for all pairs **succeed**. The status of these routes becomes **Available**.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The health check convergence routing feature is in the beta stage. If you need a trial, please contact your account manager.</div>


<span id="N1C51z64"></span>
## Limits


* The health check convergence routing feature only takes effect when health check is enabled on the IPsec\-VPN connection. If health check is disabled on the IPsec\-VPN connection, the health check convergence routing feature will not automatically converge routes, even if enabled.

* The health check convergence routing feature only supports converging static routes with next hops as VPN attachments. It does not support converging BGP routes.


<span id="8eUo0MeF"></span>
## Procedure


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the area under **Basic information**, select the ** Intra\-region attachments** tab.

4. Click the name of the target VPN attachment to enable or disable the health check convergence routing feature.
