---
title: "Managing a Bandwidth Package"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/Manage_Shared_Bandwidth_Package"
---

<span id=".5YWx5Lqr5bim5a695YyF566A5LuL"></span>
## Bandwidth Package overview

You can add multiple IPv6 Internet bandwidths in the same region to a Bandwidth Package, sharing one Internet bandwidth for reducing costs. For more information, see [What is Bandwidth Package](https://docs.byteplus.com/en/docs/bandwidthpackage/What-is-Bandwidth-Package).

<span id=".5Yqg5YWl5YWx5Lqr5bim5a695YyF"></span>
## Add to a Bandwidth Package

<span id=".57qm5p2f6ZmQ5Yi2"></span>
### Limits


* To add an IPv6 Internet bandwidth to a Bandwidth Package, the following conditions must be met:

   * Both follow the same IP protocol.

   * Both are in the same region.

* Related management actions are not supported by the managed IPv6 Internet bandwidth service associated with BytePlus Official Service.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to [the IPv6 Gateway console](https://console.byteplus.com/eip/ipv6s).

2. In the top menu bar, select your target region.

3. Click **Manage** to the right of the target IPv6 gateway instance, entering the IPv6 Internet bandwidth tab on the details page.

4. In the IPv6 address list, click  **··· \> Add EIP to BWP** to the right of the target EIP, popping up the Add to Shared Bandwidth Package window.

5. Select your target Bandwidth Package instance, and click **Add** to complete the action.


<span id=".5pON5L2c57uT5p6c"></span>
### Results


* The IPv6 Internet bandwidth invalidates its original bandwidth cap and shares the bandwidth of Bandwidth Package.

* The IPv6 Internet bandwidth's billing items of bandwidth fee and data transfer fee become invalid. For billing item details, see [Pay-as-you-go](https://docs.byteplus.com/en/docs/IPv6/Pay-as-you-go).

* In the IPv6 Internet bandwidth list, you can view the Bandwidth Package that the IPv6 address is added to and the maximum bandwidth of the Bandwidth Package.


<span id=".56e75Ye65YWx5Lqr5bim5a695YyF"></span>
## Remove from a Bandwidth Package

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to [the IPv6 Gateway console](https://console.byteplus.com/eip/ipv6s).

2. In the top menu bar, select your target region.

3. Click **Manage** to the right of the target IPv6 gateway instance to enter the IPv6 Internet bandwidth tab on the details page.

4. In the IPv6 address list, click  **··· \> Remove from Bandwidth Package ** to the right of the target IPv6 Internet bandwidth. A dialog box appears to confirm removal.

5. After confirming the information is correct, click **Remove** to complete the action.


<span id=".5pON5L2c57uT5p6c"></span>
### Results


* The original bandwidth cap of IPv6 Internet bandwidth restores valid.

* The bandwidth and traffic fees for IPv6 Internet bandwidth are reactivated, with billing starting immediately.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [AddBandwidthPackageIp](https://docs.byteplus.com/en/docs/bandwidthpackage/AddBandwidthPackageIp): Add an IPv6 Internet bandwidth to a Bandwidth Package.

* [RemoveBandwidthPackageIp](https://docs.byteplus.com/en/docs/bandwidthpackage/RemoveBandwidthPackageIp): Remove an IPv6 Internet bandwidth from a Bandwidth Package.
