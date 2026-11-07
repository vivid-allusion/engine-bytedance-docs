---
title: "Upgrading domain suffix"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/upgrade-domain-suffix"
---

Cache for Redis offers a feature to upgrade the connection address domain suffix. The upgraded suffix automatically includes the instance's region information, enabling quick identification of the connection address's region. This topic describes how to upgrade the domain suffix.

## Prerequisites

The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Precautions

* After the domain name suffix of the connection address is upgraded, the domain name will take effect in all regions under BytePlus. That is, after upgrading the connection address domain name, the domain name can be resolved to the corresponding IP address in the regions of BytePlus, improving the convenience of multi\-region domain name management.

* After the connection address domain suffix is upgraded, downgrading back to the original suffix is not supported. Proceed with caution.

* After upgrading, the domain name suffix of the connection address will automatically contain the region information to which the instance belongs. If the regions where the instances are located are different, the domain name suffixes will change differently:

   * Mainland China region: The domain name suffix will change from `redis.ivolces.com` (or `redis.volces.com`) to `redis.{Region ID}.ivolces.com` (or `redis.{Region ID}.volces.com`).

   * Regions other than Mainland China: The domain name suffix will change from `redis.ibytepluses.com` (or `redis.bytepluses.com`) to `redis.{Region ID}.ibytepluses.com` (or `redis.{Region ID}.bytepluses.com`).

   The old connection address will be retained for 12 hours and will be automatically released after the expiration of the 12\-hour retention period.

* After the domain name suffix upgrade, existing established connections will continue to work normally without being automatically disconnected. However, new connections must use the new connection address domain name. Promptly update your client configuration to use the new connection address. For specific procedures, refer to [Connecting to instance](https://docs.byteplus.com/en/docs/redis/connect-to-instance).

* To upgrade the connection address domain suffix for a direct connection address or public network address, you must first apply for the corresponding connection address. For specific procedures, refer to [Applying for direct connection address](https://docs.byteplus.com/en/docs/redis/apply-direct-connection-address) and [Applying for public network address](https://docs.byteplus.com/en/docs/redis/apply-public-address).

* After upgrading the domain suffix of a direct connection address or public network address, even if you release and reapply for the corresponding connection address, the domain suffix will not revert to its original suffix. Proceed with caution.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click on the **Connectivity** tab.

5. Find the address to be upgraded under the **Connectivity** tab, and click  ![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png)icon on the right of the tags.

   > **tip**

   * > To upgrade the connection address domain suffix for a direct connection address or public network address, you must first apply for the corresponding connection address. For specific procedures, refer to [Applying for direct connection address](https://docs.byteplus.com/en/docs/redis/apply-direct-connection-address) and [Applying for public network address](https://docs.byteplus.com/en/docs/redis/apply-public-address).

   * > After upgrading the domain suffix of a direct connection address or public network address, even if you release and reapply for the corresponding connection address, the domain suffix will not revert to its original suffix. Proceed with caution.

6. Under the **Connection address** text box in the pop\-up dialog box, check **Domain name upgrade suffix**.

   > **tip**

   * > After the connection address domain suffix is upgraded, downgrading back to the original suffix is not supported. Proceed with caution.

   * > After upgrading, the domain name suffix of the connection address will automatically contain the region information to which the instance belongs. If the regions where the instances are located are different, the domain name suffixes will change differently:

      * > Mainland China region: The domain name suffix will change from `redis.ivolces.com` (or `redis.volces.com`) to `redis.{Region ID}.ivolces.com` (or `redis.{Region ID}.volces.com`).

      * > Regions other than Mainland China: The domain name suffix will change from `redis.ibytepluses.com` (or `redis.bytepluses.com`) to `redis.{Region ID}.ibytepluses.com` (or `redis.{Region ID}.bytepluses.com`).

   > The old connection address will be retained for 12 hours and will be automatically released after the expiration of the 12\-hour retention period.

   * > After the domain name suffix upgrade, existing established connections will continue to work normally without being automatically disconnected. However, new connections must use the new connection address domain name. Promptly update your client configuration to use the new connection address. For specific procedures, refer to [Connecting to instance](https://docs.byteplus.com/en/docs/redis/connect-to-instance).

   * > You can modify the prefix or port number of the connection address simultaneously in the current dialog box. The modified prefix and port number of the connection address needs to follow corresponding rules. For specific procedures, refer to [Modifying address](https://docs.byteplus.com/en/docs/redis/modify-address) and [Modifying port number](https://docs.byteplus.com/en/docs/redis/modify-port).

7. Click **OK**.

## Relevant APIs

|API |Description |
|---|---|
|[ModifyDBInstanceVisitAddress](https://docs.byteplus.com/en/docs/redis/modifydbinstancevisitaddress) |Call the ModifyDBInstanceVisitAddress API to modify the address or port number of the target connection address of the specified instance. |
