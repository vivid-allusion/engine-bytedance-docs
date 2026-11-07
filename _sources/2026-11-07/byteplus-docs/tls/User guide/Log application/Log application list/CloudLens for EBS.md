---
title: "CloudLens for EBS"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/CloudLens_for_EBS"
---

This section introduces the CloudLens for EBS cloud product monitoring log application provided in the TLS application marketplace.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">CloudLens for EBS is an invite\-only feature. To enable allowlist access for relevant business needs, contact your account manager.</div>


<span id="cde39a6e"></span>
## Overview

Focusing on elastic block storage, this application provides a resource overview and performance monitoring, offering basic information such as the number, capacity, regional distribution, and disk type distribution of cloud disks from the previous day under the current account, as well as real\-time collection and storage of second\-level monitoring data for cloud disk performance.

<span id="277f17f1"></span>
## Monitoring chart details

The monitoring chart details for TLS CloudLens for EBS are as follows:


* Resource overview

   Minute\-level metrics, including usage and performance metrics, are available free of charge.

   
   |Type |Chart |
   |---|---|
   |Capacity and quantity |* <div style="text-align: start-_pOwxG"><br>Total number of cloud disks, total capacity of cloud disks</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Total number of snapshots, total capacity of snapshots</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Proportion of cloud disks with snapshots created</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Number of ESSD FlexPL cloud disks with performance burst enabled</div><br> |
   |Distribution |* <div style="text-align: start-_pOwxG"><br>Specification type distribution (cloud disk quantity), specification type distribution (cloud disk capacity)</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Payment type distribution (cloud disk quantity), payment type distribution (cloud disk capacity)</div><br> |
   

* Performance overview

   Minute\-level metrics, including usage and performance metrics, are available free of charge.

   
   |Type |Chart |
   |---|---|
   |Performance trends |* Throughput (MBps)<br><br>* IOPS (operations/s) |
   |Top 100 cloud disk performance |* Write throughput, write IOPS, write latency (maximum), write latency (average)<br><br>* Read throughput, read IOPS, read latency (maximum), read latency (average) |
   

* Data dashboard

   Second\-level metrics, including performance metrics, support throughput, IOPS, latency, and more. Additional charges apply and can be configured as needed.

   
   |Type |Chart |
   |---|---|
   |Second\-level monitoring |* <div style="text-align: start-_pOwxG"><br>Cloud disk read/write throughput (MBps)</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Cloud disk read/write IOPS (operations/s)</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>IO latency (ms)</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Average IO read/write size (Bytes)</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>BPS threshold (%)</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>IOPS threshold (%)</div><br> |
   |Burst lo |Burst lo for a custom time period |
   


<span id="e579005e"></span>
## Steps to integrate log applications

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">After the CloudLens for EBS log application is created successfully, modification and cancellation of access are not supported.</div>



1. Log in to the [TLS console](https://console.byteplus.com/tls/).

2. In the top navigation bar, select the region where TLS is located.

3. In the left navigation bar, select **Common features** \> **Log applications**.

4. On the **Marketplace** tab, select the log application card to be integrated. For example, on the **CloudLens for EBS** card, click **Integrate application**.

5. Confirm the following information as prompted on the interface, then click **Submit**.

   
   |Parameters |Note |
   |---|---|
   |Billing information |After accessing EBS access logs, TLS will charge based on storage space, read traffic, request count, data transformation, log shipping, and more. |
   |Authorize RAM access |Grant cross\-service access permissions. |
   

6. After successful integration, you will enter the dashboard page by default.
