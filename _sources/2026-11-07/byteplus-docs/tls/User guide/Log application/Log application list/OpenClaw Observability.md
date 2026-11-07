---
title: "OpenClaw Observability"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/OpenClaw_Observability"
---

This section introduces the OpenClaw Observability application for large model monitoring, available in the TLS application marketplace.

<span id="d4eb68d4"></span>
## Overview

By integrating the OpenClaw Observability application, you can observe data and access services such as the OpenClaw Observability dashboard, Trace call chain, and CacheTrace log analysis.

<span id="a2fb5a4f"></span>
## Monitoring chart details

The monitoring chart details for the OpenClaw Observability application in TLS are as follows:


* OpenClaw Observability dashboard

   
   |Type |Chart |
   |---|---|
   |Overview |* Total tokens, total cost, number of conversations, total sessions, message analysis, error messages<br><br>* Average token consumption per conversation, average cost per conversation<br><br>* Average token consumption, average cost consumption<br><br>* Model token consumption distribution, model cost distribution<br><br>* Provider token consumption distribution, provider cost distribution<br><br>* Agent token consumption distribution, agent cost distribution<br><br>* Host token consumption distribution, host cost distribution<br><br>* Daily tokens, daily cost, daily top 5 host token consumption, daily top 5 host cost<br><br>* Top 5 tool invocation analysis, queue depth P95, message processing rate |
   |Performance analysis |* Model invocation latency P95, message processing latency P95,<br><br>* Blocked session duration P95, blocked session alerts, session state change count<br><br>* Queue wait latency P95, queue depth P95, throughput per queue lane<br><br>* Webhook processing latency P95, webhook receive rate, webhook error count |
   |Security audit |Authentication failure count, connection failure count, pairing change count, access to sensitive data |
   

* Operations observability

   
   |Type |Chart |
   |---|---|
   |Application logs |Application log charts (including time, level, subsystem, content) |
   |Operations dashboard |* Top 5 gateway subsystem Exception logs, gateway log distribution, gateway exit count, gateway configuration change count<br><br>* gateway Exception overview_Daily, tools execution failure_Daily, websocket error_Daily, configuration error_Daily<br><br>* gateway Exception distribution, tools execution failure_by cause, websocket error_by cause, configuration error_by cause |
   

* Trace call chain

   
   |Type |Chart |
   |---|---|
   |Trace analysis |Trace analysis (data retrieval limit is 50,000 entries) |
   

* CacheTrace analysis

   
   |Chart |Note |
   |---|---|
   |CacheTrace analysis |Includes RUN ID, Total Token, start time, end time, and content for CacheTrace analysis |
   

* Topic list

   Displays the projects and log topics corresponding to the following log types:

   * App logs

   * Configuration logs

   * Trace logs

   * Metric

   * Session logs

   * CacheTrace (CacheTrace logs must be configured. )


<span id="6747f42e"></span>
## Integrate log applications

For steps to integrate the OpenClaw Observability log application, see [Integrate OpenClaw observation](https://docs.byteplus.com/docs/tls/Integrate_OpenClaw_observability).

<span id="f73ba397"></span>
## Manage my applications

After successfully integrating a log application, you can perform the following management operations on the integrated log applications:


1. Log in to the [TLS console](https://console.byteplus.com/tls/).

2. In the top navigation bar, select the region where TLS is located.

3. In the left navigation bar, select **Common features** \> **Log applications**.

4. Go to the **My applications** tab. In the **Actions** column for the corresponding log application, the following management operations are supported:

   
   |Operation |Note |
   |---|---|
   |Access management |Click **Access management** to enter the **Access management** tab, where you can modify the name and description of the log application being accessed. |
   |Cancel access |Click **Cancel access**, confirm the information in the cancel access dialog, and then click **Cancel access** again. |
