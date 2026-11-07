---
title: "Connecting to instance via public address"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/connect-instance-via-public-address"
---

You can connect to and manage Redis databases through the redis\-cli tool. This topic describes how to use the redis\-cli tool to connect to Redis instances through the public network.

## Prerequisites

* A Redis instance has been created. For specific procedures, refer to [Creating an instance](https://docs.byteplus.com/en/docs/redis/create-instance).

* A database account and password have been created. For more information, refer to [Creating and managing account](https://docs.byteplus.com/en/docs/redis/manage-account).

* Public network access is enabled. For more information, refer to [Enabling public network access](https://docs.byteplus.com/en/docs/redis/apply-public-address).

   > **tip**

   > Compared with private network access, internet access has a higher latency and involves certain security risks. We recommend that you only use it in testing environments, while private network access is recommended for production environments. When devices outside the VPC no longer need to access Redis instances, promptly disable Internet access. For instructions on how to disable internet access, refer to [Releasing public address](https://docs.byteplus.com/en/docs/redis/release-public-address).

* Ensure the Redis\-cli tool is properly installed. For installation instructions, refer to [Installing redis-cli](https://docs.byteplus.com/en/docs/redis/connect-instances-through-redis-cli#.6ZmE5b2V77ya5a6J6KOFLXJlZGlzLWNsaQ==).

   > **tip**

   > To ensure compatibility, we recommend that you install a redis\-cli version compatible with the Redis version in a BytePlus ECS instance.

* Ensure that the IP address of the device where redis\-cli is installed is added to the allowlist. For more information on how to set allowlist, refer to [Setting allowlist](https://docs.byteplus.com/en/docs/redis/set-allowlist).

* Redis\-cli does not support certificate verification during connection. If you have enabled SSL, you will not be able to log in using redis\-cli. In this case, you can log in using another client such as Redisson.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the **Summary** page, click on the **Connectivity** tab.

5. In the **Public network access \> Proxy public network access** section, click the icon next to **Proxy public network address** to copy the proxy public network address.

6. Log on to the ECS instance with redis\-cli installed and run the following command:

   ```Bash
   src/redis-cli -h <Redis 实例连接地址> -p <端口号> [-c]
   ```

   |Parameters |Description |
   |---|---|
   |Redis instance address |That is, the public network address connection address obtained in step 5. For example: `redis-cnlf12q67ynjy**** redis.bytepluses.com`. |
   |Port number |The port number of the Redis instance, which is 6379 by default. |
   |`-c` |If cluster mode is enabled, this parameter only applies to Redis instances that enable sharding clusters. When you need to use a direct address connection, you need to add `-c` when connecting to the instances. For more information on direct addresses, refer to [Applying for direct connection address](https://docs.byteplus.com/en/docs/redis/apply-direct-connection-address). |

7. Enter your username and password to complete the verification. If you have not created an account, please create one first. For more information on creating an account, refer to [Creating and managing account](https://docs.byteplus.com/en/docs/redis/manage-account).

   You can choose any of the following methods to complete account password verification:

   * Enter the account and password simultaneously for verification. The command is as follows.

      ```Bash
      AUTH <username> <password>
      ```

      Or

      ```Bash
      AUTH <username>:<password>
      ```

   * Enter the password directly. The command is as follows.

      ```Bash
      AUTH <password>
      ```

   > **tip**

   * > Directly entering the password for verification is only supported when using the default account.

   * > If you forget your password, you can reset it. For specific operations, refer to [Resetting password](https://docs.byteplus.com/en/docs/redis/reset-password).

   The Redis instance is successfully connected when you see the **OK** message.

## Subsequent operations

After successful verification, you can first [set read/write splitting strategy at the connection level](https://docs.byteplus.com/en/docs/redis/set-read-write-splitting#.6K-75YaZ5YiG56a7562W55Wl6K-05piO5Y-K6K6-572u5bu66K6u) for the current connection. Then you can execute Redis\-related commands according to business needs, such as executing the `DBSIZE` command to query how many keys are in the current database. For more information on the commands supported by Cache for Redis, refer to [Supported commands](https://docs.byteplus.com/en/docs/redis/supported-command).
