---
title: "Restarting proxy node"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/restart-proxy-node"
---

Cache for Redis supports manually restarting a proxy node, which can be used for real\-time disaster recovery drills or for initiating proactive maintenance in case of service exceptions or high latency. This topic describes how to restart proxy nodes through the Redis console.

## Prerequisite

The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Precautions

* Instances that have not enabled the shard cluster feature and have selected direct connection mode do not have proxy nodes.

* Restarting proxy node impacts existing connections. Please operate during off\-peak hours and ensure that the business has a reconnection mechanism.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance name.

4. In the **Topology** pane under the **Summary** tab, click the![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_313f0c447e2102d24a607a9acf78bc11.png)icon to switch to the proxy node list.

5. In the proxy nodes list below, check the nodes to be restarted, and click **Batch restart** in the lower\-left corner of the list.

6. In the dialog box that appears, confirm the impact, then click **OK**.

   > **tip**

   > When the instance status changes from **ProxyRestarting** to **Running**, it indicates that the proxy is successfully restarted and the database can now provide services to external users. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Relevant APIs

|API |Description |
|---|---|
|[RestartDBInstanceProxy](https://docs.byteplus.com/en/docs/redis/restartdbinstanceproxy) |Call the RestartDBInstanceProxy API to restart one or more proxy nodes in a specified Redis instance. |
