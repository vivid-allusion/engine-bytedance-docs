---
title: "Pay-by-CU"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Billing-03"
---

<span id=".5qaC6L-w"></span>
## Overview

CLB supports Pay\-by\-CU. CLB instances with Pay\-by\-CU are billed based on the actually consumed performance capacity of LCUs (Loadbalancer Capacity Units). Users can use first and pay later, and activate or release on demand at any time.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Pay\-by\-CU CLB is currently in Beta. Contact customer service support to request a trial.</div>


<span id=".6LSt5Lmw6KaB5rGC"></span>
## Purchase prerequisites


* Make sure you have completed enterprise real\-name authentication for your account.

* CLBs billed by usage do not upload data for **max connections usage rate, new connections per second usage rate, QPS usage rate, and inbound and outbound bandwidth usage rate** to the CloudMonitor platform. Therefore, when configuring alert rules in the CloudMonitor console, do not configure these four metrics to avoid alert failures or false alarms caused by missing data.


<span id=".6K6h6LS56K-05piO"></span>
## Billing description

<span id=".6K6h6LS56KeE5YiZ"></span>
### CLB fee

**Billing cycle: hours**

**Billing formula: CLB fee = instance fee + LCU fee**


* **Instance fee** = instance unit price (USD/pc/hour) × usage duration (hours)

   * The unit price for CLB instances billed by usage is 0.006 USD/pc/hour.

   * Usage duration is calculated from the successful creation of the order, accurate to the second.

* **Hourly LCU fee** = LCU unit price (USD/pc) × hourly instance LCU consumption (pc)\>

   * The LCU unit price is 0.006 USD per LCU.

   * Within each billing cycle, the actual number of LCUs consumed by the CLB instance refers to the sum of LCUs consumed by **all listeners** in that CLB instance, related to each listener’s performance metrics.

      **The number of LCUs for a single listener = Max{New Connections Per Second LCU count, max connections LCU count, data processing volume LCU count, rule evaluation LCU count}** 

   * LCU Calculation Description

      
      |<div style="text-align: center"><br>Performance metric</div><br> |Metric description |Billing cycle |LCU coefficient |||LCU Calculation Description |
      |---|---|---|---|---|---|---|
      ||||TCP |UDP |HTTP/<br><br>HTTPS ||
      |New Connections Per Second (CPS) |The number of new TCP, UDP, or HTTP/HTTPS connections processed per second, measured in connections. |seconds |800 |400 |25 |Within each billing cycle, the system records the number of new connections per second. The maximum value of new connections per second is then divided by the corresponding protocol's LCU coefficient to calculate the number of LCUs used for new connections during that billing cycle.<br><br>**Calculation formula: LCU quantity = maximum new connections ÷ LCU coefficient** |
      |Concurrent connections |Number of concurrent TCP, UDP, or HTTP/HTTPS connections per minute, measured in connections. |minutes |100,000 |50,000 |3,000 connections |Within each billing cycle, the system records the concurrent connections per minute. It then divides the maximum concurrent connections per minute by the protocol’s LCU coefficient to calculate the LCU quantity for that billing cycle.<br><br>**Calculation formula: LCU Quantity = Maximum concurrent connections ÷ LCU coefficient** |
      |Data processed |CLB instance data processing volume for requests and responses using TCP, UDP, or HTTP/HTTPS protocols, measured in GB. |Hour |1 GB |1 GB |1 GB |In each billing cycle, the system sums the total data volume of all requests and responses, then divides this total by the LCU coefficient of the corresponding protocol to calculate the LCU quantity for that billing cycle.<br><br>**Formula: LCU Quantity = Total data processed ÷ LCU coefficient** |
      |Rule evaluations |Calculated from the number of forwarding rules processed by CLB instances and the queries per second. The first 30 forwarding rules per CLB instance are free (excluding default forwarding rules).<br><br><br>* When the number of forwarding rules 30, rule evaluations = QPS × (Number of forwarding rules \- 30).<br><br>* When the number of forwarding rules ≤ 30, rule evaluations = QPS. |\-\- |\-\- |\-\- |1,000 |Within each billing cycle, the system counts the number of forwarding rules and queries per second, then evaluates the rules to calculate the rule evaluation count. The maximum rule evaluation count is divided by the LCU coefficient of the corresponding protocol to determine the LCU number for that billing cycle.<br><br>**Formula: LCU Quantity = Maximum rule evaluations ÷ LCU coefficient** |
      


<span id="rEBgdFaJ"></span>
### **Internet fee**

Specifically, the internet fee of the Elastic IP (EIP) associated with the CLB instance. For details please refer to EIP Metering methods.

<span id=".6LS555So56S65L6L"></span>
## Fee example

A company created one Pay\-by\-CU internet CLB on September 20, 2024, at 10:30:00, creating only one TCP listener, and released the internet CLB at 12:00:00.

The details of this TCP listener are as follows:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_64f0f2e6204c0434e5ef0ce78f72e306.png) </span>

The calculation of LCUs for this TCP listener is as follows:


|Billing cycle |Performance metric |Value |CU equivalent |Hourly CU consumption |
|---|---|---|---|---|
|10:00:00\-11:00:00 |Value for new connections per second |6,000 connections |6,000 ÷ 800 connections/CU = 7.5 CUs |Take the maximum value, which is 7.5. |
||Value for cDoncurrent connections |80,000 connections |80,000 ÷ 100,000 connections/CU = 0.8 CUs ||
||Data processed |6GB |6 GB ÷ 1 GB/CU = 6 CUs ||
|11:00:00\-12:00:00 |Value for new connections per second |8,000 connections |8,000 ÷ 800 connections/CU = 10 CUs |The maximum value is taken, i.e., 10 CUs. |
||Value for cDoncurrent connections |100,000 connections |100,000 ÷ 100,000 connections/CU = 1 CU ||
||Data processed |6GB |6 GB ÷ 1 GB/CU = 6 CUs ||


Assume that the unit price for instances at that time is 0.006 USD/hour, and the unit price for LCUs is 0.006 USD per unit. The fee for each specific billing cycle of this CLB is as follows:


|Billing cycle |Instance fee (USD) |LCU fee (USD) |Total fee (USD) |
|---|---|---|---|
|10:00:00\-11:00:00 |0.006 x 0.5 = 0.003 |0.006 x 7.5 = 0.045 |0.048 |
|11:00:00\-12:00:00 |0.006 x 1 = 0.006 |0.006 x 10 = 0.06 |0.066 |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Refer to EIP billing for the EIP fee example.</div>
