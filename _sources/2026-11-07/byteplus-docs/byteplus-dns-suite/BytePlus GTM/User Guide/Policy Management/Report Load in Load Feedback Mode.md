---
title: "Report Load in Load Feedback Mode"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/uO4mZu"
---

This document describes how to report the load of a pool or address in the load feedback routing mode, so that BytePlus GTM can dynamically adjust the distribution ratio of the number of user requests per address based on the reported load and capacity.

<span id="what-is-load"></span>
## What is load

Load is a positive integer used to represent the actual traffic borne by a pool or address. You can set a reasonable load value for an IDC based on parameters such as bandwidth and concurrent connections. Load is a relative value, so you do not need to input the actual bandwidth or concurrent connections of the pool or address, but you need to ensure that a uniform load unit is used among different addresses or pools.

Capacity is used to represent the traffic capacity of a pool or address. Therefore, the load cannot exceed the capacity.

Load and capacity must use the same estimation standard and unit. For example, if the capacity is estimated based on the bandwidth of the IDC, the load must also be estimated based on the bandwidth of the IDC.

<span id="what-is-load-feedback"></span>
## What is load feedback

If you choose the capacity routing mode of the intelligent routing policy, BytePlus GTM will return the address with the lowest access latency, provided that the capacity of the address or pool is not exceeded. In your business scenario, if the capacity of the pool or address may change, because the capacity of the address or pool cannot be updated in real\-time, the traffic scheduling ratio may not match the actual capacity of the pool or address.

In the load feedback routing mode of the intelligent routing policy, you can call the [Report Load API](https://docs.byteplus.com/docs/byteplus-dns-suite/qxfnGO) to report the real\-time load, target load, and capacity information of the pool or address to BytePlus GTM. BytePlus GTM will dynamically adjust the traffic distribution of the pool or address based on the information you report, ensuring that the real\-time load of the pool or address does not exceed the target load. Additionally, BytePlus GTM can predict the distribution of user requests based on the information you report, thereby more accurately scheduling traffic.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before the load is reported, the real\-time load and target load of all pools or addresses are by default 80% of the capacity.</div>


<span id="example-business-scenario"></span>
## Example Business Scenario

In the example business scenario D of [Getting Started](https://docs.byteplus.com/docs/byteplus-dns-suite/3es3ss), the traffic capacity of the Beijing IDC has changed. The capacity of the IDC with IP address `1.0.0.1` has decreased from 200 to 100; the capacity of the IDC with IP address `1.0.0.2` has decreased from 100 to 50.

At the same time, you monitored the current load of the IDC:


* The current load of the IDC with IP address `1.0.0.1` is 120.

* The current load of the IDC with IP address `1.0.0.2` is 60.


You want the load of the IDC to be adjusted to the following values:


* The load of the IDC with IP address `1.0.0.1` does not exceed 90.

* The load of the IDC with IP address `1.0.0.2` does not exceed 45.


<span id="prerequisites"></span>
## Prerequisites

Before reporting the load, you have already [configured the GTM instance](https://docs.byteplus.com/docs/byteplus-dns-suite/0_OA55) in the load feedback routing mode. The status of the GTM instance is **running**.

<span id="steps"></span>
## Steps

Refer to the following steps to report the load of the address in the load feedback routing mode.


1. Call the [UpdateLoad API](https://docs.byteplus.com/docs/byteplus-dns-suite/qxfnGO) to report the current load and target load for the two addresses `1.0.0.1` and `1.0.0.2`.

   
   |Address |Current load |Target load |Capacity |
   |---|---|---|---|
   |`1.0.0.1` |120 |90 |100 |
   |`1.0.0.2` |60 |45 |50 |
   

   ```JSON
   POST https://open.byteplusapi.com?Action=UpdateLoad&Version=2023-01-01
   
   {
       "GtmId":"8234cb50-f957-4be9-b515-55c5d419ea9e",
       "Timestamp": 1700805259,
       "Statistics": [
           {
               "AddrValue": "1.0.0.1",
               "CurrentLoad": 120,
               "TargetLoad": 90,
               "Capacity": 100
           },
           {
               "AddrValue": "1.0.0.2",
               "CurrentLoad": 60,
               "TargetLoad": 45,
               "Capacity": 50
           }
       ]
   }
   ```
   

2. Monitor the load changes of the IDC periodically (for example, every minute). If the current load of the IDC changes, you must call the [Report Load API](https://docs.byteplus.com/docs/byteplus-dns-suite/qxfnGO) again to report the latest data. BytePlus GTM adjusts the traffic distribution of the address pool or target address every minute based on the latest data you report.
