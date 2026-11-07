---
title: "Enabling Capacity storage"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Enabling_Capacity_storage"
---

Capacity storage can be used as a cold data storage medium to store infrequently used data, and its price is more favorable than that of ordinary storage media. This article describes how to enable Capacity storage.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

When you enable Capacity storage for an existing instance, the instance must be in the **Running** state.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

You can choose any of the following methods to activate Capacity storage.


* Method 1: Enable Capacity storage when creating an instance

   When creating an instance, choose to enable Capacity storage. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/HBase/Creating_an_instance_1).

* Method 2: Enabling Capacity storage for an existing instance

   1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

   2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   3. On the **Instances** page, click the name of the target instance.

   4. In the **Configuration** area of the **Summary** page, click **Enable Capacity storage** next to **Capacity storage space**.

   5. On the **Capacity storage space** page, select the capacity volume size. The value range is 800 GiB to 1,000,000 GiB in steps of 10 GiB.

   6. Click **Confirm order**.

   7. On the **Confirm order** page, confirm the order details, read and check the terms, and click **Buy now**.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

[Configure hot and cold data separation](https://docs.byteplus.com/en/docs/HBase/Configure_hot_and_cold_data_separation)

<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[ModifyColdStorage](https://docs.byteplus.com/en/docs/HBase/ModifyColdStorage) |Call the ModifyColdStorage API to enable Capacity storage for an instance or modify the Capacity storage space size. |
