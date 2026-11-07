---
title: "Overdue payments"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/vke_verdue_payments"
---

Byteplus EMR on VKE cluster instances are at risk of shutdown if overdue payments occur. The system will remind or notify you to prevent any impact on your services.


|Billing methods |Overdue payment policy |
|---|---|
|Pay\-As\-You\-Go |* An account balance less than 0 yuan is considered overdue.<br><br>* Within 2 hours after an account becomes overdue, EMR and VKE will remain in the "**Running**" state, and you will receive an overdue notification.<br><br>* If the account remains overdue for more than 2 hours, the resources of your EMR cluster will enter a retention period, and resource usage will be restricted. The EMR service will be shut down, and the related resources will enter the "**Stopped**" state.<br><br>   * Overdue for 2 hours < retention period < overdue for 15 days and 2 hours<br><br>   * During the retention period, the following operations are restricted:<br><br>      * Create virtual cluster<br><br>      * Expand virtual cluster<br><br>      * Shrink virtual cluster<br><br>      * Expand disk<br><br>      * Change node configuration<br><br>      * Release virtual cluster<br><br>      * All service operations<br><br>   * During the retention period, after settling the bill, EMR nodes that were shut down due to overdue payments will automatically start and enter the "**Recovering**" state, and finally enter the "**Running**" state.<br><br>* If the retention period is exceeded, your resources will be forcibly reclaimed, and all data and configurations within the relevant clusters will be released. Once resources are reclaimed, they cannot be restored.<br><br>* Please [top up](https://docs.byteplus.com/zh-CN/docs/byteplus-platform/docs-overview-2) and settle your overdue bill within the specified period to avoid disruption to your cluster usage. |
