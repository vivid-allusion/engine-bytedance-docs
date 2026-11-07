---
title: "Disabling IPv6 Internet bandwidth"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/Delete_IPv6_Internet_bandwidth"
---

If an IPv6 address no longer requires connectivity with the internet, you can disable IPv6 Internet bandwidth by this action.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The IPv6 Internet bandwidth is not added to any Bandwidth Package. If added, [remove it from the Bandwidth Package](https://docs.byteplus.com/en/docs/IPv6/Manage_Shared_Bandwidth_Package#.56e75Ye65YWx5Lqr5bim5a695YyF) first.

<span id=".5pON5L2c6K-05piO"></span>
## Instructions


* You cannot manually disable IPv6 Internet bandwidth for public dual\-stack Application Load Balancer (ALB) instances. When you [delete a public dual-stack ALB instance](https://docs.byteplus.com/en/docs/clb/Managing-instances), the system automatically disables its IPv6 Internet bandwidth.

* You cannot disable the managed IPv6 Internet bandwidth service associated with BytePlus Official Service.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the IPv6 Gateway console](https://console.byteplus.com/eip/ipv6s).

2. In the top menu bar, select your target region.

3. Click **Manage** to the right of the target IPv6 gateway instance, entering the IPv6 Internet bandwidth tab on the details page.

4. In the IPv6 Internet bandwidth list, click **Disable Internet bandwidth** to the right of the target IPv6 address. A dialog box appears to confirm disabling.

5. After confirming the information is correct, click **Disable** to complete the action.

   > Support selecting multiple IPv6 addresses with the network type of **Internet** to batch disable IPv6 Internet bandwidth.   
   

<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[ReleaseIpv6AddressBandwidth](https://docs.byteplus.com/en/docs/IPv6/ReleaseIpv6AddressBandwidth): Disable the specified IPv6 Internet bandwidth.
