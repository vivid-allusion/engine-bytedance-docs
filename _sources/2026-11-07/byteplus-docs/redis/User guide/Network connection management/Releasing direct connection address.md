---
title: "Releasing direct connection address"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/release-direct-connection-address"
---

You can release the direct connection address when clients no longer require direct access to the Redis instance. This article describes how to release direct connection address.

## Prerequisites

You have applied for direct connection address. For specific procedures, refer to [Applying for direct connection address](https://docs.byteplus.com/en/docs/redis/apply-direct-connection-address).

## Precautions

After releasing the direct connection address, the Redis instance will no longer support the Redis cluster protocol, and applications will no longer access the Redis instance via the direct connection address. ensure that the direct address configured by the application has been modified to another type of address, such as a private network address. For more details about connection address types, refer to [Connection address types](https://docs.byteplus.com/en/docs/redis/view-address).

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click on the **Connectivity** tab.

5. In the **private network access \> Direct connection private network access** section under the **Connectivity** tab, in the **Actions** column, click ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9624d842fa735d878a2e10c641f7d568.png).

6. In the pop\-up dialog box, click **OK**.

## Relevant APIs

|API |Description |
|---|---|
|[DeleteDBEndpointDirectLinkAddress](https://docs.byteplus.com/en/docs/redis/deletedbendpointdirectlinkaddress) |Call the DeleteDBEndpointDirectLinkAddress API to release the direct connection address for target Redis instance. |
