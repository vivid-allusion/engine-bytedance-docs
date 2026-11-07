---
title: "View the usage of your enterprise"
product: "TRAE"
product_code: "trae"
source: "https://docs.byteplus.com/en/docs/trae/view-enterprise-usage"
---

In the [TRAE Enterprise Console](https://console.enterprise.trae.ai/), go to **Enterprise configuration** \> **Usage management** panel to view the actual usage for the enterprise as a whole, each member, and each conversation.

<span id="602f0e7b"></span>
## **View your enterprise's overall usage**

In the usage cards on top of the **Usage Dashboard** tab, you can view the overall usage of your enterprise, including usage for TRAE built\-in models and enterprise built\-in models. 

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/431d1f1ce3cb4fb79c4b278481809759) </span>

For TRAE built\-in models, you can view the following data:


|**Statistic** |**Description** |
|---|---|
|Overall usage |During the current billing cycle, the overall amount consumed by your enterprise for all sessions, including basic usage and excess usage. |
|Basic usage |During the current billing cycle, the amount consumed from the built\-in basic usage quota of the seats purchased. |
|Excess usage |During the current billing cycle, the amount consumed after exceeding the basic usage quota, including the usage from resource packages and pay\-as\-you\-go service. |


For enterprise built\-in models, you can view the overall token usage for each model.

<span id="cb4c3dc6"></span>
## View usage by member

In the **Member usage** area of the **Usage Dashboard** tab, you can view the usage for each member, including:


|**Statistic** |**Description** |
|---|---|
|Total current cycle usage (USD)  |During the current billing cycle, the amount consumed by the member for all sessions, including basic usage and excess usage. |
|Base session usage (USD)  |During the current billing cycle, the amount consumed by the member from the basic usage quota. The number on the left represents actual usage, and the number on the right represents the usage quota set by the administrator for the member. |
|Excess session usage (USD)  |During the current billing cycle, the additional amount consumed by the member after exceeding the basic usage quota, including usage from resource packages and pay\-as\-you\-go service. |


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/3464b1bb4a0c4306a7ec1fcc50a5aee0) </span>

When a member currently has an unexpected usage, you can modify the quota for the member:


1. In the **Actions** column, click **Modify quota**.

2. In the Designated member quota modification popup, modify the member's excess usage limit.


To restore a member's usage limit to the default setting, click  **···**  \> **Clear single quota** in the **Actions ** column. 

<span id="05e7ecf1"></span>
## View usage by session

In the **Usage Details** tab, you can view the usage details for each complete session within your enterprise.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">Currently, only usage details for TRAE built\-in models can be viewed.</div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a049022eda7f445cbeaa01380e3ba4c9) </span>

Field descriptions are as follows:


|**Field** |**Description** |
|---|---|
|Time |The time when the session occurred. |
|Member |The username and email address of the member who initiated the session. |
|Client |The client where the session occurred: TRAE IDE or TRAE plugins. |
|TRAE Built\-in Model |The TRAE built\-in model used in the session. |
|Session ID |The unique identifier for each complete session. Double\-click the TRAE avatar in the session flow to view detailed information. |
|Token Consumption |The total number of tokens consumed in each complete session. To view detailed input and output data, you need to export the usage data. |
|Amount Spent |The amount corresponding to the total number of tokens consumed in each complete session. Calculated based on the list price of the invoked model. |
|Model Calls |The total number of times the model is called in each complete session. |
|Consumption Source |The source of token and amount consumption: basic usage or excess usage. |
