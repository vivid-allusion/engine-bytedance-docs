---
title: "Billing Rules for Resource Subscription Change"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/Billing_Rules_for_Resource_Subscription_Change"
---

If your current resource subscription cannot meet your business requirements, you can initiate a subscription change through the cloud service console. BytePlus currently supports four types of subscription change:


* Change the specifications of an annual or monthly subscription

* Change from an annual or monthly subscription to pay\-as\-you\-go

* Change from pay\-as\-you\-go to an annual or monthly subscription

* Change pay\-as\-you\-go specifications



---



<span id="i-change-specifications-of-an-annual-or-monthly-subscription"></span>
# I. Change Specifications of an Annual or Monthly Subscription

Such changes include two scenarios: resource upgrades and resource downgrades.


* Upgrades: When a resource subscription is upgraded, the new (hourly) list price is equal to or greater than the original list price, and the system calculates the price difference using the upgrade formula.

* Downgrades: When a resource subscription is downgraded, the new (hourly) list price is lower than the original list price, and the system calculates the price difference using the downgrade refund formula. When a subscription is downgraded and renewed at the same time, the system first applies the downgrade refund formula. If the calculation results in a refund, the price difference is processed accordingly. If the calculation leads to an additional charge, the system recalculates the price difference using the upgrade formula and requires payment for the difference.


Notes:


1. As discounts may expire, the price shown on the change request page may differ from the price confirmed upon order completion. Please consider the latter as the final price.

2. Fees for upgrading or scaling up resources can be paid through your credit control balance or online payment methods. On the other hand, any refunds resulting from downgrading resources will be issued back through the original payment method, in accordance with our *Refund Flow*.

3. If you initiate a request for a specification upgrade or scale\-up, and the associated change order is created but not paid on the same day as the request:

   1. Completing the payment within the order's validity period will ensure the price remains as quoted on the request day.

   2. Alternatively, you can cancel the order and reinitiate the change process.

4. The calculations presented here are for illustrative purposes only and have been rounded to two decimal places. For a more accurate calculation of upgrade/scale\-up costs or downgrade refund amounts, it is advised to be precise up to 16 decimal places to avoid discrepancies with the amounts shown on the website.

5. Theoretically, a specification change combines two operations: unsubscribing the original service and purchasing a new one. Therefore, a single change operation may generate several associated orders, specifically:

   1. Specification change \- Pre\-tax payable amount for the new purchase: This is the theoretical cost of the new service, calculated using the upgrade or downgrade formula.

   2. Specification change \- Pre\-tax payable amount for the unsubscribed service: If there is a pending renewal order, two specification change \- unsubscription orders will be generated. Each order's theoretical pre\-tax remaining value will be calculated separately using the upgrade or downgrade formula.

   3. Pre\-tax payable total: It refers to the sum of pre\-tax payable amounts of all orders under a single change operation. Each order's pre\-tax payable amount is derived theoretically using the upgrade or downgrade formula and is used only for the calculation of the pre\-tax payable total.

   4. Pre\-tax real value of instance after change: It is used for calculating the pre\-tax remaining value for any subsequent changes or refunds.

      1. Pre\-tax real value of instance after change = Pre\-tax payable total for current change + Pre\-tax remaining real value before change

      2. Pre\-tax remaining real value before change = min

      3. Pre\-tax remaining real value of original order = Pre\-tax real value of original order \* (Remaining duration/Total order duration), measured to the secondFor both new and renewal orders, the pre\-tax real value equals to their pre\-tax payable amount.


<span id="upgrade"></span>
## Upgrade

**Pre\-tax payable total of upgrade order**

 **= New configuration cost (pre\-tax) \- Remaining value of original configuration (pre\-tax)** 

 **= New configuration list price (hourly) \* Remaining duration (hours) \* Discount \- Original configuration list price (hourly) \* Remaining duration (hours) \* Discount**

Notes:


1. Rules on calculating the hourly list price of the new configuration:

   1. For daily billing, the hourly list price of the new configuration = daily list price/24.

   2. For monthly billing, the hourly list price of the new configuration = monthly list price/30/24.

   3. For annual billing, the hourly list price of the new configuration = annual list price/365/24.

2. Remaining duration = [Instance expiration time (accurate to the second) \- Time of order submission on the configuration option page (accurate to the second)]/3600

3. Discount: A new discount will be applied to the upgraded configuration based on the remaining duration to align with the system's latest discount levels. Meanwhile, the original configuration retains its initially applied discount.

4. Configuration cost = The sum of all billing items associated with this configuration/instance



|Type |Calculation Rules |Example |
|---|---|---|
|**No changes in configuration, billing item, or billing item attribute value (usage)**  |The billing item is calculated using the list prices in both new and original configurations |For a monthly\-billed public IP, the billing item is the bandwidth, which has monthly list prices subject to tiered pricing as follows: USD 23/M for [0, 2M], USD 25/M for (2M, 5M], and USD 100/M for (5M, +∞), with a 15% discount for one\-year commitment. In this example, the billing item attribute value remains consistent at 3M before and after the change, and the remaining duration is assumed to be 367 days, then:<br><br>**Pre\-tax** payable total of upgrade order<br><br>= New configuration cost \- Remaining value of original configuration<br><br>= 3M bandwidth list price/30/24 \* 367 \* 24 \- 3M bandwidth list price/30/24 \* 367 \* 24<br><br>= USD 0 |
|**Configuration or billing item changed** |The billing item is calculated using the discounted prices in both new and original configurations |For a cloud server instance with the billing item ecs.g2i.large priced at a monthly list rate of USD 246, along with a 17% discount for one\-year commitment and a 30% discount for two\-year commitment, a client who subscribes to an ecs.g2i.large instance for two years pays a pre\-tax amount of USD 246 \* 24 \* 0.7 = USD 4132.8. After upgrading to the ecs.g2i.xlarge configuration, which has a monthly list price of USD 492, assume a remaining duration of 367 days, then:<br><br>**Pre\-tax** payable total of upgrade order<br><br>= New configuration cost \- Remaining value of original configuration<br><br>= ecs.g2i.xlarge list price/30/24 \* 367 \* 24 \* one\-year discount \- ecs.g2i.large list price/30/24 \* 367 \* 24 \* original discount<br><br>= 492/30/24 \* 367 \* 24 \* 0.83 \- 246/30/24 \* 367 \* 24 \* 0.7<br><br>= USD 2889.02 |
|**No changes in configuration or billing item, with increased billing item attribute value (usage)**  |1. Fixed unit price/Tiered unit price: The cost for the original attribute value (usage) is calculated using the list price, whereas the cost for the incremental part of the attribute value (usage) is calculated using the discounted price. The incremental attribute value (usage) = Post\-change attribute value \- Pre\-change attribute value |For a monthly\-billed public IP, the billing item is the bandwidth, which has monthly list prices subject to tiered pricing as follows: USD 23/M for [0, 2M], USD 25/M for (2M, 5M], and USD 100/M for (5M, +∞), with a 15% discount for a one\-year commitment. The original bandwidth is 3M, and is increased to 7M following the upgrade. Assume the remaining duration is 367 days, then:<br><br>**Pre\-tax** payable total of upgrade order<br><br>= New configuration cost \- Remaining value of original configuration<br><br>= Original 3M bandwidth list price/30/24 \* 367 \* 24 + 4M bandwidth list price/30/24 \* 367 \* 24 \* one\-year discount \- Original 3M bandwidth list price/30/24 \* 367 \* 24<br><br>= (2M \* 23 + 1M \* 25)/30/24 \* 367 \* 24 + (2M \* 25 + 2M \* 100)/30/24 \* 367 \* 24 \* 0.85 \- (2M \* 23 + 1M \* 25)/30/24 \* 367 \* 24<br><br>= USD 2599.58 |
||Volume\-based unit price/Volume\-based total price: The billing item is calculated using the discounted price in both new and original configurations. |For the monthly\-billed Elastic Block Storage Extreme SSD PL0 data disk, the list price is set at USD 0.5 per GiB, with a 17% discount for a one\-year commitment and a 30% discount for a two\-year commitment. The pricing follows a tiered unit price model: USD 0.5/GiB for [0, 20GiB], USD 0.4/GiB for (20GiB, 50GiB], and USD 0.3/GiB for (50GiB, +∞). A client who purchases 20GiB for two years gets a pre\-tax payable amount of 20GiB \* USD 0.5/GiB \* 24 months \* 0.7 = USD 168. If the attribute value (usage) before the upgrade is 20GiB and is increased to 60GiB after the upgrade, with a remaining duration of 367 days, then:<br><br>**Pre\-tax** payable total of upgrade order<br><br>= New configuration cost \- Remaining value of original configuration<br><br>= 60GiB list price/30/24 \* 367 \* 24 \* one\-year discount \- 20GiB list price/30/24 \* 367 \* 24 \* original discount<br><br>= 0.3 \* 60/30/24 \* 367 \* 24 \* 0.83 \- 0.5 \* 20/30/24 \* 367 \* 24 \* 0.7<br><br>= USD 97.14 |


<span id="downgrade"></span>
## Downgrade

In instances where the capacity of your annually or monthly subscribed instances exceeds your business requirements, you can downgrade the specifications at any time, provided that the cloud product console supports such a change. The system calculates the refund for a specification downgrade according to the following rules:

**Pre\-tax payable total of downgrade order**

 **= New configuration cost \- Refundable remaining value of original configuration**

 **= New configuration (hourly) list price \* Remaining duration (hours) \* Discount \- Pre\-tax real value of original order/Total order duration \* Remaining duration**

 **= New configuration (hourly) list price \* Remaining duration (hours) \* Discount \- (Pre\-tax real value of original order \- Pre\-tax real value of original order \* Used duration/Total order duration \* Downgrade refund coefficient)** 

 **= New configuration (hourly) list price \* Remaining duration (hours) \* Discount \- (Pre\-tax real value of original order \- Pre\-tax real value of original order \* Used duration/Total order duration) \* Downgrade refund coefficient**

Notes:


1. Rules on calculating the hourly list price of the new configuration:

   1. For daily billing, the hourly list price of the new configuration = daily list price/24.

   2. For monthly billing, the hourly list price of the new configuration = monthly list price/30/24.

   3. For annual billing, the hourly list price of the new configuration = annual list price/365/24.

2. Remaining duration = [Instance expiration time (accurate to the second) \- Time of order submission on the configuration option page (accurate to the second)]/3600

3. Used duration = Time of downgrade order submission \- Original order start time, accurate to the second.

4. Discount: A new discount will be applied to the upgraded configuration based on the remaining duration to align with the system's latest discount levels.

5. Configuration cost = The sum of all billing items associated with this configuration/instance

6. If the cloud service's billing rules state no refunds for downgrading (refer to the specific cloud service's billing documentation), the refund after downgrading will be zero.

7. Real order value:

   1. For both new and renewal orders, the pre\-tax real value equals to their pre\-tax payable amount.

   2. Pre\-tax real value of instance after change: It will be employed in calculations of the pre\-tax real value for any subsequent change and of the remaining value for a refund.

      1. Pre\-tax real value of instance after change = Pre\-tax payable total for current change + Pre\-tax remaining real value before change

      2. Pre\-tax remaining real value before change = min

      3. Pre\-tax remaining real value of original order = Pre\-tax real value of original order \* (Remaining duration/Total order duration), measured to the second


**Downgrade example**

A client initially purchased a cloud server with a specification of 4C8G for one year, with a list price of USD 100 per month. The client was eligible for a 15% discount for a full year's subscription (no discount is offered for commitment less than a year) and was charged a pre\-tax total of USD 1,020 for the year. After using the service for half a year (assuming 180 days remain), the client downgrades it to a 2C4G configuration at a list price of USD 50 per month. Then:

Pre\-tax payable total of downgrade order

= New configuration cost \- Refundable remaining value of original configuration

= New configuration list price/30 days/24 hours \* Remaining duration (hours) \* Discount \- (Pre\-tax real value of original order \- Pre\-tax real value of original order \* Used duration/Total order duration \* Downgrade refund coefficient)

= 50/30/24 \* 180 \* 24 \* 1 \- (1020 \- 1020 \* 185/365 \* 1)

= 300 \- 503.01

= USD \-203.01

&nbsp;

<span id="ii-change-from-an-annual-or-monthly-subscription-to-pay-as-you-go"></span>
# II. Change from an Annual or Monthly Subscription to Pay\-As\-You\-Go


* Specification change \- New purchase: For pay\-as\-you\-go resources, payment is made after use. When changing the specifications, the order amount is 0. The cost is reflected in the subsequent usage bill.

* Specification change \- Unsubscription: The remaining value is calculated according to the non\-seven\-day refund policy. For detailed rules, refer to [BytePlus - Billing Center - Unsubscription Management](https://docs.byteplus.com/en/byteplus-platform/docs/unsubscription-management).


&nbsp;

<span id="iii-change-from-pay-as-you-go-to-annual-or-monthly-subscription"></span>
# III. Change from Pay\-As\-You\-Go to Annual or Monthly Subscription


* Specification change \- New purchase: Cost is calculated as if this is a new purchase.

* Specification change \- Unsubscription: For pay\-as\-you\-go resources, payment is made after use. When changing the specifications, the order amount is 0. The cost is reflected in the subsequent usage bill.


&nbsp;

<span id="iv-change-pay-as-you-go-specifications"></span>
# IV. Change Pay\-As\-You\-Go Specifications


* For pay\-as\-you\-go resources, payment is made after use. The cost of changing the specifications is reflected in the subsequent usage bill.
