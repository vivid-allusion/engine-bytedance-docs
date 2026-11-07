---
title: "Enabling or disabling private network access"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/Enabling_or_disabling_private_network_access"
---

The private network access feature for Cache for Redis instances can be enabled or disabled on demand. This topic describes how to enable and disable direct private network access.

## Prerequisite

The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Precautions

* The private network access feature cannot be disabled for instances with the shard cluster feature enabled.

* For instances where the shard cluster feature is not enabled, the private network access feature supports two modes: proxy and direct connection. These two modes can be enabled or disabled independently, but cannot be disabled simultaneously.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click on the **Connectivity** tab.

5. On the **Connectivity** tab, in the **Proxy connection private network access** or **Direct connection private network access** section, click **Enable** or **Disable**, then click **OK** in the dialog box that appears.

> **tip**

> The port number for proxy connection private network addresses and direct connection private network addresses is 6379 by default and can be modified within the range of 1024 to 65535. For details on modifying the port number, see [Modifying port](https://docs.byteplus.com/en/docs/redis/modify-port?lang=zh).
