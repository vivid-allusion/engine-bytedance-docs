---
title: "Backup overview"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Backup-overview"
---

To prevent data loss, you can back up index data by creating snapshots. If data loss occurs or you want to retrieve data from a specific time period, you can restore index data.

<span id="264dea67"></span>
## Snapshot

A snapshot is not taken in real time, and it is captured within a specific time window instead. As a result, a snapshot contains data from a particular moment within that time period. When a snapshot is being taken, you can still index documents or perform other operations. However, new documents or updates are typically not included in the snapshot.

Snapshots can be created both automatically and manually. Select a method that fits your business needs. We recommend that you do not enable manual and automatic methods simultaneously, as it impact instance performance.


|**Method** |**Description** |
|---|---|
|Automatic |Snapshots are automatically captured within a specified time window based on predefined rules.<br><br>These snapshots are incremental, automatically eliminating duplicate data. In other words, they store only the data that has changed since the last successful snapshot. This feature not only saves storage space but also reduces network transmission costs and shortens the snapshot creation time. |
|Manual |Snapshots are manually captured to back up current data or indices of the instance.<br><br>A manually created snapshot always backs up the entire index data. |


<span id="c965fefb"></span>
## Snapshot\-based restoration

This feature allows you to restore index data within the same instance or to a different instance.
