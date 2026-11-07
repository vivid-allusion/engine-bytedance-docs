---
title: "Billing conversion"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Billing-methods-change"
---

BytePlus supports billing conversion. You can convert metering methods at any time based on your business requirements. The metering method becomes effective upon conversion.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the maximum bandwidth for an Elastic IP Address (EIP) before and after conversion is different, it has no impact on usage.</div>


<span id=".6K6h6LS56L2s5o2i5qaC6KeI"></span>
## Overview

EIP supports multiple billing conversions. Details are as follows:


|Billing conversion |Maximum bandwidth of the target metering method |Fee description |Update maximum bandwidth simultaneously |
|---|---|---|---|
|Convert Pay\-by\-bandwidth to Pay\-by\-data\-transfer |1 Mbps\-200 Mbps |No payment or refund involved. |Supported |
|Convert Pay\-as\-you\-go to Pay\-by\-bandwidth |1 Mbps\-1000 Mbps |||
|Convert Pay\-by\-bandwidth to Subscription |1 Mbps\-1000 Mbps |Pay the fee for a Subscription EIP. |Not supported |
|Convert Subscription to Pay\-by\-bandwidth |1 Mbps\-1000 Mbps |Refund the remaining balance of a Subscription EIP. ||


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Pay\-by\-data\-transfer under Pay\-as\-you\-go is referred to as <strong>Pay\-by\-data\-transfer</strong>.</div>


* <div data-tips="true" data-tips-type="tip">Pay\-by\-bandwidth under Pay\-as\-you\-go is referred to as <strong>Pay\-by\-bandwidth</strong>.</div>


* <div data-tips="true" data-tips-type="tip">Pay\-by\-bandwidth under Subscription is referred to as <strong>Subscription</strong>.</div>



<span id=".5oyJ5bim5a695LiK6ZmQ6K6h6LS56L2s5Li65oyJ5a6e6ZmF5rWB6YeP6K6h6LS5"></span>
## Convert Pay\-by\-bandwidth to Pay\-by\-data\-transfer

<span id=".57qm5p2f6ZmQ5Yi2"></span>
### Limits


* The total value of your account's available balance and EIP\-eligible coupons is not less than USD 100.00. Your available balance must be no less than 0. For details, see [Recharge guide](https://docs.byteplus.com/en/docs/byteplus-platform/billing_account).

* If the pre\-conversion maximum bandwidth is greater than the post\-conversion maximum bandwidth (200 Mbps), the converted bandwidth defaults to the maximum of 200 Mbps.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Decreasing maximum bandwidth may affect business traffic and lead to packet loss. Evaluate the possible impacts of the action on your business and proceed with caution.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to [the EIP console](https://console.byteplus.com/eip/eips). 

2. In the top menu bar, select the region and project of your target EIP.

3. In the EIP list, click  **··· \> Change configuration** to the right of the target EIP.

4. Select **Pay\-by\-data\-transfer** and change Maximum bandwidth as needed.

5. Follow the console guidance to review and accept the legal terms. 

6. Click **Buy now** to complete the conversion. 


<span id=".5oyJ5a6e6ZmF5rWB6YeP6K6h6LS56L2s5Li65oyJ5bim5a695LiK6ZmQ6K6h6LS5"></span>
## Convert Pay\-as\-you\-go to Pay\-by\-bandwidth

<span id=".57qm5p2f6ZmQ5Yi2"></span>
### Limits


* The total value of your account's available balance and coupons available for EIP is not less than USD 100.00. Your available balance must be no less than 0. For details, see [Recharge guide](https://docs.byteplus.com/en/docs/byteplus-platform/billing_account).

* During conversion, adjust the maximum bandwidth based on your business requirements.

* When you make changes, the purchased maximum bandwidth cannot exceed **the regional bandwidth upper limit**. For more information, see [Regional bandwidth limits](https://docs.byteplus.com/en/docs/eip/Limits#.5Zyw5Z-f57qn5bim5a696ZmQ5Yi2).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Decreasing maximum bandwidth may affect business traffic and lead to packet loss. Evaluate the possible impacts of the action on your business and proceed with caution.   </div>
   

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to [the EIP console](https://console.byteplus.com/eip/eips). 

2. Select the region and project of your target EIP.

3. In the EIP list, click  **··· \> Change configuration** to the right of the target EIP.

4. Select **Pay\-by\-bandwidth** and change Maximum bandwidth as needed.

5. Follow the console guidance to review and accept the legal terms. 

6. Click **Buy now** to complete the conversion. 


<span id=".5oyJ5bim5a695LiK6ZmQ6K6h6LS56L2s5Li65YyF5bm05YyF5pyI"></span>
## Convert Pay\-by\-bandwidth to Subscription

<span id=".57qm5p2f6ZmQ5Yi2"></span>
### Limits


* You cannot adjust the maximum bandwidth during the conversion. To adjust, complete the billing conversion, and then [modify the maximum bandwidth](https://docs.byteplus.com/en/docs/eip/Modifying-the-maximum-bandwidth).

* The start time of the billing cycle for Subscription is the time when the order of billing method change is created.

* EIPs with enhanced protection do not support this billing method change.

* EIPs that are added to Bandwidth Packages or are associated with Network Load Balancer (NLB) instances do not support switching to Subscription.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to [the EIP console](https://console.byteplus.com/eip/eips). 

2. In the top menu bar, select the region and project of your target EIP.

3. In the EIP list, click  **··· \> Switch to subscription** to the right of the target EIP.

4. Select a specific duration for **Purchase time**. You can check **Automatic renewal** as needed.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If <strong>Automatic renewal</strong> is checked, the system automatically deducts the renewal fee from your available balance and coupons available for the EIP 7 days before the expiration. If you do not check <strong>Automatic renewal</strong>, you need to manually renew. For more details, see <a href="https://docs.byteplus.com/en/docs/eip/Renewal">Instructions on renewal</a>.   </div>
   

5. Follow the console guidance to review and accept the legal terms. 

6. Click **Buy now** to complete the conversion. 


<span id=".5oyJ5YyF5bm05YyF5pyI6L2s5Li65oyJ5bim5a695LiK6ZmQ6K6h6LS5"></span>
## Convert Subscription to Pay\-by\-bandwidth

<span id=".57qm5p2f6ZmQ5Yi2"></span>
### Limits


* The total value of your account's available balance and coupons available for EIP is not less than USD 100.00. Your available balance must be no less than 0. For details, see [Recharge guide](https://docs.byteplus.com/en/docs/byteplus-platform/billing_account).

* Expired Subscription EIPs do not support billing method change. Renew them before proceeding.

* EIPs with enhanced protection do not support this billing method change.

* You cannot adjust the maximum bandwidth during the conversion. To adjust, complete the billing conversion, and then [modify the maximum bandwidth](https://docs.byteplus.com/en/docs/eip/Modifying-the-maximum-bandwidth).


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to [the EIP console](https://console.byteplus.com/eip/eips). 

2. In the top menu bar, select the region and project of your target EIP.

3. In the EIP list, click  **··· \> Switch to pay\-by\-bandwidth** to the right of the target EIP.

4. Follow the console guidance to review and accept the legal terms. 

5. Click **Buy now** to complete the conversion.
