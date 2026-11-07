---
title: "Applying for direct connection address"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/apply-direct-connection-address"
---

Cache for Redis adopts the proxy\-server architecture by default. You can directly access the data shards at the instance backend through a direct connection address (similar to a native architecture that directly connects to the Redis server). This topic describes how to apply for a direct connection address.

## Limits

* Only Redis instances with sharing cluster enabled support direct connection addresses. For more details, refer to [Product architecture](https://docs.byteplus.com/en/docs/redis/product-component-architecture).

* If the number of shards in an instance exceeds 8, the button to request a direct address will be disabled on the Redis console. To request direct addresses for scenarios involving the use of more than 8 shards, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support.

## Precautions

* When a client first uses a direct connection address to access an instance, the direct connection address will be resolved to the fixed Virtual IP (VIP) address allocated by Redis to all shards, and then routed to each data shard via the Redis cluster protocol. Therefore, your client needs to support the Redis cluster protocol.

* If you release the direct connection address and then apply for a new one, the IP address corresponding to the newly applied direct connection address may be different from the previous one. It is recommended to use the direct connection address domain name instead of IP address to access the Redis instance, to avoid connection issues caused by IP address changes.

* Access through direct addresses to save time in processing requests through proxies. In theory, this can shorten the response time of the server to the client, but automatic load balancing, automatic read/write splitting, and other advanced features are lost. We recommend that you exercise due caution when selecting the address type according to your actual needs.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click on the **Connectivity** tab.

5. In the **Private network access \> Direct private network access** section under the **Connectivity** tab, click **Apply**.

6. In the pop\-up dialog box, enter the port number of the direct address, and then click **OK**.

   > **tip**

   * > Direct connection addresses support port numbers ranging from 1024 to 4000 and from 5100 to 64512. After submitting the request, you can also modify the domain name and port number of the direct address. For specific procedures, refer to [Modifying connection address](https://docs.byteplus.com/en/docs/redis/modify-address) and [Modifying port number](https://docs.byteplus.com/en/docs/redis/modify-port).

   * > After submitting the request, you can use the **Direct connect address** received to access Redis instances. To access instances using a direct connection address, refer to [Connecting to instance via a direct address](https://docs.byteplus.com/en/docs/redis/connect-instance-through-direct-connection-address).

## Relevant APIs

|API |Description |
|---|---|
|[CreateDBEndpointDirectLinkAddress](https://docs.byteplus.com/en/docs/redis/createdbendpointdirectlinkaddress) |Call the CreateDBEndpointDirectLinkAddress API to apply for a direct connection address for target Redis instance. |
