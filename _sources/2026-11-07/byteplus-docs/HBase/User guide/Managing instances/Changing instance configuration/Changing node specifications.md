---
title: "Changing node specifications"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Changing_node_specifications"
---

This article describes how to modify the node specifications of an HBase instance.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* During the node specification change process, the instance may be disconnected for 1 to 3 minutes. Please proceed with caution. It is recommended to perform conversion operation during off\-peak hours, and ensure clients are configured with proper retry mechanisms.

* The specifications of the Master node and Region Server node can be upgraded and downgraded together, or one can be upgraded and the other downgraded, or the specification of only one node can be changed.

* If your instance has a high\-availability Thrift connection address enabled, you must also evaluate and adjust the Thrift Server specifications after changing the RegionServer node specifications to ensure service stability. For details, see [Changing high-availability Thrift Server configurations](https://bytedance.larkoffice.com/docx/NFcvdXQU3othO9xL5IOcDaMvnqc#share-W0rndGtZbonsHaxL3rQc9feKnbh).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. In the **Configuration** area of the **Summary** page, click **Change specification** next to **Node specification**.

5. On the **Change specification** page, confirm the current instance specifications and select appropriate specifications for the Master and Region Server nodes based on business needs.

6. Click **Confirm order**.

7. On the **Confirm order** page, confirm the changed instance order details, read and check the terms, and click **Buy now**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[ModifyDBInstanceSpec](https://docs.byteplus.com/en/docs/HBase/ModifyDBInstanceSpec) |Call the ModifyDBInstanceSpec interface to modify the node specifications of a specified HBase instance. |
