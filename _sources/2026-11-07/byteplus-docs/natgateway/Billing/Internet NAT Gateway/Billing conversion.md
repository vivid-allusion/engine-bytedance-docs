---
title: "Billing conversion"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Billing-method-change"
---

BytePlus supports billing conversion. You can convert metering method for an Internet NAT Gateway at any time based on your business requirements.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_555162d59165f2348956477c4de83581.png) </span>

<span id="Qw362lBs"></span>
## Instructions


* Internet NAT Gateway instances do not support converting from Pay\-by\-CU to Subscription.

* You cannot modify specification of the Internet NAT Gateway during conversion. To modify it, [change the sepcification for an Internet NAT Gateway](https://docs.byteplus.com/en/docs/natgateway/Changing-the-specification-of-an-Internet-NAT-gateway) after the completion of billing conversion.

* The post\-conversion billing cycle for a Subscription Internet NAT Gateway starts at the end of billing conversion.

* After converting from Subscription to Pay\-as\-you\-go, the platform will deduct fees for the used service period. It will then refund the remaining paid amount (actual cash paid, excluding coupon deductions) to your BytePlus account balance. Used coupons are non\-refundable. For detailed refund calculation rules, see the related section of [Resource Subscription Change](https://docs.byteplus.com/en/docs/byteplus-platform/Billing_Rules_for_Resource_Subscription_Change#.5LqM44CB5YyF5bm05YyF5pyI6L2s5oyJ6YeP6K6h6LS5).

* The billing conversion may change the performance cap of the Internet NAT Gateway. Carefully assess the potential impact on your business before proceeding. For performance cap, see [Performance](https://docs.byteplus.com/en/docs/natgateway/Specifications).


<span id=".5oyJ6KeE5qC86K6h6LS55LiO5oyJ5L2_55So6YeP6K6h6LS55LqS6L2s"></span>
## Prerequisites

Ensure that the total value of your account's [available balance](https://docs.byteplus.com/en/docs/6269/100429) and coupons applicable to Internet NAT Gateways is not less than 100.00 USD, and the available balance must be no less than 0. For procedure, see [Recharge guide](https://docs.byteplus.com/en/docs/6269/100434).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select the region and project.

3. In the Internet NAT Gateway list, click  **··· \> Modify Billing method** to the right of the target Internet NAT Gateway.

4. Select the metering method according to your business scenario.

   
   <Tabs>
   <Tab zoneid="iL1z1wcUt4" title="Convert to Pay-by-CU">
   <TabTitle>Convert to Pay-by-CU</TabTitle>
   
   1. Select **Pay\-by\-CU** as the metering method.
   
      > With Pay\-by\-CU, you don't need to specify the instance type. For details on performance cap and billing rules, see [Pay-by-CU](https://docs.byteplus.com/en/docs/natgateway/Pay-by-CU).   
      
   
   2. Follow the console guidance to review and accept the legal terms, and click **Submit** to complete billing conversion.
   
   
   </Tab>
   <Tab zoneid="Y0OORaK5KB" title="Convert to Pay-by-specification">
   <TabTitle>Convert to Pay-by-specification</TabTitle>
   
   1. Select **Pay\-by\-specification** as the metering method.
   
   2. Select the specification of the Internet NAT Gateway.
   
      > Billing will be based on usage duration after specifying the instance type.   
      
   
   3. Follow the console guidance to review and accept the legal terms, and click **Submit** to complete billing conversion.
   
   
   </Tab>
   <Tab zoneid="vZJqd1EvXu" title="Convert to Subscription">
   <TabTitle>Convert to Subscription</TabTitle>
   
   Only **Pay\-by\-specification** Internet NAT Gateways support converting to Subscription.
   
   
   1. Select the **Subscription** as the metering method.
   
   2. Select the purchase duration for the Internet NAT Gateway, and check **Automatic renewal** as needed.
   
      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">tip   </div>
      
   
      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If <strong>Automatic renewal</strong> is checked, the system automatically deducts the renewal fee from your available balance and coupons available for the Internet NAT Gateway 7 days before the expiration. If left <strong>Automatic renewal</strong> unchecked, you need to manually renew. For more details, see <a href="https://docs.byteplus.com/en/docs/natgateway/Renewals">Renewal</a>.   </div>
      
   
   3. Follow the console guidance to review and accept the legal terms, and click **Submit** to complete billing conversion.ip
   
   
   </Tab>
   </Tabs>
