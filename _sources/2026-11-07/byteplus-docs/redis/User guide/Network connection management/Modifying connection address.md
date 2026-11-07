---
title: "Modifying connection address"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modify-address"
---

Cache for Redis allows you to modify an instance's connection address. You can update the connection address of a new instance to match the original instance's address, eliminating the need to change client connection address code. This topic describes the relevant procedures.

## Prerequisites

The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Precautions

After modifying the connection address, existing connections will be disconnected. Promptly modify the connection information of the client and use the new connection address to connect to the instance. For specific procedures, refer to [Connecting to instance](https://docs.byteplus.com/en/docs/redis/connect-to-instance).

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click on the **Connectivity** tab.

5. Under the **Connectivity** tab, in the address table of the target access group (**Proxy private network access/Direct private network access/Proxy public network access**), in the **Actions** column, click ![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png)icon.

   > **tip**

   > To modify the connection address of direct connection addresses or public network addresses, you must first apply for the corresponding connection address. For specific procedures, refer to [Applying for direct connection address](https://docs.byteplus.com/en/docs/redis/apply-direct-connection-address) and [Applying for public address](https://docs.byteplus.com/en/docs/redis/apply-public-address).

6. In the pop\-up dialog box, enter the new connection address.

   > **tip**

   * > Currently, you can only modify the prefix of the connection address, specifically the part before `redis.ibytepluses.com`  or `redis.bytepluses.com` .

   * > The modified address prefix must meet all the following requirements:

      * > It consists of lowercase letters, numbers, or hyphens (\-).

      * > Start with a letter and end with a letter or number.

      * > The length is 8 to 53 characters.

   * > The modified connection address needs to be globally unique and cannot have the same name as any connection address in any region of BytePlus.

   * > You can simultaneously check **Upgrade domain name suffix** in the current dialog box. After upgrading, the domain name suffix of the connection address will automatically contain the region information to which the instance belongs. If the regions where the instances are located are different, the domain name suffixes will change differently:

      * > Mainland China region: The domain name suffix will change from `redis.ivolces.com` (or `redis.volces.com`) to `redis.{Region ID}.ivolces.com` (or `redis.{Region ID}.volces.com`).

      * > Regions other than Mainland China: The domain name suffix will change from `redis.ibytepluses.com` (or `redis.bytepluses.com`) to `redis.{Region ID}.ibytepluses.com` (or `redis.{Region ID}.bytepluses.com`).

   > The old connection address will be retained for 12 hours and will be automatically released after the expiration of the 12\-hour retention period. For more details, refer to [Upgrading domain name suffix](https://docs.byteplus.com/en/docs/redis/upgrade-domain-suffix).

   * > You can modify the port number of the connection address simultaneously in the current dialog box. The modified port number of the connection address needs to follow corresponding rules. For specific procedures, refer to [Modifying port number](https://docs.byteplus.com/en/docs/redis/modify-port).

7. Click **OK**.

## Relevant APIs

|API |Description |
|---|---|
|[ModifyDBInstanceVisitAddress](https://docs.byteplus.com/en/docs/redis/modifydbinstancevisitaddress) |Call the ModifyDBInstanceVisitAddress API to modify the address or port number of the target connection address of the specified instance. |
