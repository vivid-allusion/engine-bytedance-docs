---
title: "Changing the billing method"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Changing_the_billing_method"
---

<span id=".5qaC6L-w"></span>
## Overview

Classic Load Balancer (CLB) supports two types of billing methods: Pay\-as\-you\-go and Subscription. Each billing type includes different metering methods. Changing the metering methods of CLB instances as needed can help you save costs.

This topic introduces the conversion between different metering methods for CLB.

<span id=".6L2s5o2i5a6e5L6L6K6h6LS55pa55byP"></span>
## CLB instance


<Tabs>
<Tab zoneid="cI6yDOXzWj" title="Changing billing method from Pay-as-you-go to Subscription">
<TabTitle>Changing billing method from Pay-as-you-go to Subscription</TabTitle>

**Prerequisites**


* The CLB instance is not stopped.

* The EIP associated with a public CLB instance is not added to the Bandwidth Package.

* The Elastic IP (EIP) associated with the public CLB instance is charged using the pay\-by\-bandwidth billing method.


**Action description**


* The public CLB instance and its associated EIP are converted to Subscription. Subscription fees for both the CLB instance and its associated EIP need to be paid.

* When converting a private CLB instance to Subscription, the metering method of its associated EIP is not affected. Only the Subscription fee for the CLB instance needs to be paid.


**Procedures**


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click ··· \> Manage instance configuration \> Convert to subscription on the right of the target CLB instance.

4. Configure relevant parameters based on the table below.

   
   |Parameter |Explanation |Example |
   |---|---|---|
   |Duration |Select the subscription duration for the CLB instance. The billing change time marks the start of the subscription period. |3 months |
   |Automatic renewal |Select whether to enable automatic renewal; it is unchecked by default. Check the option to enable automatic renewal. |\- |
   |Agreement |Follow the console guidance to review and accept Legal. |Check |
   

5. Click Submit to enter the order information confirmation page.

6. Click Next step to enter the payment page.

7. Select a payment method and click Buy to finish the payment.


</Tab>
<Tab zoneid="ceRkLbeKKp" title="Changing billing method from Subscription to Pay-as-you-go">
<TabTitle>Changing billing method from Subscription to Pay-as-you-go</TabTitle>

**Prerequisites**


* Make sure the CLB instance is not suspended and modification protection is not enabled.


**Action description**


* The public CLB instance and its associated Elastic IP (EIP) are both switched to Pay\-as\-you\-go billing. The CLB instance uses Pay\-as\-you\-go, and the EIP uses pay\-by\-bandwidth. The residual value amount of the yearly/monthly subscription amount will be refunded. The residual value includes cash and credit limits and excludes the part offset by cash coupons. For more information about the refunding formula, see Unsubscribe rules for Non 7\-Day No Fault Return.

* A private CLB instance is converted to Pay\-as\-you\-go, and the metering methods of its associated EIP remain unchanged.


**Procedures**


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click ··· \> Modify Instance Spec \> Convert to pay\-as\-you\-go on the right side of the target CLB instance.

4. Follow the console guidance to review and accept Legal.

5. Click Submit to enter the order information confirmation page.

6. Click Next step to complete the billing methods ch


</Tab>
</Tabs>


<span id=".6L2s5o2i5YWs572R6K6h6LS55pa55byP"></span>
## Elastic IP Address

<span id=".5oyJ5a6e6ZmF5rWB6YeP6K6h6LS56L2s5o2i5Li65oyJ5bim5a695LiK6ZmQ6K6h6LS5"></span>
### Switching between pay\-by\-data\-transfer and pay\-by\-bandwidth

**Action description**


* Private CLB instances without attached EIPs do not support this operation.

* When the EIP associated with a CLB instance has been added to the shared bandwidth package, the public billing change only takes effect after the EIP is removed from the bandwidth package.

* When the EIP is changed from pay\-by\-bandwidth to pay\-by\-data\-transfer, if the Internet bandwidth before billing conversion exceeds 200 Mbps, the Internet bandwidth after billing conversion defaults to 200 Mbps. Assess the impact on your service carefully before proceeding.


**Procedures**


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click ··· \> Public \> Edit EIP configuration to the right of the target CLB instance.

4. Select the Metering methods pay\-by\-bandwidth or pay\-by\-data\-transfer.

5. Follow the console guidance to review and accept Legal.

6. Click Submit to finish the billing method conversion.

7. Click Go to console to jump to the EIP list page to view the billing method of the target EIP.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[ConvertLoadBalancerBillingType](https://docs.byteplus.com/en/docs/clb/ConvertLoadBalancerBillingType)

&nbsp;
