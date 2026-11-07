---
title: "Modifying port"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modify-port"
---

Cache for Redis supports modifying the port numbers of proxy connection private network addresses, direct connection private network addresses, and public network addresses. This topic describes how to modify the port number of the connection address.

## Prerequisites

The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Precautions

* After modifying the port number, the original connection will be disconnected. Promptly modify the connection information of the client and use the new port to connect to the instance. For specific procedures, refer to [Connecting to instance](https://docs.byteplus.com/en/docs/redis/connect-to-instance).

* Modifying the port will temporarily affect access to some services. Operate with caution.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click on the **Connectivity** tab.

5. In the address table of the target access group (**Proxy private network access**/**Direct private network access**/**Proxy public network access**) under the **Connectivity** tab, click![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png)icon next to the corresponding port number field.

   > **tip**

   > To modify the port number of direct connection addresses or public network addresses, you must first apply for the corresponding connection address. For specific procedures, refer to [Applying for direct connection address](https://docs.byteplus.com/en/docs/redis/apply-direct-connection-address) and [Applying for public address](https://docs.byteplus.com/en/docs/redis/apply-public-address).

6. In the pop\-up dialog box, enter the new port number, then click **OK**.

   > **tip**

   * > For instances with the shard cluster feature enabled:

      * > The supported port range for proxy private network addresses and proxy public network addresses is 1024 to 65535.

      * > Direct connection addresses support port numbers ranging from 1024 to 4000 and from 5100 to 64512.

   * > For instances without the shard cluster feature enabled, the supported port range for proxy connection private network addresses, direct connection private network addresses, and proxy public network addresses is 1024 to 65535.

## Relevant APIs

|API |Description |
|---|---|
|[ModifyDBInstanceVisitAddress](https://docs.byteplus.com/en/docs/redis/modifydbinstancevisitaddress) |Call the ModifyDBInstanceVisitAddress API to modify the address or port number of the target connection address of the specified instance. |
