---
title: "Adding to a Bandwidth Package"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Adding-an-EIP-to-a-Bandwidth-Package"
---

This topic describes how to add an Elastic IP Address (EIP) to a Bandwidth Package.

<span id=".57qm5p2f6ZmQ5Yi2"></span>
## Limits

To add an EIP to a Bandwidth Package, the following conditions must be met:


* Both are in the same region.

* Both have the same ISP.

* Both have the same security protection type.

* The EIP uses pay\-as\-you\-go billing.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [EIP console](https://console.byteplus.com/eip/eips).

2. In the top menu bar, select the region and project of your target EIP.

3. In the EIP list, click  **··· \> Add EIP to BWP** to the right of the target EIP.

4. Select the target Bandwidth Package instance, click **Add** to complete the action.


<span id=".5pON5L2c57uT5p6c"></span>
## Result


* Adding to a Bandwidth Package does not affect the service of the EIP. The EIP's original maximum bandwidth becomes invalid and shares the bandwidth of the Bandwidth Package.

* The EIP's billing items for bandwidth fee and traffic fee become invalid. Only the IP config fee remains valid. For more billing item details, see [Pay-as-you-go](https://docs.byteplus.com/en/docs/eip/Pay-as-you-go).

* In the EIP list, you can view the Bandwidth Package added to the EIP and the maximum bandwidth of the Bandwidth Package.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[AddBandwidthPackageIp](https://docs.byteplus.com/en/docs/bandwidthpackage/AddBandwidthPackageIp): Add an EIP to a Bandwidth Package.
