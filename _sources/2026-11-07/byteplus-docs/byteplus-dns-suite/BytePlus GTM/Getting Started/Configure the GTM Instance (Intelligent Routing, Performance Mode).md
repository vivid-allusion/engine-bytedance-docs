---
title: "Configure the GTM Instance (Intelligent Routing, Performance Mode)"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/FT4Bjd"
---

After you create a GTM instance, you need to configure the GTM instance and then start the GTM instance.

This document explains how to configure a GTM instance in the performance routing mode of the intelligent routing policy, to implement example business scenario B.

<span id="example-business-scenario-b"></span>
## Example business scenario B

Your website domain name is `www.example.com`, and the DNS service provider is BytePlus DNS. The website servers are deployed in multiple data centers. The geolocations and access point IP addresses of these data centers are shown in the following table. The capacity of all data centers is sufficient.


|Geolocation |IP address ||ISP |
|---|---|---|---|
|Shanghai |`203.0.113.1` |`203.0.113.2` |China Telecom |
|Zhejiang |`203.0.113.3` |`203.0.113.4` |China Mobile |
|Beijing |`203.0.113.5` |`203.0.113.6` |BGP |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The IP addresses in the documentation are for example purposes only and do not represent real IP addresses.</div>


Your business requirement is to reduce the latency for users accessing your website as much as possible.

<span id="操作步骤"></span>
## Steps

Refer to the following steps to configure the GTM instance you created.


1. Open the [Instance management page](https://console.byteplus.com/dns-suite/gtm/instances).

2. In the **Domain** column, find **www.example.com**.

3. In the corresponding **Action** column, click **Configure**.

4. In the **Basic information** section of the **Instance configuration** page, configure the basic information for the GTM instance. After completing the setup, click **Next step**.

   
   |Parameter |Description |
   |---|---|
   |**Policy** |The policy type for the GTM instance. Set to **Intelligent routing**. |
   |**Routing mode** |The routing mode for the intelligent routing policy. Set to **Performance**. |
   

5. In the **Add traffic targets** section of the **Instance configuration** page, click **Add traffic target** to add the following pools. After adding, click **Next step**.

   **Pool 1**

   
   |Parameter |Description |
   |---|---|
   |**Name** |Telecom\-Shanghai\-data center |
   |**Address type** |IPv4 |
   |**Address** |Add two addresses:<br><br><br>* **Address**: 203.0.113.1<br><br>* **Address**: 203.0.113.2 |
   

   **Pool 2**

   
   |Parameter |Description |
   |---|---|
   |**Name** |Mobile\-Zhejiang\-data center |
   |**Address type** |IPv4 |
   |**Address** |Add two addresses:<br><br><br>* **Address**: 203.0.113.3<br><br>* **Address**: 203.0.113.4 |
   

   **Pool 3**

   
   |Parameter |Description |
   |---|---|
   |**Name** |BGP\-Beijing\-data center |
   |**Address type** |IPv4 |
   |**Address** |Add two addresses:<br><br><br>* **Address**: 203.0.113.5<br><br>* **Address**: 203.0.113.6 |
   

6. In the **Enable health check** section of the **Instance configuration** page, keep the default settings and click **Next step**.

7. In the **Start routing** section of the **Instance configuration** page, retain the check in the **Enable** checkbox within the **Start routing** option. Review whether the expected routing diagram fits the needs of the example business scenario. After confirming there are no mistakes, click **Submit**.


After submission, you are redirected to the **Instance management** page. At the same time, BytePlus GTM starts routing user requests for this GTM instance. Once enabled, the status of the GTM instance changes to **Running**.

At this point, the GTM instance routes user requests visiting your domain to appropriate IP addresses according to your configuration and performs health checks on the IP addresses. See [View Health Check Task Sets and Tasks](https://docs.byteplus.com/docs/byteplus-dns-suite/_q5mIh) for information on how to view the health check status of target addresses.

<span id="Follow-up Steps"></span>
## Follow\-up steps

Next, you can verify whether the traffic meets the requirements of the example business scenario A. Refer to [Validate Traffic](https://docs.byteplus.com/docs/byteplus-dns-suite/RWiva6).
