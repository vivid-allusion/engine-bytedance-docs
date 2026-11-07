---
title: "Enabling fast specification change"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Enabling_fast_specification_change"
---

Enabling fast specification change is a feature toggle for older instances. Once enabled, general\-type instances can scale up or down without a restart. This document describes how to enable fast specification change.

## Precautions

This is an allowlist feature. To use it, [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical support and apply.

## Procedure

1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the instance name of the target instance to enter the **Summary** page.

4. In the **Basic information** section, click **Enable** next to **Fast specification change**.

5. Select the execution method in the dialog box that pops up.

   * **Execute now** (default): Immediately starts the fast specification change. The instance enters the **Upgrading version** state. At this time, other operations are not allowed on the instance.

   * **Execute during maintainable window**: Starts the fast specification change during the maintenance time window. For details about the maintenance time window, refer to [Configuring maintenance window](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Configuring_maintenance_window).

   > **tip**

   > After the fast specification change is enabled, the instance will experience a transient disconnection when completing the capability upgrade and switch. Therefore, we recommend that you perform this operation during off\-peak hours and ensure that the application has an automatic reconnection mechanism.

6. Click **OK**.

## Subsequent Operations

[Changing node specifications](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Changing_node_specifications)
