---
title: "CloudLens for ALB"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/CloudLens_for_ALB"
---

This section introduces CloudLens for ALB, the basic service monitoring log application provided in the TLS application marketplace.

<span id="cde39a6e"></span>
## Overview

The log observability capabilities of cloud products built on ALB instances support monitoring center display, access overview, second\-level metric monitoring, and additional features.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/10da438b93334d829c35fa11e2b51778) </span>

<span id="63729fec"></span>
## Monitoring chart details

The monitoring chart details for TLS CloudLens for ALB are as follows:


|Type |Chart |
|---|---|
|ALB second\-level metric monitoring |* <div style="text-align: start-_pOwxG"><br>QPS</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Success rate</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Access latency, upstream latency</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Request traffic, response body traffic</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Status code 3xx, status code 2xx, error status code</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Upstream 3xx status code, upstream 2xx status code, upstream error status code</div><br> |
|ALB access overview |* PV compared to yesterday, PV compared to last week<br><br>* UV compared to yesterday, UV compared to last week<br><br>* PV province distribution, PV country distribution<br><br>* UV province distribution, UV country distribution<br><br>* Today's access PV, PV in the past 7 days<br><br>* Today's access UV, UV in the past 7 days<br><br>* Top 10 access provinces, Top 10 access cities<br><br>* Top 10 access UserAgent, Top 10 access Host |
|ALB monitoring center |* PV, access PV<br><br>* Average latency<br><br>* Status distribution<br><br>* Traffic<br><br>* Request success rate, access failure rate<br><br>* Number of request 4xx, number of request 499, number of request 404, number of request 5xx, number of request 504<br><br>* P50 latency, P90 latency, P99 latency<br><br>* Top request Host, Top request Url, Top request backend |


<span id="3788886f"></span>
## Steps to integrate log applications

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Description</div>


<div data-tips="true" data-tips-type="default">After the CloudLens for ALB log application is successfully created, you can modify the access configuration, but you cannot cancel the access.</div>



1. Log in to [TLS console](https://console.byteplus.com/tls/).

2. In the top navigation bar, select the region where TLS is located.

3. In the left navigation bar, select **Common features** \> **Log applications**.

4. On the **Marketplace** tab, select the log application card to be integrated. For example, on the **CloudLens for ALB** card, click **Integrate application**.

5. Confirm the following information according to the interface prompts, then click **Submit**.

   
   |Parameters |Description |
   |---|---|
   |Billing information |After integrating ALB access logs, TLS will charge based on storage space, read traffic, request count, data transformation, log shipping, and other factors. |
   |Authorize RAM access |Grant cross\-service access permissions. |
   

6. By default, after successful integration, you enter the dashboard page.


<span id="a4d4502b"></span>
## Manage integration configuration

After successful integration of the log application, you can perform management operations on the integrated log applications:


1. Log in to [TLS console](https://console.byteplus.com/tls/).

2. In the top navigation bar, select the region where TLS is located.

3. In the left navigation bar, select **Common features** \> **Log applications**.

4. Go to the **My applications** tab, and in the **Actions** column for the corresponding log application, click **Integration management**.

5. Expand the ALB data dashboard, click **Integration configuration** on the right. On the integration configuration tab, the following management operations are supported:

   
   |Operations |Description |
   |---|---|
   |Select region |In the region drop\-down list, you can select the region where the instance is located. |
   |Disable monitoring collection |In the monitoring column for **Instance**, click **Disable** to disable monitoring collection for that instance.<br><br>You can select multiple instances. Click **Batch disable** to disable monitoring for the selected instances. |
   |Enable monitoring collection |In the monitoring column for **Instance**, click **Enable** to enable monitoring collection for that instance.<br><br>You can select multiple instances. Click **Batch enable** to enable monitoring for the selected instances. |
   


&nbsp;


&nbsp;
