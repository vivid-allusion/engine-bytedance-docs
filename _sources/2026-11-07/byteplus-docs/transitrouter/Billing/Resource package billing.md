---
title: "Resource package billing"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Resource-pack-billing"
---

<span id=".566A5LuL"></span>
## Overview​

A Resource Package is a prepaid, usage\-offsetting product offered by the Transit Router (TR) service. Once purchased, it is applied to cover your traffic processing costs. It is also referred to as the TR Traffic Processing Package. The TR traffic processing package is applicable to scenarios with massive inbound traffic of TR instances, effectively reducing your TR cost.

Changes in the lifecycle of the TR traffic processing package do not affect the TR service, and only impact the fees you pay for using TR.

<span id=".6KeE5qC85ZKM5a6a5Lu3"></span>
## Specification and pricing

The prices of TR traffic processing packages vary by specifications, as shown in the table below.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the table below, PB is the traffic unit, where 1 PB = 1,024 TB and 1 TB = 1,024 GB.</div>



|Specification of TR traffic processing package |Pricing (USD) |
|---|---|
|10 PB |999,800 |
|100 PB |9,998,000 |


<span id=".5L2_55So6K-05piO"></span>
## Notes

<span id=".5oq15omj6K-05piO"></span>
### Offsetting


* TR traffic processing packages are periodic packages whose reset cycle is not aligned with the calendar month.

   > A periodic resource package provides a fixed total volume of credits per reset cycle. The remaining balance decreases as you use the service, and any unused balance cannot be carried over to the next cycle. The balance automatically resets to the full volume when a new cycle begins, and remains available until either exhausted or the cycle ends.   
   

* You can only use TR traffic processing packages to offset traffic processing fees incurred within the same region as the package.

* TR traffic processing packages are stackable. When you have multiple active packages under a single account, they are applied in the following order:

   * Apply the TR traffic processing package whose current cycle ends first.

   * When multiple packages share the same cycle end date, apply the TR traffic processing package whose current cycle started earlier.

* After all purchased TR traffic processing packages are exhausted, any additional usage incurs the traffic processing fee on a Pay\-as\-you\-go basis by default.


<span id=".5aSx5pWI6K-05piO"></span>
### Expiration


* The expiration time of a TR traffic processing package is determined by its effective date and purchase duration.

* A purchased TR traffic processing package expires at 23:59:59 on the expiration date.

* After the TR traffic processing package expires, any unused balance cannot be offset. You can use other eligible TR traffic processing packages in this account to offset traffic processing fees. If no TR traffic processing package is available, traffic processing fees will be billed on a Pay\-as\-you\-go basis.


<span id=".57ut6LS56K-05piO"></span>
### Renewal

The TR traffic processing package supports both automatic renewal and manual renewal.


* **Automatic renewal**: When you purchase a TR traffic processing package, you can enable automatic renewal for it. If enabled, the system will renew it automatically 7 days before expiration. The fee will be deducted from the account balance (including cash balance and available coupons), prioritizing coupons. If the account balance is insufficient during automatic renewal, the renewal will fail.

* **Manual renewal**: If you do not enable automatic renewal for a TR traffic processing package when purchasing it, renew it promptly before expiration to avoid service disruption.


<span id=".6YCA6K6i6K-05piO"></span>
### Unsubscription


* TR traffic processing packages support 7\-day free cancellation. Each account can unsubscribe 10 TR traffic processing packages per calendar year by default.

* You can freely and fully refund a TR traffic processing package that meets the following conditions:

   * The package is already effective.

   * The package is within seven days of purchase and unused.

   * The package has not been renewed.


<span id=".6K6h6LS556S65L6L"></span>
### Billing example

<span id=".6LWE5rqQ5L2_55So6K-05piO"></span>
#### Resource usage description

A company created the network scenario shown below using TRs. As business volume increased, the inbound traffic on the TR grew significantly. Specific usage over a 30\-day period is detailed in **Table 1**. This led to a substantial rise in traffic processing fees. To reduce costs, the company purchased TR traffic processing packages detailed in **Table 2**.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3102944be080910febb806bb4a0c0d5e.png) </span>

**Table 1 TR inbound traffic**


|Network instance attachment ||Inbound traffic |
|---|---|---|
|VPC |Attach vpc01 |9,000,000 GB |
|VPN Connect |Attach IPsec\-VPN connection |11,000,000 GB |


**Table 2 TR traffic processing packages**


|No. |Specification of TR traffic processing package |Regions |Duration |Enable automatic renewal |Purchase time |Effective time |Expires on |
|---|---|---|---|---|---|---|---|
|1 |10 PB |China (Guangzhou) |1 month |Yes |July 10, 2024 10:00:00 |Instant effect |August 10, 2024 23:59:59 |
|2 |10 PB |China (Beijing) |1 month |Yes |July 10, 2024 10:00:00 |Instant effect |August 10, 2024 23:59:59 |


<span id=".5pSv5LuY6LS555So6K6h566X"></span>
#### Fee calculation

The fees paid by the company before and after the purchase of TR traffic processing packages over a 30\-day period are calculated as follows:


* Before purchasing, the traffic processing fee is calculated by Pay\-as\-you\-go.

   Total TR traffic cost of the company = 0.13 USD/GB × (9,000,000 GB + 11,000,000 GB) = 2,600,000 USD

* After purchase, the traffic processing fee is offset according to the offsetting rule.

   Total TR traffic cost of the company = 999,800 USD + 999,800 USD + 0.13 USD/GB × (11,000,000 GB \- 10 PB × 1024 TB/PB × 1024 GB/TB) = 2,066,451.2 USD


<span id=".566h55CG6LWE5rqQ5YyF"></span>
## Manage resource packages

<span id=".6LSt5Lmw6LWE5rqQ5YyF"></span>
### Purchase a package


1. Log in to the Transit Router  console.

2. In the top navigation bar, select the target project.

3. In the left navigation pane, select the **Resource Package**.

4. Click **Create package** and configure parameters based on the table below.

   
   |Parameter |Description |
   |---|---|
   |Package category |Fixed as TR Traffic Processing Package. |
   |Package specification |See [Specification and pricing](https://docs.byteplus.com/en/docs/transitrouter/Resource-pack-billing#.6KeE5qC85ZKM5a6a5Lu3). |
   |Package type |Periodic |
   |Refresh cycle |Non\-calendar month<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">During the package purchase duration, the specifications and usage for each non\-calendar month package reset.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Upon reset, the unused balance is cleared directly but not carried over to the next cycle.</div><br> |
   |Regions |The region to which the package belongs. For available regions, see [Areas and regions](https://docs.byteplus.com/en/docs/transitrouter/Product-Overview-05).<br><br>You can only use the package to offset traffic processing fees incurred within the same region as the package. |
   |Duration |Configure a period between 1 and 12 months based on your requirements.<br><br>After selecting the purchase duration, specify whether to enable automatic renewal based on your requirements. |
   |Effective on |The default is effective immediately, but you can specify an effective time as needed. |
   |Purchase quantity |Support batch purchase. The valid values are integers from 1 to 999. |
   

5. Click **Buy now** to confirm the package information.

6. Follow the console guidance to review and accept the Legal.

7. Click **Next** and follow the guidance to complete the order payment.

8. Click **Go to console** to view the purchased package.


<span id=".6K6-572u5L2Z6YeP6aKE6K2m"></span>
### Set the remaining balance alert

After completing the package purchase, you can set the remaining balance alert to monitor usage, manage packages efficiently, and reduce service costs. For detailed rules and the configuration procedure, see Set margin alert.

<span id=".57ut6LS5L-mAgOiuoui1hOa6kOWMhQ=="></span>
### Renew or unsubscribe a package

After completing the package purchase, you can renew or unsubscribe via the TR console and Billing center.

<span id=".5Lit6L2s6Lev55Sx5Zmo5o6n5Yi25Y-w5pON5L2c"></span>
#### Via the TR console


1. Log in to [the Resource Package console](https://console.byteplus.com/trbandwidthpkg/resourcePkg).

2. In the top navigation bar, select the target project.

3. Click **Renew** or **Unsubscribe** to the right of the target package to complete the action.


<span id=".6LS555So5Lit5b-D5pON5L2c"></span>
#### Via the Billing center


1. Log in to [the Resource package console](https://console.byteplus.com/finance/resource-package).

2. Select the **Resource package** tab.

3. Click **Renew** or **Unsubscribe** to the right of the target package to complete the action.
