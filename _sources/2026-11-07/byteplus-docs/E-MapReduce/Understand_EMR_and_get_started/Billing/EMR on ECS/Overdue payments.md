---
title: "Overdue payments"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs_overdue_payments"
---

E\-MapReduce (EMR) cluster instances are at risk of being stopped if payment is overdue. The system will remind or notify you, so please [Renewal policy](https://docs.byteplus.com/docs/E-MapReduce/109016) promptly to avoid any impact on your services.


|**Billing methods** |**Arrears policy** |
|---|---|
|Pay\-As\-You\-Go |* An account is in arrears if the account balance is less than zero yuan.<br><br>* Within two hours after the account becomes overdue, EMR and ECS will remain in the  **"Running"**  state, and the account will receive an overdue notification.<br><br>* If your account is overdue for more than two hours, the resources of your EMR cluster will enter a retention period and resource usage will be restricted. The EMR service will be shut down, and the related resources will be in the "**Expired**" status.<br><br>   * Overdue by 2 hours < resource retention period < overdue by 15 days and 2 hours<br><br>   * During the retention period, the following specific operations are restricted:<br><br>      * Create a cluster<br><br>      * Cluster expansion<br><br>      * Scale in clusters<br><br>      * Disk expansion<br><br>      * Reconfigure nodes<br><br>      * Release clusters<br><br>      * All service operations<br><br>   * During the resource retention period, after the bill is settled, EMR nodes that were previously shut down due to overdue payments will automatically start and enter the **Recovering** state, and eventually enter the **Running** state.<br><br>* If the resource retention period is exceeded, your resources will be forcibly reclaimed, and the data and configurations within the associated clusters will be released. Once resources are reclaimed, they cannot be restored.<br><br>* Please promptly recharge and settle any overdue bills within the specified time to avoid being unable to use the cluster normally. |
|Subscription |* If the account balance is less than zero, the account is in arrears.<br><br>* If your account is overdue, you can still use any purchased EMR clusters that have not yet expired as usual.<br><br>* However, if you need to purchase new instances or expand the disk capacity of nodes, you must settle any outstanding account balance at the time of billing before you can perform these operations. |
