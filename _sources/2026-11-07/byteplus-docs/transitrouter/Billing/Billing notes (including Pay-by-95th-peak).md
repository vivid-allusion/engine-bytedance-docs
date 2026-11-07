---
title: "Billing notes (including Pay-by-95th-peak)"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Billing-rules"
---

This topic describes detailed billing rules for each billing item of the Transit Router (TR).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before purchasing TR resources, ensure your account meets the <a href="https://docs.byteplus.com/en/docs/transitrouter/Billing-overview#.6LSt5Lmw6KaB5rGC">purchase prerequisites</a>.</div>


<span id=".6K6h6LS56KeE5YiZ"></span>
## Billing rules

<span id=".5Zyw5Z-f5YaF6LS555So"></span>
### Regional fees

Regional fees include the attachment fee and the traffic processing fee. The specific billing formulas are shown in the table below.


|Billing items |Formula |Billing description |
|---|---|---|
|Connection fee |Attachment fee = Instance unit price (USD/attach/hour) x Attachment count (attach) x Usage duration (hours) |* **Attachment count** refers to the number of network instances connected to the TR during a billing period.<br><br>* **Usage duration** refers to the total time an attachment is used, measured from its successful creation until its successful release. Any usage lasting less than one hour is rounded up to one hour.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Adding or removing attachments will change the attachment fee. The amount on the bill shall prevail.</div><br> |
|Traffic processing fee |Traffic processing fee = Processing unit price (USD/GB) x Inbound traffic (GB) |**Inbound traffic** refers to the traffic from attachments forwarded into the TR instance. It represents the sum of all traffic originating from network instances connected to the TR.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Adding or removing attachments will change the traffic processing fee. The amount on the bill shall prevail.</div><br> |


<span id=".6Leo5Zyw5Z-f6LS555So"></span>
### Cross\-regional fees

Cross\-region bandwidth packages support two metering methods: Subscription and Pay\-by\-95th\-peak.


* Subscription is a prepaid metering method, and is applicable to scenarios with long\-term use and relatively stable bandwidth requirements. This can significantly reduce your costs.

* Pay\-by\-95th\-peak is a postpaid billing method. This allows you to activate and release resources on demand at any time without purchasing a large amount of resources in advance. The fee is calculated based on the greater of the monthly 95th peak cost or the monthly guaranteed cost.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The Pay\-as\-you\-go (Pay\-by\-95th\-peak) feature is in the beta stage and is available only for accounts that have completed <a href="https://docs.byteplus.com/en/docs/6261/64937">enterprise real\-name authentication</a>. Please contact your account manager.   </div>
   


<Tabs>
<Tab zoneid="kMwb4pytQY" title="Subscription">
<TabTitle>Subscription</TabTitle>

TR cross\-region bandwidth packages are billed based on the tiered pricing for the bandwidth package's range. The specific formulas are shown in the table below.


|Billing items |Bandwidth range |Formula |
|---|---|---|
|Cross\-region bandwidth fee |Over 0 through 100 Mbps |Cross\-region bandwidth fee = Unit price for 0\-100 Mbps (USD/Mbps/month) x Bandwidth (Mbps) x Purchase duration (months) |
||Over 100 through 1,000 Mbps |Cross\-region bandwidth fee = [Unit price for 0–100 Mbps (USD/Mbps/month) x 100 + Unit price for 100–1,000 Mbps (USD/Mbps/month) x (Bandwidth \- 100) (Mbps)] x Purchase duration (months) |
||Over 1,000 Mbps |Cross\-region bandwidth fee = [Unit price for 0–100 Mbps (USD/Mbps/month) x 100 + Unit price for 100–1,000 Mbps (USD/Mbps/month) x 900 + Unit price for over 1,000 Mbps (USD/Mbps/month) x (Bandwidth \- 1,000) (Mbps)] x Purchase duration (months) |





</Tab>
<Tab zoneid="ndd6uLamev" title="Pay-by-95th-peak">
<TabTitle>Pay-by-95th-peak</TabTitle>

**Cross\-region bandwidth fee = MAX {Monthly 95th peak bandwidth x Valid 95th peak days / Days in the month, Monthly guaranteed bandwidth x Valid guaranteed days / Days in the month} x Bandwidth unit price**


* **Monthly 95th peak bandwidth**: Sort all valid bandwidth samples in descending order by their peak values, discard the top 5% of samples, and take the 95th percentile peak value as the monthly peak bandwidth. Valid bandwidth refers to the greater average value between outbound traffic and inbound traffic within each 5\-minute interval.

* **Valid 95th peak days**: The number of days in the month on which actual traffic usage is greater than zero.

* **Monthly guaranteed bandwidth**: The average of daily guaranteed bandwidth in the month (Sum of daily guaranteed bandwidth / Valid guaranteed days). Daily guaranteed bandwidth = Bandwidth cap x Daily guaranteed ratio (Default: 20%). As the daily bandwidth cap of the bandwidth package or the guarantee ratio may change, the daily guaranteed bandwidth may vary.

* **Valid guaranteed days**: The number of calendar days in the month when the bandwidth package is billed by Pay\-by\-95th\-peak.

* **Days in the month**: The number of calendar days in the month. E.g., 31 days in March, and 30 days in April.

* **Bandwidth unit price**: The unit price varies based on the bandwidth range to which the bandwidth package's cap belongs.


Cross\-region bandwidth packages are billed based on tiered pricing for bandwidth ranges. The specific formulas are shown in the table below.


|Billing items |Bandwidth range |Formula ||
|---|---|---|---|
|||Monthly 95th peak cost |Monthly guaranteed cost |
|Cross\-region bandwidth fee |Over 0 through 100 Mbps |Monthly 95th peak cost = Unit price for 0–100 Mbps (USD/Mbps/month) x Monthly peak bandwidth (Mbps) x [Valid days (days) / Days in the month (days)] |Monthly guaranteed cost = Unit price for 0–100 Mbps (USD/Mbps/month) x Monthly guaranteed bandwidth (Mbps)x [Valid guaranteed days (days) / Days in the month (days)] |
||Over 100 through 1,000 Mbps |Monthly 95th peak cost = [Unit price for 0–100 Mbps (USD/Mbps/month) x 100 + Unit price for 100–1,000 Mbps (USD/Mbps/month) x (Monthly peak bandwidth \- 100) (Mbps)] x [Valid days (days) / Days in the month (days)] |Monthly guaranteed cost = [Unit price for 0–100 Mbps (USD/Mbps/month) x 100 + Unit price for 100–1,000 Mbps (USD/Mbps/month) x (Monthly guaranteed bandwidth \- 100) (Mbps)] x [Valid guaranteed days (days) / Days in the month (days)] |
||Over 1,000 Mbps |Monthly 95th peak cost = [Unit price for 0–100 Mbps (USD/Mbps/month) x 100 + Unit price for 100–1,000 Mbps (USD/Mbps/month) x 900 + Unit price for over 1,000 Mbps (USD/Mbps/month) x (Monthly peak bandwidth \- 1,000) (Mbps)] x [Valid days (days) / Days in the month (days)] |Monthly guaranteed cost = [Unit price for 0–100 Mbps (USD/Mbps/month) x 100 + Unit price for 100–1,000 Mbps (USD/Mbps/month) x 900 + Unit price for over 1,000 Mbps (USD/Mbps/month) x (Monthly guaranteed bandwidth \- 1,000) (Mbps)] x [Valid guaranteed days (days) / Days in the month (days)] |





</Tab>
</Tabs>
