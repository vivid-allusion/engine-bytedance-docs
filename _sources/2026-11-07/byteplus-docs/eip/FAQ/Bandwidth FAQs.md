---
title: "Bandwidth FAQs"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Bandwidth-FAQs"
---

* **Feature**

   * [Can I use the bandwidth of an EIP with a different account?](https://docs.byteplus.com/en/docs/48/10144#.5YWs572RSVDluKblrr3mmK_lkKbmlK_mjIHot6jluJDlj7fkvb_nlKjvvJ8=)

   * [How do I view the bandwidth of an EIP?](https://docs.byteplus.com/en/docs/48/10144#.5aaC5L2V5p-l55yL5YWs572RSVDluKblrr3vvJ8=)

   * [How do I troubleshoot when EIP bandwidth exceeds the limit?](https://docs.byteplus.com/en/docs/48/10144#.5aaC5L2V5o6S5p-l5YWs572RSVDluKblrr3otoXov4fpmZDliLbvvJ8=)

   * [How to modify the bandwidth of an EIP?](https://docs.byteplus.com/en/docs/48/10144#.5YWs572RSVDlpoLkvZXkv67mlLnluKblrr3vvJ8=)

   * [What is the relationship between EIP bandwidth and upload/download speed?](https://docs.byteplus.com/en/docs/48/10144#.5YWs572RSVDluKblrr3kuI7kuIrkvKAv5LiL6L296YCf546H5piv5LuA5LmI5YWz57O777yf)

   * [How to increase the bandwidth cap of an EIP?](https://docs.byteplus.com/en/docs/48/10144#2Eu00fyb)

* **Rate limiting**

   * [What is the range of the maximum bandwidth for an EIP?](https://docs.byteplus.com/en/docs/48/10144#.5YWs572RSVDluKblrr3kuIrpmZDojIPlm7TmmK_lpJrlsJHvvJ8=)

   * [Why is it necessary to set a bandwidth cap for Pay-by-data-transfer EIPs?](https://docs.byteplus.com/en/docs/48/10144#.5Li65LuA5LmI5oyJ5a6e6ZmF5rWB6YeP6K6h6LS555qE5YWs572RSVDpnIDopoHorr7nva7luKblrr3kuIrpmZDvvJ8=)

   * [How to limit the outbound and inbound traffic speed of an EIP?](https://docs.byteplus.com/en/docs/48/10144#.5YWs572RSVDlh7rjgIHlhaXmlrnlkJHmtYHph4_lpoLkvZXpmZDpgJ_vvJ8=)

   * [What changes in bandwidth occur when a Pay-as-you-go EIP is added to a Bandwidth Package? What is the range of the maximum bandwidth for a Bandwidth Package?](https://docs.byteplus.com/en/docs/48/10144#.5oyJ6YeP6K6h6LS55YWs572RSVDliqDlhaXliLDlhbHkuqvluKblrr3ljIXlkI7vvIzluKblrr3kvJrmnInku4DkuYjlj5jljJbvvJ_lhbHkuqvluKblrr3ljIXnmoTluKblrr3kuIrpmZDojIPlm7TmmK_lpJrlsJHvvJ8=)

   * [How to calculate download speed through the bandwidth of an EIP?](https://docs.byteplus.com/en/docs/48/10144#.5aaC5L2V6YCa6L-H5YWs572RSVDluKblrr3mjqjnrpfkuIvovb3pgJ_luqbvvJ8=)

   * [Why does the EIP bandwidth not reach the configured bandwidth cap?](https://docs.byteplus.com/en/docs/48/10144#OwvGQyWA)


<span id=".5Yqf6IO9"></span>
## Feature

<span id=".5YWs572RSVDluKblrr3mmK_lkKbmlK_mjIHot6jluJDlj7fkvb_nlKjvvJ8="></span>
### Can I use the bandwidth of an EIP with a different account?

Not supported.

<span id=".5aaC5L2V5p-l55yL5YWs572RSVDluKblrr3vvJ8="></span>
### How do I view the bandwidth of an EIP?

You can refer to the following steps to view the bandwidth (limit) of an EIP.

> The bandwidth lower limit varies for EIPs with different bandwidth specifications. Please refer to the [fee description](https://docs.byteplus.com/en/docs/eip/Subscription#.6LS555So6K-05piO) for details.



1. Log in [to the EIP console](https://console.byteplus.com/eip/eips).

2. In the top menu bar, select the region and project of your target EIP.

3. Click the name/ID of the target EIP.

4. View the bandwidth cap in the billing information on the EIP details page.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After adding an EIP to a Bandwidth Package, its original bandwidth cap becomes invalid and shares the bandwidth cap of the Bandwidth Package.</div>


<span id=".5aaC5L2V5o6S5p-l5YWs572RSVDluKblrr3otoXov4fpmZDliLbvvJ8="></span>
### How to troubleshoot when EIP bandwidth exceeds the limit?

You can [view EIP monitoring](https://docs.byteplus.com/en/docs/eip/Viewing-monitoring-data) to determine if the EIP traffic exceeds the bandwidth cap. EIP monitoring metrics are collected every 30 seconds, averaging the metric over that period.

The following two scenarios both indicate EIP traffic exceeds the bandwidth cap:


* On the monitoring page, outbound and inbound bandwidth show they have reached the bandwidth cap, and the rate limiting packet loss is greater than 0.

* On the monitoring page, outbound and inbound bandwidth do not reach the bandwidth cap, but the rate limiting packet loss is greater than 0. This scenario occurs because burst traffic is short\-lived and the outbound and inbound bandwidth metrics average over 30 seconds, so the bandwidth metrics do not reflect the burst.


If the internet traffic exceeds the bandwidth cap of an EIP, you can choose to increase the maximum bandwidth or add to a Bandwidth Package.

<span id=".5YWs572RSVDlpoLkvZXkv67mlLnluKblrr3vvJ8="></span>
### How to modify the bandwidth of an EIP?

To modify the bandwidth of an EIP, see [Modifying the maximum bandwidth](https://docs.byteplus.com/en/docs/eip/Modifying-the-maximum-bandwidth).

<span id=".5YWs572RSVDluKblrr3kuI7kuIrkvKAv5LiL6L296YCf546H5piv5LuA5LmI5YWz57O777yf"></span>
### What is the relationship between EIP bandwidth and upload/download speed?

The bandwidth unit is bps (bit/s), representing the number of bits transmitted per second.

The speed unit is Bps (Byte/s), representing the number of bytes transmitted per second.

1 Byte = 8 bits, so speed = bandwidth / 8.

For example: bandwidth 1 M refers to 1 Mbps, which converts to: 1 Mbps = 1000 Kbps = 1000/8 Kbps = 125 Kbps. In practice, environmental factors (such as device performance and network peak hours) cause upload/download speeds to be slightly lower than calculated results.

<span id="2Eu00fyb"></span>
### How to increase the bandwidth cap of an EIP?

An EIP can increase its bandwidth cap by [joining a Bandwidth Package](https://docs.byteplus.com/en/docs/eip/Adding-an-EIP-to-a-Bandwidth-Package). After joining a Bandwidth Package, the EIP shares the package's bandwidth, increasing its bandwidth cap while the original bandwidth cap becomes invalid. For bandwidth caps of the Bandwidth Package, please refer to [bandwidth caps](https://docs.byteplus.com/en/docs/bandwidthpackage/Limits#.5bim5a696ZmQ5Yi2).


|Metering method |Description |
|---|---|
|Pay\-as\-you\-go |Supports joining the Shared Bandwidth Package; see [Limits](https://docs.byteplus.com/en/docs/bandwidthpackage/Limits#.5Yqg5YWl5YWx5Lqr5bim5a695YyF6ZmQ5Yi2) for joining restrictions. |
|Subscription |Subscription EIPs do not support joining the Shared Bandwidth Package.<br><br>If your business requires subscription bandwidth traffic, it is advisable to [enable](https://docs.byteplus.com/en/docs/bandwidthpackage/Creating-a-Bandwidth-Package) the subscription Shared Bandwidth Package, then [convert billing](https://docs.byteplus.com/en/docs/eip/Billing-methods-change#.5oyJ5YyF5bm05YyF5pyI6L2s5Li65oyJ5bim5a695LiK6ZmQ6K6h6LS5) to change the **subscription** EIP to **pay\-as\-you\-go** before joining the Shared Bandwidth Package. |


<span id=".6ZmQ6YCf"></span>
## Rate limiting

<span id=".5YWs572RSVDluKblrr3kuIrpmZDojIPlm7TmmK_lpJrlsJHvvJ8="></span>
### What is the bandwidth cap range for an EIP?


|Billing method |Metering method |Bandwidth cap at application (Mbps) |Bandwidth cap at modification (Mbps) |Description |
|---|---|---|---|---|
|Pay\-as\-you\-go |Pay\-by\-data\-transfer |1 – 200 |1 – 200 |If the default bandwidth cap does not meet your needs, contact customer service support. |
||Pay\-by\-bandwidth |1 \- 500 |1 – 1000 ||
|Subscription |Pay\-by\-bandwidth |1 – 500 |1 \- 1000 ||


<span id=".5Li65LuA5LmI5oyJ5a6e6ZmF5rWB6YeP6K6h6LS555qE5YWs572RSVDpnIDopoHorr7nva7luKblrr3kuIrpmZDvvJ8="></span>
### Why is it necessary to set a bandwidth cap for Pay\-by\-data\-transfer EIPs?

Avoid generating significant outbound traffic due to program errors or malicious access to control costs.

<span id=".5YWs572RSVDlh7rjgIHlhaXmlrnlkJHmtYHph4_lpoLkvZXpmZDpgJ_vvJ8="></span>
### How to set rate limits for outbound and inbound traffic of an EIP?


* Inbound bandwidth:

   * If you set the bandwidth cap ≤ 10 Mbps, the platform assigns 10 Mbps inbound bandwidth by default.

   * If you set the bandwidth cap \> 10 Mbps, the allocated inbound bandwidth matches your setting.

* Outbound bandwidth: The allocated outbound bandwidth matches your setting.


<span id=".5oyJ6YeP6K6h6LS55YWs572RSVDliqDlhaXliLDlhbHkuqvluKblrr3ljIXlkI7vvIzluKblrr3kvJrmnInku4DkuYjlj5jljJbvvJ_lhbHkuqvluKblrr3ljIXnmoTluKblrr3kuIrpmZDojIPlm7TmmK_lpJrlsJHvvJ8="></span>
### What changes in bandwidth occur when a Pay\-as\-you\-go EIP is added to a Bandwidth Package? What is the range of the maximum bandwidth for a Bandwidth Package?

After an EIP joins a Bandwidth Package, its original bandwidth cap becomes invalid and shares the bandwidth cap of the Bandwidth Package.

The bandwidth cap range for a Bandwidth Package is 2 to 5000 Mbps.

<span id=".5aaC5L2V6YCa6L-H5YWs572RSVDluKblrr3mjqjnrpfkuIvovb3pgJ_luqbvvJ8="></span>
### How to calculate download speed using EIP bandwidth?

You can calculate the download speed based on the maximum bandwidth of the EIP associated with your ECS:

**Download speed (MB/s) = EIP maximum bandwidth (Mbps)**  ÷ **8**

For example, if the maximum bandwidth of the EIP associated with the ECS is 15 Mbps, the peak download speed is 15 Mbps ÷ 8 = 1.875 MB/s; if the maximum bandwidth of the EIP associated with the ECS is 10 Mbps, the peak download speed is 10 Mbps ÷ 8 = 1.25 MB/s.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">If you set the bandwidth cap to less than 10 Mbps (inclusive), the platform defaults to allocate 10 Mbps for inbound bandwidth.</div>


* <div data-tips="true" data-tips-type="default">If you set the bandwidth cap to more than 10 Mbps, the platform allocates the same value for inbound bandwidth.</div>



<span id="OwvGQyWA"></span>
### Why does the EIP bandwidth not reach the configured bandwidth cap?

EIP adopts a distributed high reliability cluster architecture, and all traffic is evenly distributed to multiple traffic forwarding servers within the cluster. Therefore, the maximum bandwidth cap of the EIP you set is evenly distributed among the traffic forwarding servers in the cluster.

**The traffic limit for a single connection = EIP maximum bandwidth ÷ number of traffic forwarding servers in the EIP cluster.** 

For example, if the maximum bandwidth of the EIP you set is 1600 Mbps and the EIP cluster employs 4 traffic forwarding servers, then the traffic limit for a single connection will be 1600 Mbps ÷ 4 = 400 Mbps.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The EIP can only achieve the maximum bandwidth you set when multiple connections are established. If the number of connections is too low, you cannot reach the set bandwidth cap.</div>


* <div data-tips="true" data-tips-type="default">When the total bandwidth of an EIP instance exceeds 1000 Mbps, the platform automatically enables distributed rate limiting rules.</div>
