---
title: "Instance status table"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Instance_status_table"
---

This document describes the status table for EMR Servereless OLAP instances.


|**Status** |**Note** |**Allowed operations** |
|---|---|---|
|Pending payment |The instance creation order has not been paid. The instance will be created only after the order is paid. |*  |
|Starting |The instance is being created. |*  |
|Running |The instance is running normally. |Instance scaling, restart, configuration upgrade, release |
|Deactivated |After the instance expires, it becomes unavailable. Renewing the instance restores it to the running state.<br><br>After payment is overdue, the instance is retained for 15 days. After the retention period, it is automatically released. |Renew |
|Releasing |The instance is being released. |*  |
|Changing |The instance is undergoing scaling, restart, or configuration upgrade. After the operation is completed, the instance returns to the running state. |*  |
|Exception |EMR Servereless OLAP instance process exceptions, or upgrades, scaling, restart, or configuration changes cause the EMR Servereless OLAP service to be unavailable. |Release, renew |
