---
title: "Automatic and manual renewal"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/automatic-manual-renewal"
---

A subscription instance has an expiring date. Renew the instance promptly before it is closed and deleted to avoid affecting your business due to instance expiration. This topic introduces how to enable automatic renewal and manual renewal.

## Prerequisites

The target yearly or monthly subscription instance needs to meet the following conditions at the same time:

* The instance status is not **Creating, Unavailable, or Deleting**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

* The target instance is not deleted compulsorily. After a subscription instance expires, it will be retained for a period of time but not deleted immediately, and you will need to renew it before it is forcibly deleted. For more details on renewal, refer to [Renewal](https://docs.byteplus.com/en/docs/redis/renewal).

## Enable automatic renewal

> **tip**

> For details on auto\-renewal rules for billing center, refer to [Auto\-renewal rules](https://docs.byteplus.com/en/docs/byteplus-platform/docs-auto-renewal-rules).

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. You can go to the **Enable auto\-renewal** page via any of the methods below.

   |Method description |Procedure |
   |---|---|
   |Enter through the Redis instance list page |1. In the top menu bar, select the project and region to which the instance belongs.<br><br>2. On the **Instances** page, click the target instance.<br><br>3. On the **Summary** tab, in the **Billing information** area, click **Enable** next to **Automatic renewal**. |
   |Enter through the upper right corner navigation |1. In the upper right corner of the console, click the user's image and select **Billing.** <br><br>2. In the left navigation bar of the **Billing center** page, select **Renewal management.** <br><br>3. On the **Renewal management** page, use the search and filtering functions to find the target Redis instance in **Manual renewal ** or **Non\-renewal upon expiration instances** tab.<br><br>4. Select the target instances, then click **Enable auto\-renewal** below the instances list.<br><br>   > **tip**<br>   <br><br>   > You can also select multiple instances to enable the automatic renewal feature in batches.<br>    |

3. on the **Enable auto\-renewal** page, in the **Confirm renewal information** area, confirm the information about the instance to be renewed (such as the instance ID and the current expiration time), and then configure the following parameters according to your business needs.

   |Parameters |Description |
   |---|---|
   |Set interval for auto\-renewal |The length of each renewal. The available lengths are listed below:<br><br><br>* Monthly renewal: 1 to 11 months.<br><br>* Annual renewal: 1 to 3 years. |
   |Set auto\-renewal times |You can choose the number of auto\-renewals according to your business needs with the following range of values:<br><br><br>* **Unlimited**.<br><br>* **Custom**.<br><br>   > **tip**<br>   <br><br>   * > If **Custom** is selected, you must also set the specific number of times. You can set a maximum of 100 automatic renewals each time.<br>   <br><br>   * > After the custom count is used up, it will revert to manual renewal. Proceed with caution.<br>    |

4. Click **Enable**.

   > **tip**

   > On the **Auto\-renewal** tab, you can check the details about the instances for which the auto renewal function has been successfully enabled, such as expiration time, renewal cycle, and so on.

## Manual renewal

> **tip**

> For details on manual renewal rules for billing center, refer to [Manual renewal rules](https://docs.byteplus.com/en/docs/byteplus-platform/docs-manual_renewal_rules).

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. You can go to the **Renew** page via any of the methods below.

   |Method description |Procedure |
   |---|---|
   |<br>Enter through the Redis instance list page<br> |* Method 1<br><br>   1. In the top menu bar, select the project and region to which the instance belongs.<br><br>   2. On the **Instances** page, in the **Actions** column to the right of the target subscription instance, select  **... \> Renew**.<br><br>* Method 2<br><br>   1. In the top menu bar, select the project and region to which the instance belongs.<br><br>   2. On the **Instances** page, click the target instance.<br><br>   3. On the **Summary** tab, in the **Billing information** area, click **Renew** next to **Billing method**. |
   |Enter through the upper right corner navigation |1. In the upper right corner of the console, click the user's image and select **Billing**.<br><br>2. In the left navigation bar of the **Billing center ** page, select **Renewal management.** <br><br>3. On the **Renewal management** page, use the search and filtering functions to find the target Redis instance in the **Auto\-renewal**, **Manual renewal** or **Non\-renewal upon expiration instances** tab.<br><br>4. In the **Actions** column to the right of the target instance, click **Renew**.<br><br>   > **tip**<br>   <br><br>   > You can also select multiple instances, then click **Batch renew** below the instance list to renew multiple instances simultaneously.<br>    |

3. On the **Renew** page, first confirm the instance information to be renewed (such as instance ID and current expiration time) in the **Renewal confirmation** area. Then, in the **Renewal cycle** area, configure the following parameters according to your business needs.

   |Renewal cycle |Description |
   |---|---|
   |Specifying purchase period |Supports renewing instances by the whole month or the whole year. The available durations are as follows:<br><br><br>* Monthly renewal: 1 to 11 months.<br><br>* Annual renewal: 1 to 3 years.<br><br><br>> **tip**<br><br><br>> You can also check **Set all expiration dates to** and set the renewal expiration date. After the setting is completed, it will take effect on all monthly subscribed (non\-natural month) instances involved in this renewal operation. For more details, refer to [Unified expiration day](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unified_expiration_day).<br> |
   |Specifying an expiration time |Supports specifying the specific year, month, and day when the instance expires. After renewal, the expiration times of the instances involved in this operation will be exactly the same.<br><br>> **tip**<br><br><br>> After specifying the expiration time, the expiration times of all the instances involved in this renewal operation will be exactly the same. For more details, refer to [Specifying expiration time](https://docs.byteplus.com/en/docs/byteplus-platform/docs-specifying-an-expiration-time).<br> |

4. In the lower\-right corner of the page, click **Pay**.

5. On the **Confirm order information** page, confirm the order details, and click **Next step**.

   > **tip**

   > After successful renewal, you can return to the Instances page to check the new expiration time of the target subscription instance.
