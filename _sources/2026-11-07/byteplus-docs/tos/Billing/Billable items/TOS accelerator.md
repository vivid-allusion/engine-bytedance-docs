---
title: "TOS accelerator"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/TOS_Accelerator_fee"
---

You are charged for the accelerator capacity and provisioned bandwidth when you use the TOS accelerator feature. This topic explains how you are charged for TOS accelerator.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">This topic only provides a description of billable items. For specific prices, see <a href="https://www.byteplus.com/en/pricing?product=TOS&tab=1">TOS pricing details</a>.</div>


* <div data-tips="true" data-tips-type="default">Storage capacity is calculated in binary units. For example, 1 GiB equals 1,024 MiB.</div>


* <div data-tips="true" data-tips-type="default">Provisioned bandwidth is calculated in decimal units. For example, 1 GB/s equals 1,000 MB/s.</div>


* <div data-tips="true" data-tips-type="default">Currently, only Asia Pacific (Johor) region is supported. If you need to use TOS accelerator in another region, please contact your account manager for assistance.</div>



<span id="kPxRLKZj"></span>
## Billable item


|**Billable item** |**Description** |**Formula** |
|---|---|---|
|TOS accelerator read\-only cache\-basic300\-Storage |When using a TOS accelerator in read\-only cache mode, you are charged based on the applied capacity, regardless of how much data is stored. |**Pay\-as\-you\-go**: Hourly storage cost = Applied capacity (GiB) × Monthly rate ÷ 30 (days) ÷ 24 (hours) |
|TOS accelerator read/write cache\-basic125\-Storage |When using TOS accelerator in read/write cache mode, you are charged based on the storage usage and time of use. You are billed hourly for each hour of peak storage usage. |**Pay\-as\-you\-go**: Storage cost for a given hour= Peak storage usage of the hour (GiB) × Monthly rate ÷ 30 (days) ÷ 24 (hours) |
|TOS accelerator read/write cache\-basic125\-Provisioned bandwidth |When using TOS accelerator in read\-write cache mode with provisioned bandwidth enabled, you are charged based on the amount of provisioned bandwidth applied and how long it is used for. This fee is settled once per hour.<br><br>If you enable provisioned bandwidth for your TOS accelerator, the baseline bandwidth provided by the accelerator capacity is free. You are only billed for the portion of provisioned bandwidth that exceeds the baseline. The billable provisioned bandwidth for a given hour is calculated as follows:<br><br><br>* Provisioned bandwidth \> Peak baseline bandwidth of the hour: Billable provisioned bandwidth = Provisioned bandwidth applied \- Peak baseline bandwidth of the hour.<br><br>* Provisioned bandwidth <= Peak baseline bandwidth of the hour: Billable provisioned bandwidth = 0. |**Pay\-as\-you\-go**: Provisioned bandwidth cost for a given hour = Billable provisioned bandwidth of the hour (MB/s) × Monthly rate ÷ 30 (days) ÷ 24 (hours) |


<span id="4I2NwDYI"></span>
## Example

Suppose you create an accelerator in read/write cache mode with provisioned bandwidth enabled. The default performance density is 125 MB/s per TiB. During a given hour, the peak storage usage is 10 TiB, and the provisioned bandwidth for that hour is 2 GB/s. The fees incurred during this hour total approximately $3.6356. The billing details are as follows:


|Billable item |Unit price |Length of time |Formula |Total cost |
|---|---|---|---|---|
|TOS accelerator read\-only cache\-basic125\-Storage |0.187 $/GiB/month |1 hour |* Billable storage usage = 10 TiB = 10,240 GiB<br><br>* Storage cost = Peak storage usage × Monthly rate ÷ 30 (days) ÷ 24 (hours) = 10,240 × 0.187 ÷ 30 ÷ 24 = $2.6596 |Total cost =<br><br>Storage cost + Provisioned bandwidth cost = $2.6596 + $0.976 = $3.6356 |
|TOS accelerator read/write cache\-basic125\-Provisioned bandwidth |0.937 $/MB/s/month |1 hour |* Peak baseline bandwidth = 10 TiB × 125 MB/s/TiB = 1,250 MB/s<br><br>* Billable provisioned bandwidth = 2,000 MB/s \- 1,250 MB/s = 750 MB/s<br><br>* Provisioned bandwidth cost = Billable provisioned bandwidth × Unit price ÷ 30 (days) ÷ 24 (hours) = 750 × 0.937 ÷ 30 ÷ 24 = $0.976 ||


&nbsp;
