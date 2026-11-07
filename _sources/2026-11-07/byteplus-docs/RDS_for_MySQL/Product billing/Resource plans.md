---
title: "Resource plans"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Resource_plans"
---

This topic describes how to purchase resource plans for RDS for MySQL.

<span id="MB8cpfBz"></span>
## Background information

Resource plans are a prepaid, account\-level cost\-saving solution provided by RDS for MySQL. After you purchase a resource plan, the resources in the plan can be used to deduct the resource usage fees of all instances under your account in a specific region. Compared to regular billing, resource plans offer more competitive pricing for resources, which significantly reduces instance usage fees.

<span id="pa3VpElz"></span>
### Resource plan types

Currently, only storage\-type resource plans are supported.

<span id="FEanuvmy"></span>
### Resource plan specifications

RDS for MySQL currently provides storage\-type resource plans in the following specifications: 100 GiB, 200 GiB, 300 GiB, 500 GiB, 1,000 GiB, 2,000 GiB, 5,000 GiB, and 10,000 GiB.

<span id="c3tseu2X"></span>
### Deduction targets

A storage\-type resource plan can be used to deduct the basic backup storage space, cross\-regional backup storage space, and storage space for backups of deleted instances under an account.

<span id="iZ4BNAZw"></span>
### Deduction rules

You can purchase multiple resource plans. If you have multiple active resource plans, the one with the earliest due time is used for deduction first.


* The total backup storage space usage is calculated every hour and deducted from your purchased storage plan capacity based on the deduction factor. If the deduction amount exceeds the total storage plan capacity, the excess amount is charged on a pay\-as\-you\-go basis.

* Deductions are made against the total capacity of the storage plan every hour.

   * For example, if you purchase a 100 GiB storage plan for one month, 100 GiB of the plan's capacity is available every hour during that month to deduct backup storage space usage.

   * Any unused portion from the previous hour is cleared every hour.

* Overage deduction within a single hour is supported. If the storage plan specification is 100 GiB, but only 200 GiB of basic backup storage space under the account is being deducted, a deduction of 1,800 seconds per hour is supported for this 200 GiB of basic backup storage space. The excess part is converted to pay\-as\-you\-go.

* When a storage plan is used for deduction, basic backup storage space, cross\-regional backup storage space, and deleted instance backup storage space are deducted in billing order.


<span id="NCTq7hOg"></span>
### Deduction factor

When a resource plan is used for different storage spaces, the deduction factor varies. It also varies for resources in different regions, as shown in the table below.


|**Deduction item**<br><br> |**China (Beijing),** <br><br>**China (Shanghai),** <br><br>**China (Guangzhou)**  |**China (Hong Kong)** <br><br> |**Asia Pacific (Johor)**  |**Asia Pacific (Jakarta)** <br><br> |
|---|---|---|---|---|
|Basic backup storage space |0.5854 |0.5854 |0.5723 |0.7024 |
|Cross\-regional backup storage space |0.5854 |0.5854 |0.5723 |0.7024 |
|Deleted instance backup storage space |0.1463 |0.1464 |0.1431 |0.1463 |


<span id="TUnOadUE"></span>
#### **Deduction example**

An account purchased a 100 GiB storage resource plan in the North China 2 (Beijing) region. The account has a local SSD instance with 60 GiB of storage space in the North China 2 (Beijing) region. The instance has 300 GiB of basic backup storage space and 200 GiB of cross\-regional backup storage space. The deduction method for the storage plan is as follows:


1. Basic backup storage space eligible for deduction with the storage resource plan: 300 \- 60 = 240 GiB

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Each RDS for MySQL instance has a free basic backup storage space of the same size as the instance storage space.   </div>
   

   1. Remaining storage plan quota after deducting basic backup storage space: 100 \- 240 \* 0.16 = 61.6 GiB

2. Cross\-regional backup storage space deducted by the storage plan: 61.6 / 0.64 = 96.25 GiB

3. Normally billed cross\-regional backup storage space: 200 \- 96.25 = 103.75 GiB


<span id="70WVwsyr"></span>
### Price

Unit: USD/month


|<div style="text-align: center"><br>Specification</div><br> |All regions |
|---|---|
|<div style="text-align: center"><br>100 GiB</div><br> |<div style="text-align: center"><br>8.20</div><br> |
|<div style="text-align: center"><br>200 GiB</div><br> |<div style="text-align: center"><br>16.40</div><br> |
|<div style="text-align: center"><br>300 GiB</div><br> |<div style="text-align: center"><br>24.60</div><br> |
|<div style="text-align: center"><br>500 GiB</div><br> |<div style="text-align: center"><br>41.00</div><br> |
|<div style="text-align: center"><br>1000 GiB</div><br> |<div style="text-align: center"><br>82.00</div><br> |
|<div style="text-align: center"><br>2000 GiB</div><br> |<div style="text-align: center"><br>164.00</div><br> |
|<div style="text-align: center"><br>5000 GiB</div><br> |<div style="text-align: center"><br>410.00</div><br> |
|<div style="text-align: center"><br>10000 GiB</div><br> |<div style="text-align: center"><br>820.00</div><br> |


<span id="dtLR90Pd"></span>
## Precautions


* Storage plans are available by subscription only. You can purchase a subscription for 1 to 12 months or 1 to 5 years.

* Storage plans do not support upgrades or renewals.

* You cannot unsubscribe from a storage plan once it is active. For an ineffective plan, only a "7\-day unconditional unsubscription" is supported; a "non\-7\-day unconditional unsubscription" is not supported. Each account can only perform a '7\-day unconditional unsubscription' once per calendar year. For RDS for MySQL, storage plans and instances share the same '7\-day unconditional unsubscription' quota.

* To unsubscribe from a storage plan, go to the [Billing Center](https://console.byteplus.com/finance/resource-package/).


<span id="zT40Xqki"></span>
## Purchasing resource plans


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the Region to which the resource plans belong.

3. In the left\-side navigation pane, click **Resource plans** to go to the resource plans page.

4. In the upper\-left corner of the Resource plans page, click **Purchase new resource plan**. On the buy storage plan page, complete the settings and click **Confirm order** to go to the **Confirm order information** page.



|Parameter |Note |
|---|---|
|Database type |Choose **MySQL**. |
|Billing method |Select **storage plan**. |
|Storage plan specification |Select the specifications for the storage plan as needed. |
|Effective time |You can set the plan to take effect **Immediately after purchase** or at a **Specific time**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you select a specific time, you need to configure the effective time for the resource plan.</div><br> |
|Specify time |The specific time when the resource plans take effect. |
|Subscription duration |Select the purchase duration for the resource plan. |



5. On the **Confirm order information** page, reconfirm the order information, and click **Next step**.

6. On the **Submit payment information** page, confirm the payment details, select a payment method, click **To pay**, and follow the prompts to complete the purchase of the resource plan.


<span id="Thi3Ky5M"></span>
## View resource plan usage details


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the Region to which the resource plans belong.

3. In the left\-side navigation pane, click **Resource plans** to go to the resource plans page.

4. In the \*\*Resource plans\*\* list, click **Details** in the **operation** column for the target resource plan. On the displayed **Storage plan details** page, you can view the details of the storage plan, including its basic information and usage record.


<span id="DyCeRn1v"></span>
## View the deduction details of a resource plan


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the Region to which the resource plans belong.

3. In the left\-side navigation pane, click **Resource plans** to go to the resource plans page.

4. In the Resource plans list, click **Deduction details** in the **Actions** column for the target resource plan. You are redirected to the **Resource plan management** page in the Billing Center. The **Resource plan management** page displays the detailed deduction information for the resource plan.
