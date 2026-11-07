---
title: "Pay-by-95th-peak"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/Pay-by-traditional-95th-percentile"
---

This topic describes Pay\-by\-95th\-peak details for Bandwidth Package.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Pay\-by\-95th\-peak is in the beta stage. If you need a trial, please contact your account manager.</div>


<span id=".6LSt5Lmw5YmN5o-Q"></span>
## Prerequisites


* You have completed enterprise real\-name authentication for your account.

* Your account is not in arrears. For related procedure, see [Recharge guide](https://docs.byteplus.com/en/docs/6269/100434).


<span id=".6K6h6LS55YWs5byP"></span>
## Formula

**Single Bandwidth Package cost = MAX [(Monthly 95th peak × Effective days of 95th peak / Billing month days), (Monthly guaranteed bandwidth × Effective days of guarantee / Billing month days)] × Monthly bandwidth unit price**


* **Monthly 95th peak (Mbps):**  Sample the average values for both inbound and outbound bandwidth every five minutes, and take the greater one as a valid peak bandwidth point. When calculating at the end of the calendar month, sort all valid peak bandwidths in descending order, discard the top 5% of points, and then take the first point from the remaining points as the monthly 95th peak value for the Bandwidth Package.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Monthly 95th peak</strong> samples 288 data points per day. If the point count is less than 288, use points with a bandwidth of 0 Mbps as supplements.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can <a href="https://docs.byteplus.com/en/docs/bandwidthpackage/FAQs#wKEWsiYf">view the reference estimates of monthly 95 peak bandwidth and monthly guaranteed bandwidth</a> on the Bandwidth Package console, with a timeliness of T+1. For example, the bandwidth estimate for October 2024 viewed on October 21st is based on daily peaks from October 1 to October 20, 2024. Actual billing bandwidth is subject to the final bill.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The cost of a single Bandwidth Package is determined by the monthly 95th peak fee and the guaranteed bandwidth fee, <strong>taking the greater of the two. The estimates of monthly 95th peak</strong> and <strong>monthly guaranteed bandwidth</strong> cannot be directly compared, as actual bandwidth usage varies.   </div>
   

* **Effective days of 95th peak:**  Days with actual bandwidth usage greater than 0 Mbps.

* **Billing days:**  Days in the calendar month when the Bandwidth Package is used.

* **Daily guaranteed bandwidth (Mbps):**  Multiply the daily bandwidth cap by the daily guarantee ratio, resulting in the daily guaranteed bandwidth. As the daily bandwidth cap of the Bandwidth Package or the guarantee ratio may change, the daily guaranteed bandwidth may vary.

   * Daily bandwidth cap (Mbps): The bandwidth cap set daily for the Bandwidth Package. If the specification is modified, the maximum bandwidth of the day will apply.

   * Daily guarantee ratio: While enjoying multiple\-fold elastic bandwidth, you need to pay a guaranteed fee **proportionally**. The ratio defaults to 20%, and is subject to the actual display in the console.

* **Monthly guaranteed bandwidth (Mbps):**  Divide the sum of all daily guaranteed bandwidth by the effective days of guarantee.

* **Effective days of guarantee:**  Calendar days in the month when the Bandwidth Package is billed by Pay\-by\-95th\-peak.


<span id="GvjoVHfm"></span>
## Monthly bandwidth price


|**ISP** |**Name** |**Fee** |
|---|---|---|
|BGP (multi\-ISP) |Monthly bandwidth price |14.3 USD/Mbps |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The monthly bandwidth unit price in <a href="https://console.byteplus.com/eip/cbwps">the Bandwidth Package console</a> shall prevail.</div>


<span id=".57uT566X5ZGo5pyf"></span>
## Settlement cycle

Billing cycle and settlement cycle are both based on the calendar month.

View last month’s billing data after 12:00 on the second calendar day of each calendar month; for billing details, see [Bill management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-bill-details).

<span id=".6LS555So56S65L6L"></span>
## Fee example

On July 15 (the billing month has 31 days), Mr. B purchased a Pay\-by\-95th\-peak Bandwidth Package with BGP (Multi\-ISP). The number of days in July with actual bandwidth usage greater than 0 Mbps was 16 (i.e., the effective days of the 95th peak are 16). Assuming the monthly bandwidth unit price is 120.00 USD/Mbps and the guarantee ratio is 20%.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The calculation results in this example are rounded to two decimal places. Actual amounts are subject to the official bill in the console.</div>



* The process to sample the monthly 95th peak is as follows:

   The average values for both inbound and outbound bandwidth were sampled every five minutes, with the greater taken as a valid peak bandwidth point. A total of 288 points were sampled daily. When calculating the monthly peak bandwidth, all valid points were sorted in descending order. The top 5% points (288 × 16 × 5% = 230.4) were discarded. The 231st point was taken as the monthly 95th peak (100 Mbps).

   **Monthly 95th peak × Effective days of 95th peak / Billing month days = 100 Mbps × 16/31 = 51.61 Mbps**

* The monthly guaranteed bandwidth calculation for the Bandwidth Package is as follows:

   All daily guaranteed bandwidth is summed (sum is 1280 Mbps). The sum is divided by 17 days (the effective days of guarantee), resulting in the monthly guaranteed bandwidth of 75.29 Mbps.

   
   |Date |Daily bandwidth cap (Mbps) |Guaranteed ratio |Daily guaranteed bandwidth (Mbps) |
   |---|---|---|---|
   |July 15 |200 |20% |40 |
   |July 16 |200 |20% |40 |
   |July 17 to July 31 |400 |20% |80 |
   

   **Monthly guaranteed bandwidth × Effective days of guarantee / Billing month days = 75.29 Mbps × 17 / 31 = 41.29 Mbps**


The **greater value** between the monthly 95th peak and the guaranteed bandwidth was taken for billing. Resulting in:

**Bandwidth Package fee of July = MAX [(Monthly 95th peak × Effective days of 95th peak / Billing month days), (Monthly guaranteed bandwidth × Effective days of guarantee / Billing month days)] × Monthly bandwidth unit price = MAX (51.61, 41.29) × 120.00 USD/Mbps = 6193.20 USD**
