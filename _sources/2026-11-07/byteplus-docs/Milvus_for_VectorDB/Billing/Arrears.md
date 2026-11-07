---
title: "Arrears"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Arrears"
---

If the available credit, including account balance and vouchers, in your account is less than the bill to be settled, your account will be considered in arrears, and you will receive an SMS or email notification of low balance. You can view the arrears details by referring to [Billing management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-bill-details).

## Overdue explanation

Volcengine regularly checks whether your account balance is sufficient to cover all orders and bills for products and services on the platform. If your account balance is insufficient or below zero, it is considered in arrears. When your account is in arrears, Volcengine will send arrears notifications to you through methods including but not limited to internal messages and emails.

After the account is overdue, the instance enters a retention period with restricted usage. After the retention period expires, the instance will be forcibly reclaimed. Resources cannot be recovered once reclaimed. Please recharge and settle the overdue bill within the specified time (before the resource is forcibly reclaimed) to avoid interruption in using Milvus for VectorDB resources. After you settle the bills, the Milvus for VectorDB instance suspended due to the bills will automatically start and enter the **Running** state.

> **tip**

* > When the account is in arrears, you must settle overdue bills and confirm that the available credit in your account, including account balance and vouchers, is at least USD 100. Otherwise, you cannot create a Milvus for VectorDB instance.

* > Regardless of whether your resources are frozen or released, you should settle billed fees based on the actual amount.

## **Pay\-as\-you\-go instances**

For pay\-as\-you\-go instances, the platform bills hourly and deducts in real time after billing. If your available credit, including account balance and vouchers, is less than the bill amount to settle, your account will be considered in arrears, and you will receive SMS or email notifications of about insufficient balance.

The following table describes the resource status at each stage after your account is in arrears.

|**Duration of arrears** |**Description** |
|---|---|
|Within 2 hours after being in arrears |The instance is usable, and billing proceeds normally. |
|2 to 170 hours after being in arrears |The billing type becomes In arrears. The instance is in the Suspended state and cannot be used. During this period, no billing occurs for the instance.<br><br>You need to top up your account in the [Billing center](https://console.byteplus.com/finance/account-overview/). Once you settle the overdue bills and the available credit is greater than 0, the instance status will become Running. |
|After 170 hours after being in arrears |The instance will be deleted, and all nodes and data of the instance will be permanently cleared and cannot be recovered. |

## **Subscription instances**

Even if your account is in arrears, you can still use subscription instances you have purchased. However, before settling the overdue bills, you cannot create new instances or renew existing instances.

### **Expiration**

Only subscription instances are affected by due status. Pay\-as\-you\-go instances have no usage time limit; you only need to ensure your account has sufficient balance.

The resource status at each stage after due date is shown in the table below:

|**Expiration time** ||**Impact** |**Operation** |
|---|---|---|---|
|15 days after the due date |By 12:00 the next day after due date |The billing type becomes **Expired**. The instance status remains **Running**, and the instance is usable. |You need to renew the instance. For detailed steps, see [Renew subscription instances](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Renew_a_subscription_instance). |
||From 12:00 next day after due date to 15 days |The billing type becomes **Overdue**. The instance is in the **Suspended** state and cannot be used. |You need to renew the instance. Then, the instance status automatically returns to running. |
|15 days after the due date ||All nodes and data of the instance will be permanently cleared. |Cannot be restored. |

## Pay\-as\-you\-go storage

You are billed for storage space hourly based on the total used storage capacity. This method applies to the same rules as pay\-as\-you\-go. If the available credit, including account balance and vouchers, in your account is less than the bill to be settled, your account will be considered in arrears, and you will receive an SMS or email notification of low balance.

The following table describes the resource status at each stage after your account is in arrears.

|**Duration of arrears** |**Description** |
|---|---|
|Within 2 hours after being in arrears |The instance is usable, and billing proceeds normally. |
|2 to 170 hours after being in arrears |The billing type becomes **In arrears**. The instance is in the **Suspended** state and cannot be used. During this period, no billing occurs for the instance.<br><br>You need to top up your account in the [Billing center](https://console.byteplus.com/finance/account-overview/). Once you settle the overdue bills and the available credit is greater than 0, the instance status will become Running. |
|After 170 hours after being in arrears |The instance is forcibly deleted, and data cannot be restored. |
