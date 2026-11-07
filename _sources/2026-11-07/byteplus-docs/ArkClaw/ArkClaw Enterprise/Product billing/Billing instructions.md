---
title: "Billing instructions"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Billing_instructions"
---

This topic mainly introduces the billing method of ArkClaw, seat editions/individual Claw instance types, and validity period to help you clearly understand the relevant billing rules.


<card mode="container" href="" iconSet="1" iconSize="" icon="" >

Background

ArkClaw Enterprise supports two space management types: seat management and instance management.


* Spaces of seat management type: Seats are subscribed to and expire as a whole under a unified subscription. Within the purchased seat quota, you can activate and assign Claw instances as needed, and you can also use the managed ModelArk Plans.

* Spaces of instance Management type: There is no "seat" concept. It is managed based on individual Claw instances. All Claw instances under this space must be created, assigned, and managed separately. Different instances have independent validity periods, and managed ModelArk Plans are not supported.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default"><strong>Independent Claw instances can only be purchased if you have enabled the beta feature "space management type" and selected "instance management" as the space management type when activating the ArkClaw space. If needed, please contact your account manager to enable this feature</strong>.</div>


</card>



<span id="BnEEvXWQ"></span>
## Billing method

ArkClaw instances use a  **"subscription"**  prepaid billing method. Fees are charged based on the **seat edition/individual Claw instance type** you select, **quantity**, and **purchase duration**. The relevant fees already include all computing, storage, and network resource costs required for your use of ArkClaw.

> Subscription is a billing method where you pay before using the service. In scenarios where long\-term use of ArkClaw instances is required, you can purchase subscription instances by prepaying for multiple months or years. You can receive more discounts on yearly subscriptions. For the specific discount, see the actual result on the **purchase page**.


<span id="FczjMl5G"></span>
### Value\-added fees

During your use of ArkClaw, if you actively invoke the model service or web search service, separate charges will apply based on a **pay\-as\-you\-go** method.


* Model services: When ArkClaw is configured with the models from Foundation models and actually invokes them, the token consumption fees will be charged by the model service. For detailed billing rules, see [Billing description of model services](https://docs.byteplus.com/en/docs/ModelArk/1544106).

* Web search: When ArkClaw triggers the web search, the fees for `web_search` calls will be charged by the web search service. For detailed billing rules, see [Billing description of web search](https://docs.byteplus.com/en/docs/searchinfinity/Searchinfinity_pricing).


<span id="Q8ldd5U3"></span>
## Seat edition/individual Claw instance type

ArkClaw Enterprise offers a variety of seat editions/instance types to meet the computing and storage needs of different business scenarios. Detailed specifications are shown in the following table:


|Seat edition/individual Claw instance type |Billing unit |CPU |Memory |Volume (exclusive, persistent storage) |Cloud disk |Applicable scenario |Fees (ArkClaw only) |
|---|---|---|---|---|---|---|---|
|Starter edition |arkclaw.starter |2 cores |4 GiB |60 GiB |10 GB |Designed for ‌trials and lightweight tasks‌. It supports basic conversations and limited tool invocations. |62 USD/month |
|Standard edition |arkclaw.standard |4 cores |8 GiB |80 GiB |20 GB |The edition for daily use in production. It supports medium\-complexity workflows and multi\-turn conversations. |124 USD/month |
|Premium edition |arkclaw.premium |8 cores |16 GiB |160 GiB |40 GB |Suitable for complex workloads. It can handle parallel invocations of multiple tools and workflows for medium\-sized projects. |248 USD/month |
|Ultimate edition |arkclaw.ultimate |16 cores |32 GiB |160 GiB |80 GB |Designed for large\-scale projects and high\-load scenarios. It supports end\-to\-end orchestration of complex processes. |496 USD/month |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Seat editions support the purchase of any specification of Coding Plan.</div>


   * <div data-tips="true" data-tips-type="default">Coding Plan Team</div>


      * <div data-tips="true" data-tips-type="default">Coding Plan Team Lite</div>


      * <div data-tips="true" data-tips-type="default">Coding Plan Team Pro</div>


* <div data-tips="true" data-tips-type="default"><strong>Minimum requirement of Purchasing</strong> <strong>CodingPlan</strong>: You can flexibly purchase Coding Plan  seats according to actual needs, but the following total quantity requirements must be met:</div>


   * <div data-tips="true" data-tips-type="default"><strong>When the number of managed CodingPlan seats is less than 5</strong> (such as the first purchase), make sure that the final total number of the <strong>managed</strong> seats reaches 5 or more for this purchase.</div>


   * <div data-tips="true" data-tips-type="default"><strong>When the number of managed CodingPlan seats reaches 5</strong> (such as subsequent purchases), the number of purchased seats is not limited, and you can add seats as needed (add 1 or 2 seats).</div>


* <div data-tips="true" data-tips-type="default"><strong>Billing note</strong>: For the final settlement price of the first purchase or subsequent purchases, refer to the actual order amount on the purchase page.</div>



<span id="g7y5vXvE"></span>
## Validity period

<span id="IozOgqmK"></span>
### Spaces of seat management type

The validity period of ArkClaw is the duration you purchase (based on UTC+8 time). The start of a billing cycle is when the resource is activated (accurate to the second), and the end is at 23:59:59 on the expiration date.

For example, if you purchase a monthly subscription for ArkClaw Starter at 14:00:00 on March 23, 2026, with a purchase duration of 1 month, the billing cycle is: 14:00:00 on March 23, 2026 \- 23:59:59 on April 23, 2026.

<span id="K3fjwg4t"></span>
### Spaces of instance management type

The validity period of each ArkClaw instance is calculated independently based on its own purchase duration. The start of a billing cycle is when the resource is activated, and the end is at 23:59:59 on the expiration date, based on UTC+8 time.

For example, if you purchase a monthly subscription for ArkClaw Starter instance at 14:00:00 on March 23, 2026, with a purchase duration of 1 month, the billing cycle for this instance would be from March 23, 2026 14:00:00 to April 23, 2026 23:59:59.

Different instances have different expiration dates. Renewal or unsubscription operations only affect the corresponding instance and do not affect the validity period of other instances within the same space.
