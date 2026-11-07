---
title: "Configure the GTM Instance (Basic Routing)"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/ItJU_b"
---

After you create a GTM instance, you need to configure the GTM instance and then start the GTM instance.

This document describes how to configure a GTM instance under the basic routing policy to implement example business scenario A.

<span id="example-business-scenario-a"></span>
## Example business scenario A

Your website domain name is `www.example.com`, and the DNS service provider is BytePlus DNS. The website servers are deployed in multiple data centers. The geolocations and access point IP addresses of these data centers are shown in the following table.


|**Geolocation** |**IP address** ||ISP |
|---|---|---|---|
|Shanghai |`203.0.113.1` |`203.0.113.2` |China Telecom |
|Zhejiang |`203.0.113.3` |`203.0.113.4` |China Mobile |
|Beijing |`203.0.113.5` |`203.0.113.6` |BGP |


The traffic capacity of the data centers is as follows:


* The traffic capacity of the data center data centers with IP addresses `203.0.113.1`, `203.0.113.2`, `203.0.113.3`, `203.0.113.4`, and `203.0.113.6` is the same.

* The traffic capacity of the data center with IP address `203.0.113.5` is twice that of the data center with IP address `203.0.113.6`.


Your business requirements are as follows:


* User requests from China Telecom / Shanghai are all allocated to the Shanghai data center.

* User requests from the China Mobile / Zhejiang are all allocated to the Zhejiang data center.

* User requests from other ISPs and geolocations are all allocated to the Beijing data center.

* User requests are allocated to different data centers in proportion to their traffic capacity.


<span id="operation-steps"></span>
## Steps

Follow the steps below to configure your created GTM instance.


1. Open the [Instance management page](https://console.byteplus.com/dns-suite/gtm/instances).

2. In the **Domain** column, find **www.example.com**.

3. In the corresponding **Action** column, click **Configure**.

4. On the **Instance configuration** page, find the **Basic information** section and configure the basic information of the GTM instance. After completing the configuration, click **Next step**.

   
   |Parameter |Description |
   |---|---|
   |**Policy** |GTM instance's policy type. Set to **Basic routing**. |
   |**Load balancing** |Whether to enable load balancing. Set to **Enabled**. |
   

5. In the **Add pool** section of the **Instance configuration** page, click  **+ Add pool** to create the following pools.

   **Pool 1**

   
   |Parameter |Description |
   |---|---|
   |**Name** |Telecom\-Shanghai\-data center |
   |**Address type** |IPv4 |
   |**Address** |Add two addresses:<br><br><br>* **Address**: 203.0.113.1; **Weight**: 1<br><br>* **Address**: 203.0.113.2; **Weight**: 1 |
   

   **Pool 2**

   
   |Parameter |Description |
   |---|---|
   |**Name** |Mobile\-Zhejiang\-data center |
   |**Address type** |IPv4 |
   |**Address** |Add two addresses:<br><br><br>* **Address**: 203.0.113.3; **Weight**: 1<br><br>* **Address**: 203.0.113.4; **Weight**: 1 |
   

   **Pool 3**

   
   |Parameter |Description |
   |---|---|
   |**Name** |BGP\-Beijing\-data center |
   |**Address type** |IPv4 |
   |**Address** |Add two addresses:<br><br><br>* **Address**: 203.0.113.5; **Weight**: 2<br><br>* **Address**: 203.0.113.6; **Weight**: 1 |
   

6. In the **Enable health check** section of the **Instance configuration** page, retain the default settings and click **Next step**.

7. In the **Configure policy** section of the **Instance configuration** page, click  **+ Add rule** to add the following rules.

   **Rule\-1**

   
   |Parameter |Description |
   |---|---|
   |**Name** |Telecom\-Shanghai |
   |**Line** |ISP line / China Telecom / East China / Shanghai |
   |**Pool** |Telecom\-Shanghai\-data center |
   

   **Rule\-2**

   
   |Parameter |Description |
   |---|---|
   |**Name** |Mobile\-Zhejiang |
   |**Line** |ISP line / China Mobile / East China / Zhejiang |
   |**Pool** |Mobile\-Zhejiang\-data center |
   

   **Rule\-3**

   
   |Parameter |Description |
   |---|---|
   |**Name** |Others |
   |**Line** |Default line |
   |**Pool** |BGP\-Beijing\-data center |
   

8. On the **Instance configuration** page, find the **Start routing** section and leave the **Enable** checkbox checked in the **Start routing** option. Review whether the expected traffic view meets the requirements of the example business scenario. After confirming there are no errors, click **Submit**.


After submission, you are redirected to the **Instance management** page. At the same time, BytePlus GTM starts routing user requests for this GTM instance. Once enabled, the status of the GTM instance changes to **Running**.

At this point, the GTM instance routes user requests visiting your domain to appropriate IP addresses according to your configuration and performs health checks on the IP addresses. See [View Health Check Task Sets and Tasks](https://docs.byteplus.com/docs/byteplus-dns-suite/_q5mIh) for information on how to view the health check status of target addresses.

<span id="Follow-up Steps"></span>
## Follow\-up steps

Next, you can verify whether the traffic routing meets the requirements of the example business scenario A. Refer to [Validate Traffic](https://docs.byteplus.com/docs/byteplus-dns-suite/RWiva6).
