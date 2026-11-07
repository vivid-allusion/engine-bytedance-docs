---
title: "Upgrading storage type"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Upgrading_storage_type"
---

NDB for MySQL supports upgrading the storage type from smart compressed to IO performance. This article describes how to upgrade the storage type.

<span id="qIsZ5kNj"></span>
## Prerequisites

The storage type of the instance is **Intelligent compression**. For details about the two storage types and their price differences, refer to [Storage type comparison](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Storage#hGEe8xbZ).

<span id="aVChPQVu"></span>
## Limitations

You can only upgrade the storage type from smart compressed to IO performance. Downgrading the storage type is not supported.

<span id="cvNW1OMN"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the instance name of the target instance to enter the **Summary** page.

4. In the **Configuration** area, click **Upgrade storage type** to the right of **Storage type**.

5. In the pop\-up **Upgrade storage type** dialog box, confirm the storage type and configuration fee before and after the change, and click **OK**.


<span id="G9TDwggp"></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[ModifyDBInstanceStorageType](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceStorageType) |Call the ModifyDBInstanceStorageType API to modify the storage type. |
