---
title: "Payment rules for Paypal"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/Payment_rules_for_Paypal"
---

<span id="qAtkL4I7"></span>
# **Business Rationale**

To support a smooth order experience and provide convenient payment options, BytePlus has implemented specific business rules for customers who have only PayPal as their payment method. 

<span id="VrQXrN93"></span>
# **Core Business Rules**

When a customer account has only PayPal as its payment method, the following product purchasing rules apply:


|**Product Category** |**Description** |**Examples** |
|---|---|---|
|**Monthly/Daily Subscription**<br><br> |All monthly/daily subscription which needed to be paid before usage are allowed for purchase with PayPal |Resource packs, saving plans, coding plans, Oneart, etc. |
|**Pay\-as\-you\-go Products** |Only when both of the following conditions have been met, the products with pay as you go can be allowed to purchase with PayPal<br><br><br>* Specific  products that have been whitelisted for PayPal payment.<br><br>* AND These products must have corresponding deductible resources (resource packs, coding plans, saving plans, etc.) |ModelArk, Seedream |


<span id="kd7fpRsJ"></span>
# **Error Handling and Customer Guidance**

If a customer with only PayPal payment method attempts to purchase non\-allowed products, the system will return specific error codes and messages:


|**Customer Payment Scenario** |**Description** |
|---|---|
|**For accounts paying directly to byteplus** |You are requested to provide an alternative payment method other than PayPal before enabling the pay\-as\-you\-go products in BytePlus |
|**For accounts paying through a trustee account, instead of directly to byteplus** |You are requested to contact the main account to provide an alternative payment method other than PayPal before enabling the pay\-as\-you\-go products in BytePlus. |
