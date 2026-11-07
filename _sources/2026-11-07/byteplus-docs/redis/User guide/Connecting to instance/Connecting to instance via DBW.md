---
title: "Connecting to instance via DBW"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/connecting_to_an_instance_via_dbw"
---

Database Workshop (DBW) is a unified cloud management platform for managing the lifecycle of multiple types of databases. You can use DBW to quickly remotely connect to and manage Redis databases online. This topic describes how to connect to a Redis instance via DBW.

## Background information

DBW is a database SaaS product that integrates database graphical user interface (GUI), fault troubleshooting, and auditing. It provides web\-terminal management capabilities such as comprehensive observation and analysis, intelligent risk checking, and autonomous operation and maintenance, offering you stable, safe, and efficient database management cloud services. For more details, refer to [What is Database Workshop](https://docs.byteplus.com/en/docs/DBW/what-is-database-workbench).

## Prerequisites

* A Redis instance has been created. For specific procedures, refer to [Creating instance](https://docs.byteplus.com/en/docs/redis/create-instance).

* The database login account and password have been set for the Redis instance. For specific procedures, refer to [Creating and managing account](https://docs.byteplus.com/en/docs/redis/create-manage-account).

* The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Precautions

* When you select **Authorize Database Workshop to add service IPs to the corresponding database instance allowlist**, the IP address of the DBW backend service host will be added to the allowlist of the database instance. The name format of this allowlist is `DBW_Sole_***_***_***_Redis`.

* During the process of connecting to Redis using DBW, do not modify, disassociate, or delete the above allowlist; otherwise, you will not be able to open a new command window to execute commands, but the current window can still continue to execute command operations.

* For community edition instances of Cache for Redis, after enabling password\-free access, the `default` account default is allowed to access Redis instances in the DBW without the password. For specific procedures, refer to [Password-free access](https://docs.byteplus.com/en/docs/redis/pwd-free-access).

* Logging onto the DBW database interaction platform is temporarily not supported for instances with SSL encryption enabled. If you want to log in, please first disable the SSL encryption service of the instance. For specific procedures, refer to [Setting SSL encryption](https://docs.byteplus.com/en/docs/redis/setup-ssl).

   If you successfully connect to a Redis instance through DBW and then enable the SSL encryption service for the instance, the original connection will not be disconnected and you can still continue to execute other commands, but you cannot open a new command window.

## Log on to DBW via Redis console

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, find the target instance, and click **Login to DBW** in the **Actions** column on the right side of the instance.

4. In the pop\-up dialog box, set the following instance connection parameters.

   |Parameters |Description |
   |---|---|
   |Instance type |**Cache for Redis** is selected by default. No modification is required. |
   |Instance name |The target Redis instance in Step 3 is selected by default.<br><br>To log in to a different Redis instance, select the corresponding Redis instance from the drop\-down list. |
   |Database account |Enter the database account. |
   |Database password |Enter the password corresponding to the database account. If you forget the password, you can modify it through the Redis console. For specific procedures, refer to [Resetting password](https://docs.byteplus.com/en/docs/redis/reset-password). |

5. Select **Authorize Database Workshop to add service IPs to the corresponding database instance allowlist**, and click **Log in**.

   > **tip**

   > You can also check **Remember password** at the same time. After checking, you don't need to enter the password when logging in to this Redis instance with the same account in the future.

## Connect to a Redis instance via DBW

1. Log in to the [DBW console](https://console.byteplus.com/dbw).

2. In the top menu bar, select the project and region to which the instance belongs.

3. In the left\-side navigation pane, select **Data Management** \> **Data Interaction Console**.

4. In the pop\-up dialog box, set the following instance connection parameters.

   |Parameters |Description |
   |---|---|
   |Instance type |Select **Cache for Redis** from the drop\-down list. |
   |Instance name |Select the target Redis instance from the drop\-down list. |
   |Database account |Enter the database account. |
   |Database password |Enter the password corresponding to the database account. If you forget the password, you can modify it through the Redis console. For specific procedures, refer to [Resetting password](https://docs.byteplus.com/en/docs/redis/reset-password). |

5. Select **Authorize Database Workshop to add service IPs to the corresponding database instance allowlist**, and click **Log in**.

   > **tip**

   > You can also check **Remember password** at the same time. After checking, you don't need to enter the password when logging in to this Redis instance with the same account in the future.

## Subsequent operations

After successfully connecting to a Redis instance through DBW, you can first set the [read/write splitting strategy at the connection level for the current connection](https://docs.byteplus.com/en/docs/redis/set-read-write-splitting#.6K-75YaZ5YiG56a7562W55Wl6K-05piO5Y-K6K6-572u5bu66K6u), then you can execute various command statements according to business needs in the command window of the DBW data interaction console. At the same time, you can also manage databases and key\-value pairs visually (such as creating, querying, deleting, etc.). For specific procedures, refer to:

* [Executing commands](https://docs.byteplus.com/en/docs/DBW/executing-commands-for-redis)

* [Key value management](https://docs.byteplus.com/en/docs/DBW/key-value-management-for-redis)
