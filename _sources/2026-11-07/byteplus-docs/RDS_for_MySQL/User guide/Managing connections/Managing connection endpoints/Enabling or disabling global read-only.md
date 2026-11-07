---
title: "Enabling or disabling global read-only"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_or_disabling_global_read-only"
---

Enabling global read\-only ensures that a MySQL instance can only be read from, not written to. This topic describes how to enable or disable global read\-only for an instance.

## Prerequisites

An instance is created and in the **Running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

## Precautions

Enabling global read\-only will set the instance to read\-only mode, which only supports query operations and doesn't support any update, write, delete or other update operations. Operate carefully.

## Procedure

1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the top menu bar, select the project and region for the instance.

> **tip**

> If the project of the instance has not been set, the project should be selected as **All resources**.

3. Click **Instances** in the left navigation bar.

4. Click the name of the target instance on the **Instances** page to go to the **Summary** page.

5. On the **Summary** page, in the **Configuration** section, click the edit switch for **Global read\-only**.

6. In the **Switch global read\-only** dialog box, click the switch button and then click **OK**.

## Related API

|API |Description |
|---|---|
|[ModifyDBInstanceGlobalReadOnly](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstanceglobalreadonly) |Call the ModifyDBInstanceGlobalReadOnly API to enable or disable the global read\-only feature for an instance. |
