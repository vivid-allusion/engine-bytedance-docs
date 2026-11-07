---
title: "Changing storage size"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Changing_storage_size"
---

This article describes how to modify the storage size of an HBase instance.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The default storage space limit supported by each instance is 20,000 GiB, with a step size of 10 GiB. You can contact technical support to raise the limit by [submitting a ticket](https://console.byteplus.com/ticket/createTicketV2/).

* When scaling down, the target storage space cannot be less than 140% of the currently used storage space. Please make a reasonable choice based on your actual business situation. You can view the current amount of storage space used by an instance in the **Configuration** area of the **Summary** page.


<span id=".6LS555So6K-05piO"></span>
## Billing Instructions

Pay\-as\-you\-go instances are postpaid. After scaling up or down, the system will bill you hourly based on the new storage capacity.

Yearly or monthly subscription instances require prepayment. After scaling up or down, the system will charge or refund based on the upgrade or downgrade formula. For details, see [Billing Rules for Resource Subscription Change](https://docs.byteplus.com/en/docs/byteplus-platform/Billing_Rules_for_Resource_Subscription_Change).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. In the **Configuration** area of the **Summary** page, click **Change storage size** next to **Storage space**.

5. On the **Storage space** page, confirm the current instance specifications and select the target storage space.

6. Click **Confirm order**.

7. On the **Confirm order** page, confirm the order details, read and check the terms, and click **Buy now**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[ModifyDBInstanceStorageCapacity](https://docs.byteplus.com/en/docs/HBase/ModifyDBInstanceStorageCapacity) |Call the ModifyDBInstanceStorageCapacity interface to modify the storage capacity of the HBase instance. |
