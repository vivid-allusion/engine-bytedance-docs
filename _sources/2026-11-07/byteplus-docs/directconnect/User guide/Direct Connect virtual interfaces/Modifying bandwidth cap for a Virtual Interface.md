---
title: "Modifying bandwidth cap for a Virtual Interface"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Modifying-the-virtual-interface-bandwidth-limit"
---

<span id=".5pON5L2c6IOM5pmv"></span>
## Background

You can configure a bandwidth cap to limit rate for Direct Connect (DC) Virtual Interfaces whose bandwidth is not limited. You can also adjust the bandwidth cap of the Virtual Interface at any time as your business grows.

<span id=".5pON5L2c6K-05piO"></span>
## Instructions


* This bandwidth cap applies to the Virtual Interface’s outbound and inbound bandwidths (from a VPC to a data center and from a data center to a VPC).

* The bandwidth cap per Virtual Interface cannot exceed the [link bandwidth](https://docs.byteplus.com/en/docs/directconnect/Modify-dedicated-line-bandwidth) of its associated DC Connection.

* If the cap value is equal to the maximum bandwidth of this Virtual Interface, packet loss may occur when the actual bandwidth is greater than the set value.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [DC Virtual Interface console](https://console.byteplus.com/dc/VirtualInterface).

2. In the top menu bar, select the region where the target Virtual Interface is deployed.

3. In the Virtual Interface list, click the name of the target Virtual Interface.

4. On the details page, click **Modify** next to **Bandwidth limit**.

5. In the pop\-up dialog box, configure the bandwidth limit.

   * If the bandwidth limit is not enabled for the Virtual Interface initially, you can turn on the **Bandwidth limit** switch and then set the bandwidth limit for the Virtual Interface.

   * If the bandwidth speed limit is already enabled for the Virtual Interface initially, you modify the bandwidth limit here or turn off the **Bandwidth limit** switch to cancel rate limiting for the Virtual Interface.

6. Click **Save** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[ModifyDirectConnectVirtualInterfaceAttributes](https://docs.byteplus.com/en/docs/directconnect/ModifyDirectConnectVirtualInterfaceAttributes): Modify the name, description, bandwidth, and other configurations of a specified Virtual Interface.
