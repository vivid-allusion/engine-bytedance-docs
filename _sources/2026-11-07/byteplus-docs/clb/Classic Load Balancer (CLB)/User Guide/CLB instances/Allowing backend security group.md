---
title: "Allowing backend security group"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Allowing-backend-security-group"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

After the Classic Load Balancer (CLB) instance Enables Allow backend security group feature, the security group of its backend server no longer verifies the traffic of the CLB, allowing by default, which simplifies the configuration actions of the CLB for you.

<span id=".5pON5L2c6K-05piO"></span>
## Action description


* Enable Allow Backend Security Group feature:

   * This only applies to backend servers within server\-type backend server groups; backend servers in IP\-type backend server groups still require [security group configuration](https://docs.byteplus.com/en/docs/clb/Configuring-a-server-security-group).

   * If the subnet where its backend server is located is configured with Network Access Control List, the traffic from CLB to backend servers is still restricted by the Network Access Control List.

   * If you want to restrict IP access to backend server services, use [Access Control Lists overview](https://docs.byteplus.com/en/docs/clb/Access-control-list-01) for control.

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Enable Allow backend security group feature, effective only for new connections, previously established connections will still go through backend security group rule validation.   </div>
   

* Disable the Allow backend security group feature, existing connections will still bypass the security group rule verification and only apply to new connections. New connections will go through backend security group rule verification.


<span id=".5byA5ZCvL-WFs-mXreaUvumAmuWQjuerr-WuieWFqOe7hA=="></span>
## Toggle Allow Backend Security Group Traffic


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click the name of the target CLB instance.

4. On the CLB Overview tab:

   * Enable: Turn on the Allow backend security group switch, and click Confirm to complete the actions.

   * Disable: Turn off the Allow backend security group switch, and click Confirm to complete the actions.
