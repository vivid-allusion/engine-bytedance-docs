---
title: "Arrears and expiration"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/expiration_or_arrears_instructions"
---

To ensure normal operation of your services, you need to renew or recharge in time after the Database Transmission Service (DTS) task expires or is overdue. This topic describes the arrears and expiration of Database Transmission Service (DTS).

<span id=".5qyg6LS56K-05piO"></span>
## Arrears


* Pay\-as\-you\-go task

   Recharge and settle the overdue bills within 7 days, otherwise you will not be able to use the DTS resources. Beyond the retention period, resources will be forcibly recycled, and the related data can not be recovered. Regardless of whether your task resources are frozen or released, you should settle the fees on the issued bill.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For pay\-as\-you\-go tasks, the platform issues bills on an hourly basis and deducts fees in real time after the bill is issued. If the available balance (including account balance and cash coupons) in your account is less than the amount specified in the bill to be settled, your account is deemed to be overdue, and you will receive an SMS or email reminder about the insufficient balance.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the account is overdue, the pay\-as\-you\-go task will display <strong>Suspended for arrears</strong> under <strong>Billing method</strong> in the task list. Currently, the task only supports deletion and termination actions.   </div>
   

   The status of resources for each stage after arrears is as follows:



|**Time in arrears** |**Description** |**Subsequent operations** |
|---|---|---|
|Within 2 hours of arrears |The task is running normally. |Go to [Billing center](https://console.byteplus.com/finance/account-overview) to top up the current account. |
|After 2 hours of arrears |The task is unavailable and will be suspended. In the suspended state, the task only supports deletion and termination operations. |Go to [Billing center](https://console.byteplus.com/finance/account-overview) to top up the current account. After the overdue bill is settled and the available quota is greater than USD 0, the task status will automatically return to **In progress**. |
|After 7 days of suspension |The task is forcibly deleted. |It can not be retrieved. |



* Subscription task

   Even if the account is overdue, you can still use the purchased DTS subscription task normally. However, before making up the outstanding fees, you can not perform new task purchases or renewal operations.


<span id=".5Yiw5pyf6K-05piO"></span>
## Expiration

Only subscription tasks are affected by expiration. There is no limit on the usage duration for pay\-as\-you\-go tasks. You only need to ensure that your account has sufficient balance. The state of resources for each stage after expiration is as follows:


|**Expiration time** |**Description** |**Subsequent operations** |
|---|---|---|
|Due until 12:00 on the second day |**Billing method** will be displayed as **Expired**, but the task status is still **In progress**. The task can be used normally. |Renew a subscription task. For more information, refer to [Renewal management](https://docs.byteplus.com/en/docs/DTS/renewal_management). |
|Within 7 days after expiration |**Billing method** will be displayed as **Expired**, and the task status is **Suspended**. The task is unavailable. |To renew subscription for a suspended task, refer to [Renewal management](https://docs.byteplus.com/en/docs/DTS/renewal_management) for detailed instructions.<br><br>Upon renewal, the task status will automatically return to **In Progress**. |
|After 7 days expiration |The task is forcibly deleted. |It can not be retrieved. |
