---
title: "Cloning an ALB instance"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Cloning_an_ALB_instance"
---

Cloning an instance creates a new ALB instance whose attributes, listeners, access control policies, forwarding rules, log shipping, and custom configurations are all consistent with the original ALB instance.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Cloning ALB instance is currently in beta stage. For trial requests, please contact the account manager.</div>


<span id="di7uvmEg"></span>
## Action notes

ALB instances that meet any of the following conditions do not support cloning:


* WAF safety protection is enabled

* Anycast EIP is attached

* A multi\-zone ALB instance bound to EIPs of different ISPs

* QUIC listener has been created


<span id="IFzvDti2"></span>
### Procedures


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the target project and region.

3. In the left\-side navigation pane, select **Instance**.

4. Click  **··· \> Clone** on the right side of the target ALB instance.

5. Configure relevant parameters based on the table below.

   
   |Parameters |Notes |Example |
   |---|---|---|
   |Instance name/ID |Displays the name and ID of the ALB instance being cloned. |alb\-test/alb\-1ho9mrn587zeo67hpivgk\*\*\*\* |
   |Virtual Private Cloud (VPC) |Displays the VPC to which the cloned ALB instance belongs. The new ALB instance will also be created within this VPC. |VPC\-test |
   |New name |Enter the name of a new ALB instance. |ALB\-new |
   |Update EIP configuration |When cloning a public ALB instance, you can choose whether to update the public network configuration.<br><br>If you select Yes, see [Creating an ALB instance](https://docs.byteplus.com/en/docs/clb/Creating-an-instance) documentation to complete the **IPv4 EIP** and **IPv6 EIP configuration**. |No |
   

6. Enter the new ALB name and click **OK** to complete the operation.


<span id="S0RFQv3F"></span>
## Related documents

[CloneLoadBalancer](https://docs.byteplus.com/en/docs/clb/CloneLoadBalancer)
