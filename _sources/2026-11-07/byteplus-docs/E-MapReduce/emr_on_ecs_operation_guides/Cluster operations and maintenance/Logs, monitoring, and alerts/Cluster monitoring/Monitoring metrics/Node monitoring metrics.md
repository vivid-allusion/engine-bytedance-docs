---
title: "Node monitoring metrics"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Node_monitoring_metrics"
---

This document provides detailed information about Node monitoring metrics.

<span id="6b4f6438"></span>
# Limits

Only supported for EMR\-V3.8.0 and later cluster versions.

<span id="2aee5d97"></span>
# Overview

The Overview page allows filtering by time period and viewing Top N charts for node load metrics.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0942621015664585b0296a7019bfd1f0~tplv-goo7wpa0wc-image.image) </span>

Supported load metrics are listed in the table below:


|**metric name** |**Unit** |
|---|---|
|Top N node memory usage |% |
|Top N node CPU usage |% |
|Top N node system disk storage usage |% |
|Top N node data disk storage usage |% |
|Top N node total disk read throughput |KB/s |
|Top N node total disk write throughput |KB/s |
|Top N node total network inbound throughput |B/s |
|Top N node total network outbound throughput |B/s |


<span id="35c9ef9b"></span>
# Node

The Node page allows filtering by time period and viewing load metric charts for single or multiple nodes, with up to 100 nodes displayed at a time.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ecb8fffa5e594fe5a16d80580a5493fa~tplv-goo7wpa0wc-image.image) </span>

Details of supported load metrics are as follows:


* CPU

   
   |**Metric type** |**metric name** |**Unit** |
   |---|---|---|
   |CPU usage |CPU usage |% |
   |CPU usage details |CPU usage (User) |% |
   ||CPU usage (System) |% |
   ||CPU usage (IoWait) |% |
   ||CPU usage (Other) |% |
   |Average system load per CPU core |vCPU 1\-minute average load |Not applicable |
   ||vCPU 5\-minute average load |Not applicable |
   ||vCPU 15\-minute average load |Not applicable |
   

* Memory

   
   |**Metric type** |**metric name** |**Unit** |
   |---|---|---|
   |Memory usage |Memory usage |% |
   |Memory details |Total memory |GiB |
   ||Memory available |GiB |
   ||Memory free |GiB |
   

* Disk

   
   |**metric name** |**Unit** |
   |---|---|
   |Disk free space |GB |
   |Disk usage |% |
   |Total disk |GiB |
   |Disk read IOPS |ops/s |
   |Disk write IOPS |ops/s |
   |Disk read bandwidth |B/s |
   |Disk write bandwidth |B/s |
   |Disk inode usage |% |
   

* Network

   
   |**Metric type** |**metric name** |**Unit** |
   |---|---|---|
   |Network inbound and outbound rate |Network inbound rate |KiB/s |
   ||Network outbound rate |KiB/s |
   |Network packet inbound and outbound rate |Network packet inbound rate |Packet/s |
   ||Network packet inbound and outbound rate |Packet/s |
   |Network error packet count |Network error packet received count |count |
   ||Network error packet sent count |count |
   |TCP connection count by state |Total TCP connection count |count |
   ||TCP ESTABLISHED connection count |count |
   ||TCP LISTEN connection count |count |
   ||TCP TIMEWAIT connection count |count |
   |TCP packet send and receive count |TCP packet received count |count |
   ||TCP packet sent count |count |
