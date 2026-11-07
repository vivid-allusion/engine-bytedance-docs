---
title: "Billing items"
product: "TRAE"
product_code: "trae"
source: "https://docs.byteplus.com/en/docs/trae/billing-items"
---

TRAE Enterprise includes three billing items: seat, pay\-as\-you\-go billing, and resource package.

<span id="7f10d321"></span>
## Seat

The seat is the basic sales unit of TRAE Enterprise. The unit price per seat and the minimum purchase quantity vary by plan type. When purchasing a plan, fees are charged based on the actual number of seats purchased.

The enterprise can add members in TRAE equal to the number of seats purchased. When the maximum number of seats is reached, new members cannot be invited to join the enterprise.

<span id="e7331ea8"></span>
### Seat built\-in features

The following features are included with each seat:


|**Feature** |**Quota** |
|---|---|
|Agent / Chat |Billed by token. The corresponding amount is deducted according to the list price of the model. |
|Completion |Billed by token. |
|Inline Chat |Unlimited |
|Fast Apply |Unlimited |
|AI Fix |Unlimited |


<span id="f636f13e"></span>
### Seat release rules

When a member is removed, whether their seat can be released depends on the amount of tokens they have consumed in AI chats during the current month:


* **Consumption ≤ 1 million**: The seat will be released immediately. You can invite a new member to join.

* **Consumption \> 1 million**: The seat will be released in the following month. You can invite a new member to join at that time.


<span id="ca1216e2"></span>
### Seat cancellation

After canceling a seat, the member who previously occupied the seat will no longer be able to use TRAE Enterprise. For specific cancellation rules, refer to "[Unsubscription Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management)".

<span id="639b5749"></span>
## Pay\-as\-you\-go billing

Once pay\-as\-you\-go billing is enabled, if your enterprise's resource usage exceeds the quota included in the subscribed plan, any subsequent LLM usage will be billed based on the actual number of tokens consumed.

<span id="627c2ff6"></span>
### Important notes

Pay\-as\-you\-go billing is settled on an hourly post\-payment basis, so there may be an hourly delay in invoicing. The account will only enter an overdue status after the billing and deduction process has been completed. Before that, the enterprise can continue to use the TRAE Enterprise normally, while additional charges may continue to accrue.

<span id="098690e8"></span>
### **Billing formula**

For large language models, a token is the basic unit of text processing, which can represent a word, a character, or a subword fragment.

In pay\-as\-you\-go billing, all built\-in models of TRAE Enterprise are charged based on token usage. Using GPT models as an example, the billing formula is as follows:

GPT model service fee = (input token usage × input token unit price) + (output token usage × output token unit price) + (cache read token usage × cache read token unit price)

<span id="2a3ac85e"></span>
### **Model pricing**

The following table shows pricing for all built\-in models of TRAE Enterprise:


|**Model Name** |**Context Length** |**Input**<br><br>USD / million tokens |**Cache Read**<br><br>USD / million tokens |**Output**<br><br>USD / million tokens |
|---|---|---|---|---|
|GPT\-5.4 |<=272k |$2.500 |$0.250 |$15.000 |
||\>272k |$5.000 |$0.500 |$22.500 |
|GPT\-5.2 |\- |$1.750 |$0.175 |$14.000 |
|Gemini\-3.1\-Pro\-Preview |<=200k |$2.000  |$0.200  |$12.000 |
||\>200k |$4.000  |$0.400  |$18.000  |
|Gemini\-3\-Flash\-Preview |\- |$0.500 |$0.050 |$3.000 |
|GLM\-4.7 |\- |$0.600 |$0.110 |$2.200 |
|MiniMax\-M2.7 |\- |$0.300 |$0.060 |$1.200 |
|Kimi\-K2.5 |\- |$0.600 |$0.120 |$3.000 |
|DeepSeek\-V3.2 |[0k, 32k] |$0.280 |$0.056 |$0.420 |
| |(32k, 128k] |$0.560 |$0.056 |$0.840 |


<span id="4dac9fd6"></span>
## Resource package

A resource package is a prepaid package that provides additional usage credits. When the quota included in the plan is exhausted, the enterprise administrator can purchase resource packages to ensure that members can continue using AI features in TRAE Enterprise. Charges are calculated based on the actual token usage and the list price of the model used, and are deducted from the balance of resource packages.

The details of the resource package are as follows:


* Available resource package amounts: USD 10, USD 100, and USD 1,000. 

*  Each resource package is valid for 12 months and takes effect immediately upon purchase. 

*  After purchasing a resource package, pay\-as\-you\-go billing is enabled by default. Once the resource package balance is depleted, billing will automatically switch to pay\-as\-you\-go. 

*  Multiple resource packages can be purchased, and their balances will be accumulated automatically. 

*  If multiple resource packages are active at the same time, the system will consume the package with the earliest expiration date first. 

*  Resource packages are non\-refundable once purchased. 

*  After the subscribed plan expires, any remaining resource package balance can no longer be used, even if the package has not yet expired.


For information on how to purchase a resource package, refer to [Purchase resource packages](https://docs.byteplus.com/docs/trae/purchase-resource-packages).

<span id="90d27b5e"></span>
## Quota consumption order

When members use LLMs in TRAE Enterprise, available quotas are consumed in the following order:


1.  ** In\-plan quota** – The quota included with each seat in the subscribed plan is consumed first. 

2.  **Resource package** – Once the in\-plan quota is exhausted, usage is deducted from resource package balances (with the package that expires first being consumed first). 

3.  **Pay\-as\-you\-go billing** – After all resource package balances have been exhausted, usage will automatically be billed on a pay\-as\-you\-go basis, unless pay\-as\-you\-go billing has been disabled by the enterprise.


<span id="884417bb"></span>
## Service suspension for overdue enterprises

Seats are billed on a prepaid basis. If an enterprise account becomes overdue during the subscription period, TRAE will not suspend the features and benefits of the plan the enterprise has subscribed to, and members can continue to log in to and use TRAE Enterprise normally.

Pay\-as\-you\-go billing follows a postpaid model. If a billing deduction fails after invoicing, resulting in an overdue account, TRAE will automatically suspend pay\-as\-you\-go billing 2 hours after the account becomes overdue. At that point, the enterprise will no longer be able to use this service.

Once the enterprise has topped up the account for enough balance, pay\-as\-you\-go billing will be restored.
