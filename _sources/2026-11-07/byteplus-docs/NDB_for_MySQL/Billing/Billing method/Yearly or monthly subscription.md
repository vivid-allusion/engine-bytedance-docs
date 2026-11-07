---
title: "Yearly or monthly subscription"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Yearly_or_monthly_subscription"
---

Subscription is a billing method where you pay in advance when creating an instance. Subscription instance means the calculate billing type is Subscription, and the storage billing type can be Subscription or Pay\-as\-you\-go. Yearly or monthly subscription instances are more affordable than pay\-as\-you\-go instances and are suitable for long\-term use. This topic describes how to purchase NDB for MySQL instances using the Subscription billing method.

<span id=".6LSt5Lmw5Zy65pmv"></span>
## Purchase scenarios

Based on the billing methods for compute nodes and storage space, subscription instances fall into the following two purchase scenarios:


* **Yearly or monthly subscription for compute + Pay\-as\-you\-go for storage**: You prepay for compute nodes for the purchased duration, while storage space is charged hourly based on actual usage and deducted from your account.

* **Yearly or monthly subscription for compute + Subscription for storage + Pay\-as\-you\-go for excess storage**: When purchasing the instance, you prepay for both compute nodes and storage space for the selected duration. If your actual data usage later exceeds the purchased storage capacity, you can continue to use the instance normally. Any storage usage beyond the prepaid capacity will incur hourly charges to your account.


<span id=".6LSt5Lmw5pe26ZW_"></span>
## **Purchase duration**

Subscription NDB for MySQL instances offer various purchase durations. You can choose a duration based on your business needs:


* **Monthly subscription**: You can purchase for 1 to 9 months in the console. The purchase duration is not limited when you call the [CreateDBInstance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateDBInstance) API.

* **Yearly subscription**: You can purchase for 1 to 3 years in the console. The purchase duration is not limited when you call the [CreateDBInstance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateDBInstance) API.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can get a discount for a purchase duration of one year or more. The specific discount is subject to the actual order page in the console.   </div>
   

<span id=".57uT566X5ZGo5pyf"></span>
## Settlement cycle

The billing cycle of a subscription NDB for MySQL instance is based on the purchase duration of its compute nodes (UTC+8). The cycle starts when the resource is enabled (accurate to the second) and ends at 23:59:59 on the expiration date.

For example, when a subscription instance is created at 14:00:00 on July 1, 2023 and the purchase duration is one month, then the billing cycle is from 14:00:00 on July 1, 2023 to 23:59:59 on August 1, 2023.

<span id=".5Y-Y5pu06YWN572u"></span>
## Changing instance configuration

You can change the configuration of a Subscription instance in real time. After the change is successful, you can view the latest specifications for the instance on the **Instance list** page. For how to modify the configuration, refer to [Changing instance configuration](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Changing_node_specifications). After changing the configuration of a Subscription instance, you may receive a refund or be required to pay the price difference. For more information about the billing rules for changing the configuration of Subscription instances, refer to [Billing Rules for Resource Subscription Change](https://docs.byteplus.com/en/docs/byteplus-platform/Billing_Rules_for_Resource_Subscription_Change).

<span id=".6YCA6K6i5a6e5L6L"></span>
## Unsubscribe instance

After you unsubscribe from (delete) a Subscription NDB for MySQL instance, the refund will be credited to your account balance. Note that used vouchers are non\-refundable. For how to unsubscribe from an instance, refer to [Unsubscribe from yearly/monthly subscription instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Deleting_or_unsubscribing_an_instance). For more information about refund calculation rules, refer to [Unsubscribe management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Even if your account is in arrears, you can still use the subscription NDB for MySQL instances you have purchased normally. Before making up the outstanding fees, you cannot perform billing operations such as creating new instances, renewal, and changing configuration. For more details, see [Arrears](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Arrears_and_expiration).
