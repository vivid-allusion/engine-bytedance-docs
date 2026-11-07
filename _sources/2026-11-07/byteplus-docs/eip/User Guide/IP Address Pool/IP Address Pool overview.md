---
title: "IP Address Pool overview"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/IP_address_pool_overview"
---

<span id=".5LuA5LmI5pivSVDlnLDlnYDmsaA="></span>
## What is IP Address Pool

An IP address pool is a collection of multiple IP addresses, which can be allocated to Elastic IP Address (EIP) for use at any time.

If you need to use an EIP within a specific CIDR block, create an IP address pool first and add CIDR blocks supported by BytePlus public network IPs to the pool. Select a pre\-created IP address pool when creating an EIP. The EIP instance's IP address is allocated from the CIDR blocks in that IP address pool.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The IP address pool is in the beta stage. To request a trial, please contact your account manager.</div>



* The IP address pool only supports adding IPv4 CIDR blocks.

* Only pay\-as\-you\-go EIPs in the same region and with the same ISP can use an IP address pool for IP address allocation.

* EIPs with enhanced protection cannot use an IP address pool for IP address allocation.


<span id=".6YWN6aKd6ZmQ5Yi2"></span>
## Quota

IP addresses in the IP address pool occupy the EIP quota only after being allocated to the EIP. The main account's quota in a single region is as follows:


|Quota parameter |Description |Maximum |Other notes |
|---|---|---|---|
|ippool |Number of IP address pools that can be created per region |16 |If you need to use resources exceeding the quota, contact customer service support. |
|ippool_ip |Number of IP addresses across all IP address pools created per region |256 ||


<span id=".6K6h6LS56K-05piO"></span>
## Billing notes

The IP address pool charges an IP holding fee for each IP address within the CIDR block from the time the block is added, regardless of whether the IP is allocated as an EIP.


* After the IP address is allocated from the IP address pool to an EIP, you no longer need to pay the [IP config fee](https://docs.byteplus.com/en/docs/eip/Pay-as-you-go).

* If you delete a CIDR block and add it again, charges apply for each IP address in the newly added block. If you repeatedly add the same CIDR block within the same hour, this incurs the charge only once.



|Billing item |Formula |Unit price |Billing cycle |
|---|---|---|---|
|IP holding fee |IP holding fee = Unit price of IP holding fee (USD/hour per IP) × Usage duration (hours) × Number of IPs (IPs) |&nbsp;<br><br>0.007 USD/hour/IP |Fees are settled hourly on the hour (based on UTC+8 time, and partial hours are rounded up), with bills issued and payments deducted accordingly. For details, see [Bill management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-bill-details). |


<span id=".5qyg6LS56K-05piO"></span>
## Arrears notes

Account in arrears will lead to the IP address pool being suspended, making the IP address segments unusable and even deleted. The system has set a retention period for resources. Within this period, resources are retained, and you can continue using them after recharging your account and clearing overdue bills without affecting resource functions. After the retention period expires, IP address resources will be forcibly reclaimed, and related data cannot be recovered. Regardless of whether your instance resources are suspended or released, you must settle all issued bills based on the actual charges.

The following figure shows the operating and billing status of IP address pool resources after arrears:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b9e35c7cc56e21983e72749a49293eb4.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"> Platform sends SMS/email/internal messages based on  <a href="https://docs.byteplus.com/en/docs/message_center/Basic-Message-Receiving-Configuration">your settings</a> to remind you during IP address pool enters arrears, suspension, and release stages.</div>


<span id=".5L2_55So5rWB56iL"></span>
## Use process


1. [Create an IP address pool](https://docs.byteplus.com/en/docs/eip/Create_an_IP_address_pool) and [add a CIDR block](https://docs.byteplus.com/en/docs/eip/Manage_IP_address_pools#.5re75Yqg572R5q61).

2. Specify an IP address pool to [apply for an EIP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP).
