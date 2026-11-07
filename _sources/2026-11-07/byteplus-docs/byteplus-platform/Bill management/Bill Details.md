---
title: "Bill Details"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/docs-bill-details"
---

**Bill details**

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260623033145-1512479019633.png" /></div>



1. **Filter**:

* Billing cycle: The billing cycle is the current month by default. You can select one billing cycle only.

* Payer/Owner: View the bills in both the Payer and Owner accounts.

* Order/Bill no.: Search for a bill by its order number or bill number.

* Instance ID/name: Search for a bill by its instance ID or instance name.

2. **Table columns:** 

* Billing cycle: The cycle to which the bills belong.

* Payer: The account responsible for paying the bill.

* Seller: The account associated with the entity that sells the service.

* Owner: The account held by the individual or entity that uses the service.

* Country/Region: The country or region selected when you register the account.

* Product: The name of the cloud product.

* Business mode: Byteplus provides common business and financially\-hosted business.

* Billing mode: The billing mode of the product or service, such as subscription and pay\-as\-you\-go.

* Consumption time: The payment time in the case of pre\-payment, or the start and end time in the case of post\-payment.

* Usage: The duration of a subscription order or the billing duration of a pay\-as\-you\-go order.

* Usage unit: The unit of measurement for the usage duration.

* Transaction time: The deduction time of a consumption record. If the billing for post\-payment is delayed and the monthly bill is generated no later than the third working day of the following month, the transaction time and consumption time may belong to different months. For example, the date of bill generation and fee deduction for the previous month is on the 2nd of the current month.

* Order/Bill no.: The order number of pre\-payment, or the bill number of post\-payment.

* Billing type: The type of the bill, such as consumption\-use, refund\-unsubscription, and billing adjustment\-manual service.

* Settlement type: The settlement type of the bill, including no settlement, settlement by balance, and settlement by quota.

* Instance ID/name: The instance ID or instance name of the bill.

* Configuration name: The configuration information of the instance or billing item.

* Billing unit: The billing unit of the instance or billing item.

* Region: The region of the instance or billing item.

* Availability zone: The availability zone of the instance or billing item.

* Impact factor: The factor information of the instance or billing item that impacts price.

* Extra specs: The additional notes of the instance or billing item.

* Unit price: The unit price of the product or service, only available for publication pricing. For special pricing models, such as tiered pricing, the unit price is not provided.

* Price unit: The unit of measurement for the price.

* Usage: The usage of the product or service.

* Usage unit: The unit of measurement for the usage.

* Package usage: The amount deducted from resource packages.

* Gross amount: The consumption amount calculated based on the list of products. Certain offline contractual bills have no discount, which means, the gross amount is equal to the amount after discount.

* Discount amount: The amount of discount generated based on contracts, activities, and other applicable factors.

* Amount(truncated): The amount that is distributed among corresponding bill details based on the rounded amount of the bill. In certain cases, if a bill number corresponds to multiple bill details, the rounded amount of specific bill details may be negative.

* Amount after discount: The amount is calculated by subtracting the discount amount and truncated amount from the gross amount.

* Coupon used: The amount that is deducted from the total cost using coupons.

* Pre\-tax amount(payment currency): The amount payable before taxes is calculated by subtracting the coupon deduction from the discounted price.

* Tax: The tax amount is calculated by multiplying the amount payable before taxes by the tax rate.

* Post\-tax amount(payment currency): The amount payable after taxes is calculated by adding the amount payable before taxes to the tax amount.

* Amount paid: The amount paid using a credit card.

* Amount due: The amount that has been billed but remains unpaid. In particular, the amount paid using a credit card is recorded as part of the overdue amount.

* Seller entity: The entity that provides services.

3. **Custom column:**  You can select specific data fields that you want to display. The bill details page displays data as you selected.


<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260623041331-1677578054533.png" width="454px" /></div>



&nbsp;

4. **Export bill(CSV):**  You can export all fields of bill data or specific parameters based on your applied filters.


<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260623041407-1459863564837.png" width="558px" /></div>



&nbsp;

* Current filter results: Export the exact data that is displayed on the page.

* Whole table: Export all fields of the bill data.
