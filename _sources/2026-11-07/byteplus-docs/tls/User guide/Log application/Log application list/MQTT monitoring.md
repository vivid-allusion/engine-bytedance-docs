---
title: "MQTT monitoring"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/MQTT_monitoring"
---

This section introduces the MQTT monitoring log application for basic service monitoring provided by the TLS application marketplace.

<span id="8eac7c9f"></span>
## Overview

Based on the standard OpenTelemetry protocol, the call chain flame graph displays the full link status of MQTT message requests, as well as statistics on the number of requests, number of errors, and error rate.

<span id="f659e5f1"></span>
## Monitoring chart details

The details of the TLS MQTT call chain observability monitoring charts are as follows:


|Type |Chart |
|---|---|
|Performance overview analysis |* Number of requests, top 5 services by number of requests, requests per minute<br><br>* Number of errors, top 5 services by number of errors, errors per minute<br><br>* Error rate, top 5 services by error rate, error rate per minute<br><br>* Average latency, top 5 services by average latency, average request latency<br><br>* P95 latency, top 5 services by P95 latency, average P95 request latency |
|Call chain analysis |Display information such as TraceId, status, total latency, start time, end time, and other information |


<span id="6c67bafc"></span>
## Integrate log application


1. Log in to the [TLS console](https://console.byteplus.com/tls/).

2. In the top navigation bar, select the region where TLS is located.

3. In the left navigation pane, select **Common features** \> **Log applications**.

4. On the **Marketplace** tab, select the log application card to be integrated. For example, on the **MQTT** card, click **Integrate application**.

5. Configure the integration application parameters, then click **Integrate application**. The system will automatically redirect to the MQTT console of the Cloud Native Message Engine.

6. Configure the instance in the MQTT console.

   Create an MQTT instance, create a Trace instance for the MQTT instance, configure message tracing, and configure the project.

7. View monitoring charts.

   Return to the TLS console, go to the **Marketplace** tab, on the **MQTT** card, click **View integration list**, and click the name of the integrated log application to view the MQTT call chain observability monitoring charts.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can view the corresponding Trace instance in the TLS console. For details, please refer to <a href="https://docs.byteplus.com/docs/tls/manage_trace_instances">Manage trace instances</a>.   </div>
   

<span id="93dde0a5"></span>
## Delete my application

After the log application is successfully integrated, you can manage the integrated log application:


1. Log in to the [TLS console](https://console.byteplus.com/tls/).

2. In the top navigation bar, select the region where TLS is located.

3. In the left navigation pane, select **Common features** \> **Log applications**.

4. Go to the **Marketplace** tab, on the **MQTT** card, click **View integration list.** 

5. In the **Actions** column of the corresponding log application, click **Delete**. In the delete pop\-up window, confirm deletion of the log application, and click **Delete** again.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">After deleting an integrated MQTT application, the corresponding Trace instance for MQTT in TLS will be deleted synchronously, but the MQTT instance created in the MQTT console will not be deleted.</div>
