---
title: "Pay-by-CU"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Pay-by-LCU"
---

<span id=".5qaC6L-w"></span>
## File transfer overview

NLB supports Pay\-by\-CU, a billing method based on the actual consumption of Loadbalancer Capacity Unit (LCU) by NLB instances. This is a post\-paid billing method, allowing users to activate or release instances whenever necessary.

<span id=".6K6h6LS56K-05piO"></span>
## Billing Description

<span id=".6K6h6LS56KeE5YiZ"></span>
### NLB instance fee

**Billing cycle: per hour**

**Billing formula: NLB instance fee = Instance fee + LCU fee**


* **Instance fee = Instance unit price (USD/Hour) × Usage duration (Hour)** 

   * **0.02**USD/hour per instance.

   * Usage duration is calculated from the time the order is submitted, with durations of less than one hour billed as one hour.

* **LCU fee = LCU unit price (USD/unit) × Number of LCUs consumed per hour by the instance (unit)** 

   * **0.005**USD/unit.

   * The number of LCUs for an instance = Sum of the LCUs consumed by all listeners in the NLB instance.

      * The number of LCUs for a single listener = Max{Number of LCUs required for New Connections Per Second, Number of LCUs required for Max Connections, Number of LCUs required for processed data}

      * LCU Calculation Description

         
         |Performance Metric |Metric Description |Measurement Cycle |<div style="text-align: center"><br>LCU Coefficient</div><br> |||LCU Calculation Description |
         |---|---|---|---|---|---|---|
         ||||<div style="text-align: center"><br>TCP</div><br> |<div style="text-align: center"><br>UDP</div><br> |TLS ||
         |New Connections Per Second |Number of new TCP, UDP, or TLS connections processed per second, measured in connections. |Second |800<br><br>connections/item |<div style="text-align: center"><br>400</div><br><br><br><div style="text-align: center"><br>connections/item</div><br> |<div style="text-align: center"><br>50</div><br><br><br><div style="text-align: center"><br>connections/item</div><br> |**Calculation formula: Number of LCUs = Maximum New Connections Per Second ÷ LCU coefficient**<br><br>Maximum new connections: Maximum new connections are calculated by taking the highest value among the new connections per second within billing cycle. |
         |Max Connections |Number of concurrent TCP, UDP, or TLS connections maintained per minute, measured in connections. |Minute |<div style="text-align: center"><br>100,000</div><br><br><br><div style="text-align: center"><br>connections/CU</div><br> |<div style="text-align: center"><br>50,000</div><br><br><br><div style="text-align: center"><br>connections/item</div><br> |<div style="text-align: center"><br>3000</div><br><br><br><div style="text-align: center"><br>connections/CU</div><br> |**Calculation formula: LCU quantity = Maximum max connections ÷ LCU coefficient**<br><br>Maximum max connections: Max connections are calculated by taking the highest value among the max connections per minute within billing cycle. |
         |Processed data |Amount of TCP, UDP, or TLS requests and responses processed by the NLB instance, measured in GB. |Hour |<div style="text-align: center"><br>1</div><br><br><br><div style="text-align: center"><br>GB/item</div><br> |<div style="text-align: center"><br>1</div><br><br><br><div style="text-align: center"><br>GB/item</div><br> |<div style="text-align: center"><br>1</div><br><br><br><div style="text-align: center"><br>GB/item</div><br> |**Calculation formula: Number of LCUs = Total processed data ÷ LCU coefficient**<br><br>Total data processed: The total data volume is calculated by summing the data of all requests and responses within billing cycle. |
         

* **Resource pack:**  If a resource pack is purchased, the instance and LCU fees will be deducted from the resource pack first. Any usage exceeding the pack limit will be billed according to the formula specified above. [Learn more](https://docs.byteplus.com/en/docs/clb/NLBPackages)


<span id="poMWJ6D4"></span>
### Internet Fee

When the internet NLB instance is configured with internet connectivity via Elastic IP (EIP) or IPv6 gateway, the corresponding internet fees will be billed through the Elastic IP (EIP) or IPv6 gateway.


* Refer to Elastic IP billing for the [EIP fee](https://docs.byteplus.com/en/docs/eip/Pay-as-you-go).

* Refer to IPv6 gateway billing for the [IPv6 Internet bandwidth fee](https://docs.byteplus.com/en/docs/IPv6/Pay-as-you-go).


<span id="iwAm9G8U"></span>
### Price Calculator

Through the [Price Calculator](https://www.byteplus.com/en/pricing?product=NLB&tab=2), you can view the instance unit price and LCU unit price (this price is for reference only, actual fees are subject to the console), and estimate the NLB fee based on the bandwidth demand of your business scenario.

<span id=".6LS555So56S65L6L"></span>
## Billing example

One enterprise created one Pay\-by\-CU internet NLB at 10:30:00 on September 20, 2024, and **only created one TCP listener** before releasing the internet NLB at 12:00:00.

The details of this TCP listener are as follows:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_78f92d27895bfe36a5e79e157f26949c.png) </span>

The calculation of LCUs for this TCP listener is as follows:


|Billing cycle  |Performance Metric |Valid Value |Number of CUs |Number of CUs consumed by the instance every hour |
|---|---|---|---|---|
|10:00:00\-11:00:00 |New Connections Per Second |6000 |6,000 ÷ 800 connections/CU = 7.5 CUs |Take the maximum value, which is 7.5. |
||Max connections value |80,000 |80,000 ÷ 100,000 connections/CU = 0.8 CUs ||
||Processed data |6GB |6GB ÷ 1GB/item = 6 items ||
|11:00:00\-12:00:00 |New Connections Per Second |8000 |8,000 ÷ 800 connections/CU = 10 CUs |Take the maximum value, which is 10. |
||Max connections value |100,000 |100,000 ÷ 100,000 connections/CU = 1 CU ||
||Processed data |6GB |6GB ÷ 1GB/item = 6 items ||


Assume the instance unit price at that time is **0.02**USD/instance/hour, and the LCU unit price is **0.005**USD/unit. The fee for each billing cycle of the NLB is as follows:


|Billing cycle  |Instance fee (USD) |LCU fee (USD) |Fee (USD) |
|---|---|---|---|
|10:00:00\-11:00:00 |0.02 x 1 = 0.02 |0.005 x 7.5 = 0.0375 | 0.0575 |
|11:00:00\-12:00:00 |0.02 x 1 = 0.02 |0.005 x 10 = 0.05 |0.07 |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Refer to <a href="https://docs.byteplus.com/en/docs/eip/Pay-as-you-go">Elastic IP billing</a> for the EIP fee.</div>


* <div data-tips="true" data-tips-type="default">Refer to <a href="https://docs.byteplus.com/en/docs/IPv6/Pay-as-you-go">IPv6 gateway billing</a> for the IPv6 Internet bandwidth fee.</div>
