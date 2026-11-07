---
title: "Configure the GTM Instance (Intelligent Routing, Capacity Mode)"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/zHuTsr"
---

After you create a GTM instance, you need to configure the GTM instance and then start the GTM instance.

This document explains how to configure a GTM instance in the capacity routing mode of the intelligent routing policy, to implement example business scenario C.

<span id="example-business-scenario-c"></span>
## Example business scenario C

Your website domain name is `www.example.com`, and the DNS service provider is BytePlus DNS. The website servers are deployed in multiple data centers. The geolocations, access point IP addresses, and capacities of these data centers are shown in the following table.


|Geolocation |IP address |ISP |Capacity |
|---|---|---|---|
|Shanghai |`203.0.113.1` |China Telecom |100 |
||`203.0.113.2` ||100 |
|Zhejiang |`203.0.113.3` |China Mobile |100 |
||`203.0.113.4` ||100 |
|Beijing |`203.0.113.5` |BGP |200 |
||`203.0.113.6` ||100 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Capacity is used to represent the data center's traffic capacity, which can be set based on indicators such as bandwidth and concurrent connections. In this tutorial, capacity values are set for each data center based on bandwidth.</div>


* <div data-tips="true" data-tips-type="tip">The IP addresses in the documentation are for example purposes only and do not represent real IP addresses.</div>



Your business requirement is to reduce the latency for users accessing your website as much as possible, while not exceeding the data center capacity.

<span id="steps"></span>
## Steps

Refer to the following steps to configure your created GTM instance.


1. Open the [Instance management page](https://console.byteplus.com/dns-suite/gtm/instances).

2. In the **Domain** column, find **www.example.com**.

3. In the corresponding **Action** column, click **Configure**.

4. On the **Instance configuration** page, find the **Basic information** section and configure the basic information of the GTM instance. After completing configuration, click **Next step**.

   
   |Parameter |Description |
   |---|---|
   |**Policy type** |The policy type of the GTM instance. Set to **Intelligent routing**. |
   |**Routing mode** |The routing mode of the intelligent routing policy. Set to **Capacity**. |
   

5. On the **Instance configuration** page, in the **Add traffic targets** section, click **Add traffic target** to add the following pools. After adding, click **Next**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Capacity is a positive integer used to indicate the traffic capacity of the pool or address. You can set a reasonable capacity for your data center based on parameters such as bandwidth and concurrent connections. Capacity is a relative value, so you do not need to input the actual data of the address, but you need to ensure the capacity units are consistent among different addresses or pools.   </div>
   

   **Pool 1**

   
   |Parameter |Description |
   |---|---|
   |**Name** |Telecom\-Shanghai\-data center |
   |**Address type** |IPv4 Address |
   |**Address** |Add two addresses:<br><br><br>* **Address**: 203.0.113.1；**Address capacity**: 100<br><br>* **Address**: 203.0.113.2；**Address capacity**: 100 |
   

   **Pool 2**

   
   |Parameter |Description |
   |---|---|
   |**Name** |Mobile\-Zhejiang\-data center |
   |**Address type** |IPv4 Address |
   |**Address** |Add two addresses:<br><br><br>* **Address**: 203.0.113.3；**Address capacity**: 100<br><br>* **Address**: 203.0.113.4；**Address capacity**: 100 |
   

   **Pool 3**

   
   |Parameter |Description |
   |---|---|
   |**Name** |BGP\-Beijing\-data center |
   |**Address type** |IPv4 Address |
   |**Address** |Add two addresses:<br><br><br>* **Address**: 203.0.113.5；**Address capacity**: 200<br><br>* **Address**: 203.0.113.6；**Address capacity**: 100 |
   

6. On the **Instance configuration** page, in the **Enable health check** section, keep the default settings and click **Next**.

7. On the **Instance configuration** page, in the **Start routing** section, retain the checked status of the **Enable** checkbox in **Start routing**. Review the expected routing graph to check if it meets the requirements of your example business scenario. After confirming it's correct, click **Submit**.


After submission, you are redirected to the **Instance management** page. At the same time, BytePlus GTM starts routing user requests for this GTM instance. Once enabled, the status of the GTM instance changes to **Running**.

At this point, the GTM instance routes user requests visiting your domain to appropriate IP addresses according to your configuration and performs health checks on the IP addresses. See [View Health Check Task Sets and Tasks](https://docs.byteplus.com/docs/byteplus-dns-suite/_q5mIh) for information on how to view the health check status of target addresses.

<span id="后续步骤"></span>
## Follow\-up steps

Next, you can verify whether the traffic meets the requirements of the example business scenario A. Refer to [Validate Traffic](https://docs.byteplus.com/docs/byteplus-dns-suite/RWiva6).
