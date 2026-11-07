---
title: "Billing overview"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Billing_overview"
---

This topic describes the billing information for Elastic File Storage (EFS).

<span id="yfET7G4W"></span>
## Billing method


|**Billing method** |**Note** |
|---|---|
|Pay\-as\-you\-go |Postpaid billing, where usage is charged after consumption. |


<span id="TmmMddyp"></span>
## Billable item


|**Billable item** |**Note** |
|---|---|
|Storage capacity |Charges are based on actual usage (peak value). |
|Provisioned Bandwidth |If you set provisioned bandwidth mode for an EFS file system instance, you need to configure provisioned bandwidth for it. The provisioned bandwidth fees will generate accordingly. |
|Burst Bandwidth |When an EFS file system instance enables burst bandwidth, if the peak bandwidth exceeds max(baseline bandwidth, provisioned bandwidth), burst bandwidth fees are generated. |


<span id="Yn9b6fFz"></span>
## Billing cycle

EFS tracks the usage on an hourly basis and generates bills based on the usage.

<span id="xm8ffe4i"></span>
## Billing formula

<span id="1buUAAKL"></span>
### Storage capacity billing formula


* EFS is billed based on the standard storage capacity and length of time. Fees are settled hourly based on the peak storage capacity for that hour.

* The unit price for storage capacity is USD/GiB/month. In practice, the system converts USD/GiB/month into USD/GiB/hour. The conversion formula is: hourly unit price = monthly unit price ÷ 30 (days) ÷ 24 (hours).

* **Hourly storage capacity fee calculation formula: hourly storage capacity fee = peak storage capacity of the hour × monthly unit price ÷ 30 (days) ÷ 24 (hours)** .


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Storage capacity is calculated in binary units. For example, 1 GiB = 1,024 MiB.</div>


<span id="gCKuwr6X"></span>
### Provisioned bandwidth billing formula


* EFS calculates fees based on the configured provisioned bandwidth value and length of time. Configuration changes are supported, and fees are settled hourly.

* The unit price for provisioned bandwidth is USD/MB/s/month. In practice, the system converts USD/MB/s/month into USD/MB/s/hour. The conversion formula is: hourly unit price = monthly unit price ÷ 30 (days) ÷ 24 (hours).

* File system instances using provisioned bandwidth mode also share baseline bandwidth from storage capacity without extra cost. Therefore, when calculating the provisioned bandwidth fee, only the bandwidth that exceeds the baseline bandwidth is charged.

   <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260512034422-1612609441874.png) </span>

   * When provisioned bandwidth \> hourly baseline bandwidth peak: provisioned bandwidth to be charged = provisioned bandwidth \- hourly baseline bandwidth peak.

   * When provisioned bandwidth ≤ hourly baseline bandwidth peak: provisioned bandwidth to be charged = 0.

* Hourly costs formula for provisioned bandwidth: **hourly provisioned bandwidth costs = billable provisioned bandwidth for the hour × monthly unit price ÷ 30 (days) ÷ 24 (hours)** .


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Provisioned bandwidth is calculated in decimal units. For example, 1 GB/s = 1000 MB/s.</div>


<span id="P4yE3PWo"></span>
### Burst bandwidth billing formula


* EFS calculates fees based on the actual burst bandwidth value and length of time. Fees are settled hourly.

* The unit price for burst bandwidth is USD/MB/s/month. In practice, the system converts USD/MB/s/month into USD/MB/s/hour. The conversion formula is: hourly unit price = monthly unit price ÷ 30 (days) ÷ 24 (hours).

* For file system instances with burst bandwidth enabled, when the instance bandwidth peak exceeds max(baseline bandwidth value, provisioned bandwidth value), burst bandwidth fees are generated.

   <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260513083322-1499131991195.png) </span>

* Hourly costs formula for burst bandwidth: **hourly burst bandwidth costs= burst bandwidth usage for the hour × monthly unit price ÷ 30 (days) ÷ 24 (hours)** .


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Burst bandwidth is calculated in decimal units. For example, 1 GB/s = 1000 MB/s.</div>
