---
title: "Adding or removing an EIP to or from the Bandwidth Package"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/CLB-instances-08"
---

Elastic IP (EIP) and IPv6 Internet bandwidth can be associated with a Shared Bandwidth Package, sharing the bandwidth of the Shared Bandwidth Package, which helps reduce internet costs.

This topic describes how to add or remove the EIP or IPv6 Internet bandwidth of a CLB instance from a Shared Bandwidth Package.

<span id=".5Yqg5YWl5YWx5Lqr5bim5a695YyF"></span>
## Bandwidth package

After the EIP or IPv6 Internet bandwidth is associated with a Shared Bandwidth Package, they will share the bandwidth of the Shared Bandwidth Package. During peak business periods, multiple EIP or IPv6 Internet bandwidths might compete for bandwidth. Therefore, before associating the EIP or IPv6 Internet bandwidth of a CLB instance with a Shared Bandwidth Package, please first [view cloud monitor](https://docs.byteplus.com/en/docs/bandwidthpackage/Viewing-monitoring-data) to carefully evaluate the usage of the Shared Bandwidth Package. Adjust the bandwidth of the Shared Bandwidth Package as needed to avoid business disruptions caused by bandwidth competition.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites


* To associate the EIP of a CLB instance with a Shared Bandwidth Package, the following conditions must be met:

   * The EIP and bandwidth package are in the same Region.

   * The EIP and bandwidth package use the same protection mode.

   * The billing type of the EIPs is Post Paid.

   * The ISP Type of both must be the same.

* To add the IPv6 internet bandwidth of the CLB instance to the Shared Bandwidth Package, the following conditions must be met simultaneously:

   * The protocol of the Shared Bandwidth Package is dual\-stack (IPv4&IPv6).

   * Both of them are in the same Region.

   * The ISP Type of both must be the same.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to[ the CLB console](https://console.byteplus.com/clb/LoadBalancer). 

2. In the top menu bar, select the target region and target project.

3. Click the  **··· \> Access to Internet \> Add to Shared Bandwidth Package** or  **··· \> Access to Internet \> Add to IPv6 Shared Bandwidth Package** button on the right side of the target CLB instance.

4. On the configuration page, select a project and a bandwidth package to which the instance will be added.

5. Click **Confirm** button to complete the actions.


<span id=".5pON5L2c57uT5p6c"></span>
### Result


* The original maximum bandwidth of EIP or IPv6 Internet bandwidth becomes invalid, sharing the bandwidth of the Shared Bandwidth Package.

* The bandwidth fee and traffic fee of billing items for EIP or IPv6 Internet bandwidth become invalid, only the IP configuration fee is effective. For more information on the billing items, refer to [Pay-as-you-go of Elastic IP](https://docs.byteplus.com/en/docs/eip/Pay-as-you-go) and [Pay-as-you-go of IPv6 Internet bandwidth](https://docs.byteplus.com/en/docs/IPv6/Pay-as-you-go).

* In the EIP or IPv6 Internet bandwidth list, you can view the Shared Bandwidth Package they are added to and the maximum bandwidth of the Shared Bandwidth Package.


<span id=".56e75Ye65YWx5Lqr5bim5a695YyF"></span>
## Removing an IPv6 Internet Bandwidth instance from the bandwidth package

After an EIP or IPv6 Internet bandwidth is removed from the Shared Bandwidth Package, it will no longer use the bandwidth of the Shared Bandwidth Package and will revert to its own maximum bandwidth. Therefore, before removing an EIP or IPv6 Internet bandwidth from the Shared Bandwidth Package, please first enter the details page of the [EIP](https://console.byteplus.com/eip/eips)  or [IPv6 Internet bandwidth](https://console.byteplus.com/eip/ipv6s)   to view whether its bandwidth meets the business operation needs of the current CLB instance. If not, please adjust the bandwidth of the EIP or IPv6 Internet bandwidth before removing it to avoid affecting business operation due to insufficient bandwidth.

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to[ the CLB console](https://console.byteplus.com/clb/LoadBalancer). 

2. In the top menu bar, select the target region and target project.

3. Click  **··· \> Access to Internet \> Remove from Shared Bandwidth Package** or  **··· \> Access to Internet \> Remove from IPv6 Shared Bandwidth Package**.

4. Click **Confirm** button to complete the actions.


<span id=".5pON5L2c57uT5p6c"></span>
### Result


* Restore the maximum bandwidth of the EIP or IPv6 Internet bandwidth.

* Restore the billing items of bandwidth and traffic fees for the EIP or IPv6 Internet bandwidth, and billing starts immediately.


<span id=".55u45YWz5paH5qGj"></span>
## Related document


* [AddBandwidthPackageIp](https://docs.byteplus.com/en/docs/bandwidthpackage/AddBandwidthPackageIp)

* [RemoveBandwidthPackageIp](https://docs.byteplus.com/en/docs/bandwidthpackage/RemoveBandwidthPackageIp)
