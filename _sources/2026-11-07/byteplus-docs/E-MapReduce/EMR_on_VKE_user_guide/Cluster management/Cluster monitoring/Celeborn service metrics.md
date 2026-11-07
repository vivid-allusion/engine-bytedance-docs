---
title: "Celeborn service metrics"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Celeborn_service_metrics"
---

This document provides detailed information about Celeborn metrics.

Celeborn metrics consist of the following three sections:


* [Overview](https://docs.byteplus.com/docs/E-MapReduce/109066#bb5bf5a4)

* [Celeborn Master](https://docs.byteplus.com/docs/E-MapReduce/109066#3f6fdf60)

* [Celeborn Worker](https://docs.byteplus.com/docs/E-MapReduce/109066#e7c99821)


<span id="bb5bf5a4"></span>
## Overview


|metric name |Unit |
|---|---|
|Celeborn OfferSlotsTime P99 |Time |
|Celeborn OfferSlotsTime P75 |Time |
|Celeborn OfferSlotsTime P50 |Time |
|Celeborn Partition size |Bytes |
|Celeborn Worker count |Count |
|Celeborn Lost Worker count |Count |
|Celeborn Excluded Worker count |Count |
|Celeborn RunningApplication count |Count |
|Celeborn ActiveShuffle size |Bytes |
|Celeborn ActiveShuffleFile count |Count |
|Celeborn DiskFile count |Count |
|Celeborn DiskBytes write size |Bytes |
|Celeborn PrimaryPushDataTime P99 |Time |
|Celeborn PrimaryPushDataTime P75 |Time |
|Celeborn PrimaryPushDataTime P50 |Time |
|Celeborn ReplicaPushDataTime P99 |Time |
|Celeborn ReplicaPushDataTime P75 |Time |
|Celeborn ReplicaPushDataTime P50 |Time |
|Celeborn FlushDataTime P99 |Time |
|Celeborn FlushDataTime P75 |Time |
|Celeborn FlushDataTime P50 |Time |
|Celeborn CommitFilesTime P99 |Time |
|Celeborn CommitFilesTime P75 |Time |
|Celeborn CommitFilesTime P50 |Time |
|Celeborn ReserveSlotsTime P99 |Time |
|Celeborn ReserveSlotsTime P75 |Time |
|Celeborn ReserveSlotsTime P50 |Time |
|Celeborn SortTime P99 |Time |
|Celeborn SortTime P75 |Time |
|Celeborn SortTime P50 |Time |
|Celeborn SlotsAllocated Count |Count |
|Celeborn ActiveConnection Count |Count |
|Celeborn NettyMemory |Bytes |
|Celeborn SortingFiles Count |Count |
|Celeborn DeviceOSFreeBytes |Bytes |
|Celeborn DeviceOSTotalBytes |Bytes |
|Celeborn DeviceCelebornFreeBytes |Bytes |
|Celeborn DeviceCelebornTotalBytes |Bytes |


<span id="3f6fdf60"></span>
## Celeborn Master


|metric name |Unit |
|---|---|
|Celeborn Master JVM CPU usage time |Time |
|Celeborn Master is primary | |
|Celeborn Master FGC times |Times |
|Celeborn Master heap memory usage rate |Percentage |
|Celeborn Master Pool Size |Count |
|Celeborn Master Core Pool Size |Count |
|Celeborn Master Maximum Core Pool Size |Count |
|Celeborn Master Largest Core Pool Size |Count |


<span id="e7c99821"></span>
## Celeborn Worker


|metric name |Unit |
|---|---|
|Celeborn Worker RunningApplication count |Count |
|Celeborn Worker ActiveShuffle size |Bytes |
|Celeborn Worker ActiveShuffleFile count |Count |
|Celeborn Worker DiskFile count |Count |
|Celeborn Worker DiskBytes write size |Bytes |
|Celeborn Worker heap memory usage rate |Percentage |
|Celeborn Worker FGC times |Count |
|Celeborn Worker Pool Size |Count |
|Celeborn Worker Core Pool Size |Count |
|Celeborn Worker Maximum Core Pool Size |Count |
|Celeborn Worker Largest Core Pool Size |Count |
