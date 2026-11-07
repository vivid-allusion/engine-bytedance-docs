---
title: "Billing overview"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/Billing-overview"
---

Bandwidth Package supports four metering methods: Pay\-by\-bandwidth, Pay\-by\-main\-traffic, Pay\-by\-95th\-peak, and Subscription. You can select the appropriate method based on your current requirements.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Pay\-by\-95th\-peak is in the beta stage. To request a trial, please contact your account manager.</div>



<span id=".6K6h6LS55pa55byP5a-55q-U"></span>
## Comparison of metering methods


|Metering method |Payment time |Settlement cycle |Recommended scenarios |
|---|---|---|---|
|Pay\-by\-bandwidth |Postpaid |Hour<br><br>> The system settles the fees for the previous hour on the hour (UTC+8). |Applicable to services with temporary resource use and stable bandwidth |
|Pay\-by\-main\-traffic |Postpaid |Hour<br><br>> The system settles the fees for the previous hour on the hour (UTC+8). |Applicable to services with temporary resource use and unstable or unpredictable bandwidth |
|Pay\-by\-95th\-peak |Postpaid |Calendar month<br><br>> The billing data for the previous month becomes available after 12:00 on the 2nd calendar day of each month. For more information, see [Bill management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-bill-details). |Applicable to services with large and frequent bandwidth fluctuations |
|Subscription |Prepaid |Non\-calendar month |Applicable to services with stable peak bandwidth and long\-term use of Bandwidth Package |


<span id=".6K6h6LS55oC76KeI"></span>
## Billing


|Billing method |Metering method |Formula |
|---|---|---|
|Pay\-as\-you\-go |[Pay-by-bandwidth](https://docs.byteplus.com/en/docs/bandwidthpackage/Pay-by-bandwidth) |Bandwidth Package fee = Bandwidth unit price (USD/hour per Mbps) × Maximum bandwidth (Mbps) × Usage duration (hours) |
||[Pay-by-main-traffic](https://docs.byteplus.com/en/docs/bandwidthpackage/Pay-by-domain-traffic) |Bandwidth Package fee = Traffic unit price (USD/GB) × Main traffic (GB) |
||[Pay-by-95th-peak](https://docs.byteplus.com/en/docs/bandwidthpackage/Pay-by-traditional-95th-percentile) |Bandwidth Package fee = MAX [(Monthly 95th peak × Effective days of 95th peak / Billing month days), (Monthly guaranteed bandwidth × Effective days of guarantee / Billing month days)] × Monthly bandwidth unit price |
|Subscription |[Subscription](https://docs.byteplus.com/en/docs/bandwidthpackage/Subscription) |Bandwidth Package fee = Bandwidth unit price (USD/month per Mbps) × Maximum bandwidth (Mbps) × Usage duration (months) |


<span id=".6K6h6LS55paH5qGj566A5LuL"></span>
## Billing documentation

<span id=".5oyJ6YeP6K6h6LS5"></span>
### Pay\-as\-you\-go

You can understand all aspects of pay\-as\-you\-go billing for Bandwidth Package by seeing the documentation listed below.


|Billing documentation |Description |
|---|---|
|[Pay-by-bandwidth](https://docs.byteplus.com/en/docs/bandwidthpackage/Pay-by-bandwidth) |Introduces the details of Pay\-by\-bandwidth. |
|[Pay-by-main-traffic](https://docs.byteplus.com/en/docs/bandwidthpackage/Pay-by-domain-traffic) |Introduces the details of Pay\-by\-main\-traffic. |
|[Pay-by-95th-peak](https://docs.byteplus.com/en/docs/bandwidthpackage/Pay-by-traditional-95th-percentile) |Introduces the details of Pay\-by\-95th\-peak. |
|[Billing conversion](https://docs.byteplus.com/en/docs/bandwidthpackage/Billing-methods-change) |Introduces the fees and procedure for billing conversion. |
|[Specification changes](https://docs.byteplus.com/en/docs/bandwidthpackage/Bandwidth-modifications) |Introduces the changes in fees when modifying the maximum bandwidth. |
|[Arrears](https://docs.byteplus.com/en/docs/bandwidthpackage/Arrears) |Introduces the status changes of resources due to account arrears. |


<span id=".5YyF5bm05YyF5pyI"></span>
### Subscription

You can understand all aspects of subscription billing for Bandwidth Package by seeing the documentation listed below.


|Billing documentation |Description |
|---|---|
|[Subscription](https://docs.byteplus.com/en/docs/bandwidthpackage/Subscription) |Introduces the billing items, settlement cycle, and fee formulas. |
|[Billing conversion](https://docs.byteplus.com/en/docs/bandwidthpackage/Billing-methods-change) |Introduces the fees and procedure for billing conversion. |
|[Specification change](https://docs.byteplus.com/en/docs/bandwidthpackage/Bandwidth-modifications) |Introduces the impact on fees when modifying the maximum bandwidth. |
|[Renewal](https://docs.byteplus.com/en/docs/bandwidthpackage/Renewal) |Introduces the features of renewal. |
|[Unsubscription](https://docs.byteplus.com/en/docs/bandwidthpackage/Unsubscription) |Introduces the features of unsubscription. |
|[Expiration](https://docs.byteplus.com/en/docs/bandwidthpackage/Expiration) |Introduces the expiration\-related status of resources. |


<span id=".5YWs572RSVAvSVB2NuWFrOe9keW4puWuveS-p-iuoei0ueWPmOWMlg=="></span>
## Billing changes for elastic IP address/IPv6 Internet bandwidth

When an Elastic IP Address (EIP)/IPv6 Internet bandwidth is added to or removed from a Bandwidth Package, the billing changes for the EIP/IPv6 Internet bandwidth are as follows:


|Cloud resource |EIP metering method |Billing item |Add to Bandwidth Package |Remove from Bandwidth Package |
|---|---|---|---|---|
|EIP |Pay\-by\-bandwidth |IP config fee |Unchanged ||
|||Bandwidth fee |No charge |Charge |
||Pay\-by\-data\-transfer |IP config fee |Unchanged ||
|||Traffic fee |No charge |Charge |
|IPv6 Internet bandwidth |Pay\-by\-bandwidth |Bandwidth fee |No charge |Charge |
||Pay\-by\-data\-transfer |Traffic fee |No charge |Charge |
