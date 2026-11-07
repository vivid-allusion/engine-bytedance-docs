---
title: "Enabling extension module"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/enable_extended_module"
---

Cache for Redis supports extension modules such as ExBloomFilter, ExString, ExTimeSeries, Valkey\-Search, and Valkey\-Json on top of the native Redis data structures, meeting diverse business scenario requirements. This topic describes how to enable extension modules on console.

## **Prerequisites**

* The database version of the instance must be Redis 7.0.

* The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## **Precautions**

* To use the extension module, [submit a ticket](https://console.byteplus.com/workorder/create/) to technical support to apply for usage.

* Enabled extension modules do not support disabling. For more information about extension modules, refer to [Extension module](https://docs.byteplus.com/en/docs/redis/extended-data-structure).

## **Billing instructions**

The current extension module features are free to use. We will inform you, on our website or via a product notification, before a service charge is officially introduced.

## **Procedure**

### **Enable when creating instance**

When creating a Redis instance, you can directly enable the extension module feature and select the desired modules. For specific procedures, refer to [Creating instance](https://docs.byteplus.com/en/docs/redis/create-instance).

### **Enable after instance creation**

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. In the **Configuration area** of the **Summary** tab, click **Enable** next to **Module**.

   > **tip**

   > If you have already enabled some modules, click **Edit** next to **Module**.

5. In the pop\-up dialog box, select the modules to enable, then click **OK**.

   > **tip**

   * > Enabled extension modules do not support disabling. For more information about extension modules, refer to [Extension module](https://docs.byteplus.com/en/docs/redis/extended-data-structure).

   * > Using the Valkey\-Search module consumes a large amount of CPU. Therefore, if the Valkey\-Search module is checked, after enabling the extension module, promptly upgrade the instance node specifications. It is recommended to select a node type with more cores for instance. For specific procedures, refer to [Modifying node specifications](https://docs.byteplus.com/en/docs/redis/modify-node-spec).

   * > After selecting the Valkey\-Search module, if you need to create a JSON\-formatted index, you must also select the Valkey\-JSON module.
