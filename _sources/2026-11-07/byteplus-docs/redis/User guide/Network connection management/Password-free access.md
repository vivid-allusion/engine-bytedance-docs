---
title: "Password-free access"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/pwd-free-access"
---

Cache for Redis supports **instance\-level password\-free access**, which covers **proxy private networks and direct private networks**. Public network access is not applicable (requires separate authentication). This topic describes how to use password\-free access feature.

## Precautions

* Cache for Redis supports enabling password\-free access feature directly when creating instance. For specific procedures, refer to [Creating instance](https://docs.byteplus.com/en/docs/redis/create-instance).

* After enabling password\-free access, if no account is entered, the default account is used, allowing access to the Redis instance without a password.

* After enabling password\-free access, it also remains compatible with connecting to Redis instances using account and password authentication. You can still connect to the Redis instance with an account and password.

* To ensure database security, account and password information must be verified when connecting to the Redis instance via public network address with any account, regardless of whether the password\-free feature is enabled.

* For data security reasons, it is not allowed to add the address `0.0.0.0/0` to the allowlist of the instance while enabling the password\-free access function. To enable password\-free access, first delete the `0.0.0.0/0` address from the instance allowlist. For specific procedures, refer to [Setting allowlist](https://docs.byteplus.com/en/docs/redis/edit-allowlist).

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click on the **Connectivity** tab.

5. On the **Connectivity** tab, in the **Password\-free access** module at the top, turn on the password\-free access switch to enable it for the current instance.

   > **tip**

   > If you no longer require password\-free access, you can disable **Password\-free access**. After disabling the function, the client connections that originally used the password\-free access function will be disconnected. It is recommended that you first connect to the Redis instance using account password verification on the client before turning off the password\-free access function.

## Subsequent operations

After enabling password\-free access, you can directly connect to Redis instances without executing the command `AUTH <Username> <Password>` after executing the command `redis-cli -h <Redis instance address> -p <Port number> [-c]`.

For more information on how to connect to Redis instances, refer to [Connecting to instance via private address](https://docs.byteplus.com/en/docs/redis/connect-instance-via-private-address).

## Relevant APIs

|API |Description |
|---|---|
|[ModifyDBInstanceVpcAuthMode](https://docs.byteplus.com/en/docs/redis/modifydbinstancevpcauthmode) |Call the ModifyDBInstanceVpcAuthMode API to enable or disable password\-free access. |
