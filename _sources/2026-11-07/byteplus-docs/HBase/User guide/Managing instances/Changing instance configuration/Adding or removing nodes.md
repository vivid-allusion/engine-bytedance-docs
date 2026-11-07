---
title: "Adding or removing nodes"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Adding_or_removing_nodes"
---

This article describes how to increase or decrease the number of Region Server nodes in an HBase instance.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Only the number of Region Server nodes can be increased or decreased. The number of Master nodes is fixed and cannot be increased or decreased.

* When reducing the number of nodes, the instance may be disconnected for 1 to 3 minutes. Please proceed with caution. It is recommended to perform conversion operation during off\-peak hours, and ensure clients are configured with proper retry mechanisms.

* If a high\-availability Thrift connection address is enabled for the instance, you must evaluate and adjust the Thrift Server specifications after changing the number of Region Server nodes to ensure service stability. For details, see [Changing high-availability Thrift Server configurations](https://bytedance.larkoffice.com/docx/NFcvdXQU3othO9xL5IOcDaMvnqc#share-W0rndGtZbonsHaxL3rQc9feKnbh).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the top menu bar, select the project and region for the instance.

3. You can access the **add or remove nodes** page in any of the following ways.

   * **Method 1**:

      1. On the **Instances** page, click the name of the target instance.

      2. In the **Configuration** area of the **Summary** page, click **Add or remove nodes** next to **Number of nodes**.

   * **Method 2**:

      1. On the **Instances** page, find the target instance.

      2. Click the **Add or remove nodes** in the **Actions** column to the right of the target instance.

4. On the **Add or remove nodes** page, confirm the current instance specifications and enter the desired number of Region Server nodes after the **Number of nodes** field. The number of Region Server nodes ranges from 2 to 100.

5. Click **Confirm order**.

6. On the **Confirm order** page, confirm the changed instance order details, read and check the terms, and click **Buy now**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[ModifyRSNodeCount](https://docs.byteplus.com/en/docs/HBase/ModifyRSNodeCount) |Call the ModifyRSNodeCount interface to modify the number of RegionServer nodes of the instance. |
