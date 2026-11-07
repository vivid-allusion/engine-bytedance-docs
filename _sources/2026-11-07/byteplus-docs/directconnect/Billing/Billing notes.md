---
title: "Billing notes"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Billing-overview"
---

When you use BytePlus Direct Connect (DC), you'll encounter fees charged by both BytePlus and non\-BytePlus providers. The diagram below illustrates how these fees are typically structured. For more billing items and formulas, see [Billing items](https://docs.byteplus.com/en/docs/53/10389#ZRSDU6By).


|Biller type |Billing items |Billing notes for Dedicated Lines |Billing notes for Shared Lines |Metering method |
|---|---|---|---|---|
|**Non\-BytePlus** |Optical cable installation fee |This is the cost to install the optical cable that will run between your on\-premises data center and the BytePlus access point. It will be charged by the line operator providing services for you. You need to consult your line operator on pricing and line planning. |This is the cost to install the optical cable that will run between your on\-premises data center and your selected BytePlus partner (also referred to as the line operator). The related fees are charged by the BytePlus partner you choose. You need to contact the partner directly to inquire about the price. |Subject to the billing rules of the actual biller |
||In\-house cable rental fee |When your line operator enters a data center resides in a non\-BytePlus property to install your optical cable, you may be required to pay in\-house cable rental fees to the third\-party property. ||Subject to the billing rules of the actual biller |
||Optical module |BytePlus provides free optical modules of 1 Gbps and 10 Gbps supporting transmission distances of up to 10 km.<br><br>If you need optical modules of 40 Gbps and 100 Gbps, or 1 Gbps and 10 Gbps ones supporting transmission distances over 10 km, prepare them by yourself. |Not applicable |Subject to the billing rules of the actual biller |
|**BytePlus** |[Port occupancy fee](https://docs.byteplus.com/en/docs/53/10389#ZRSDU6By) |The port occupancy fee is charged based on the Port Spec for the Dedicated Line.<br><br>Currently supports only **Subscription**. |Charge the port occupancy fee based on the port specification for the Shared Line.<br><br>Currently supports only **Subscription**.<br><br>**Paid by the actual user (tenant) who uses the Shared line** |Subscription |
||[Outbound traffic fee](https://docs.byteplus.com/en/docs/53/10389#ZRSDU6By) |Charged based on the total outbound traffic from the cloud egressing through the DC Gateway​​.<br><br>Only outbound traffic fees are charged. Inbound traffic is free.<br><br>Currently only supports **Pay\-as\-you\-go**. |Charged based on the total outbound traffic from the cloud egressing through the DC Gateway.<br><br>Only outbound traffic is charged. Inbound traffic is free.<br><br>Currently only supports **Pay\-as\-you\-go**.<br><br>**Paied by the actual user (tenant) who uses the Shared Line** |Pay\-as\-you\-go |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Port occupancy fee</strong> and <strong>Outbound traffic fee</strong> are mandatory billing items for the DC Connection service. To use the DC Connection properly, both the port resources and outbound traffic services must be in an available status.</div>


<span id="ZRSDU6By"></span>
## Billing items

<span id="AfNeKtRD"></span>
### Port occupancy fee

BytePlus charges the port occupancy fee on the access side of the Direct Connect (DC) Connection. Port Occupancy Fee refers to the cost of occupying port resources on the BytePlus access switch when using the DC Connection.


|Topic |Description |
|---|---|
|Metering method |The metering method is **Subscription** for the port occupancy fee. Subscription is a prepaid method. After the DC Connection is completed and reported, you need to pay the full amount upfront for your purchase duration at one time to use the DC service. |
|Formula |**Port occupancy fee per port (USD) = Port Spec unit price (USD/month) × Purchase duration (months)**  |
|Expiration |Subscription resources you have purchased are unaffected by your account balance. After Subscription port resources expire, you can renew or unsubscribe. For details, see [Expiration](https://docs.byteplus.com/en/docs/directconnect/Expiration). |


<span id="6dGDbSam"></span>
### Outbound traffic fee

BytePlus charges the outbound traffic fee on the DC Gateway side. Outbound traffic refers to the total traffic through a single DC Gateway from the cloud to the on\-premises data center.


|Topic |Description |
|---|---|
|Metering method |The metering method is **Pay\-as\-you\-go** for the outbound traffic fee. Pay\-as\-you\-go is a postpaid method that allows you to use resources first and pay for them afterward. In the Pay\-as\-you\-go method, BytePlus calculates the fee based on your actual traffic usage. |
|Formula |**Outbound traffic fee (USD) = Outbound traffic unit price (USD/GB) × Outbound traffic usage (GB)** <br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Outbound traffic fee is charged by account, meaning the bill includes all outbound traffic fees generated by dedicated line gateways across all regions under a single account. You can view fee details in the bill. For detailed instructions, see <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-of-bill-management">Overview of Bill Management</a>.</div><br> |
|Settlement cycle |The billing cycle and period for the outbound traffic fee are calculated and settled hourly. That is, the system issues bills on the hour of each hour (UTC+8), and deducts fees from the account balance according to the bill amount. If the account balance cannot cover issued bills, the account will be in arrears. To avoid service disruption, recharge promptly. For procedure, see [Recharge](https://docs.byteplus.com/en/docs/6269/100434). |
|Arrears |Pay\-as\-you\-go resources will be affected if the account is in arrears. If the platform identifies the current account is in arrears, all Pay\-as\-you\-go resources within this account will be affected. To avoid disruption to your business, settle your overdue payments promptly. For procedure, see [Arrears](https://docs.byteplus.com/en/docs/directconnect/Arrears). |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If your outbound traffic volume is high, you can purchase an Outbound Traffic Package to offset the outbound traffic fees generated by DC Gateways in your account. This option offers better rates than pay\-as\-you\-go billing. For more details, see <a href="https://docs.byteplus.com/en/docs/directconnect/Outbound_Traffic_Package_overview">Outbound Traffic Package overview</a>.</div>


<span id="HiqSifQa"></span>
## Resource pricing

You can check the prices of Dedicated Lines and Shared Lines on the [Pricing calculator](https://www.byteplus.com/en/pricing?product=DirectConnect&tab=2) page, including their billing items (the port occupancy fee and the outbound traffic fee) and related costs. The amount presented by Pricing calculator is for reference only. Specific fees are subject to the amount on the actual order in [the Direct Connect console](https://console.byteplus.com/dc/region:dc+cn-shanghai/PhysicalConnection?).

<span id="wV7Giqcu"></span>
## View bills

You can review the billing details of all cloud resources within your account. Additionally, you can customize the view by configuring fields and applying filters based on various statistical dimensions and time periods. You can also export a complete dataset with all billing fields to meet your specific needs.
