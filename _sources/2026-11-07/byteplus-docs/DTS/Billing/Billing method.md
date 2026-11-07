---
title: "Billing method"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/billing_methods"
---

Database Transmission Service (DTS) supports different billing methods for different task types. This topic describes the billing methods supported by DTS.


|**Billing method** |**Supported task types** |**Description** |
|---|---|---|
|Pay\-as\-you\-go |* Data migration task<br><br>* Data synchronization task<br><br>* Data subscription task<br><br>* Data verification task |* This is a post\-payment mode that bills based on the actual amount of resources used, without the need to purchase resources in advance.<br><br>* It is suitable for short\-term use and business scenarios with large instantaneous fluctuations in business volume. It can be released immediately after use, saving costs.<br><br>* When configuring a migration task<br><br>   * You can create a full data migration task for free.<br><br>   * During the promotional period, you can create cloud migration tasks from non\-BytePlus instances to BytePlus instances free of charge. After the promotion, these tasks will be billed on a pay\-as\-you\-go basis.<br><br>   * No charges are incurred during the suspension of a data migration task.<br><br>   * When a task has started billing, no fee will be charged if the migration fails.<br><br>* When configuring a subscription task<br><br>   * Billing for a data subscription task will start after the task is launched.<br><br>   * Billing continues during the suspension of a data subscription task.<br><br>   * When a task has started billing, no fee will be charged if the subscription fails.<br><br>* When configuring a synchronization task<br><br>   * For a synchronization task, billing for the sync link begins once incremental synchronization starts, including periods when it is suspended.<br><br>   * Billing continues during the suspension of a data synchronization task.<br><br>   * When a task has started billing, no fee will be charged if the synchronization fails.<br><br>* When configuring a data verification task<br><br>* For more information about data verification task billing, refer to [Billing method for data verification task](https://docs.byteplus.com/en/docs/DTS/Data_verification_billing_method). |
|Subscription |* Data synchronization task<br><br>* Data subscription task |* The prepaid model requires payment before resource usage, meaning fees are paid at the time of task creation.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the source or target instances expire and become non\-functional, DTS may still maintain a connection. To prevent ongoing charges, promptly adjust or release your DTS tasks.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">It is best suited for business scenarios with stable traffic that require long\-term resource usage. It is more cost\-effective than pay\-as\-you\-go models, with longer commitments resulting in greater discounts.</div><br> |


&nbsp;

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can view the estimated cost of a specific task in the price calculator. For more information, refer to <a href="https://www.byteplus.com/en/pricing?product=DTS&tab=2">DTS price calculator</a>.</div>
