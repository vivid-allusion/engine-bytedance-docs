---
title: "Allowing backend security group"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Allowing-backend-security-group"
---

<span id="DJ2YdMIs"></span>
## Scenarios

After turning on the **Allow backend security group traffic** feature for the server group, the security group of its backend servers no longer checks the NLB traffic and allows it by default. This simplifies your NLB configuration operations.

<span id="WD0EGgAX"></span>
## Action description

Regarding the **Allow backend security group traffic** feature, the following notes apply:


* **Scope of the feature:**  This feature is supported only for server\-type server groups and not for IP\-type server groups.

* **When turning on the feature:** 

   * Existing connections (created before enabling) still follow security group rules;

   * New connections (created after enabling) do not follow security group rules.

* **When turning off the feature:** 

   * Existing connections (connections that existed before closing) continue to bypass security group rule checks.

   * New connections (connections created after closing) resume security group rule checks.

* **Additional note**: If you need to restrict IP access to backend servers through security groups, do not enable this feature.


<span id="EfBVtg54"></span>
## Turn on/off traffic allowance for backend security groups


1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the left navigation pane, select **Server group**.

3. In the top menu bar, select the target project and region.

4. Click Edit Basic information on the right side of the target server group:

   * Enable: Turn on the Allow backend security group switch, and click Confirm to complete the actions.

   * Disable: Turn off the Allow backend security group switch, and click Confirm to complete the action.
