---
title: "Arrears description"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Arrears_description"
---

AI Native BaaS for Supabase provides services based on the AI Native Database Platform (AIDAP). AIDAP currently supports only pay\-as\-you\-go billing. Under this billing method, bills are issued hourly and settled immediately. If your available balance (including account balance and cash coupons) is less than the bill to be settled, your account is deemed to be in arrears, and you will receive an SMS or email reminder about the insufficient balance. Top up your account and settle outstanding bills within the arrears retention period (7 days). Otherwise, you will be unable to use AI Native Database Platform resources. After the arrears retention period, resources will be forcibly reclaimed and data cannot be restored. You must settle payment for issued bills regardless of whether your resources are frozen or released.

The resource states after arrears at each stage are shown in the table below:


|**Overdue duration** |**tip** |**How to resume** |
|---|---|---|
|Within 2 hours of being overdue |Normal use. |Can be used normally. It is recommended to [recharge](https://console.byteplus.com/finance/renew/) the account to avoid affecting usage after being overdue for more than 2 hours. |
|After being overdue for 2 hours |Unavailable and terminated. The workspace is unavailable in a terminated status.<br><br> |You need to top up your account. Once outstanding bills are settled and the available balance is greater than 0, the instance status automatically returns to **Running**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The EIP bound to the workspace will be automatically released 2 hours after the account becomes overdue. Recharging the account will not restore the binding. You need to re\-enable public network access and associate the EIP with the workspace again. For more details, refer to <a href="https://docs.byteplus.com/en/docs/330/Supabase-Configuring_workspace_public_network_access">Enabling public network access</a>.</div><br> |
|Shut down for 7 days |The workspace is forcibly deleted. |You can only purchase a new workspace after recharging. You cannot continue to use the original one. |
