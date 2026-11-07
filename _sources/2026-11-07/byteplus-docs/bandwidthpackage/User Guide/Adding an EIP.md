---
title: "Adding an EIP"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/Adding-an-EIP"
---

You can add multiple elastic IP addresses (EIPs) to a Bandwidth Package instance to share the same bandwidth resources. This helps reduce your Internet access costs.

This topic describes how to add EIPs to a Bandwidth Package.

> You can also refer to [Adding EIPs to a Bandwidth Package](https://docs.byteplus.com/en/docs/eip/Adding-an-EIP-to-a-Bandwidth-Package).


<span id="limits"></span>
## Limits

To add EIPs to a Bandwidth Package, the following conditions must be met:


* The EIPs and the Bandwidth Package use the same IP protocol.

* The EIPs and the Bandwidth Package belong to the same region.

* The billing type of the EIPs or IPv6 Internet Tunnel Bandwidth is Post Paid.


<span id="procedure"></span>
## Procedure


1. Log on to the [Bandwidth Package console](https://console.byteplus.com/eip/cbwps).

2. In the top navigation bar, select the region and project to which the target Bandwidth Package belongs.

3. In the Bandwidth Package list, click **Manage EIP** next to the target Bandwidth Package.

4. Click **Add EIP** and select **Apply for an EIP and add** or **Select from EIPs**.

   * Click **Apply for an EIP and add**, and select **Number**. After the application is successful, the EIP is automatically added to the Bandwidth Package instance.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The number of EIPs that can be applied for is limited by the quota. For more information, refer to <a href="https://docs.byteplus.com/en/docs/bandwidthpackage/Limits">Quota limits</a>.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">By default, EIPs applied for using the method above are added to the project to which the Bandwidth Package instance belongs.      </div>
      

   * Click the **Select from EIPs** tab and select one or more EIPs.

5. Click **OK**.


<span id="operation-results"></span>
## Operation results


* The original maximum bandwidth values of these EIPs become invalid, and the EIPs share the bandwidth of the Bandwidth Package.

* The bandwidth fees and traffic fees of these EIPs become invalid, and only the IP configuration fees are valid. For more information on the billing items, refer to [Pay-as-you-go](https://docs.byteplus.com/en/docs/eip/Pay-as-you-go).

* In the EIP list, you can view the name and maximum bandwidth of the Bandwidth Package to which an EIP is added.
