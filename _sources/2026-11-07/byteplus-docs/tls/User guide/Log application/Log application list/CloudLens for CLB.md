---
title: "CloudLens for CLB"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/CloudLens_for_CLB"
---

This section introduces the basic service monitoring log application CloudLens for CLB provided in the TLS application marketplace.

<span id="cde39a6e"></span>
## Overview

The log observability capabilities of cloud products built on CLB instances support monitoring center display, access overview, and second\-level metric monitoring.

<span id="63729fec"></span>
## Monitoring chart details

The monitoring chart details for TLS CloudLens for CLB are as follows:


|Type |Chart |
|---|---|
|CLB second\-level metric monitoring |* <div style="text-align: start-_pOwxG"><br>QPS</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Success rate</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Access latency, upstream latency</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Request traffic, response body traffic</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Status code 3xx, status code 2xx, error status code</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Upstream 3xx status code, upstream 2xx status code, upstream error status code</div><br> |
|CLB access overview |* PV compared to yesterday, PV compared to last week<br><br>* UV compared to yesterday, UV compared to last week<br><br>* PV province distribution, PV country distribution<br><br>* UV province distribution, UV country distribution<br><br>* Today's access PV, access PV in the past 7 days<br><br>* Today's access UV, access UV in the past 7 days<br><br>* Top 10 provinces by access, Top 10 cities by access<br><br>* Top 10 accessed UserAgent, Top 10 accessed Host |
|CLB monitoring center |* Traffic<br><br>* Status distribution<br><br>* PV, access PV<br><br>* Request success rate, access failure rate<br><br>* Number of 4xx requests, number of 499 requests, number of 404 requests, number of 5xx requests, number of 504 requests<br><br>* Average latency, P50 latency, P90 latency, P99 latency<br><br>* Top requested Host, Top requested Url, Top requested backend |


<span id="3788886f"></span>
## Steps to integrate log applications

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">After the CloudLens for CLB log application is successfully created, you can modify the access configuration, but canceling access is not supported.</div>



1. Log in to the [TLS console](https://console.byteplus.com/tls/).

2. In the top navigation bar, select the region where TLS is located.

3. In the left navigation bar, select **Common features** \> **Log applications**.

4. On the **Application marketplace** tab, select the log application card to be integrated. For example, on the **CloudLens for CLB** card, click **Integrate application**.

5. Confirm the following information as prompted on the interface, then click **Submit**.

   
   |Parameters |Description |
   |---|---|
   |Billing information |After CLB access logs are integrated, TLS charges based on storage space, read traffic, number of requests, data transformation, log shipping, and many other factors. |
   |Authorize RAM access |Grant cross\-service access permissions. |
   

6. After successful integration, you will be directed to the dashboard page by default.


<span id="a4d4502b"></span>
## Manage integration configuration

After successfully integrating the log application, you can perform related management operations on the integrated log application:


1. Log in to the [TLS console](https://console.byteplus.com/tls/).

2. In the top navigation bar, select the region where TLS is located.

3. In the left navigation bar, select **Common features** \> **Log applications**.

4. Go to the **My applications** tab, and in the **Actions** column for the corresponding log application, click **Integration management**.

5. Expand the CLB data dashboard, click **Integration configuration** on the right, and on the integration configuration tab, the following management operations are supported:

   
   |Operation |Description |
   |---|---|
   |Select region |You can select the region where the instance is located from the region drop\-down list. |
   |Disable monitoring |Click **Instance** in the Monitoring column and then **Disable** to disable monitoring for that instance.<br><br>You can select multiple instances and click **Batch Disable** to disable monitoring for the selected instances. |
   |Enable monitoring |Click **Instance** in the Monitoring column and then **Enable** to enable monitoring for that instance.<br><br>You can select multiple instances and click **Batch Enable** to enable monitoring for the selected instances. |
   


&nbsp;


&nbsp;
