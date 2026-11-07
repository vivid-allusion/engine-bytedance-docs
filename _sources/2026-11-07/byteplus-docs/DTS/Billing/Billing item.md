---
title: "Billing item"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/billing_items"
---

This topic describes the specific billing items and billing rules of Database Transmission Service (DTS).

<span id=".5pWw5o2u6L-B56e75Lu75Yqh6K6h6LS56aG5"></span>
## Billing items for the data migration task


|**Billing item** |**Billing method** |**Billing cycle** |**Description** |
|---|---|---|---|
|Link configuration fee |Pay\-as\-you\-go |The billing cycle is 1 hour, and the fee will be automatically deducted from your account balance. |* The fee is charged only when incremental migration is performed for the migration task, and no fee is charged during full migration, user migration, and database & table schema migration.<br><br>* During the promotional period, you can create cloud migration tasks from non\-BytePlus instances to BytePlus instances free of charge. After the promotion, these tasks will be billed according to the standard pricing for the configured link.<br><br>* You can create full data migration tasks for free.<br><br>* No fees are incurred in the following scenarios:<br><br>   * No fees are incurred if the task fails to create.<br><br>   * No charges are incurred during the suspension of a data migration task.<br><br>   * When a task has started billing, no fee will be charged if the migration fails. |
|Public network traffic fees |Pay\-as\-you\-go |Currently no charge. |Currently no charge. |
|Private network traffic fee |Pay\-as\-you\-go |Currently no charge. |Currently no charge. |


<span id=".5pWw5o2u5ZCM5q2l5Lu75Yqh6K6h6LS56aG5"></span>
## Billing items for the data synchronization task


|**Billing item** |**Billing method** |**Billing cycle** |**Description** |
|---|---|---|---|
|Link configuration fee |Pay\-as\-you\-go |The billing cycle is 1 hour, and the fee will be automatically deducted from your account balance. |* For a synchronization task, billing for the sync link begins once incremental synchronization starts, including periods when it is suspended.<br><br>* Billing continues during the suspension of a data synchronization task. No fee is charged for a failed task creation.<br><br>* When a task has started billing, no fee will be charged if the synchronization fails. |
||Subscription |Purchased on a monthly basis. |The fee is deducted immediately after purchase. |
|Public network traffic fees |Pay\-as\-you\-go |Currently no charge. |Currently no charge. |
|Private network traffic fee |Pay\-as\-you\-go |Currently no charge. |Currently no charge. |


<span id=".5pWw5o2u6K6i6ZiF5Lu75Yqh6K6h6LS56aG5"></span>
## Billing items for the data subscription task


|**Billing item** |**Billing method** |**Billing cycle** |**Description** |
|---|---|---|---|
|Link configuration fee |Pay\-as\-you\-go |The billing cycle is 1 hour, and the fee will be automatically deducted from your account balance. |* Billing starts after the subscription task is started.<br><br>* Billing continues during the suspension of a data subscription task. No fee is charged for a failed task creation.<br><br>* After the task starts billing, no fee is charged if the task subscription fails. |
||Subscription |Purchased on a monthly basis. |The fee is deducted immediately after purchase. |
|Public network traffic fees |Pay\-as\-you\-go |Currently no charge. |Currently no charge. |
|Data traffic fee |Pay\-as\-you\-go |Currently no charge. |Currently no charge. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<span id=".5pWw5o2u5qCh6aqM5Lu75Yqh6K6h6LS56aG5"></span>
## <div data-tips="true" data-tips-type="warning">DTS does not charge for the data consumption link of the RocketMQ version of the message queue for BytePlus AIDAP for PostgreSQL at this time.</div>


<span id="11XstmaU"></span>
## Billing items for the data verification task


|**Billing item** ||**Billing method** |**Billing cycle** |**Description** |
|---|---|---|---|---|
|Full verification |Content verification |Pay\-as\-you\-go |The billing cycle is 1 hour, and the fee will be automatically deducted from your account balance. |For more information, refer to [Billing method for data verification task](https://docs.byteplus.com/en/docs/DTS/Data_verification_billing_method). |
|Full verification |Row verification |Pay\-as\-you\-go |Currently no charge. ||
|Full verification |Primary key verification |Pay\-as\-you\-go |Currently no charge. ||
|Increment verification ||Pay\-as\-you\-go |The billing cycle is 1 hour, and the fee will be automatically deducted from your account balance. ||
|Schema verification ||Pay\-as\-you\-go |Currently no charge. ||
|Public network traffic fees ||Pay\-as\-you\-go |Currently no charge. ||
|Private network traffic fee ||Pay\-as\-you\-go |Currently no charge. ||
