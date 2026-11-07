---
title: "Switch from Pay-as-you-go to Mixed Billing (Partially subscription)"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Switch_from_Pay-as-you-go_to_Mixed_Billing"
---

BytePlus offers the feature of switching from pay\-as\-you\-go to mixed billing (partly subscription) for the Container Registry, allowing you to convert pay\-as\-you\-go instances into partially subscription instances, pre\-reserve resources and significantly save costs for long\-term scenarios.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Currently, only standard instances support this feature, and the proxy cache registry does not support switching billing methods.</div>


* <div data-tips="true" data-tips-type="warning">For a comparison of the costs before and after the conversion, refer to <a href="https://docs.byteplus.com/en/docs/cr/billing-items">Billing Items</a>.</div>



<span id="background"></span>
## Background


* Pay\-as\-you\-go: The Container Registry CR supports a postpaid pay\-as\-you\-go billing method, where you use first and pay later, with the bill amount calculated by multiplying the usage by the unit price, and this amount is directly deducted from your account balance.

* Mixed billing: In the mixed billing mode, **Instance fee** and **Quota expansion fee** are charged on a subscription basis and need to be prepaid before use, but they offer more favorable discounts compared to pay\-as\-you\-go billing. **Outbound Public Network Traffic** and **Storage Capacity** still follow the pay\-as\-you\-go rules.


<span id="prerequisites"></span>
## Prerequisites


* The instance status is either **Running** or **Stopped**.

* The billing method for the target instance is **Pay\-as\-you\-go**.

* The account has no arrear.


<span id="procedure"></span>
## Procedure


1. Log in to the [Container Registry console](https://console.byteplus.com/cr).

2. At the top navigation bar, select the region and project to which the target instance belongs.

3. In the left navigation tree, select **Instances list**.

4. In the target instance area, click on  **··· \> Volume to mix billing.** 

5. Confirm the instance information and complete the related settings following the interface prompts.



|**Parameter** |**Description** |
|---|---|
|Purchase duration |Set the purchase duration. |
|Automatic renewal |Select whether to enable automatic renewal, by default it is not checked. |



6. Click **Confirm** to complete the payment and billing method conversion.
