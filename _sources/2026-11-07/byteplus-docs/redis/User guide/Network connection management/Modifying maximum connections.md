---
title: "Modifying maximum connections"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modify-max-conn-number"
---

Redis cache database supports modifying the maximum number of connections. This allows you to increase the maximum connections for a single shard without changing the current instance specification, helping you easily cope with demand peaks caused by a large number of concurrent program requests.

## Precautions

* Increasing the maximum number of connections has no impact on your business.

* The default connection number of each Redis single shard for all specifications is 10,000, and the **overall number of connections of an instance cannot exceed 1,000,000 at most**. Therefore, if you need to increase the number of connections, ensure that the upper limit of the overall number of connections of an instance = min[(number of shards × maximum number of connections of a single shard), 1,000,000]. For more details, refer to [Connection number description](https://docs.byteplus.com/en/docs/redis/product-specification#.6L-e5o6l5pWw6K-05piO).

* If you need to reduce the maximum number of connections, you must ensure that the number of existing connections does not exceed the modified maximum number of connections. Otherwise, it will cause the existing connections to be disconnected and also prevent new connections from being established.

* After the maximum number of connections is reached, the system will refuse to create new connections.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. In the **Configuration** area of the **Summary** tab, click ![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png) icon after **Max connections.**

5. In the popped\-up dialog box, set the **Max connections per shard** according to business needs.

   > **tip**

   * > The default number of connections per Redis shard for all specifications is 10,000, with a value range of 10,000 to 50,000 and with a step size of 1,000.

   * > **The maximum number of connections for the entire instance cannot exceed 1,000,000**. Therefore, if you need to increase the number of connections, ensure that the upper limit of the overall number of connections of an instance = min[(number of shards × maximum number of connections of a single shard), 1,000,000].

   > For example, if you purchased a 51\-shard instance and adjusted the maximum number of connections per shard from the default 10,000 to 20,000, then the overall maximum number of connections for the instance is min[(51 x 20,000), 1,000,000] = 1,000,000. For more details, refer to [Connection number description](https://docs.byteplus.com/en/docs/redis/product-specification#.6L-e5o6l5pWw6K-05piO).

   * > After the maximum number of connections is reached, the system will refuse to create new connections.

6. Click **OK**.

   After modifying the maximum number of connections, the instance status changes to **ParameterModifying**. When the instance status changes to **Running**, it indicates a successful modification, and the database can then provide services. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Relevant APIs

|API |Description |
|---|---|
|[ModifyDBInstanceMaxConn](https://docs.byteplus.com/en/docs/redis/modifydbinstancemaxconn) |Call the ModifyDBInstanceMaxConn API to modify the maximum number of connections per shard of the specified Redis instance. |
