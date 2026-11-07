---
title: "Billing item"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Billing-items"
---

The billing items of CLB instances vary according to the instance type, as shown in the table below.

> Tip: In the table below, `--` indicates that the fee is not charged, and `✓` indicates that the fee is charged.



|Type |Instance Fee |Specification Configuration Fee |Internet Fee |
|---|---|---|---|
|Internet |✓ |✓ |✓ |
|Virtual Private Cloud (VPC) |✓ |✓ |\-\- |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If the billing type of a public CLB instance is <strong>Pay\-as\-you\-go</strong> and it has been added to a Shared Bandwidth Package, no internet fee will be charged for this CLB instance.</div>


* <div data-tips="true" data-tips-type="tip">If a private CLB instance is associated with an Elastic IP (EIP), its EIP fee is already included in the fee of the EIP product and will not be shown in the CLB bill. Therefore, this fee is not described here. For details, refer to <a href="https://docs.byteplus.com/en/docs/eip/Billing-overview">EIP product billing</a>.</div>


* <div data-tips="true" data-tips-type="tip">If a private CLB instance with activated IPv6 internet bandwidth is associated with an IPv6 gateway product, its internet bandwidth fee will be charged by the IPv6 gateway product and won't be reflected in the CLB bill. Therefore, this fee is not described here. For details, refer to <a href="https://docs.byteplus.com/en/docs/IPv6/Pay-as-you-go">IPv6 gateway Billing</a>.</div>



Fees listed in the above table are described as follows:

> The usage duration mentioned below is calculated from the time the order is successfully created.



* Instance fee: charged based on the usage duration.

* Specification configuration fee: charged based on the actual usage duration and the instance specification specified by the user.

   Max Connection, New Connections Per Second, Queries Per Second (QPS), and maximum bandwidth vary according to the specification. You can select an appropriate specification based on the performance requirements of the specific scenarios. For more information about specifications, refer to [CLB instance specifications](https://docs.byteplus.com/en/docs/clb/Product-Overview-02).

* Internet fees: Based on the CLB instance's Billing methods and internet Metering methods, IP configuration fees, bandwidth fees, or traffic fees are charged.
