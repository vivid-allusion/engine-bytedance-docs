---
title: "Creating an Egress Only rule"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/Create_only_active_outgoing_rules"
---

After enabling IPv6 internet bandwidth for the IPv6 address of your Elastic Compute Service (ECS) or secondary network interface: If you don't want the IPv6 address to be accessed by IPv6 internet terminals, create an Egress Only rule. This rule blocks access from IPv6 internet terminals to your ECS or secondary network interface.

&nbsp;

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After an Egress Only rule is created, traffic from Internet IPv6 terminals accessing your ECS or network interface's IPv6 address is immediately interrupted. Proceed with caution.</div>


* <div data-tips="true" data-tips-type="tip">Managed IPv6 addresses associated with BytePlus Official Service do not support creating Egress Only rules.</div>



<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An IPv6 address with IPv6 Internet bandwidth enabled is allocated to an ECS instance or a secondary network interface.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [IPv6 Gateway console](https://console.byteplus.com/eip/ipv6s).

2. In the top menu bar, select your target region.

3. In the IPv6 Gateway instances list, click the name of target instance to go to the details page.

4. In the Egress Only rule tab, click **Create Egress Only rule**.

5. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Name |Type the name for the Egress Only rule. |OnlyOutRule\-1 |
   |Regular granularity |Select the granularity for the Egress Only rule. Supports selecting ECS and secondary network interface. |Elastic Compute Service |
   |Specified instance |Select your target instance to create the Egress Only rule. |ECS\-1 |
   

6. Click **OK** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[CreateIpv6EgressOnlyRule](https://docs.byteplus.com/en/docs/IPv6/CreateIpv6EgressOnlyRule): Create an Egress Only rule for a specified ECS instance.
